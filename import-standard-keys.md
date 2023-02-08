---

copyright:
  years: 2018, 2023
lastupdated: "2023-02-08"

keywords: standard key, import key, key material, import key api, bring your own key, byok, encryption key, import standard encryption key, upload standard encryption key, import secret, persist secret, store secret, upload secret, store encryption key

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Importing standard keys
{: #import-standard-keys}

You can add your existing encryption keys with the {{site.data.keyword.cloud_notm}} console, or programmatically with the {{site.data.keyword.hscrypto}} key management service API.

## Importing standard keys with the {{site.data.keyword.cloud_notm}} console
{: #import-standard-key-gui}
{: ui}

[After you create an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision), complete the following steps to enter your existing standard key with the {{site.data.keyword.hscrypto}} GUI.

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. To import a key, select the **KMS keys** tab in the side menu.
5. In the **Keys** table, click **Add key** and select **Import a key**.

    Specify the key's details:

    | Setting | Description |
    | --- | --- |
    | Key type | The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. From the list of key types, select **[Standard key](/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept)**. |
    | Key name | A unique, human-readable alias for easy identification of your key. To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location. |
    | Key alias | (Optional) One or more unique, human-readable aliases that you want to assign to your key for easy recognition. Alias size can be 2 - 90 characters. You can set up to five key aliases for the key, with each separated by a comma. \n \n Note: Each alias must be alphanumeric, case sensitive, and cannot contain spaces or special characters other than dashes (-) or underscores (_). The alias cannot be a version 4 UUID and must not be a {{site.data.keyword.hscrypto}} reserved name: `allowed_ip`, `key`, `keys`, `metadata`, `policy`, `policies`, `registration`, `registrations`, `ring`, `rings`, `rotate`, `wrap`, `unwrap`, `rewrap`, `version`, `versions`. |
    | Key ring ID | Select a key ring from the list that contains the existing key rings. If you don't assign a key ring, the key is added to the `default` key ring. For more information about key rings, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | Key material | The base64 encoded key material, such as a symmetric key, that you want to manage in the service. For more information, see [Base64 encoding your key material](#encode-key-material-standard-key). Ensure that the key material meets the following requirements: \n * The key can be up to 7,500 bytes. \n * The key must be base64-encoded. |
    | Expiration date | (Optional) Set the date and time when the key gets expired. After the expiration date, the key moves into the _Deactivated_ state. For more information about key state, see [Monitoring the lifecycle of encryption keys](/docs/hs-crypto?topic=hs-crypto-key-states). |
    | Description | (Optional) Add an extended description for your key. It needs to be two to 240 characters in length. |
    {: caption="Table 1. Describes the settings to import a standard key" caption-side="bottom"}

6. When you finish filling out the key's details, click **Import key** to confirm.

## Importing standard keys with the API
{: #import-standard-key-api}
{: api}

Import a standard key by making a `POST` call to the following endpoint:

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Call the [{{site.data.keyword.hscrypto}} key management service API](/apidocs/hs-crypto){: external} with the following cURL command.

    ```cURL
    curl -X POST \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>",
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
    | `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
    | `return_preference` | Optional: A header that alters server behavior for `POST` and `DELETE` operations. When you set the `return_preference` variable to `return=minimal`, the service returns only the key metadata, such as the key name and ID value, in the response entity-body. When you set the variable to `return=representation`, the service returns both the key material and the key metadata. |
    | `key_alias` | A unique, human-readable name for easy identification of your key.<br><br>Important: To protect your privacy, do not store your personal data as metadata for your key. |
    | `key_description` | Optional: An extended description of your key.<br><br>Important: To protect your privacy, do not store your personal data as metadata for your key. |
    | `YYYY-MM-DD` \n \n `HH:MM:SS.SS` | Optional: The date and time that the key expires in the system, in RFC 3339 format. If the `expirationDate` attribute is omitted, the key does not expire. |
    | `key_material` | The base64 encoded key material, such as a symmetric key, that you want to manage in the service. For more information, see [Base64 encoding your key material](#encode-key-material-standard-key).<br><br>Ensure that the key material meets the following requirements:<br><br>* The key can be up to 7,500 bytes.<br>* The key must be base64-encoded. |
    | `key_type` | A boolean value that determines whether the key material can leave the service.<br><br>When you set the `extractable` attribute to `true`, the service designates the key as a standard key that you can store in your apps or services. |Table 2. Describes the variables needed to add a standard key with the {{site.data.keyword.hscrypto}} key management service API

    To protect the confidentiality of your personal data, avoid entering personally identifiable information (PII), such as your name or location, when you add keys to the service. For more examples of PII, see section 2.2 of the [NIST Special Publication 800-122](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: external}.
    {: tip}

    A successful `POST /v2/keys` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.hscrypto}} key management service API.

3. Optional: Verify that the key was added by running the following call to get the keys in your {{site.data.keyword.hscrypto}} service instance.

    ```cURL
    curl -X GET \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

## Importing standard keys with the CLI
{: #import-standard-key-cli}
{: cli}

Complete the following steps to import standard keys that uses the {{site.data.keyword.keymanagementserviceshort}} CLI, which is integrated in {{site.data.keyword.hscrypto}}:

1. [Set up the {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli).

2. Import a standard key with the following command:

    ```
    ibmcloud kp key create
    ```
    {: pre}

    You can find extra parameters for this command in the [{{site.data.keyword.keymanagementserviceshort}} CLI reference](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference#kp-key-create).

## Base64 encoding your key material
{: #encode-key-material-standard-key}

When you import an existing standard key, it is required to include the encrypted key material that you want to store and manage in the service.

### Using OpenSSL to encode existing key material
{: #open-ssl-encoding-standard-key}

1. Download and install [OpenSSL](https://github.com/openssl/openssl#for-production-use){: external}.
2. Base64 encode your key material string by running the following command:

    ```
    $ openssl base64 -in <infile> -out <outfile>
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `infile` | The name of the file where your key material string resides. |
    | `outfile `| The name of the file where your base64-encoded key material is created when the command is run. |
    {: caption="Table 3. Describes the variables needed to base64 encode your key material" caption-side="bottom"}

    If you want to output the base64 material in the command line directly rather than a file, run the command `openssl enc -base64 <<< '<key_material_string>'`, where *key_material_string* is the key material input for your imported key.
    {: note}

### Using OpenSSL to create and encode new key material
{: #open-ssl-encoding-new-key-material-standard-key}

1. Download and install [OpenSSL](https://github.com/openssl/openssl#for-production-use){: external}.
2. Base64 encode your key material string by running the following command:

    ```
    $ openssl rand <byte_length> -base64
    ```
    {: codeblock}

    Replace the `byte_length` variable in the example request with the length of your key, which is measured in bytes. Acceptable byte length can be up to 7,500 bytes.


## What's next
{: #import-standard-key-next}

To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management service API reference doc](/apidocs/hs-crypto){: external}.
