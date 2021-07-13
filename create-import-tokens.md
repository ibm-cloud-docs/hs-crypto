---

copyright:
  years: 2018, 2021
lastupdated: "2021-07-13"

keywords: create import token, secure import, key material, key wrapping key, import token api, bring your own key, byok

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

# Creating import tokens
{: #create-import-tokens}

You can enable the secure import of root key material to the cloud by first creating an import token for your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} service instance.
{: shortdesc}

Import tokens are used to encrypt and securely bring root key material into {{site.data.keyword.hscrypto}} based on the policies that you specify. To learn more about importing your keys securely to the cloud, see [Bringing your encryption keys to the cloud](/docs/hs-crypto?topic=hs-crypto-importing-keys).

## Creating an import token with the API
{: #create-import-token-api}

Create an import token that's associated with your {{site.data.keyword.hscrypto}} service instance by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/import_token
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Set a policy for your import token by calling the [Key management API](https://{DomainName}/apidocs/hs-crypto){: external}.

    ```cURL
    curl -X POST \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/import_token \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/json' \
      -d '{
     "expiration": <expiration_time>,  \
     "maxAllowedRetrievals": <use_count>  \
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
          <td><varname>IAM_token</varname></td>
          <td><strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
        </tr>
        <tr>
          <td><varname>instance_ID</varname></td>
          <td><strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an instance ID</a>.</td>
        </tr>
        <tr>
          <td><varname>expiration_time</varname></td>
          <td>
            <p>The time in seconds from the creation of an import token that determines how long it remains valid.</p>
            <p>The minimum value is 300 seconds (5 minutes), and the maximum value is 86400 (24 hours). The default value is 600 (10 minutes).</p>
          </td>
        </tr>
        <tr>
          <td><varname>use_count</varname></td>
          <td>The number of times that an import token can be retrieved within the expiration time before it is no longer accessible. The default value is 1.</td>
        </tr>
          <caption>Table 1. Describes the variables that are needed to create an import token with the Key management API</caption>
      </table>

    A successful `POST api/v2/import_token` request creates an import token for your service instance. The response body contains the metadata that is associated with your import token, such as the creation date and policy details. The following snippet shows example output.

    ```json
    {
      "creationDate": "2019-04-08T16:58:29Z",
      "expirationDate": "2019-04-08T17:18:29Z",
      "maxAllowedRetrievals": 1,
      "remainingRetrievals": 1
    }
    ```
    {: screen}

## Creating an import token with the CLI
{: #create-import-token-cli}

Complete the following steps to create an import token using the {{site.data.keyword.keymanagementserviceshort}} CLI, which is integrated in {{site.data.keyword.hscrypto}}:

1. [Set up the {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli).

2. Create an import token with the following command:

  ```
  ibmcloud kp import-token create
  ```
  {:pre}

  You can find more parameters for this command in the [{{site.data.keyword.keymanagementserviceshort}} CLI reference](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference#kp-import-token-create).

## Retrieving an import token with the API
{: #retrieve-import-token-api}

Retrieve the import token that's associated with your {{site.data.keyword.hscrypto}} service instance by making a `GET` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/import_token
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Retrieve the import token that is associated with your service instance by calling the [Key management API](https://{DomainName}/apidocs/hs-crypto){: external}.

    ```cURL
    curl -X GET \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/import_token \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
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
          <td><varname>IAM_token</varname></td>
          <td><strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
        </tr>
        <tr>
          <td><varname>instance_ID</varname></td>
          <td><strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
        </tr>
        <caption>Table 1. Describes the variables that are needed to retrieve an import token with the key management API</caption>
      </table>

    A successful `GET api/v2/import_token` request retrieves the import token for your service instance. The response body contains the metadata that is associated with your import token, such as the creation date and policy details. The following snippet shows example output with truncated values.

    ```json
    {
      "creationDate": "2019-04-08T16:58:29Z",
      "expirationDate": "2019-04-08T17:18:29Z",
      "maxAllowedRetrievals": 1,
      "remainingRetrievals": 0,
      "payload": "MIICIjANBgkqhkiG...",
      "nonce": "8zJE9pKVdXVe/nLb"
    }
    ```
    {: screen}

    The response body also contains the public encryption key that you can use to [encrypt a root key](/docs/hs-crypto?topic=hs-crypto-importing-keys#using-import-tokens) before you upload the key material to a {{site.data.keyword.hscrypto}} service instance.

    In the example, the `payload` value represents the public key that is associated with the import token. This value is base64 encoded. For extra security, {{site.data.keyword.hscrypto}} also provides a `nonce` value that is used to verify the originality of a key import request to the service. To learn more about how to use these values, check out [Tutorial: Creating and importing encryption keys](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys).

## Retrieving an import token with the CLI
{: #retrieve-import-token-cli}

Complete the following steps to retrieve an import token using the {{site.data.keyword.keymanagementserviceshort}} CLI, which is integrated in {{site.data.keyword.hscrypto}}:

1. [Set up the {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli).

2. Retrieve an import token with the following command:

  ```
  ibmcloud kp import-token show
  ```
  {:pre}

  You can find more parameters for this command in the [{{site.data.keyword.keymanagementserviceshort}} CLI reference](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference#kp-import-token-show).

## What's next
{: #create-import-token-next-steps}

- To find out more about using an import token to securely bring encryption keys to {{site.data.keyword.cloud_notm}}, check out [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys).
- For a guided tutorial on using import tokens in {{site.data.keyword.hscrypto}}, see [Tutorial: Creating and importing encryption keys](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys).
