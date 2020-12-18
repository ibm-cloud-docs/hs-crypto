---

copyright:
  years: 2018, 2020
lastupdated: "2020-11-17"

keywords: rotate, rotate key, rotate encryption key, rotate root key, rotate root key manually, key rotation, rotate key api

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Rotating root keys manually
{: #rotate-keys}

You can rotate your [root keys](#x6946961){: term} on demand by using {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

When you rotate your root key, you shorten the lifetime of the key, and you limit the amount of information that is protected by that key.

To learn how key rotation helps you meet industry standards and cryptographic best practices, see [Key rotation](/docs/hs-crypto/concepts?topic=hs-crypto-key-rotation).

## Rotating root keys in the console
{: #rotate-root-key-gui}

If you prefer to rotate your root keys by using a graphical interface, you can use the {{site.data.keyword.cloud_notm}} console.

[After you create or import your existing root keys into the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys), complete the following steps to rotate a key:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **Key management service keys** page, use the **Keys** table to browse the keys in your service.
5. Select the key that you want to rotate and click the overflow icon (⋯) to open a list of options for the key.
6. From the options menu, click **Rotate key**.

    If you initially provided the key material for the key, specify the following details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key material</td>
        <td>
          <p>The new base64 encoded key material that you want to store and manage in the service.</p>
          <p>Ensure that the key material meets the following requirements:</p>
          <p>
            <ul>
              <li>The key must be 128, 192, or 256 bits.</li>
              <li>The bytes of data, for example 32 bytes for 256 bits, must be encoded by using base64 encoding.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the <b>Rotate key</b> settings</caption>
    </table>

7.  Click **Rotate key** to confirm.

## Rotating root keys with the API
{: #rotate-root-key-api}

You can rotate a root key by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/rotate
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api)

2. Copy the ID of the root key that you want to rotate.

    You can find the ID for a key in your service instance by [retrieving a list of your keys](/docs/hs-crypto?topic=hs-crypto-view-keys), or by accessing the {{site.data.keyword.cloud_notm}} console.

3. Replace the key with new key material by running the following cURL command.

    ```cURL
    curl -X POST \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <key_material>'
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
        <td><strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier for the root key that you want to rotate.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>The new base64 encoded key material that you want to store and manage in the service. This value is required if you initially imported the key material when you added the key to the service.</p>
          <p>To rotate a key that was initially generated by {{site.data.keyword.hscrypto}}, omit the <code>payload</code> attribute and pass an empty request entity-body. To rotate an imported key, provide a key material that meets the following requirements:</p>
          <p>
            <ul>
              <li>The key must be 128, 192, or 256 bits.</li>
              <li>The bytes of data, for example 32 bytes for 256 bits, must be encoded by using base64 encoding.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to rotate a specified key in {{site.data.keyword.hscrypto}}.</caption>
    </table>

    A successful rotation request returns an HTTP `204 No Content` response, which indicates that your root key was replaced by new key material.

4. Optional: Verify that the key was rotated by running the following call to browse the keys in your {{site.data.keyword.hscrypto}} service instance.

    ```cURL
    curl -X GET \
    https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    Review the `lastRotateDate` value in the response entity-body to inspect the date and time that your key was last rotated.

    ```json
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "type": "application/vnd.ibm.kms.key+json",
          "id": "02fd6835-6001-4482-a892-13bd2085f75d",
          "name": "test-root-key",
          "state": 1,
          "extractable": false,
          "crn": "crn:v1:bluemix:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
          "imported": false,
          "creationDate": "2020-03-12T03:50:12Z",
          "createdBy": "...",
          "algorithmType": "AES",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "CBC_PAD"
          },
          "algorithmBitSize": 256,
          "algorithmMode": "CBC_PAD",
          "lastUpdateDate": "2020-03-12T03:50:12Z",
          "lastRotateDate": "2020-03-12T03:49:01Z",
          "keyVersion": {
            "id": "2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
            "creationDate": "2020-03-12T03:50:12Z"
          },
          "dualAuthDelete": {
            "enabled": false
          },
          "deleted": false
        }
      ]
    }
    ```
    {: screen}

    The `keyVersion` attribute contains identifying information that describes the latest version of the root key.

    You can also list the versions that are available for the key by using the
    {{site.data.keyword.hscrypto}} key management API. To learn more, see
    [Viewing key versions](/docs/hs-crypto?topic=hs-crypto-view-key-versions).
    {: tip}


### Using an import token to rotate a key
{: #rotate-root-keys-secure-api}

If you initially imported a root key by using an import token, you can rotate the key by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/rotate
```

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To rotate a key, you must be assigned a _Writer_ or _Manager_ access policy for the instance or key. To learn how IAM roles map to {{site.data.keyword.hscrypto}} service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Retrieve the ID of the key that you want to rotate.

    You can retrieve the ID for a specified key by making a `GET /v2/keys` request, or by viewing your keys in the {{site.data.keyword.cloud_notm}} console.

3. [Create and retrieve an import token](/docs/hs-crypto?topic=hs-crypto-create-import-tokens).

4. Use the import token to encrypt the key material that you want to use to rotate the existing key.

   To learn how to use an import token, check out [Tutorial: Creating and importing encryption keys](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys).

5. Replace the existing key with new key material by running the following cURL command.

    ```cURL
    curl -X POST \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/rotate \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -d '{
      "type": "application/vnd.ibm.kms.key+json",
      "name": "<key_alias>",
      "description": "<key_description>",
      "extractable": <key_type>,
      "payload": "<encrypted_key>",
      "encryptionAlgorithm": "RSAES_OAEP_SHA_256",
      "encryptedNonce": "<encrypted_nonce>",
      "iv": "<iv>"
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
        <td><strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier for the key that you want to rotate.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instanc ID</a>.</td>
      </tr>
       <tr>
        <td><varname>key_alias</varname></td>
        <td><strong>Required.</strong> A unique, human-readable name for easy identification of your key. To protect your privacy, do not store your personal data as metadata for your key.</td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>An extended description of your key. To protect your privacy, do not store your personal data as metadata for your key.</td>
      </tr>
      <tr>
        <td><varname>encrypted_key</varname></td>
        <td>
          <p><strong>Required.</strong> The encrypted key material that you want to store and manage in the service. The value must be base64 encoded.</p>
          <p>Ensure that the key material meets the following requirements:</p>
          <p>
            <ul>
              <li>The key must be 128, 192, or 256 bits.</li>
              <li>The bytes of data, for example 32 bytes for 256 bits, must be encoded by using base64 encoding.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>A boolean value that determines whether the key material can leave the service.</p>
          <p>When you set the <code>extractable</code> attribute to <code>false</code>, the service designates the key as a root key that you can use for <code>wrap</code> or <code>unwrap</code> operations.</p>
        </td>
      </tr>
      <tr>
        <td><varname>encrypted_nonce</varname></td>
        <td>
          <p><strong>Required.</strong> The AES-GCM encrypted nonce that ensures that the bits you send as part of a request are exactly the same as what we receive. The nonce validates the key that you are restoring. To learn more, see <a href="/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-encrypt-nonce" target="_blank">Tutorial: Creating and importing encryption keys</a></p>
        </td>
      </tr>
       <tr>
        <td><varname>iv</varname></td>
        <td>
          <p><strong>Required.</strong> The initialization vector (IV) that is generated by the AES-GCM algorithm when you encrypt a nonce. This value is used to decode the key for storage in the {{site.data.keyword.hscrypto}} system. To learn more, see <a href="/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-encrypt-nonce" target="_blank">Tutorial: Creating and importing encryption keys</a></p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to restore keys with th{{site.data.keyword.hscrypto}} API.</caption>
    </table>

    A successful rotation request returns an HTTP `204 No Content` response, which indicates that your root key was replaced by the new key material.

6. Optional: Verify that the key was rotated by retrieving details about the key.

    ```cURL
    curl -X GET \
    https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_id>/metadata \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>'
    -H 'accept: application/vnd.ibm.kms.key+json'
    ```
    {: codeblock}

    Review the `lastRotateDate` and `keyVersion` values in the response entity-body to inspect the date and time that your key was last rotated.

    You can also list the versions that are available for the key by using the {{site.data.keyword.hscrypto}} API. To learn more, see [Viewing key versions](/docs/hs-crypto?topic=hs-crypto-view-key-versions).

## What's next
{: #rotate-key-next}

- After you rotate a root key, new cryptographic key material becomes available for protecting the data encryption keys (DEKs) that are associated with the root key. Learn how to reencrypt or rewrap your DEKS without exposing the keys in their plaintext form, see [Rewrapping keys](/docs/hs-crypto?topic=hs-crypto-rewrap-keys).
- To learn how envelope encryption helps you control the security of at-rest data in the cloud, see [Protecting data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
