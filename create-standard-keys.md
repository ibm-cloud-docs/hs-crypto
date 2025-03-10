---

copyright:
  years: 2018, 2024
lastupdated: "2024-10-09"

keywords: standard key, encryption key, create standard key, create encryption key, add key, key material, key management, create secret, persist secret, create encryption key, encryption key api, api key

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Creating standard keys
{: #create-standard-keys}

You can create a standard encryption key with the UI, or programmatically with the {{site.data.keyword.hscrypto}} key management service API.
{: shortdesc}

## Creating standard keys with the UI
{: #standard-key-gui}
{: ui}

[After you create an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision), complete the following steps to create a standard key with the UI.

If you enable [dual authorization settings for your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth), keep in mind that any keys that you add to the service require an authorization from two users to delete keys.
{: note}

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. To create a new key, select the **KMS keys** tab in the side menu.
5. In the **Keys** table, click **Add key**, and select **Create a key**.

    Specify the key's details:

    | Setting | Description |
    | --- | --- |
    | Key type | The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. From the list of key types, select **[Standard key](/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept)**. |
    | Key name | A unique, human-readable alias for easy identification of your key. To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location. |
    | Key alias | (Optional) One or more unique, human-readable aliases that you want to assign to your key for easy recognition. Alias size can be 2 - 90 characters. You can set up to five key aliases for the key, with each separated by a comma. \n \n Note: Each alias must be alphanumeric, case-sensitive, and cannot contain spaces or special characters other than dashes (-) or underscores (_). The alias cannot be a version 4 UUID and must not be a {{site.data.keyword.hscrypto}} reserved name: `allowed_ip`, `key`, `keys`, `metadata`, `policy`, `policies`, `registration`, `registrations`, `ring`, `rings`, `rotate`, `wrap`, `unwrap`, `rewrap`, `version`, `versions`. |
    | Key ring ID | Select a key ring from the list that contains the existing key rings. If you don't assign a key ring, the key will be added to the `default` key ring. For more information about key rings, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | Expiration date | (Optional) Set the date and time when the key gets expired. After the expiration date, the key moves into the Deactivated state. For more information about key state, see [Monitoring the lifecycle of encryption keys](/docs/hs-crypto?topic=hs-crypto-key-states). |
    | Description | (Optional) Add an extended description for your key. It needs to be 2 to 240 characters in length. |
    {: caption="Describes the settings to create a key" caption-side="bottom"}

5. When you finish filling out the key's details, click **Create key** to confirm.

## Creating standard keys with the API
{: #create-standard-key-api}
{: api}

Create a standard key by making a `POST` call to the following endpoint.

 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Call the [{{site.data.keyword.hscrypto}} key management service API](/apidocs/hs-crypto){: external} with the following cURL command.

    ```sh
    curl -X POST \
      "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys" \
      -H "authorization: Bearer <IAM_token>" \
      -H "bluemix-instance: <instance_ID>" \
      -H "content-type: application/vnd.ibm.kms.key+json" \
      -H "x-kms-key-ring: <key_ring_ID>" \
      -H "correlation-id: <correlation_ID>" \
      -H "prefer: <return_preference>" \
      -d '{
              "metadata": {
                  "collectionType": "application/vnd.ibm.kms.key+json",
                  "collectionTotal": 1
              },
              "resources": [
                  {
                      "type": "application/vnd.ibm.kms.key+json",
                       "name": "<key_name>",
                       "aliases": [alias_list],
                       "description": "<key_description>",
                       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
                       "extractable": <key_type>
                  }
              ]
          }'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.
    
    | Variable | Description |
    | --- | --- |
    | `region` | The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `IAM_token` | Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `key_ring_ID` | **Optional.** The unique identifier of the target key ring that you want to assign the key to. If unspecified, the header is automatically set to `default` and the key will belong to the default key ring in the specified {{site.data.keyword.hscrypto}} instance. \n \n For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
    | `return_preference` | Optional: A header that alters server behavior for `POST` and `DELETE` operations. \n \n When you set the `return_preference` variable to `return=minimal`, the service returns only the key metadata, such as the key name and ID value, in the response entity-body. When you set the variable to `return=representation`, the service returns both the key material and the key metadata. |
    | `key_name` | A unique, human-readable name for easy identification of your key. \n \n **Important:** To protect your privacy, do not store your personal data as metadata for your key. |
    | `alias_list` | **Optional.** One or more unique, human-readable aliases assigned to your key. \n \n **Important:** To protect your privacy, do not store your personal data as metadata for your key. \n \n Each alias must be alphanumeric, case-sensitive, and cannot contain spaces or special characters other than dashes (-) or underscores (_). The alias cannot be a version 4 UUID and must not be a {{site.data.keyword.hscrypto}} reserved name: `allowed_ip`, `key`, `keys`, `metadata`, `policy`, `policies`, `registration`, `registrations`, `ring`, `rings`, `rotate`, `wrap`, `unwrap`, `rewrap`, `version`, `versions`. Alias size can be 2 - 90 characters (inclusive). |
    | `key_description` | Optional: An extended description of your key. \n \n **Important:** To protect your privacy, do not store your personal data as metadata for your key. |
    | `YYYY-MM-DD` \n \n `HH:MM:SS.SS` | Optional: The date and time that the key expires in the system, in RFC 3339 format. If the `expirationDate` attribute is omitted, the key does not expire. |
    | `key_type` | A boolean value that determines whether the key material can leave the service. \n \n When you set the `extractable` attribute to `true`, the service creates a standard key that you can store in your apps or services. |
    {: caption="Describes the variables needed to add a standard key with the API" caption-side="bottom"}

    To protect the confidentiality of your personal data, avoid entering personally identifiable information (PII), such as your name or location, when you add keys to the service. For more examples of PII, see section 2.2 of the [NIST Special Publication 800-122](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: external}.
    {: tip}

    A successful `POST /v2/keys` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.hscrypto}} key management service API.

3. Optional: Verify that the key was created by running the following call to get the keys in your {{site.data.keyword.hscrypto}} service instance.

    ```cURL
    curl -X GET \
      https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


## What's next
{: #standard-key-next}

To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management service API reference doc](/apidocs/hs-crypto){: external}.
