---

copyright:
  years: 2018, 2022
lastupdated: "2022-02-16"

keywords: set up api, api key, cryptographic operations, use ep11 api, access ep11 api, ep11 over grpc, using api

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}

# Performing cryptographic operations with the GREP11 API
{: #set-up-grep11-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides an Enterprise PKCS #11 (EP11) API over gRPC (also referred to as *GREP11 API*) to remotely access the {{site.data.keyword.hscrypto}} service instance for data encryption and management.
{: shortdesc}

## Retrieving your IBM Cloud credentials
{: #retrieve-grep11-credentials}

To work with the API, you need to generate your service and authentication credentials. To gather your credentials:

1. [Generate an {{site.data.keyword.cloud_notm}} IAM access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
2. [Retrieve the instance ID that uniquely identifies your {{site.data.keyword.hscrypto}} service instance](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

## Generating a GREP11 API request
{: #form-grep11-api-request}

In order to remotely access cloud HSM on {{site.data.keyword.hscrypto}} to perform cryptographic operations, you need to generate a GREP11 API request, and pass the GREP11 API endpoint URL, service ID API key, IAM endpoint, and instance ID through the API call.

You can also enable mutual TLS for GREP11 API to add another layer of authentication. For more information, see [Enabling the second layer of authentication for EP11 connections](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11).

### Example: Generating random data using the `GenerateRandomRequest()` function
{: #generate-random-request-example}

GREP11 API supports programming languages with [gRPC libraries](https://grpc.io/docs/){: external}. Two sample GitHub repositories are provided for you to test the GREP11 API:

- [The sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external}
- [The sample GitHub repository for JavaScript](https://github.com/IBM-Cloud/hpcs-grep11-js){: external}

You can use the following Golang code example to generate random data by calling the `GenerateRandom` function.

This example assumes that extra required Golang packages are included through import statements, such as the [gRPC](https://godoc.org/google.golang.org/grpc){: external} and [http](https://golang.org/pkg/net/http/){: external} packages. The `import pb "github.com/IBM-Cloud/hpcs-grep11-go/grpc"` statement is used by GREP11 to perform API function calls.
{: note}

```Golang
import pb "github.com/IBM-Cloud/hpcs-grep11-go/grpc"

// Data structure and supporting methods used for GREP11 authentication
// IAMPerRPCCredentials type defines the fields required for IBM Cloud IAM authentication
// This type implements the gRPC PerRPCCredentials interface

type IAMPerRPCCredentials struct {
	expiration  time.Time
	updateLock  sync.Mutex
	Instance    string // Always Required - IBM Cloud HPCS instance ID
	AccessToken string // Required if APIKey nor Endpoint are specified - IBM Cloud IAM access token
	APIKey      string // Required if AccessToken is not specified - IBM Cloud API key
	Endpoint    string // Required if AccessToken is not specified - IBM Cloud IAM endpoint
}

// GetRequestMetadata is used by GRPC for authentication
func (cr *IAMPerRPCCredentials) GetRequestMetadata(ctx context.Context, uri ...string) (map[string]string, error) {
	// Set token if empty or Set token if expired
	if len(cr.APIKey) != 0 && len(cr.Endpoint) != 0 && time.Now().After(cr.expiration) {
		if err := cr.getToken(ctx); err != nil {
			return nil, err
		}
	}

	return map[string]string{
		"authorization":    cr.AccessToken,
		"bluemix-instance": cr.Instance,
	}, nil
}

// RequireTransportSecurity is used by gRPC for authentication
func (cr *IAMPerRPCCredentials) RequireTransportSecurity() bool {
	return true
}

// getToken obtains a bearer token and the expiration
func (cr *IAMPerRPCCredentials) getToken(ctx context.Context) (err error) {
	cr.updateLock.Lock()
	defer cr.updateLock.Unlock()

	// Check if another thread has updated the token
	if time.Now().Before(cr.expiration) {
		return nil
	}

	var req *http.Request
	client := http.Client{}
	requestBody := []byte("grant_type=urn:ibm:params:oauth:grant-type:apikey&apikey=" + cr.APIKey)

	req, err = http.NewRequest("POST", cr.Endpoint+"/identity/token", bytes.NewBuffer(requestBody))
	if err != nil {
		return err
	}

	req.Header.Set("Content-Type", "application/x-www-form-urlencoded")
	req = req.WithContext(ctx)
	resp, err := client.Do(req)
	if err != nil {
		return err
	}

	respBody, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		return fmt.Errorf("failed to read response body: %s", err)
	}
	defer resp.Body.Close()

	iamToken := struct {
		AccessToken string `json:"access_token"`
		ExpiresIn   int32  `json:"expires_in"`
	}{}

	err = json.Unmarshal(respBody, &iamToken)
	if err != nil {
		return fmt.Errorf("error unmarshaling response body: %s", err)
	}

	cr.AccessToken = fmt.Sprintf("Bearer %s", iamToken.AccessToken)
	cr.expiration = time.Now().Add((time.Duration(iamToken.ExpiresIn - 60)) * time.Second)

	return nil
}

// Generating a GREP11 API function call

// The following IBM Cloud items need to be changed prior to running the sample program
const address = "<grep11_server_address>:<port>"

var callOpts = []grpc.DialOption{
  grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{})),
  grpc.WithPerRPCCredentials(&util.IAMPerRPCCredentials{
    APIKey:   "<ibm_cloud_apikey>",
    Endpoint: "https://iam.cloud.ibm.com",
    Instance: "<hpcs_instance_id>",
  }),
}

conn, err := grpc.Dial(address, callOpts...)
if err != nil {
		panic(fmt.Errorf("Could not connect to server: %s", err))
}
defer conn.Close()

cryptoClient := pb.NewCryptoClient(conn)

rngTemplate := &pb.GenerateRandomRequest{
		Len: (uint64)(ep11.AES_BLOCK_SIZE),
}

// Generate 16 bytes of random data for the initialization vector
rng, err := cryptoClient.GenerateRandom(context.Background(), rngTemplate)
if err != nil {
		panic(fmt.Errorf("GenerateRandom Error: %s", err))
}
iv := rng.Rnd[:ep11.AES_BLOCK_SIZE]
fmt.Println("Generated IV")
```
{: codeblock}

In the example, update the following variables:

* Replace `<grep11_server_address>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance console, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**. Alternatively, you can dynamically [retrieve the API endpoint URL](/apidocs/hs-crypto#getinstance){: external}. The returned value includes the following. Depending on whether you are using public or [private network](/docs/hs-crypto?topic=hs-crypto-secure-connection), use the public or private service endpoint value that is returned in the `ep11` section.

    ```
    {
      "instance_id": "<instance_ID>",
      "kms": {
        "public": "api.<region>.hs-crypto.cloud.ibm.com:<port>",
        "private":"api.private.<region>.hs-crypto.cloud.ibm.com:<port>"
      },
      "ep11": {
        "public": "ep11.<region>.hs-crypto.cloud.ibm.com:<port>",
        "private":"ep11.private.<region>.hs-crypto.cloud.ibm.com:<port>"
      }
    }
    ```
    {: screen}

* Replace `<ibm_cloud_apikey>` with the service ID API key that you created. The service ID API Key can be created by following the instruction in [Managing service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.

* Replace `<instance_ID>` with the instance ID that uniquely identifies your service instance. Retrieve the instance ID by following the instruction in [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

If the sample request is processed successfully, random data with a length of 16 bytes will be returned, as specified in `ep11.AES_BLOCKSIZE`.

The previous authentication example as well as more Golang code examples can be found at:
 -  [GREP11 API examples](https://github.com/IBM-Cloud/hpcs-grep11-go/tree/master/examples){: external}
 -  [IBM Cloud IAM support for GREP11](https://github.com/IBM-Cloud/hpcs-grep11-go/blob/master/util/util.go){: external}

## What's next
{: #set-up-grep11-api-next-steps}

You're all set to start managing your encryption keys and data. To find out more about managing your data using the cloud HSM function of {{site.data.keyword.hscrypto}}, [check out the GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
