---

copyright:
  years: 2021, 2024
lastupdated: "2024-05-20"

keywords: delete keys, purge, automatic purge, manual purge, delete, destroy

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# About deleting and purging keys
{: #delete-purge-keys}

You can delete an encryption key and the key material if you are a _[Manager](/docs/hs-crypto?topic=hs-crypto-manage-access)_ for your {{site.data.keyword.hscrypto}} instance.
{: shortdesc}

If a key is no longer needed, you can delete and ultimately purge keys. This action shreds the key material and makes any of the data encrypted with the keys inaccessible.

When you delete a key, the key moves into a [Destroyed state](/docs/hs-crypto?topic=hs-crypto-key-states). Within 30 days after the deletion, the key can still be viewed and restored. After 90 days, the key is automatically purged and you will no longer able to view the key. The data that is associated with the key is also permanently removed from the {{site.data.keyword.hscrypto}} instance. If you want to purge a key before 90 days, you can also do it manually 4 hours after it is moved into the Destroyed state.

After a key is purged, the associated data can no longer be accessed. As a result, it is not suggested to [destroy resources](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#data-deletion) in production environments unless it is necessary.
{: important}

The following table lists the timeframes in which you can view, restore, and purge the key after you delete a key.

| Time from key deletion  | Name of key state | Can view or access key data? | Can restore? | Can user initiate purge? |
|-------------------------|-------------------|---------------------------|--------------|--------------------------|
| 1 second–4 hours | Destroyed         | Yes                       | Yes          | No                       |
| 4 hours–30 days       | Destroyed         | Yes                       | Yes          | Yes                      |
| 30–90 days              | Destroyed         | Yes                       | No           | Yes                      |
| After 90 days           | Purged (not a key state technically)        | No                        | No           | Yes                      |
{: caption="Table 1. Lists how users can interact with keys during certain time intervals after a key is deleted." caption-side="bottom"}

Because purged keys are inaccessible and no longer restorable, _Purged_ is not a key state technically. However, it can be useful to think of _Purged_ as being a state because nonexistence is part of the lifecycle of a key.
{: note}

The following table lists the APIs that you can use to retrieve data that is related to a deleted key before the key becomes purged.

| API               | Description                                              |
|------------------ |----------------------------------------------------------|
| [Get a key](/docs/hs-crypto?topic=hs-crypto-retrieve-key)                       | Retrieve key details.                                     |
| [Get key metadata](/docs/hs-crypto?topic=hs-crypto-view-key-details)     | Retrieve key metadata.                                    |
| [Get registrations](/docs/hs-crypto?topic=hs-crypto-view-protected-resources) | Retrieve a list of registrations associated with the key. |
{: caption="Table 2. Lists the API that users can use to view details about a key and the registrations." caption-side="bottom"}

After a key is purged, you receive a 404 HTTP Not Found error when you call any API methods that use the key ID of a purged key. If you need to retain any data that is associated with a purged key, it is suggested to make the necessary API or CLI calls to retrieve and store that data in your own storage device.
{: tip}

## Considerations before you delete and purge a key
{: #delete-purge-keys-considerations}

{{site.data.keyword.hscrypto}} blocks the deletion of any key that is actively protecting any registered cloud resources. Before you delete a key, bare the following considerations in mind:

1. [Review the registered IBM resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources) that are associated with the key. If needed, you can [force deletion on a key](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-key-force) that protects a registered cloud resource. However, the action can't succeed if the associated resource is not erasable because of a [retention policy](/docs/cloud-object-storage?topic=cloud-object-storage-immutable#immutable-terminology-policy){: external}. The policy is a WORM (Write-Once-Read-Many) policy that is set on the customer's relevant cloud resource.
2. Verify whether a key has a retention policy by checking the `preventKeyDeletion` field of the [registration details](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources-api) for the key. You must then contact an account owner to remove the retention policy on each resource that is associated with the key before you can delete the key.
3. Verify the deletion authorization policy of the key. By default, keys in {{site.data.keyword.hscrypto}} require only a single deletion authorization by one user with the _Manager_ role. However, if a [dual authorization policy is set](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy), two users with the _Manager_ role are needed to approve the deletion.
4. Make sure that you are assigned the _KMS Key Purge_ role if you want to purge a key manually. For more information about service access roles, see [IAM service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).

## What's next
{: #delete-purge-keys-next}

- To learn how to delete keys that hold a single authorization policy, see [Deleting keys by using a single authorization](/docs/hs-crypto?topic=hs-crypto-delete-keys).
- To learn how to delete keys that hold a dual authorization policy, see [Deleting keys by using dual authorization](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys).
- To learn how to manually purge keys, see [Purging keys manually](/docs/hs-crypto?topic=hs-crypto-purge-keys).
