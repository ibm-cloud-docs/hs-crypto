---

copyright:
  years: 2018, 2024
lastupdated: "2024-06-04"

keywords: data encryption key, key material, unwrap call, unwrap key, decrypt key, decrypt data encryption key, access data encryption key, unwrap api

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Unwrapping data encryption keys with root keys
{: #unwrap-keys}

You can unwrap a [data encryption key (DEK)](#x4791827){: term} to access the contents by using the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} key management service API, if you are a privileged user. Unwrapping a DEK decrypts and checks the integrity of the contents, returning the original key material to your {{site.data.keyword.cloud_notm}} data service.
{: shortdesc}

To learn how key wrapping helps you control the security of at-rest data in the cloud, see [Envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).

## Unwrapping keys by using the API
{: #unwrap-key-api}

[After you make a wrap call to the service](/docs/hs-crypto?topic=hs-crypto-wrap-keys), you can unwrap a specified data encryption key (DEK) to access the contents by making a `POST` call to the following endpoint.

{{site.data.keyword.hscrypto}} is continuously replacing port-based API endpoints with instance-based API endpoints. For example, for public key management endpoint URLs, the format is changed from `api.<region>.hs-crypto.cloud.ibm.com:<port>` to `<instance_ID>.api.<region>.hs-crypto.appdomain.cloud`. For a complete list of the endpoint URL schemes and more information about which regions now support instance-based endpoint URLs, see [Instance-based endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints). Note that, for any new service instances created after the dates specified in the table, only instance-based endpoint URLs can be applied. No impact to existing service instances is expected, as the current port-based endpoint scheme stays intact for the time being. However, it is suggested to use the new instance-based scheme wherever possible especially for new projects.
{: note}
 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/actions/unwrap
```
{: codeblock}

Root keys that contain the same key material can unwrap the same data encryption key (WDEK).
{: note}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Copy the ID of the [root key](#x6946961){: term} that you used to perform the initial wrap request.

    You can retrieve the ID for a key by making a `GET /v2/keys` request, or by viewing your keys in the UI.

3. Copy the `ciphertext` value that was returned during the initial wrap request.

4. Run the following cURL command to decrypt and authenticate the key material.

    ```sh
    curl -X POST \
      'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'x-kms-key-ring: <key_ring_ID>' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
      "ciphertext": "<encrypted_data_key>"
    }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.
    
    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `key_ID` | **Required.** The unique identifier for the root key that you used for the initial wrap request. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your{{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `key_ring_ID` | **Optional.** The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} searches for the key in every key ring that is associated with the specified instance. It is suggested to specify the key ring ID for a more optimized request. \n \n Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | `correlation_ID` | **Optional.** The unique identifier that is used to track and correlate transactions. |
    | `encrypted_data_key` | The `ciphertext` value that was returned during a wrap operation. |
    {: caption="Table 1. Describes the variables needed to unwrap keys in {{site.data.keyword.hscrypto}}" caption-side="bottom"}

    The original key material is returned in the response entity-body. The response body also contains the ID of the key version that was used to unwrap the supplied ciphertext. The following JSON object shows a sample returned value.

    ```json
    {
      "plaintext": "Rm91ciBzY29yZSBhbmQgc2V2ZW4geWVhcnMgYWdv",
      "keyVersion": {
        "id": "02fd6835-6001-4482-a892-13bd2085f75d"
      }
    }
    ```
    {: screen}

    If {{site.data.keyword.hscrypto}} detects that you rotated
    the root key that is used to unwrap and access your data, the service also returns a newly wrapped data encryption key (`ciphertext`) in the unwrap response body. The latest key version (`rewrappedKeyVersion`) that is associated with the new `ciphertext` is also returned. Store and use the new
    `ciphertext` value for future envelope encryption operations so that your data is protected by the latest root key.

## Decoding your key material
{: #how-to-decode-key-material}

When you unwrap a data encryption key, the key material is returned in base64 encoding. You need to decode the key before you encrypt it.

### Using OpenSSL to decode key material
{: #open-ssl-encoding-root-unwrap}

1. Download and install [OpenSSL](https://github.com/openssl/openssl#for-production-use){: external}.
2. Base64 encode your key material string by running the following command:

    ```
    $ openssl base64 -d -in <infile> -out <outfile>
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `infile` | The name of the file where your base64 encoded key material string resides. |
    | `outfile` | The name of the file where your decoded key material is outputted after the command is run. |
    {: caption="Table 2. Describes the variables needed to decode your key material" caption-side="bottom"}

    If you want to output the decoded material in the command line directly rather than a file, run command `openssl enc -base64 -d <<< '<key_material_string>'`, where key_material_string is the returned plain text from your unwrap request.
