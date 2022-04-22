---

copyright:
  years: 2018, 2022
lastupdated: "2022-04-21"

keywords: root key, wrap key, encrypt data encryption key, protect data encryption key, key wrap api

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:external: target="_blank" .external}
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Wrapping data encryption keys with root keys
{: #wrap-keys}

You can manage and protect your encryption keys with a [root key](#x6946961){: term} by using the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} key management service API, if you are a privileged user.
{: shortdesc}

When you wrap a [data encryption key (DEK)](#x4791827){: term} with a root key, {{site.data.keyword.hscrypto}} combines the strength of multiple algorithms to protect the privacy and the integrity of your encrypted data.

To learn how key wrapping helps you control the security of at-rest data in the cloud, see [Envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).

## Wrapping keys by using the API
{: #wrap-keys-api}

You can protect a specified data encryption key (DEK) with a root key that you manage in {{site.data.keyword.hscrypto}}.

When you supply a root key for wrapping, ensure that the root key is 128, 192, or 256 bits so that the wrap call can succeed. If you create a root key in the service, {{site.data.keyword.hscrypto}} generates a 256-bit key from the HSMs, supported by the AES-CBC algorithm.

[After you designate a root key in the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys), you can wrap a DEK with advanced encryption by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/wrap
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service.](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api)

2. Copy the key material of the DEK that you want to manage and protect.

    If you have manager or writer privileges for your {{site.data.keyword.hscrypto}} service instance, [you can retrieve the key material for a specific key by making a `GET /v2/keys/<key_ID>` request](/docs/hs-crypto?topic=hs-crypto-view-keys#view-key-api).

3. Copy the ID of the root key that you want to use for wrapping.

4. Run the following cURL command to protect the key with a wrap operation.

    ```sh
    curl -X POST \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'x-kms-key-ring: <key_ring_ID>' \
      -H 'correlation-id: <correlation_ID>' \
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
        <td><strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier for the root key that you want to use for wrapping.</td>
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
        <td>
          <varname>key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. It is therefore suggested to specify the key ring ID for a more optimized request.
          </p>
          <p>
            Note: The key ring ID of keys that are created without an <code>x-kms-key-ring</code> header is: default.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-managing-key-rings">Managing key rings</a>.</p>
        </td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td><p>
          The key material of the DEK that you want to manage and protect. The <code>plaintext</code> value must be base64 encoded.
        </p>
        <p>For more information about encoding your key material, see <a href="/docs/key-protect?topic=key-protect-import-root-keys#open-ssl-encoding-root-new-key-material">Encoding your key material</a>.</p>
        <p>
          To generate a new DEK, omit the <code>plaintext</code> attribute. The service generates a random plaintext (32 bytes), wraps that value, and then returns both the generated and wrapped values in the response. The generated and wrapped values are base64 encoded and you will need to decode them in order to decrypt the keys.
        </p></td>
      </tr>
      <caption>Table 1. Describes the variables that are needed to wrap a specified key in {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Your wrapped data encryption key, containing the base64 encoded key material, is returned in the response entity-body. The response body also contains the ID of the key version that was used to wrap the supplied plaintext. The following JSON object shows an example returned value.

    ```json
    {
      "ciphertext": "eyJjaXBoZXJ0ZXh0IjoiYmFzZTY0LWtleS1nb2VzLWhlcmUiLCJpdiI6IjRCSDlKREVmYU1RM3NHTGkiLCJ2ZXJzaW9uIjoiNC4wLjAiLCJoYW5kbGUiOiJ1dWlkLWdvZXMtaGVyZSJ9",
      "keyVersion": {
        "id": "02fd6835-6001-4482-a892-13bd2085f75d"
      }
    }
    ```
    {: screen}

    If you omit the `plaintext` attribute when you make the wrap request, the service returns both the generated data encryption key (DEK) and the wrapped DEK in base64 encoded format.

    ```json
    {
      "plaintext": "Rm91ciBzY29yZSBhbmQgc2V2ZW4geWVhcnMgYWdv",
      "ciphertext": "eyJjaXBoZXJ0ZXh0IjoiYmFzZTY0LWtleS1nb2VzLWhlcmUiLCJpdiI6IjRCSDlKREVmYU1RM3NHTGkiLCJ2ZXJzaW9uIjoiNC4wLjAiLCJoYW5kbGUiOiJ1dWlkLWdvZXMtaGVyZSJ9",
      "keyVersion": {
        "id": "12e8c9c2-a162-472d-b7d6-8b9a86b815a6"
      }
    }
    ```
    {: screen}

    The `plaintext` value represents the unwrapped DEK, and the `ciphertext` value represents the wrapped DEK and are both base64 encoded. The `keyVersion.id` value represents the version of the root key that was used for wrapping.

    If you want {{site.data.keyword.hscrypto}} to generate a new data encryption key (DEK) on your behalf, you can also pass in an empty body on a wrap request. Your generated DEK, containing the base64 encoded key material, is returned in the response entity-body, along with the wrapped DEK.
    {: tip}
