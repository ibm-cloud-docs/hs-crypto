---

copyright:
  years: 2018, 2022
lastupdated: "2022-03-01"

keywords: delete, delete key, delete encryption key, curl -x delete, delete key api

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Deleting keys by using a single authorization
{: #delete-keys}

If you are a manager for your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance, you can use {{site.data.keyword.hscrypto}} to delete root keys or standard keys and the contents.

Before you delete keys, make sure you understand [the concept of deleting and purging keys](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys) and review the [considerations](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys#delete-purge-keys-considerations).


## Deleting keys with the console
{: #delete-keys-gui}
{: help}
{: support}

By default, {{site.data.keyword.hscrypto}} requires one
authorization to delete a key. If you prefer to delete your encryption keys by
using a graphical interface, you can use the {{site.data.keyword.cloud_notm}}
console.

[After you create or import your existing keys into the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys), complete the following steps to delete a key:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, use the **Keys** table to browse the keys in your service.
5. Select the key that you want to delete and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key.
6. From the options menu, click **Delete key**, enter the key name to confirm the key to be deleted, and click **Delete key**.

After you delete a key, the key moves to the _Destroyed_ state. You can [restore the deleted key](/docs/hs-crypto?topic=hs-crypto-restore-keys) within 30 days after its deletion. Metadata that is associated with the key, such as the key's deletion date, is kept in the {{site.data.keyword.hscrypto}} database.

## Deleting keys with the API
{: #delete-keys-api}

By default, {{site.data.keyword.hscrypto}} requires one authorization to delete a key. You can delete a key and the contents by making a
`DELETE` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

This action can't succeed if the key is actively protecting one or more cloud
resources. You can
[review the resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)
that are associated with the key, or
[use the `force` parameter](#delete-key-force)
at query time to delete the key.
{: important}

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Retrieve the ID of the key that you would like to delete.

    You can find the ID for a key in your service instance by [retrieving a list of your keys](/docs/hs-crypto?topic=hs-crypto-view-keys), or by accessing the {{site.data.keyword.cloud_notm}} console.

3. Run the following cURL command to permanently delete the key and the contents.

    ```sh
    curl -X DELETE \
      "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>" \
      -H "authorization: Bearer <IAM_token>" \
      -H "bluemix-instance: <instance_ID>" \
      -H "x-kms-key-ring: <key_ring_ID>" \
      -H "prefer: <return_preference>"
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
        <td><strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier for the key that you would like to delete.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td><strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td><strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td>
          <varname>key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} searches for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request.
          </p>
          <p>
            Note: The key ring ID of keys that are created without an <code>x-kms-key-ring</code> header is <code>default</code>.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-managing-key-rings">Managing key rings</a>.</p>
        </td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns a successful deletion response. When you set the variable to <code>return=representation</code>, the service returns both the key material and the key metadata.</p></td>
      </tr>
      <caption>Table 1. Describes the variables that are needed to delete keys with the {{site.data.keyword.hscrypto}} key management API.</caption>
    </table>

    If the `return_preference` variable is set to `return=representation`, the details of the `DELETE` request are returned in the response entity-body.

    The following JSON object shows a sample returned value.

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
                "name": "test-root-key",
                "aliases": [
                    "alias-1",
                    "alias-2"
                  ],
                "state": 5,
                "extractable": false,
                "crn": "crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
                "imported": false,
                "creationDate": "2020-03-10T20:41:27Z",
                "createdBy": "...",
                "algorithmType": "AES",
                "algorithmMetadata": {
                    "bitLength": "256",
                    "mode": "CBC_PAD"
                },
                "algorithmBitSize": 256,
                "algorithmMode": "CBC_PAD",
                "lastUpdateDate": "2020-03-16T20:41:27Z",
                "dualAuthDelete": {
                    "enabled": false
                },
                "deleted": true,
                "deletionDate": "2020-03-16T21:46:53Z",
                "deletedBy": "..."
            }
        ]
    }
    ```
    {: screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.hscrypto}} [key management API reference doc](/apidocs/hs-crypto){: external}.

### Using the `force` query parameter
{: #delete-key-force}

{{site.data.keyword.hscrypto}} blocks the deletion of a key that's protecting a cloud resource, such as a {{site.data.keyword.cos_full_notm}} bucket. You can force-delete a key and the contents by making a `DELETE` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?force=true
```

When you delete a key with registrations that are associated, you shred the key's contents and associated data. Any data that is encrypted by the key becomes inaccessible.
{: note}

This action can't succeed if the key is protecting a resource that's non-erasable due to a retention policy. You can verify whether a key is associated with a non-erasable resource by [checking the registration details](/docs/hs-crypto?topic=hs-crypto-view-protected-resources) for the key. Then, you must contact an account owner to remove the retention policy on each resource that is associated with the key before you can delete the key.
{: important}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Retrieve the ID of the key that you want to force delete.

    You can retrieve the ID for a specified key by making a `GET /v2/keys/`request, or by viewing your keys in the {{site.data.keyword.cloud_notm}} console.

3. Run the following cURL command to force-delete the key and the contents.

    ```sh
    curl -X DELETE \
    "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?force=true" \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H "x-kms-key-ring: <key_ring_ID>" \
    -H 'prefer: <return_preference>'
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
        <varname>region</varname>
      </td>
      <td>
        <p>
          <strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>eu-de</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides.
        </p>
        <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</p>
      </td>
    </tr>

    <tr>
      <td><varname>port</varname></td>
      <td><strong>Required.</strong> The port number of the API endpoint.</td>
    </tr>

    <tr>
      <td>
        <varname>key_ID</varname>
      </td>
      <td>
        <strong>Required.</strong> The unique identifier for the key that you would like to delete.
      </td>
    </tr>

    <tr>
      <td>
        <varname>IAM_token</varname>
      </td>
      <td>
        <p>
          <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request.
        </p>
        <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</p>
      </td>
    </tr>

    <tr>
      <td>
        <varname>instance_ID</varname>
      </td>
      <td>
        <p>
          <strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance.
        </p>
        <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</p>
      </td>
    </tr>
    <tr>
      <td>
        <varname>key_ring_ID</varname>
      </td>
      <td>
        <p>
          <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} searches for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request.
        </p>
        <p>
          Note: The key ring ID of keys that are created without an <code>x-kms-key-ring</code> header is <code>default</code>.
        </p>
        <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-managing-key-rings">Managing key rings</a>.</p>
      </td>
    </tr>
    <tr>
      <td>
        <varname>return_preference</varname>
      </td>
      <td>
        <p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p>
        <p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns a successful deletion response. When you set the variable to <code>return=representation</code>, the service returns both the key material and the key metadata.</p>
      </td>
    </tr>

    <caption>Table 1. Describes the variables that are needed to delete keys with the {{site.data.keyword.hscrypto}} key management API.</caption>
    </table>

    If the `return_preference` variable is set to `return=representation`, the details of the `DELETE` request are returned in the response entity-body.

    The following JSON object shows a sample returned value.

    ```json
    {
        "metadata": {
            "collectionType": "application/vnd.ibm.kms.key+json",
            "collectionTotal": 1
        },
        "resources": [
            {
                "id": "2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
                "type": "application/vnd.ibm.kms.key+json",
                "aliases": [
                    "alias-1",
                    "alias-2"
                ],
                "name": "test-root-key",
                "description": "...",
                "state": 5,
                "expirationDate": "2020-03-15T20:41:27Z",
                "crn": "crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:30372f20-d9f1-40b3-b486-a709e1932c9c:key:2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
                "deleted": true,
                "algorithmType": "AES",
                "createdBy": "...",
                "deletedBy": "...",
                "creationDate": "2020-03-10T20:41:27Z",
                "deletionDate": "2020-03-16T21:46:53Z",
                "lastUpdateDate": "2020-03-16T20:41:27Z",
                "extractable": false
            }
        ]
    }
    ```
    {: screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.hscrypto}} [key management API reference doc](/apidocs/hs-crypto){: external}.

## What's next
{: #delete-key-next}

- To restore a previously deleted key, check out [Restoring keys](/docs/hs-crypto?topic=hs-crypto-restore-keys).
- To create another root key, check out [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
- To delete the service instance, check out [Deleting service instances](/docs/hs-crypto?topic=hs-crypto-delete-instance)
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management API reference doc](/apidocs/hs-crypto){: external}.
