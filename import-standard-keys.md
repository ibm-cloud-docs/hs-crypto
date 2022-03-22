---

copyright:
  years: 2018, 2022
lastupdated: "2022-03-22"

keywords: standard key, import key, key material, import key api, bring your own key, byok, encryption key, import standard encryption key, upload standard encryption key, import secret, persist secret, store secret, upload secret, store encryption key

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}

# Importing standard keys
{: #import-standard-keys}

You can add your existing encryption keys with the {{site.data.keyword.cloud_notm}} console, or programmatically with the {{site.data.keyword.hscrypto}} key management service API.

## Importing standard keys with the console
{: #import-standard-key-gui}

[After you create an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision), complete the following steps to enter your existing standard key with the {{site.data.keyword.hscrypto}} GUI.

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. To import a key, select the **KMS keys** tab in the side menu.
5. In the **Keys** table, click **Add key** and select **Import a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. From the list of key types, select <strong><a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept">Standard key</a></strong>.</td>
      </tr>
      <tr>
        <td>Key name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <tr>
        <td>Key alias</td>
        <td>
          <p>(Optional) One or more unique, human-readable aliases that you want to assign to your key for easy recognition.</p>
          <p>Alias size can be 2 - 90 characters. You can set up to five key aliases for the key, with each separated by a comma.</p>
          <p>Note: Each alias must be alphanumeric, case sensitive, and cannot contain spaces or special characters other than dashes (-) or underscores (_). The alias cannot be a version 4 UUID and must not be a {{site.data.keyword.hscrypto}} reserved name: <code>allowed_ip</code>, <code>key</code>, <code>keys</code>, <code>metadata</code>, <code>policy</code>, <code>policies</code>, <code>registration</code>, <code>registrations</code>, <code>ring</code>, <code>rings</code>, <code>rotate</code>, <code>wrap</code>, <code>unwrap</code>, <code>rewrap</code>, <code>version</code>, <code>versions</code>.</p>
        </td>
      </tr>
      <tr>
        <td>Key ring ID</td>
        <td>
          <p>Select a key ring from the list that contains the existing key rings. If you don't assign a key ring, the key is added to the <code>default</code> key ring.</p>
          <p>For more information about key rings, see <a href="/docs/hs-crypto?topic=hs-crypto-managing-key-rings">Managing key rings</a>.</p>
        </td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>
          <p>The base64 encoded key material, such as a symmetric key, that you want to manage in the service. For more information, see <a href="#encode-key-material-standard-key">Base64 encoding your key material</a>.</p>
          <p>Ensure that the key material meets the following requirements:</p>
          <p>
            <ul>
              <li>The key can be up to 7,500 bytes.</li>
              <li>The key must be base64-encoded.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td>Expiration date</td>
        <td>
          <p>(Optional) Set the date and time when the key gets expired. After the expiration date, the key moves into the <em>Deactivated</em> state. For more information about key state, see <a href="/docs/hs-crypto?topic=hs-crypto-key-states">Monitoring the lifecycle of encryption keys</a>.</p>
        </td>
      </tr>
      <tr>
        <td>Description</td>
        <td>
          <p>(Optional) Add an extended description for your key. It needs to be two to 240 characters in length.</p>
        </td>
      </tr>
      <caption>Table 1. Describes the <strong>Generate new key</strong> settings</caption>
    </table>

5. When you finish filling out the key's details, click **Import key** to confirm.

## Importing standard keys with the API
{: #import-standard-key-api}

Import a standard key by making a `POST` call to the following endpoint:

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

1. Call the [{{site.data.keyword.hscrypto}} key management service API](/apidocs/hs-crypto){: external} with the following cURL command.

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
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>Optional: A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns only the key metadata, such as the key name and ID value, in the response entity-body. When you set the variable to <code>return=representation</code>, the service returns both the key material and the key metadata.</p></td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>A unique, human-readable name for easy identification of your key.</p>
          <p>Important: To protect your privacy, do not store your personal data as metadata for your key.</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>Optional: An extended description of your key.</p>
          <p>Important: To protect your privacy, do not store your personal data as metadata for your key.</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>Optional: The date and time that the key expires in the system, in RFC 3339 format. If the <code>expirationDate</code> attribute is omitted, the key does not expire. </td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>The base64 encoded key material, such as a symmetric key, that you want to manage in the service. For more information, see <a href="#encode-key-material-standard-key">Base64 encoding your key material</a>.</p>
          <p>Ensure that the key material meets the following requirements:</p>
          <p>
            <ul>
              <li>The key can be up to 7,500 bytes.</li>
              <li>The key must be base64-encoded.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>A boolean value that determines whether the key material can leave the service.</p>
          <p>When you set the <code>extractable</code> attribute to <code>true</code>, the service designates the key as a standard key that you can store in your apps or services.</p>
        </td>
      </tr>
        <caption>Table 2. Describes the variables that are needed to add a standard key with the {{site.data.keyword.hscrypto}} key management service API</caption>
    </table>

    To protect the confidentiality of your personal data, avoid entering personally identifiable information (PII), such as your name or location, when you add keys to the service. For more examples of PII, see section 2.2 of the [NIST Special Publication 800-122](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: external}.
    {: tip}

    A successful `POST /v2/keys` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.hscrypto}} key management service API.

2. Optional: Verify that the key was added by running the following call to get the keys in your {{site.data.keyword.hscrypto}} service instance.

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

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>
          <varname>infile</varname>
        </td>
        <td>
          <p>
            The name of the file where your key material string resides.
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <varname>outfile</varname>
        </td>
        <td>
          <p>
            The name of the file where your base64-encoded key material is created when the command is run.
          </p>
        </td>
      </tr>
      <caption>
        Table 3. Describes the variables that are needed to base64 encode your key material.
      </caption>
    </table>

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

    Replace the variable in the example request according to the following table.

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>
          <varname>byte_length</varname>
        </td>
        <td>
          <p>
            The length of the key, which is measured in bytes. Acceptable byte length can be up to 7,500 bytes.
          </p>
        </td>
      </tr>
      <caption>
        Table 4. Describes the variable that is needed to create and encode new key material.
      </caption>
    </table>


## What's next
{: #import-standard-key-next}

To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management service API reference doc](/apidocs/hs-crypto){: external}.
