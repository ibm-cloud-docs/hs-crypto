---

copyright:
  years: 2018, 2024
lastupdated: "2024-07-01"

keywords: view key, key configuration, key type, key metadata, list encryption key, view encryption key, retrieve encryption key, retrieve key api

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Viewing a list of root keys or standard keys
{: #view-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a centralized system to view, manage, and audit your encryption keys. Audit your keys and access restrictions to keys to ensure the security of your resources.
{: shortdesc}

Audit your key configuration regularly:

- Examine when keys were created and determine whether it's time to rotate the key.
- [Monitor API calls to {{site.data.keyword.hscrypto}} with {{site.data.keyword.cloudaccesstrailshort}}](/docs/hs-crypto?topic=hs-crypto-at-events).
- Inspect which users have access to keys and if the level of access is appropriate.

For more information about auditing access to your resources, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).

## Viewing root keys or standard keys with the UI
{: #view-key-gui}
{: ui}

If you prefer to inspect the keys in your service by using a graphical interface, you can use the UI.

[After you create or import your existing keys into the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys), complete the following steps to view your keys.

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, browse the general characteristics of your keys in the **Keys** table:

    | Column | Description |
    | --- | --- |
    | Name | The unique, human-readable name that was assigned to your key. |
    | ID  | A unique key ID that was assigned to your key by the {{site.data.keyword.hscrypto}} service. You can use the ID value to make calls to the service with the [{{site.data.keyword.hscrypto}} key management service API](/apidocs/hs-crypto). |
    | Alias | The human-readable aliases that you specify for easy recognition when you create the key. |
    | Key ring ID | The key ring that the key belongs to. |
    | Type | The type of key that describes your key's designated purpose within the service. |
    | State | The [key state](/docs/hs-crypto?topic=hs-crypto-key-states) based on [NIST Special Publication 800-57, Recommendation for Key Management](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0). These states include Pre-active, Active, Suspended, Deactivated, and Destroyed. |
    | Origin | Indicates whether the key is imported. `Created` indicates that the key is created by the service instance; `Imported` indicates that the key is imported by the user. |
    | Last updated | The date and time that the key was last updated. This field gets updated when the key is created, rotated, or any part of the key metadata is modified. |
    | Last rotated | The date and time that the key was last rotated. |
    | Created | The date and time that the key was created. |
    | Dual authorization enabled | The status of a dual authorization policy on the key. \n * `True`: Dual authorization is required to delete the key. \n * `False`: No prior authorization is required to delete the key. |
    | Set for deletion | Indicates whether a delete authorization is issued for a key. \n * `True`: An authorization to delete this key is issued by the first user. A second user with a Manager access policy can safely delete the key. \n * `False`: The key is not set for deletion. No further action is needed. |
    | Deletion expiration | The date that an authorization for deletion expires for the key. If this date passes, the authorization is no longer valid. If `False` is the value for the `Dual authorization enabled` or `Set for deletion` column of the key, the `Deletion expiration` column is left empty. |
    {: caption="Table 1. Describes the table of keys" caption-side="bottom"}

    Not all key characteristics are displayed by default. To customize how the **Keys** table is to be presented, click the **Settings icon** ![Settings icon](../icons/settings.svg "Settings") and check the columns to be displayed.
    {: tip}

    Not seeing the full list of keys that are stored in your service instance?
    Verify with your administrator that you are assigned the correct role for
    the applicable service instance or individual key. For more information
    about roles, see
    [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).

    You can also search for a specific key by using the search bar, or filter keys based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Keys** table.
    {: tip}

## Viewing root keys or standard keys with the key management service API
{: #view-key-api}
{: api}

You can retrieve the contents of your keys by using the {{site.data.keyword.hscrypto}} key management service API.

### Retrieving a list of your root keys or standard keys
{: #retrieve-keys-api}

For a high-level view, you can browse your root keys or standard keys that are managed in your provisioned instance of {{site.data.keyword.hscrypto}} by making a `GET` call to the following endpoint.

 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. View general characteristics about your keys by running the following cURL command.

    ```sh
    curl -X GET \
    "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys" \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'x-kms-key-ring: <key_ring_ID>' \
    -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.
    
    | Variable | Description |
    | --- | --- |
    | `region` | The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `IAM_token` | Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `key_ring_ID` | **Optional.** The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request. \n \n Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | `correlation_ID` | **Optional.** The unique identifier that is used to track and correlate transactions. |
    {: caption="Table 2. Describes the variables needed to view keys with the API" caption-side="bottom"}

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
  'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys?offset=<offset>&limit=<limit>' \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>'
```
{: codeblock}

Replace the `limit` and `offset` variables in your request according to the
following table.

| Variable | Description |
| --- | --- |
| offset | The number of keys to skip. For example, if you have 50 keys in your instance, and you want to list keys 26 - 50, use `../keys?offset=25`. You can also pair `offset` with `limit` to page through your available resources. |
| limit | The number of keys to retrieve. For example, if you have 100 keys in your instance, and you want to list only 10 keys, use `../keys?limit=10`. The maximum value for `limit` is 5000. |
{: caption="Table 2. Describes the limit and offset variables" caption-side="bottom"}

For usage notes, check out the following examples for setting your `limit` and `offset` query parameters.

| URL | Description |
| --- | --- |
| `.../keys` | Lists all of your available resources, up to the first 2000 keys. |
| `.../keys?limit=10` | Lists the first 10 keys. |
| `.../keys?offset=25&limit=50` | Lists keys 26 - 75. |
| `.../keys?offset=3000&limit=50` | Lists keys 3001 - 3050. |
{: caption="Table 3. Provides usage notes for the limit and offset query parameters" caption-side="bottom"}

Offset is the location of a particular key in a data set. The `offset` value is zero-based, which means that the 10th encryption key in a data set is at offset 9.
{: tip}

### Retrieving keys by state
{: #filter-keys-state-api}

By specifying the `state` parameter at query time, you can retrieve keys that are in the states that you specify.

For example, you might have keys in your service instance that are in the active, suspended, and destroyed states, but you only want to retrieve keys in the active state when you make a `GET /keys` request.

The state query parameter takes in a list of integers 0 - 5 delimited by commas with no whitespace or trailing commas. Valid states are based on NIST SP 800-57. For more information about key states, see [Key states and transitions](/docs/hs-crypto?topic=hs-crypto-key-states).
{: note}

You can use the following example request to retrieve a different set of keys.

```cURL
curl -X GET \
  'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys?state=<state_integers>' \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>'
```
{: codeblock}

Replace the `state` variable in your request according to the following table.

| Variable | Description |
| --- | --- |
| `state` | The states of the keys to be retrieved. States are integers and correspond to the Pre-active = 0, Active = 1, Suspended = 2, Deactivated = 3, and Destroyed = 5 values. For example, if you want to only list keys in the active state in your service instance, use `../keys?state=1`. You can also pair `state` with`offset` with `limit` to page through your available resources. |
{: caption="Table 4. Describes the state variable" caption-side="bottom"}

For usage notes, check out the following examples for setting your `state` query
parameter.

| URL | Description |
| --- | --- |
| `.../keys` | Lists all of your available resources, up to the first 200 keys. |
| `.../keys?state=5` | Lists keys in the deleted state. |
| `.../keys?state=2,3` | Lists keys in the suspended and deactivated state. |
{: caption="Table 5. Provides usage notes for the stage query parameter" caption-side="bottom"}

### Retrieving keys by Extractable value
{: #filter-keys-extractable-state-api}
{: api}

By specifying the `extractable` parameter at query time, you can retrieve keys whose material can leave the service.

For example, you might have both standard and root keys in your {{site.data.keyword.hscrypto}} instance, but you only want to retrieve keys with extractable key material when you make a `GET /keys` request.

The extractable query parameter takes in a boolean.
{: note}

You can use the following example request to retrieve a different set of keys.

```sh
$ curl -X GET \
    "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys?extractable=<extractable>" \
    -H "accept: application/vnd.ibm.collection+json" \
    -H "authorization: Bearer <IAM_token>" \
    -H "bluemix-instance: <instance_ID>"
```
{: codeblock}

Replace the `extractable` variable in your request according to the following table.

|Variable|Description|
|--- |--- |
|extractable|The type of keys to be retrieved. Filters keys based on the extractable property. You can use this query parameter to search for keys whose material can leave the service. If you set the parameter to true, standard keys are retrieved. If you set the parameter to false, root keys are retrieved. If the parameter is omitted, both root and standard keys are retrieved. For example, if you want to only list keys with extractable material in your service instance, use `../keys?extractable=true`. You can also pair extractable with `offset`, `limit`, and `state` to page through your available resources.|
{: caption="Table 5. Describes the extractable variable" caption-side="top"}

For usage notes, check out the following examples for setting your `extractable` query parameter.

|URL|Description|
|--- |--- |
|`../keys`|Lists all of your available resources, up to the first 200 keys.|
|`../keys?extractable=true`|Lists standard keys.|
|`../keys?extractable=false`|Lists root keys.|
{: caption="Table 6. Provides usage notes for the extractable query parameter" caption-side="top"}

### Sorting a list of keys
{: #filter-keys-sort-api}
{: api}

Using the **`sort`** parameter in the query string [sorts the list of keys](/apidocs/hs-crypto#kms-get-key-sort-api) returned based on one or more key properties. To sort on a property in descending order, prefix the term with "-". To sort on multiple key properties, use a comma to separate each property. The first property in the comma-separated list is to be evaluated before the next. 

```sh
$ curl -X GET \
    "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys?sort=<sort-value>" \
    -H "accept: application/vnd.ibm.collection+json" \
    -H "authorization: Bearer <IAM_token>" \
    -H "bluemix-instance: <instance_ID>"
```
{: codeblock}

|Variable|Description|
|--- |--- |
| sort-value | The list of properties for sorting. The key properties that can be sorted at this time are:  \n \n- id \n- state \n- extractable \n- imported \n- creationDate \n- lastUpdateDate \n- lastRotateDate \n- deletionDate \n- expirationDate |
{: caption="Table 7. Usage notes for the sort query parameter" caption-side="top"}

