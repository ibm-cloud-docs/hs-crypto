---

copyright:
  years: 2018, 2020
lastupdated: "2020-05-27"

keywords: root key, wrap key, encrypt data encryption key, protect data encryption key, key wrap api

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:external: target="_blank" .external}
{:term: .term}

# Wrapping data encryption keys with root keys
{: #wrap-keys}

You can manage and protect your encryption keys with a [root key](#x6946961){: term} by using the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} key management API, if you are a privileged user.
{: shortdesc}

When you wrap a [data encryption key (DEK)](#x4791827){: term} with a root key, {{site.data.keyword.hscrypto}}
 combines the strength of multiple algorithms to protect the privacy and the integrity of your encrypted data.

To learn how key wrapping helps you control the security of at-rest data in the cloud, see [Envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).

## Wrapping keys by using the API
{: #wrap-keys-api}

You can protect a specified data encryption key (DEK) with a root key that you manage in {{site.data.keyword.hscrypto}}
.

When you supply a root key for wrapping, ensure that the root key is 128, 192, or 256 bits so that the wrap call can succeed. If you create a root key in the service, {{site.data.keyword.hscrypto}}
 generates a 256-bit key from its HSMs, supported by the AES-CBC algorithm.

[After you designate a root key in the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys), you can wrap a DEK with advanced encryption by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api)

2. Copy the key material of the DEK that you want to manage and protect.

    If you have manager or writer privileges for your {{site.data.keyword.hscrypto}}
 service instance, [you can retrieve the key material for a specific key by making a `GET /v2/keys/<key_ID>` request](/docs/hs-crypto?topic=hs-crypto-view-keys#view-key-api).

3. Copy the ID of the root key that you want to use for wrapping.

4. Run the following cURL command to protect the key with a wrap operation.

    ```cURL
    curl -X POST \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>"
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
        <td>The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}}
 service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>The unique identifier for the root key that you want to use for wrapping.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.hscrypto}}
 service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
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
        <td><varname>data_key</varname></td>
        <td>Optional: The key material of the DEK that you want to manage and protect. The <code>plaintext</code> value must be base64 encoded. To generate a new DEK, omit the <code>plaintext</code> attribute. The service generates a random plaintext (32 bytes) and wraps that value.</td>
      </tr>
      <!--
      <tr>
        <td><varname>additional_data</varname></td>
        <td>Optional: The additional authentication data (AAD) that is used to further secure the key. Each string can hold up to 255 characters. If you supply AAD when you make a wrap call to the service, you must specify the same AAD during the subsequent unwrap call.<br></br>Important: The {{site.data.keyword.hscrypto}} service does not save additional authentication data. If you supply AAD, save the data to a secure location to ensure that you can access and provide the same AAD during subsequent unwrap requests.</td>
      </tr>
      -->
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to wrap a specified key in {{site.data.keyword.hscrypto}}
.</caption>
    </table>

    Your wrapped key, containing the base64 encoded key material, is returned in the response entity-body. The following JSON object shows an example returned value.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
    }
    ```
    {:screen}
