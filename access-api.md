---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: REST API, RESTful API, access token, instance ID

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Accessing the API
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} integrates with the {{site.data.keyword.keymanagementserviceshort}} REST API, which can be used with any programming language to store, retrieve, and generate keys.
{: shortdesc}

To work with the API, you need to generate your service and authentication credentials.

## Retrieving an access token
{: #retrieve-token}

You can authenticate with {{site.data.keyword.hscrypto}} by retrieving an access token from {{site.data.keyword.iamshort}}. With a [service ID](/docs/iam/serviceid.html#serviceids), you can work with the {{site.data.keyword.hscrypto}} API on behalf of your service or application on or outside {{site.data.keyword.cloud_notm}}, without needing to share your personal user credentials.  

If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip}

Complete the following steps to retrieve an access token:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** &gt; **Access (IAM)** &gt; **Service IDs**. Follow the process to [create a service ID](/docs/iam/serviceid.html#creating-a-service-id).
2. Use the **Access policies** section to [define an access policy for your new service ID](/docs/iam/serviceidaccess.html).

    For more information about managing access for your {{site.data.keyword.hscrypto}} resources, see [Roles and permissions](/docs/services/hs-crypto/manage-access.html#roles).
3. Use the **API keys** section to [create an API key to associate with the service ID](/docs/iam/serviceid_keys.html#serviceidapikeys). Save your API key by downloading it to a secure location.
4. Call the {{site.data.keyword.iamshort}} API to retrieve your access token.

    ```cURL
    curl -X POST \
      https://iam.cloud.ibm.com/identity/token \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    In the request, replace `<API_KEY>` with the API key that you created in step 3. The following truncated example shows the token output:

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Use the full `access_token` value, prefixed by the _Bearer_ token type, to programmatically manage keys for your service using the {{site.data.keyword.hscrypto}} API.

    Access tokens are valid for 1 hour, but you can regenerate them as needed. To maintain access to the service, refresh the access token for your API key on a regular basis by calling the {{site.data.keyword.iamshort}} API.   
    {: tip }

## Retrieving your instance ID
{: #retrieve-instance-ID}

You can retrieve the identifying information for your {{site.data.keyword.hscrypto}} service instance by using the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview). Use an instance ID to manage your encryption keys within a specified instance of {{site.data.keyword.hscrypto}} in your account.

1. Log in to {{site.data.keyword.cloud_notm}} with the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Note:** If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.

2. Select the account that contains your provisioned instance.

    You can run `ibmcloud resource service-instances` to list all service instances that are provisioned in your account.

3. Retrieve the Cloud Resource Name (CRN) that uniquely identifies your {{site.data.keyword.hscrypto}} service instance.

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    Replace `<instance_name>` with the unique alias that you assigned to your instance of {{site.data.keyword.hscrypto}}. The following truncated example shows the CLI output. The _42454b3b-5b06-407b-a4b3-34d9ef323901_ value is an example instance ID.

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## Retrieving connection information
{: #retrieve-connection-info}

Before you call any {{site.data.keyword.keymanagementserviceshort}} APIs, call the **Retrieve the connection info** API first to retrieve the connection information. For more information, see [the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

## Forming your API request
{: #form-api-request}

When you make an API call to the service, structure your API request according to how you initially provisioned your instance of {{site.data.keyword.hscrypto}}.

To build your request, pair a [regional service endpoint](/docs/services/hs-crypto/regions.html) with the appropriate authentication credentials. For example, if you created a service instance for the `us-south` region, use the following endpoint and API headers to browse keys in your service:

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### What's next
{: #api-next}

To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}. -->
