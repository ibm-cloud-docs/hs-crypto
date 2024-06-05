---

copyright:
  years: 2018, 2024
lastupdated: "2024-06-04"

keywords: rewrap key, reencrypt data encryption key, rewrap api, key id

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Rewrapping data encryption keys with root keys
{: #rewrap-keys}

Reencrypt your data encryption keys by using the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} key management service API.
{: shortdesc}

When you [rotate a root key in {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro), new cryptographic key material becomes available for protecting the data encryption keys (DEKs) that are associated with the root key. With the rewrap API, you can reencrypt or rewrap your DEKS without exposing the keys in their plain text form.

To learn how envelope encryption helps you control the security of at-rest data in the cloud, see [Protecting data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).

## Rewrapping keys by using the API
{: #rewrap-key-api}

You can reencrypt a specified data encryption key (DEK) with a root key that you manage in {{site.data.keyword.hscrypto}}, without exposing the DEK in the plain text form.

Rewrapping keys works by combining `unwrap` and `wrap` calls to the service. For example, you can emulate a `rewrap` operation by first calling the `unwrap` API to access a DEK, and then calling the `wrap` API to reencrypt the DEK by using the newest root key material.
{: note}

[After you rotate a root key in the service](/docs/hs-crypto?topic=hs-crypto-rotate-keys), rewrap a data encryption key that is associated with the root key by making a `POST` call to the following endpoint.

{{site.data.keyword.hscrypto}} is continuously replacing port-based API endpoints with instance-based API endpoints. For example, for public key management endpoint URLs, the format is changed from `api.<region>.hs-crypto.cloud.ibm.com:<port>` to `<instance_ID>.api.<region>.hs-crypto.appdomain.cloud`. For a complete list of the endpoint URL schemes and more information about which regions now support instance-based endpoint URLs, see [Instance-based endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints). Note that, for any new service instances created after the dates specified in the table, only instance-based endpoint URLs can be applied. No impact to existing service instances is expected, as the current port-based endpoint scheme stays intact for the time being. However, it is suggested to use the new instance-based scheme wherever possible especially for new projects.
{: note}
 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/actions/rewrap
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Copy the ID of the rotated root key that you used to perform the initial wrap request.

    You can retrieve the ID for a key by making a `GET api/v2/keys` request, or by viewing your keys in the UI.
3. Copy the `ciphertext` value that was returned during the latest wrap request.
4. Rewrap the key with the latest root key material by running the following cURL command.

    ```sh
    curl -X POST \
      'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/actions/rewrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H "x-kms-key-ring: <key_ring_ID>" \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
      "ciphertext": "<encrypted_data_key>"
    }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south` or `eu-de`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `key_ID` | **Required.** The unique identifier for the root key that you used for the initial wrap request. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `key_ring_ID` | **Optional.** The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request. \n \n Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
    | `encrypted_data_key` | **Required.** The `ciphertext` value that was returned by the original wrap operation. |
    {: caption="Table 1. Describes the variables needed to rewrap keys in {{site.data.keyword.hscrypto}}." caption-side="bottom"}

    The newly wrapped data encryption key, original key version (`keyVersion`) that is associated with the supplied ciphertext and latest key version (`rewrappedKeyVersion`) associated with the new ciphertext is returned in the response entity-body. The following JSON object shows an example returned value.

    ```json
    {
      "ciphertext": "eyJjaX ... h0Ijoi ... c1ZCJ9",
      "keyVersion": {
        "id": "02fd6835-6001-4482-a892-13bd2085f75d"
      },
      "rewrappedKeyVersion": {
        "id": "12e8c9c2-a162-472d-b7d6-8b9a86b815a6"
      }
    }
    ```
    {: screen}

    Store and use the new `ciphertext` value for future envelope encryption
    operations so that your data is protected by the latest root key.
