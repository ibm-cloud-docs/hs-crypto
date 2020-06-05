---

copyright:
  years: 2018, 2020
lastupdated: "2020-05-27"

keywords: rewrap key, reencrypt data encryption key, rewrap api, key id

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Rewrapping data encryption keys with root keys
{: #rewrap-keys}

Reencrypt your data encryption keys by using the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

When you [rotate a root key in {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-rotate-keys), new cryptographic key material becomes available for protecting the data encryption keys (DEKs) that are associated with the root key. With the rewrap API, you can reencrypt or rewrap your DEKS without exposing the keys in their plaintext form.

To learn how envelope encryption helps you control the security of at-rest data in the cloud, see [Protecting data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).

## Rewrapping keys by using the API
{: #rewrap-key-api}

You can reencrypt a specified data encryption key (DEK) with a root key that you manage in {{site.data.keyword.hscrypto}}, without exposing the DEK in its plaintext form.

Rewrapping keys works by combining `unwrap` and `wrap` calls to the service. For example, you can emulate a `rewrap` operation by first calling the `unwrap` API to access a DEK, and then calling the `wrap` API to reencrypt the DEK by using the newest root key material.
{: note}

[After you rotate a root key in the service](/docs/hs-crypto?topic=hs-crypto-rotate-keys), rewrap a data encryption key that is associated with the root key by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rewrap
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Copy the ID of the rotated root key that you used to perform the initial wrap request.

    You can retrieve the ID for a key by making a `GET api/v2/keys` request, or by viewing your keys in the {{site.data.keyword.hscrypto}} GUI.
3. Copy the `ciphertext` value that was returned during the latest wrap request.
4. Rewrap the key with the latest root key material by running the following cURL command.

    ```cURL
    curl -X POST \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rewrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
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
        <td><strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>eu-de</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
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
        <td><strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><varname>encrypted_data_key</varname></td>
        <td><strong>Required.</strong> The <code>ciphertext</code> value that was returned by the original wrap operation.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to rewrap keys in {site.data.keyword.hscrypto}}.</caption>
    </table>

    The newly wrapped data encryption key is returned in the response entity-body. The following JSON object shows an example returned value.

    ```
    {
      "ciphertext": "eyJjaXBoZXJ0ZXh0IjoiZkZ2T3VXM1lGSHJLTDNBeGxZUlJ4ZWlvdVl5bGs0d1M1NUlKQTBJWUdJdmxheEhmZloxYjh2VE5tNHc9IiwiaGFzaCI6ImVBaTNRcnUrbVRwMngvNjIxQW9KSW9CSWtLdkN5Nm9tUlg2TUZZS1BDb24zdnRrQ2xCOVBtL2VWazdTSWI2OW0wWVVYbE1ITEdPNVpldERQZjdlSjZRPT0iLCJpdiI6ImRyYURvRDhBbmFNTlJJYTJ1MG53WUE9PSIsInZlcnNpb24iOiIzLjAuMCIsImhhbmRsZSI6ImNiZTA4OTU4LWFlNzktNDJjMS1hYWNhLWVhY2U3NTM1ODc2OCJ9"
    }
    ```
    {:screen}

    Store and use the new `ciphertext` value for future envelope encryption operations so that your data is protected by the latest root key.


<!--
5. Optional. Verify that the key was successfully rewrapped by base64 decoding the `ciphertext` value.

    ```
    echo <ciphertext> | base64 --decode ; echo
    ```
    {: codeblock}

    Replace `<ciphertext>` with the base64 encoded value that was returned in the previous step. The following JSON object shows an example CLI output.

    ```
    {
      "ciphertext":"mIzRrwZAA8+WqRckG6gt1ji8HlEEJPSiV+TRBSR4GVr+FlAZlC5KvRriRF0=",
      "iv":"lbwxXlAW2DS7+5jGz5Y1Kg==",
      "version":"4.0.0",
      "handle":"8e309bae-b3ec-4270-9b87-89f8697fe54f"
    }
    ```
    {:screen}

    QUESTION: How do I know that the wDEK has been rewrapped? Does the version number change, or just the ciphertext value? What do the iv, version, and handle values represent (internal security parameters?)

-->
