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

# Unwrapping keys
{: #unwrap-keys}

You can unwrap a data encryption key (DEK) to access its contents by using the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} API, if you are a privileged user. Unwrapping a DEK decrypts and checks the integrity of its contents, returning the original key material to your {{site.data.keyword.cloud_notm}} data service.
{: shortdesc}

To learn how key wrapping helps you control the security of at-rest data in the cloud, see [Envelope encryption](/docs/services/key-protect/concepts/envelope-encryption.html).

## Unwrapping keys by using the API
{: #api}

[After you make a wrap call to the service](/docs/services/hs-crypto/wrap-keys.html), you can unwrap a specified data encryption key (DEK) to access its contents by making a `POST` call to the following endpoint.

```
https://keyprotect.<region>.bluemix.net/api/v2/keys/<key_id>?action=unwrap
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/services/hs-crypto/access-api.html).

2. Copy the ID of the root key that you used to perform the initial wrap request.

    You can retrieve the ID for a key by making a `GET /v2/keys` request, or by viewing your keys in the {{site.data.keyword.hscrypto}} GUI.

3. Copy the `ciphertext` value that was returned during the initial wrap request.

4. Run the following cURL command to decrypt and authenticate the key material.

    ```cURL
    curl -X POST \
      'https://keyprotect.<region>.bluemix.net/api/v2/keys/<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
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
        <td><varname>key_ID</varname></td>
        <td>The unique identifier for the root key that you used for the initial wrap request.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>The unique identifier that is assigned to your{{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns only the key metadata, such as the key name and ID value, in the response entity-body. When you set the variable to <code>return=representation</code>, the service returns both the key material and the key metadata.</p></td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>Optional: The additional authentication data (AAD) that is used to further secure the key. Each string can hold up to 255 characters. If you supply AAD when you make a wrap call to the service, you must specify the same AAD during the unwrap call.</td>
      </tr>
      <tr>
        <td><varname>encrypted_data_key</varname></td>
        <td>The <code>ciphertext</code> value that was returned during a wrap operation.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to unwrap keys in {{site.data.keyword.hscrypto}}.</caption>
    </table>

    The original key material is returned in the response entity-body. The following JSON object shows an example returned value.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg=="
    }
    ```
    {:screen}
