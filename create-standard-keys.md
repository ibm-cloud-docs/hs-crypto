---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: standard keys, standard encryption key, creating standard keys, create standard keys

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Creating standard keys
{: #create-standard-keys}

You can create a standard encryption key with the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} GUI, or programmatically with the {{site.data.keyword.hscrypto}} API.
{: shortdesc}

## Creating standard keys with the GUI
{: #standard-key-gui}

[After you create an instance of the service](/docs/services/hs-crypto/provision.html), complete the following steps to create a standard key with the {{site.data.keyword.hscrypto}} GUI.

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/){: new_window}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. To create a new key, click **Add key** and select the **Create a key** window.

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
      <tr></tr>
        <td>Key type</td>
        <td>The <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">type of key</a> that you would like to manage in {{site.data.keyword.hscrypto}}. From the list of key types, select <b>Standard key</b>.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the <b>Generate new key</b> settings</caption>
    </table>

5. When you are finished filling out the key's details, click **Create key** to confirm.

## Creating standard keys with the API

Create a standard key by making a `POST` call to the following endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/services/hs-crypto/access-api.html).

2. Call the [{{site.data.keyword.hscrypto}} API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window} with the following cURL command.

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
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
       "extractable": <key_type>
       }
     ]
    }'
    ```
    {: codeblock}

<!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
    {: tip} -->

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
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Retrieving an access token</a>.</td>
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
        <td><varname>key_type</varname></td>
        <td>
          <p>A boolean value that determines whether the key material can leave the service.</p>
          <p>When you set the <code>extractable</code> attribute to <code>true</code>, the service creates a standard key that you can store in your apps or services.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Table 2. Describes the variables that are needed to add a standard key with the {{site.data.keyword.hscrypto}} API</caption>
    </table>

    To protect the confidentiality of your personal data, avoid entering personally identifiable information (PII), such as your name or location, when you add keys to the service. For more examples of PII, see section 2.2 of the [NIST Special Publication 800-122 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    A successful `POST /v2/keys` response returns the ID value for your key, along with other metadata. The ID is a unique identifier that is assigned to your key and is used for subsequent calls to the {{site.data.keyword.hscrypto}} API.

3. Optional: Verify that the key was created by running the following call to get the keys in your {{site.data.keyword.hscrypto}} service instance.

    ```cURL
    curl -X GET \
      https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### What's next
{: #standard-key-next}

- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
