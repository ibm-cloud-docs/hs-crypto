---

copyright:
  years: 2021, 2024
lastupdated: "2024-05-30"

keywords: purge key, permanently delete key, remove key, destroy key

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Purging keys manually
{: #purge-keys}

A deleted key becomes purged automatically after 90 days of the deletion. If you want to purge a key before it gets automatically purged, make sure that you are assigned the _KMS Key Purge_ role for your {{site.data.keyword.hscrypto}} instance. A key can be purged manually only after it is deleted for 4 hours.
{: shortdesc}

Before you purge keys, make sure that you understand [the concept of deleting and purging keys](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys) and review the [considerations](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys#delete-purge-keys-considerations).

To manually purge a key, you need to be assigned the _KMS Key Purge_ role. Even a _Manager_ cannot purge a key. For more information about service access roles, see [IAM service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
{: important}

## Purging keys in the UI
{: #purge-keys-gui}
{: ui}

If you prefer to purging a key by using a graphical interface, you can use the UI by completing the following steps:

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, use the **Keys** table to browse the keys in your service.
5. Select the key that you want to purge and make sure that the state is Destroyed. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key.
6. From the options menu, click **Purge key**.
7. Check the box to confirm the action and click **Purge key**.

You are not able to purge a key if you perform the purging action in 4 hours after you delete the key.
{: note}

## Purging keys with the API
{: #purge-keys-api}
{: api}

You can purge a deleted key by making a `DELETE` call to the following endpoint:

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/purge
```

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Retrieve the ID of the key that you want to delete.

    You can find the ID for a key in your service instance by [retrieving a list of your keys](/docs/hs-crypto?topic=hs-crypto-view-keys), or by accessing the UI.

3. Run the following cURL command to permanently delete the key and the contents.

    ```sh
    curl -X DELETE \
      "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/purge" \
      -H "authorization: Bearer <IAM_token>" \
      -H "bluemix-instance: <instance_ID>" \
      -H "x-kms-key-ring: <key_ring_ID>" \
      -H "prefer: <return_preference>"
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `key_ID` | **Required.** The unique identifier for the key that you would like to delete. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the cURL request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    | `key_ring_ID` | **Optional.** The unique identifier of the key ring that the key belongs to. If it is not specified, {{site.data.keyword.hscrypto}} searches for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request. The key ring ID of keys that are created without an `x-kms-key-ring` header is `default`. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). |
    | `return_preference` | A header that alters server behavior for `POST` and `DELETE` operations. When you set the `return_preference` variable to `return=minimal`, the service returns a successful deletion response. When you set the variable to `return=representation`, the service returns both the key material and the key metadata. |
    {: caption="Table 1. Describes the variables needed to purge keys with the API" caption-side="bottom"}

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
            "id": "...",
            "name": "Root-key",
            "description": "...",
            "state": 5,
            "extractable": false,
            "keyRingID": "default",
            "crn": "...",
            "imported": false,
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "createdBy": "...",
            "algorithmType": "AES",
            "algorithmMetadata": {
              "bitLength": 256,
              "mode": "CBC_PAD"
            },
            "algorithmBitSize": 256,
            "algorithmMode": "CBC_PAD",
            "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
            "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
            "dualAuthDelete": {
              "enabled": true,
              "keySetForDeletion": true,
              "authExpiration": "YYYY-MM-DDTHH:MM:SSZ"
            },
            "deleted": true,
            "deletionDate": "YYYY-MM-DDTHH:MM:SSZ",
            "deletedBy": "...",
            "purgeAllowed": true,
            "purgeAllowedFrom": "YYYY-MM-DDTHH:MM:SSZ",
            "purgeScheduledOn": "YYYY-MM-DDTHH:MM:SSZ"
          }
        ]
    }
    ```
    {: screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.hscrypto}} [key management service API reference doc](/apidocs/hs-crypto){: external}.

## What's next
{: #purge-keys-next}

- To learn more about deleting and purging keys, see [About deleting and purging keys](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys).
