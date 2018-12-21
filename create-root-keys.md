---

copyright:
  years: 2017, 2018
lastupdated: "2018-10-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Creating root keys
{: #create-root-keys}

***Need to update the API endppoint***

You can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to create root keys by using the {{site.data.keyword.hscrypto}} GUI, or programmatically with the {{site.data.keyword.hscrypto}} API.
{: shortdesc}

Root keys are symmetric key-wrapping keys that are used to protect the security of encrypted data in the cloud. For more information about root keys, see [Envelope encryption](/docs/services/key-protect/concepts/envelope-encryption.html).

## Creating root keys with the GUI
{: #gui}

[After you create an instance of the service](/docs/services/hs-crypto/provision.html), complete the following steps to create a root key with the {{site.data.keyword.hscrypto}} GUI.

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/){: new_window}.
2. From your {{site.data.keyword.cloud_notm}} dashboard, select your provisioned instance of {{site.data.keyword.hscrypto}}.
3. To create a new key, click **Add key** and select the **Generate a new key** window.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name does not contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">type of key</a> that you would like to manage in {{site.data.keyword.hscrypto}. From the list of key types, select <b>Root key</b>.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the <b>Generate new key</b> settings</caption>
    </table>

4. When you are finished filling out the key's details, click **Generate key** to confirm.

## Creating root keys with the API
{: #api}

Create a root key by making a `POST` call to the following endpoint.

```
https://keyprotect.<region>.bluemix.net/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/services/{{site.data.keyword.hscrypto}}
hs-crypto/access-api.html).

2. Call the [{{site.data.keyword.hscrypto}} API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/hp-crypto){: new_window} with the following cURL command.

    ```cURL
    curl -X POST \
      https://keyprotect.<region>.bluemix.net/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
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
       "extractable": <key_type>
       }
     ]
    }'
    ```
    {: codeblock}

    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/hp-crypto){: new_window}.
    {: tip}

    Replace the variables in the example request according to the following table.
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>The region abbreviation, such as <code>us-south</code> or <code>eu-gb</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/services/hs-crypto/regions.html#endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/services/hs-crypto/access-api#retrieve-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>The unique identifier that is used to track and correlate transactions.</td>
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
        <td><varname>key_type</varname></td>
        <td>
          <p>A boolean value that determines whether the key material can leave the service.</p>
          <p>When you set the <code>extractable</code> attribute to <code>false</code>, the service creates a root key that you can use for <code>wrap</code> or <code>unwrap</code> operations.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to add a root key with the {{site.data.keyword.hscrypto}} API</caption>
    </table>

    To protect the confidentiality of your personal data, avoid entering personally identifiable information (PII), such as your name or location, when you add keys to the service. For more examples of PII, see section 2.2 of the [NIST Special Publication 800-122 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    A successful `POST /v2/keys` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.hscrypto}} API.

3. Optional: Verify that the key was created by running the following call to browse the keys in your {{site.data.keyword.hscrypto}} service instance.

    ```cURL
    curl -X GET \
      https://keyprotect.<region>.bluemix.net/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**Note:** After you create a root key with the service, the key stays within the bounds of {{site.data.keyword.hscrypto}}, and its key material cannot be retrieved.

### What's next

- To find out more about protecting keys with envelope encryption, check out [Wrapping keys](/docs/services/hs-crypto/wrap-keys.html).
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.bluemix.net/apidocs/hp-crypto){: new_window}.
