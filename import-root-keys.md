---

copyright:
  years: 2018, 2024
lastupdated: "2024-05-30"

keywords: root key, import key, key material, import key api, bring your own key, byok, symmetric key, import symmetric key, upload symmetric key, import root key, upload root key, import key-wrapping key, upload key-wrapping key, import crk

subcollection: hs-crypto
---

{{site.data.keyword.attribute-definition-list}}




# Importing root keys
{: #import-root-keys}

You can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to secure your existing root keys by using the UI, or programmatically with the {{site.data.keyword.hscrypto}} key management service API.
{: shortdesc}

Root keys are symmetric key-wrapping keys that are used to protect the security of encrypted data in the cloud. For more information about importing root keys, see [Bringing your encryption keys to the cloud](/docs/hs-crypto?topic=hs-crypto-importing-keys).

Plan ahead for importing keys by [reviewing your options for creating and encrypting key material](/docs/hs-crypto?topic=hs-crypto-importing-keys#plan-ahead). For added security, you can enable the secure import of the key material by using an [import token](/docs/hs-crypto?topic=hs-crypto-importing-keys#using-import-tokens) to encrypt your key material before you bring it to the cloud.
{: note}

## Importing root keys with the UI
{: #import-root-key-gui}
{: ui}

After you [create an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision), complete the following steps to add your existing root key with the {{site.data.keyword.hscrypto}} GUI.

1. [Log in to the UI](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. To import a key, select the **KMS keys** tab in the side menu.
5. In the **Keys** table, click **Add key** and select **Import a key**.

    Specify the key's details:

    | Setting | Description |
    | --- | --- |
    | Key type | The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. From the list of key types, select **[Root key](/docs/hs-crypto?topic=hs-crypto-understand-concepts#root-key-concept)**. |
    | Key name | A unique, human-readable alias for easy identification of your key. To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location. |
    | Key alias | (Optional) One or more unique, human-readable aliases that you want to assign to your key for easy recognition. Alias size can be 2 - 90 characters. You can set up to five key aliases for the key, with each separated by a comma. \n \n Note: Each alias must be alphanumeric, case-sensitive, and cannot contain spaces or special characters other than dashes (-) or underscores (_). The alias cannot be a version 4 UUID and must not be a {{site.data.keyword.hscrypto}} reserved name: `allowed_ip`, `key`, `keys`, `metadata`, `policy`, `policies`, `registration`, `registrations`, `ring`, `rings`, `rotate`, `wrap`, `unwrap`, `rewrap`, `version`, `versions`. |
    | Key ring ID | Select a key ring from the list that contains the existing key rings. If you don't assign a key ring, the key will be added to the `default` key ring. For more information about key rings, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | Key material | The base64 encoded key material, such as an existing key-wrapping key, that you want to store and manage in the service. For more information, see [Base64 encoding your key material](#encode-key-material-root-key). Ensure that the key material meets the following requirements: \n * The key must be 16, 24, or 32 bytes long, corresponding to 128, 192, or 256 bits. \n * The key must be base64-encoded. |
    | Expiration date | (Optional) Set the date and time when the key gets expired. After the expiration date, the key moves into the Deactivated state. For more information about key state, see [Monitoring the lifecycle of encryption keys](/docs/hs-crypto?topic=hs-crypto-key-states). |
    | Description | (Optional) Add an extended description for your key. It needs to be two to 240 characters in length. |
    {: caption="Table 1. Describes the settings for importing a root key" caption-side="bottom"}

6. When you finish filling out the key's details, click **Import key** to confirm.

## Importing root keys with the API
{: #import-root-key-api}
{: api}

Import symmetric keys to {{site.data.keyword.hscrypto}} by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Call the [{{site.data.keyword.hscrypto}} key management service API](/apidocs/hs-crypto){: external} with the following cURL command:

    ```cURL
    curl -X POST \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
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
    | `region` | **Required.** The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance is located. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
    | `key_alias` | **Required.** A unique, human-readable name for easy identification of your key. To protect your privacy, do not store your personal data as metadata for your key. |
    | `key_description` | An extended description of your key. To protect your privacy, do not store your personal data as metadata for your key. |
    | `YYYY-MM-DD` \n \n `HH:MM:SS.SS` | The date and time that the key expires in the system, in RFC 3339 format. If the `expirationDate` attribute is omitted, the key does not expire. |
    | `key_material` | The base64 encoded key material, such as an existing key-wrapping key, that you want to store and manage in the service. For more information, see [Base64 encoding your key material](#encode-key-material-root-key). Ensure that the key material meets the following requirements: \n * The key must be 16, 24, or 32 bytes long, corresponding to 128, 192, or 256 bits. \n * The key must be base64-encoded. |
    | `key_type` | A boolean value that determines whether the key material can leave the service. When you set the `extractable` attribute to `false`, the service designates the key as a root key that you can use for `wrap` or `unwrap` operations. |
    {: caption="Table 2. Describes the variables needed to add a root key with the API" caption-side="bottom"}

    To protect the confidentiality of your personal data, avoid entering personally identifiable information (PII), such as your name or location, when you add keys to the service. For more examples of PII, see section 2.2 of the [NIST Special Publication 800-122](https://www.nist.gov/publications/guide-protecting-confidentiality-personally-identifiable-information-pii){: external}.
    {: important}

    A successful `POST api/v2/keys` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.hscrypto}} key management service API.

3. Optional: Verify that the key was added by running the following call to browse the keys in your {{site.data.keyword.hscrypto}} service instance.

    ```cURL
    curl -X GET \
    https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>'
    ```
    {: codeblock}

## Importing root keys with the CLI
{: #import-root-key-cli}
{: cli}

Complete the following steps to import root keys by using the {{site.data.keyword.keymanagementserviceshort}} CLI, which is integrated in {{site.data.keyword.hscrypto}}:

1. [Set up the {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli).

2. Import a root key with the following command:

    ```
    ibmcloud kp key create
    ```
    {: pre}

    You can find more parameters for this command in the [{{site.data.keyword.keymanagementserviceshort}} CLI reference](/docs/key-protect?topic=key-protect-key-protect-cli-reference#kp-key-create).

## Base64 encoding your key material
{: #encode-key-material-root-key}

When importing an existing root key, it is required to include the encrypted key material that you want to store and manage in the service.

### Using OpenSSL to encode existing key material
{: #open-ssl-encoding-root-key}

1. Download and install [OpenSSL](https://github.com/openssl/openssl#for-production-use){: external}.
2. Base64 encode your key material string by running the following command:

    ```
    $ openssl base64 -in <infile> -out <outfile>
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `infile` | The name of the file where your key material string is located. Ensure that the key is 16, 24, or 32 bytes long, corresponding to 128, 192, or 256 bits. |
    | `outfile` | The name of the file where your base64-encoded key material will be created when the command has run. |
    {: caption="Table 3. Describes the variables needed to base64 encode your key material" caption-side="bottom"}

    If you want to output the base64 material in the command line directly rather than a file, run the command `openssl enc -base6<<< '<key_material_string>'`, where *key_material_string* is the key material input for your imported key.
    {: note}

### Using OpenSSL to create and encode new key material
{: #open-ssl-encoding-new-key-material-root-key}

1. Download and install [OpenSSL](https://github.com/openssl/openssl#for-production-use){: external}.
2. Base64 encode your key material string by running the following command:

    ```
    $ openssl rand <byte_length> -base64
    ```
    {: codeblock}

    Replace the `byte_length` variable in the example request with the length of your key, which is measured in bytes. Acceptable byte lengths are 16, 24, or 32 bytes, corresponding to 128, 192, or 256 bits.

## What's next
{: #import-root-key-next}

- To find out more about protecting keys with envelope encryption, check out [Wrapping keys](/docs/hs-crypto?topic=hs-crypto-wrap-keys).
- To find out instruction on creating a key, check out [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys) or [Creating standard keys](/docs/hs-crypto?topic=hs-crypto-create-standard-keys).
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management service API reference doc](/apidocs/hs-crypto){: external}.
- To find out more about using the {{site.data.keyword.keymanagementserviceshort}} CLI, check out the [{{site.data.keyword.keymanagementserviceshort}} CLI reference doc](/docs/key-protect?topic=key-protect-key-protect-cli-reference).
