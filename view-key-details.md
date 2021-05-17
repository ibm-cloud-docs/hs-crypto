---

copyright:
  years: 2018, 2021
lastupdated: "2021-05-17"

keywords: get details for a key, get key configuration, get details, view encryption key details, view encryption key, retrieve encryption key details, API examples

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
{:term: .term}

# Viewing details about a root key or a standard key
{: #view-key-details}

You can retrieve the general characteristics of a single encryption key by using
{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

Retrieving a root key or a standard key requires a _Writer_ or _Manager_ access policy, but you might
need a way to view only the details about a root key or a standard key, such as the transition history
or configuration, without retrieving the key itself. If you have _Reader_ access
permissions, you can use the {{site.data.keyword.hscrypto}} key management
API to retrieve only metadata about a root key or a standard key.

## Viewing key details with the {{site.data.keyword.cloud_notm}} console
{: #view-key-details-ui}

You can view details about a specific key with the {{site.data.keyword.cloud_notm}} console by completing the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **Key management service keys** page, use the **Keys** table to browse the keys in your service.
5. Click the overflow (...) icon to open a list of options for a specific key.
6. From the options menu, click **View key details** to view the details of the key.

## Viewing key details with the key management API
{: #view-key-details-api}

To view detailed information about a specific root key or a standard key, you can make a `GET` call to
the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID_or_alias>/metadata
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Retrieve the ID of the key that you would like to inspect.

    The ID value is used to access detailed information about the key. You can
    find the ID for a key in your service instance by
    [retrieving a list of your keys](/docs/hs-crypto?topic=hs-crypto-view-keys),
    or by accessing the {{site.data.keyword.cloud_notm}} console.

3. Get details about the key by running the following cURL command.

    ```sh
    curl -X GET \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID_or_alias>/metadata' \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'x-kms-key-ring: <key_ring_ID>' \
      -H 'correlation-id: <correlation_ID>'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following
    table.

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>

      <tr>
        <td>
          <varname>region</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The region abbreviation, such as
            <code>us-south</code> or <code>eu-de</code>, that represents the
            geographic area where your
            {{site.data.keyword.hscrypto}} instance
            resides.
          </p>
          <p>
            For more information, see
            [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <varname>key_ID_or_alias</varname>
        </td>
        <td>
          <strong>Required.</strong> The identifier or alias for the key that you want to
          inspect.
        </td>
      </tr>
      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}}
            access token. Include the full contents of the <code>IAM</code>
            token, including the Bearer value, in the cURL request.
          </p>
          <p>
            For more information, see
            [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to
            your {{site.data.keyword.hscrypto}}
            instance.
          </p>
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
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
            Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default.
          </p>
          <p>
            For more information, see
            [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings).
          </p>
        </td>
      </tr>
      <tr>
        <td>
          <varname>correlation_ID</varname>
        </td>
        <td>
          The unique identifier that is used to track and correlate
          transactions.
        </td>
      </tr>

      <caption>
        Table 1. Describes the variables that are needed to view a details about
        a key with the {{site.data.keyword.hscrypto}} key management API
      </caption>
    </table>

    A successful `GET api/v2/keys/<key_ID_or_alias>/metadata` response returns details
    about your key. The following JSON object shows an example returned value
    for a standard key.

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
          "name": "test-standard-key",
          "state": 1,
          "extractable": true,
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
          "dualAuthDelete": {
            "enabled": false
          },
          "deleted": false
        }
      ]
    }
    ```
    {: screen}

    Need to retrieve the `payload` value for a standard key? To learn more, see
    [Retrieving a root key or a standard key](/docs/hs-crypto?topic=hs-crypto-retrieve-key).
    {: tip}

    For a detailed description of the response parameters, see the
    {{site.data.keyword.hscrypto}} key management
    [REST API reference doc](/apidocs/hs-crypto){: external}.
