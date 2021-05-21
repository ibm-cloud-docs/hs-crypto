---

copyright:
  years: 2018, 2021
lastupdated: "2021-05-17"

keywords: data encryption key, key material, unwrap call, unwrap key, decrypt key, decrypt data encryption key, access data encryption key, unwrap api

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:external: target="_blank" .external}
{:term: .term}

# Unwrapping data encryption keys with root keys
{: #unwrap-keys}

You can unwrap a [data encryption key (DEK)](#x4791827){: term} to access the contents by using the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} key management API, if you are a privileged user. Unwrapping a DEK decrypts and checks the integrity of the contents, returning the original key material to your {{site.data.keyword.cloud_notm}} data service.
{: shortdesc}

To learn how key wrapping helps you control the security of at-rest data in the cloud, see [Envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).

## Unwrapping keys by using the API
{: #unwrap-key-api}

[After you make a wrap call to the service](/docs/hs-crypto?topic=hs-crypto-wrap-keys), you can unwrap a specified data encryption key (DEK) to access the contents by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/unwrap
```
{: codeblock}

Root keys that contain the same key material can unwrap the same data encryption key (WDEK).
{: note}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Copy the ID of the [root key](#x6946961){: term} that you used to perform the initial wrap request.

    You can retrieve the ID for a key by making a `GET /v2/keys` request, or by viewing your keys in the {{site.data.keyword.cloud_notm}} console.

3. Copy the `ciphertext` value that was returned during the initial wrap request.

4. Run the following cURL command to decrypt and authenticate the key material.

    ```sh
    curl -X POST \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'x-kms-key-ring: <key_ring_ID>' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
      "ciphertext": "<encrypted_data_key>"
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
        <td><strong>Required.</strong> The unique identifier for the root key that you used for the initial wrap request.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier that is assigned to your{{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td>
          <varname>key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} searches for the key in every key ring that is associated with the specified instance. It is suggested to specify the key ring ID for a more optimized request.
          </p>
          <p>
            Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default.
          </p>
          <p>
            For more information, see
            [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings).
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><varname>encrypted_data_key</varname></td>
        <td>The <code>ciphertext</code> value that was returned during a wrap operation.</td>
      </tr>
      <caption>Table 1. Describes the variables that are needed to unwrap keys in {{site.data.keyword.hscrypto}}.</caption>
    </table>

    The original key material is returned in the response entity-body. The response body also contains the ID of the key version that was used to unwrap the supplied ciphertext. The following JSON object shows a sample returned value.

    ```json
    {
      "plaintext": "Rm91ciBzY29yZSBhbmQgc2V2ZW4geWVhcnMgYWdv",
      "keyVersion": {
        "id": "02fd6835-6001-4482-a892-13bd2085f75d"
      }
    }
    ```
    {: screen}

    If {{site.data.keyword.hscrypto}} detects that you rotated
    the root key that is used to unwrap and access your data, the service also returns a newly wrapped data encryption key (`ciphertext`) in the unwrap response body. The latest key version (`rewrappedKeyVersion`) that is associated with the new `ciphertext` is also returned. Store and use the new
    `ciphertext` value for future envelope encryption operations so that your data is protected by the latest root key.

## Decoding your key material
{: #how-to-decode-key-material}

When you unwrap a data encryption key, the key material is returned in base64 encoding. You need to decode the key before you encrypt it.

### Using OpenSSL to decode key material
{: #open-ssl-encoding-root-unwrap}

1. Download and install [OpenSSL](https://github.com/openssl/openssl#for-production-use){: external}.
2. Base64 encode your key material string by running the following command:

  ```
  $ openssl base64 -d -in <infile> -out <outfile>
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
          The name of the file where your base64 encoded key material string resides.
        </p>
      </td>
    </tr>
    <tr>
      <td>
        <varname>outfile</varname>
      </td>
      <td>
        <p>
          The name of the file where your decoded key material is
          outputted after the command is run.
        </p>
      </td>
    </tr>

    <caption>
      Table 2. Describes the variables that are needed to decode your key material.
    </caption>
  </table>

  If you want to output the decoded material in the command line directly rather than a file, run command `openssl enc -base64 -d <<< '<key_material_string>'`, where key_material_string is the returned plaintext from your unwrap request.
