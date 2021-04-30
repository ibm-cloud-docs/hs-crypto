---

copyright:
  years: 2018, 2021
lastupdated: "2021-04-30"

keywords: get key, get encryption key, view encryption key, retrieve encryption key, API examples

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

# Retrieving a root key or a standard key
{: #retrieve-key}

You can retrieve a root key or standard key by using
{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

If you have a _Writer_ or _Manager_ access policy, you can retrieve the contents
of a standard key, such as its key material and policy details.

[Root keys](#x6946961){: term} stay within the bounds of a hardware security
module. The key material for a root key cannot be retrieved.
{: note}

## Retrieving a key with the key management API
{: #get-key-api}

To view detailed information about a specific key, you can make a `GET` call to
the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID_or_alias>
```
{: codeblock}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Retrieve the ID of the standard key that you would like to access or manage.

    The ID value is used to access detailed information about the standard key, such as
    the key material itself. You can retrieve the ID for a specified key by
    making a `GET /v2/keys` request, or by accessing the
    {{site.data.keyword.cloud_notm}} console.

3. Run the following cURL command to get details about your key and the key
material.

    ```sh
    curl -X GET \
      "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID_or_alias>" \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H "x-kms-key-ring: <key_ring_ID>" \
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
          <strong>Required.</strong> The identifier or alias for the key that you want to retrieve.
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
        <td>
          <varname>correlation_ID</varname>
        </td>
        <td>
          The unique identifier that is used to track and correlate
          transactions.
        </td>
      </tr>
      <caption style="caption-side:bottom;">
        Table 4. Describes the variables that are needed to view a specified key
        with the {{site.data.keyword.hscrypto}} key management API
      </caption>
    </table>

    A successful `GET api/v2/keys/<key_ID_or_alias>` response returns details about your
    key and the key material. The following JSON object shows an example
    returned value for a standard key.

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
                "aliases": [
                    "alias-1",
                    "alias-2"
                  ],
                "state": 1,
                "expirationDate": "2020-03-15T03:50:12Z",
                "extractable": true,
                "crn": "crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
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
                "deleted": false,
                "payload": "Rm91ciBzY29yZSBhbmQgc2V2ZW4geWVhcnMgYWdv..."
            }
        ]
    }
    ```
    {: screen}

    The following JSON object shows an example returned value for a root key.

    ```json
    {
        "metadata": {
            "collectionType": "application/vnd.ibm.kms.key+json",
            "collectionTotal": 1
        },
        "resources": [
            {
                "type": "application/vnd.ibm.kms.key+json",
                "id": "2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
                "aliases": [
                    "alias-1",
                    "alias-2"
                ],
                "name": "test-root-key",
                "state": 1,
                "extractable": false,
                "crn": "crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:30372f20-d9f1-40b3-b486-a709e1932c9c:key:2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
                "imported": false,
                "creationDate": "2020-03-05T16:28:38Z",
                "createdBy": "...",
                "algorithmType": "AES",
                "algorithmMetadata": {
                    "bitLength": "256",
                    "mode": "CBC_PAD"
                },
                "algorithmBitSize": 256,
                "algorithmMode": "CBC_PAD",
                "lastUpdateDate": "2020-03-05T16:39:25Z",
                "keyVersion": {
                    "id": "436901cb-f4e4-45f4-bd65-91a7f6d13461",
                    "creationDate": "2020-03-05T16:39:25Z"
                },
                "dualAuthDelete": {
                    "enabled": false
                },
                "deleted": false
            }
        ]
    }
    ```
    {: screen}

    The `payload` or key material for a root key stays within the bounds of a
    hardware security module and cannot be retrieved.
    {: note}

    For a detailed description of the response parameters, see the
    {{site.data.keyword.hscrypto}} key management
    [REST API reference doc](/apidocs/hs-crypto){: external}.
