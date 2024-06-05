---

copyright:
  years: 2018, 2024
lastupdated: "2024-06-04"

keywords: key versions, get key versions, list key versions

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Viewing root key versions
{: #view-key-versions}

View the versions that are associated with a root key by using
{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

When you rotate a root key, {{site.data.keyword.hscrypto}}
creates a new version of the key. As a security admin, you can audit the
rotation history of a root key by viewing the key version history.

Key versions are available only for root keys. To learn more about how key
rotation works in {{site.data.keyword.hscrypto}}, check out
[Comparing your key rotation options](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro#compare-key-rotation-options).
{: note}

## Viewing root key versions with the key management service API
{: #view-key-versions-api}

For a high-level view, you can list the versions that are associated with a root
key by making a `GET` call to the following endpoint.

{{site.data.keyword.hscrypto}} is continuously replacing port-based API endpoints with instance-based API endpoints. For example, for public key management endpoint URLs, the format is changed from `api.<region>.hs-crypto.cloud.ibm.com:<port>` to `<instance_ID>.api.<region>.hs-crypto.appdomain.cloud`. For a complete list of the endpoint URL schemes and more information about which regions now support instance-based endpoint URLs, see [Instance-based endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints). Note that, for any new service instances created after the dates specified in the table, only instance-based endpoint URLs can be applied. No impact to existing service instances is expected, as the current port-based endpoint scheme stays intact for the time being. However, it is suggested to use the new instance-based scheme wherever possible especially for new projects.
{: note}
 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/{id}/versions
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Retrieve the ID of the root key that you want to inspect.

    The ID value is used to access detailed information about the key. You can
    find the ID for a key in your service instance by
    [retrieving a list of your keys](/docs/hs-crypto?topic=hs-crypto-view-keys),
    or by accessing the UI.

3. Get a list of versions that are associated with the root key by running the following cURL command.

    ```sh
    curl -X GET \
      'https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/versions' \
      -H 'accept: application/vnd.ibm.kms.key.version+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'x-kms-key-ring: <key_ring_ID>' \
      -H 'bluemix-instance: <instance_ID>'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south` or `eu-de`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `key_ID` | **Required.** The unique identifier for the key that you want to inspect. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `key_ring_ID` | **Optional.** The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request. \n \n Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    {: caption="Table 1. Describes the variables needed to list key versions with the API" caption-side="bottom"}

    A successful `GET api/v2/keys/<key_ID>/versions` response returns the list
    of versions that are associated with the root key. The following JSON object
    shows an example returned value.

    ```json
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key.version+json",
        "collectionTotal": 2
      },
      "resources": [
        {
          "id": "02fd6835-6001-4482-a892-13bd2085f75d",
          "creationDate": "2020-03-05T16:39:25Z"
        },
        {
          "id": "12e8c9c2-a162-472d-b7d6-8b9a86b815a6",
          "creationDate": "2020-03-02T16:28:38Z"
        }
      ]
    }
    ```
    {: screen}

    The `resources` object lists each key version, along with the ID and
    creation date, in reverse chronological order.
