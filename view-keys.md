---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: view keys, key configuration, key type

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Viewing keys
{: #view-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a centralized system to view, manage, and audit your encryption keys. Audit your keys and access restrictions to keys to ensure the security of your resources.
{: shortdesc}

Audit your key configuration regularly:

- Examine when keys were created and determine whether it's time to rotate the key.
- Monitor API calls to {{site.data.keyword.hscrypto}} with {{site.data.keyword.cloudaccesstrailshort}}.
- Inspect which users have access to keys and if the level of access is appropriate.

For more information about auditing access to your resources, see [Managing user access with Cloud IAM](/docs/services/hs-crypto/manage-access.html).

## Viewing keys with the GUI
{: #view-key-gui}

If you prefer to inspect the keys in your service by using a graphical interface, you can use the {{site.data.keyword.hscrypto}} dashboard.

[After you create or import your existing keys into the service](/docs/services/hs-crypto/create-root-keys.html), complete the following steps to view your keys.

1. [Log in to the {{site.data.keyword.cloud_notm}} console ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/).
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
3. Browse the general characteristics of your keys from the application details page:

    <table>
      <tr>
        <th>Column</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>The unique, human-readable alias that was assigned to your key.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>A unique key ID that was assigned to your key by the {{site.data.keyword.hscrypto}} service. You can use the ID value to make calls to the service with the [{{site.data.keyword.hscrypto}} API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto).</td>
      </tr>
      <tr>
        <td>State</td>
        <td>The [key state](/docs/services/key-protect/concepts/key-states.html) based on [NIST Special Publication 800-57, Recommendation for Key Management ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf). These states include <i>Pre-active</i>, <i>Active</i>, <i>Deactivated</i>, and <i>Destroyed</i>.</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>The [key type](/docs/services/key-protect/concepts/envelope-encryption.html#key-types) that describes your key's designated purpose within the service.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the <b>Keys</b> table</caption>
    </table>

## Viewing keys with the API
{: #view-key-api}

You can retrieve the contents of your keys by using the {{site.data.keyword.hscrypto}} API.

### Retrieving a list of your keys
{: #retrieve-keys-api}

For a high-level view, you can browse keys that are managed in your provisioned instance of {{site.data.keyword.hscrypto}} by making a `GET` call to the following endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/services/hs-crypto/access-api.html).

2. Run the following cURL command to view general characteristics about your keys.

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
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
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 2. Describes the variables that are needed to view keys with the {{site.data.keyword.hscrypto}} API</caption>
    </table>

    A successful `GET /v2/keys` request returns a collection of keys that are available in your {{site.data.keyword.hscrypto}} service instance.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true,
          "imported": false
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {:screen}

    By default, `GET /keys` returns your first 2000 keys, but you can adjust this limit by using the `limit` parameter at query time. To learn more about `limit` and `offset`, see [Retrieving a subset of keys](#retrieve_subset_keys_api).
    {: tip}

### Retrieving a subset of keys
{: #retrieve-subset-keys-api}

By specifying the `limit` and `offset` parameters at query time, you can retrieve a subset of your keys, starting with the `offset` value that you specify.

For example, you might have 3000 total keys that are stored in your {{site.data.keyword.hscrypto}} service instance, but you want to retrieve keys 200 - 300 when you make a `GET /keys` request.

You can use the following example request to retrieve a different set of keys.

  ```cURL
  curl -X GET \
  https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys?offset=<offset>&limit=<limit> \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'correlation-id: <correlation_ID>' \
  ```
  {: codeblock}

  Replace the `limit` and `offset` variables in your request according to the following table.
  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><p><varname>offset</varname></p></td>
      <td>
        <p>Optional: The number of keys to skip.</p>
        <p>For example, if you have 50 keys in your instance, and you want to list keys 26 - 50, use
            <code>../keys?offset=25</code>. You can also pair <code>offset</code> with <code>limit</code> to page through your available resources.</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>limit</varname></p></td>
      <td>
        <p>Optional: The number of keys to retrieve.</p>
        <p>For example, if you have 100 keys in your instance, and you want to list only 10 keys, use
            <code>../keys?limit=10</code>. The maximum value for <code>limit</code> is 5000.</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">Table 2. Describes the <code>limit</code> and <code>offset</code> variables</caption>
  </table>

For usage notes, check out the following examples for setting your `limit` and `offset` query parameters.

<table>
  <tr>
    <th>URL</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>.../keys</code></td>
    <td>Lists all of your available resources, up to the first 2000 keys.</td>
  </tr>
  <tr>
    <td><code>.../keys?limit=10</code></td>
    <td>Lists the first 10 keys.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=25&limit=50</code></td>
    <td>Lists keys 26 - 50.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=3000&limit=50</code></td>
    <td>Lists keys 3001 - 3050.</td>
  </tr>
  <caption style="caption-side:bottom;">Table 3. Provides usage notes for the limit and offset query parameters</caption>
</table>

Offset is the location of a particular key in a data set. The `offset` value is zero-based, which means that the 10th encryption key in a data set is at offset 9.
{: tip}

### Retrieving a key by ID
{: #retrieve-key-api}

To view detailed information about a specific key, you can make a `GET` call to the following endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/services/hs-crypto/access-api.html).

2. Retrieve the ID of the key you would like to access or manage.

    The ID value is used to access detailed information about the key, such as the key material itself. You can retrieve the ID for a specified key by making a `GET /v2/keys` request, or by accessing the {{site.data.keyword.hscrypto}} GUI.

3. Run the following cURL command to get details about your key and the key material.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
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
        <td>The region abbreviation, such as <code>us-south</code> or <code>eu-gb</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. See <a href="/docs/services/hs-crypto/regions.html#endpoints">Regional service endpoints</a> for more information.</td>
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
        <td>Optional: The unique identifier that is used to track and correlate transactions.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>The identifier for the key that you retrieved in [step 1](#retrieve-keys-api).</td>
      </tr>
      <caption style="caption-side:bottom;">Table 4. Describes the variables that are needed to view a specified key with the {{site.data.keyword.hscrypto}} API</caption>
    </table>

    A successful `GET v2/keys/<key_ID>` response returns details about your key and the key material. The following JSON object shows an example returned value for a standard key.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
        "resources": [
        {
            "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true,
            "imported": false
        }
      ]
    }
    ```
    {:screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.hscrypto}} [REST API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
