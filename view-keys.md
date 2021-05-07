---

copyright:
  years: 2018, 2021
lastupdated: "2021-05-07"

keywords: view key, key configuration, key type, key metadata, list encryption key, view encryption key, retrieve encryption key, retrieve key api

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:external: target="_blank" .external}

# Viewing a list of root keys or standard keys
{: #view-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a centralized system to view, manage, and audit your encryption keys. Audit your keys and access restrictions to keys to ensure the security of your resources.
{: shortdesc}

Audit your key configuration regularly:

- Examine when keys were created and determine whether it's time to rotate the key.
- [Monitor API calls to {{site.data.keyword.hscrypto}} with {{site.data.keyword.cloudaccesstrailshort}}](/docs/hs-crypto?topic=hs-crypto-at-events).
- Inspect which users have access to keys and if the level of access is appropriate.

For more information about auditing access to your resources, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).

## Viewing root keys or standard keys with the console
{: #view-key-gui}

If you prefer to inspect the keys in your service by using a graphical interface, you can use the {{site.data.keyword.cloud_notm}} console.

[After you create or import your existing keys into the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys), complete the following steps to view your keys.

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **Key management service keys** page, browse the general characteristics of your keys in the **Keys** table:

    <table>
      <tr>
        <th>Column</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>The unique, human-readable name that was assigned to your key.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>A unique key ID that was assigned to your key by the {{site.data.keyword.hscrypto}} service. You can use the ID value to make calls to the service with the [{{site.data.keyword.hscrypto}} key management API](https://{DomainName}/apidocs/hs-crypto).</td>
      </tr>
      <tr>
        <td>Alias</td>
        <td>The human-readable aliases that you specify for easy recognition when you create the key.</td>
      </tr>
      <tr>
        <td>Ker ring ID</td>
        <td>The key ring that the key belongs to.</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>The type of key that describes your key's designated purpose within the service.</td>
      </tr>
      <tr>
        <td>State</td>
        <td>The [key state](/docs/hs-crypto?topic=hs-crypto-key-states) based on [NIST Special Publication 800-57, Recommendation for Key Management](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0). These states include <em>Pre-active</em>, <em>Active</em>, <em>Suspended</em>, <em>Deactivated</em>, and <em>Destroyed</em>.</td>
      </tr>
      <tr>
        <td>Origin</td>
        <td>Indicates whether the key is imported. `Created` indicates that the key is created by the service instance; `Imported` indicates that the key is imported by the user.</td>
      </tr>
      <tr>
        <td>Last updated</td>
        <td>The date and time that the key was last updated. This field gets updated when the key is created, rotated, or any part of the key metadata is modified. </td>
      </tr>
      <tr>
        <td>Last rotated</td>
        <td>The date and time that the key was last rotated. </td>
      </tr>
      <tr>
        <td>Created</td>
        <td>The date and time that the key was created.</td>
      </tr>
      <tr>
        <td>Dual authorization enabled</td>
        <td>The status of a dual authorization policy on the key. <ul><li>`True`: Dual authorization is required to delete the key.</li> <li>`False`: No prior authorization is required to delete the key.</li></ul></td>
      </tr>
      <tr>
        <td>Set for deletion</td>
        <td>Indicates if a delete authorization is issued for a key. <ul><li>`True`: An authorization to delete this key is issued by the first user. A second user with a Manager access policy can safely delete the key.</li> <li>`False`: The key is not set for deletion. No further action is needed. </li></ul> </td>
      </tr>
      <tr>
        <td>Deletion expiration</td>
        <td>The date that an authorization for deletion expires for the key. If this date passes, the authorization is no longer valid. If `False` is the value for the `Dual authorization enabled` or `Set for deletion` column of the key, the `Deletion expiration` column is left empty.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the <strong>Keys</strong> table</caption>
    </table>

    Not all key characteristics are displayed by default. To customize how the **Keys** table is to be presented, click the **Settings** icon and check the columns to be displayed.
    {: tip}

    Not seeing the full list of keys that are stored in your service instance?
    Verify with your administrator that you are assigned the correct role for
    the applicable service instance or individual key. For more information
    about roles, see
    [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).

    You can also search for a specific key by using the search bar, or filter keys based on your needs by clicking the **Filter** icon in the **Keys** table.
    {: tip}

## Viewing root keys or standard keys with the key management API
{: #view-key-api}

You can retrieve the contents of your keys by using the {{site.data.keyword.hscrypto}} key management API.

### Retrieving a list of your root keys or standard keys
{: #retrieve-keys-api}

For a high-level view, you can browse your root keys or standard keys that are managed in your provisioned instance of {{site.data.keyword.hscrypto}} by making a `GET` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. View general characteristics about your keys by running the following cURL command.

    ```sh
    curl -X GET \
    "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys" \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'x-kms-key-ring: <key_ring_ID>' \
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
        <td>The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td>
          <varname>key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. It is therefore recommended to specify the key ring ID for a more optimized request.
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
      <caption style="caption-side:bottom;">Table 2. Describes the variables that are needed to view keys with the {{site.data.keyword.hscrypto}} key management API</caption>
    </table>

    A successful `GET /v2/keys` request returns a collection of keys that are available in your {{site.data.keyword.hscrypto}} instance.

    ```json
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 2
      },
      "resources": [
        {
          "id": "02fd6835-6001-4482-a892-13bd2085f75d",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root-key",
          "state": 1,
          "crn": "crn:v1:bluemix:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
          "createdBy": "...",
          "creationDate": "2020-03-11T16:30:06Z",
          "lastUpdateDate": "2020-03-11T16:30:06Z",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "CBC_PAD"
          },
          "extractable": false,
          "imported": true,
          "algorithmMode": "CBC_PAD",
          "algorithmBitSize": 256,
          "dualAuthDelete": {
            "enabled": false
          }
        },
        {
          "id": "2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard-key",
          "state": 1,
          "crn": "crn:v1:bluemix:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:30372f20-d9f1-40b3-b486-a709e1932c9c:key:2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
          "createdBy": "...",
          "creationDate": "2020-03-12T03:50:12Z",
          "lastUpdateDate": "2020-03-12T03:50:12Z",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "CBC_PAD"
          },
          "extractable": true,
          "imported": false,
          "algorithmMode": "CBC_PAD",
          "algorithmBitSize": 256,
          "dualAuthDelete": {
            "enabled": false
          }
        }
      ]
    }
    ```
    {: screen}

    By default, `GET api/v2/keys` returns your first 200 keys, but you can adjust this limit by using the `limit` parameter at query time. To learn more about `limit` and `offset`, see
    [Retrieving a subset of keys](#retrieve-subset-keys-api).

    Not seeing the full list of keys? You might need to use `limit` and `offset`
    or check with your administrator to ensure you're assigned the correct level
    access to keys in your instance. To learn more, see
    [Unable to view or list keys](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-list-keys-api).
    {: tip}

### Retrieving a subset of keys
{: #retrieve-subset-keys-api}

By specifying the `limit` and `offset` parameters at query time, you can retrieve a subset of your keys, starting with the `offset` value that you specify.

For example, you might have 3000 total keys that are stored in your {{site.data.keyword.hscrypto}} service instance, but you want to retrieve keys 200 - 300 when you make a `GET /keys` request.

You can use the following example request to retrieve a different set of keys.

```cURL
curl -X GET \
  'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys?offset=<offset>&limit=<limit>' \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>'
```
{: codeblock}

Replace the `limit` and `offset` variables in your request according to the
following table.

<table>
  <tr>
    <th>Variable</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>
      <varname>offset</varname>
    </td>
    <td>
      <p>
        The number of keys to skip.
      </p>
      <p>
        For example, if you have 50 keys in your instance, and you want to list keys 26 - 50, use <code>../keys?offset=25</code>. You can also pair <code>offset</code> with <code>limit</code> to page through your available resources.
      </p>
    </td>
  </tr>

  <tr>
    <td>
      <varname>limit</varname>
    </td>
    <td>
      <p>
        The number of keys to retrieve.
      </p>
      <p>
        For example, if you have 100 keys in your instance, and you want to list only 10 keys, use <code>../keys?limit=10</code>. The maximum value for <code>limit</code> is 5000.
      </p>
    </td>
  </tr>

  <caption style="caption-side:bottom;">
    Table 2. Describes the <code>limit</code> and <code>offset</code> variables
  </caption>
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
    <td>Lists keys 26 - 75.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=3000&limit=50</code></td>
    <td>Lists keys 3001 - 3050.</td>
  </tr>
  <caption style="caption-side:bottom;">Table 3. Provides usage notes for the limit and offset query parameters</caption>
</table>

Offset is the location of a particular key in a data set. The `offset` value is zero-based, which means that the 10th encryption key in a data set is at offset 9.
{: tip}

### Retrieving keys by state
{: #filter-keys-state-api}

By specifying the `state` parameter at query time, you can retrieve keys that are in the states that you specify.

For example, you might have keys in your service instance that are in the active, suspended, and destroyed states, but you only want to retrieve keys in the active state when you make a `GET /keys` request.

The state query parameter takes in a list of integers from 0 to 5 delimited by commas with no whitespace or trailing commas. Valid states are based on NIST SP 800-57. For more information about key states, see [Key states and transitions](/docs/hs-crypto?topic=hs-crypto-key-states).
{: note}

You can use the following example request to retrieve a different set of keys.

```cURL
curl -X GET \
  'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys?state=<state_integers>' \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>'
```
{: codeblock}

Replace the `state` variable in your request according to the following table.

<table>
  <tr>
    <th>Variable</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>
      <varname>state</varname>
    </td>
    <td>
      <p>
        The states of the keys to be retrieved. States are integers and
        correspond to the Pre-activation = 0, Active = 1, Suspended = 2,
        Deactivated = 3, and Destroyed = 5 values.
      </p>
      <p>
        For example, if you want to only list keys in the active state in your
        service instance, use <code>../keys?state=1</code>. You can also pair
        <code>state</code> with<code>offset</code> with <code>limit</code> to
        page through your available resources.
      </p>
    </td>
  </tr>

  <caption style="caption-side:bottom;">
    Table 4. Describes the <code>state</code> variable.
  </caption>
</table>

For usage notes, check out the following examples for setting your `state` query
parameter.

<table>
  <tr>
    <th>URL</th>
    <th>Description</th>
  </tr>

  <tr>
    <td>
      <code>.../keys</code>
    </td>
    <td>
      Lists all of your available resources, up to the first 200 keys.
    </td>
  </tr>

  <tr>
    <td>
      <code>.../keys?state=5</code>
    </td>
    <td>
      Lists keys in the deleted state.
    </td>
  </tr>

  <tr>
    <td>
      <code>.../keys?state=2,3</code>
    </td>
    <td>
      Lists keys in the suspended and deactivated state.
    </td>
  </tr>

  <caption style="caption-side:bottom;">
    Table 5. Provides usage notes for the stage query parameter.
  </caption>
</table>
