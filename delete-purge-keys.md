---

copyright:
  years: 2021
lastupdated: "2021-05-08"

keywords: delete keys, purge, automatic purge, manual purge, delete, destroy

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

# About deleting and purging keys
{: #delete-purge-keys}

You can use {{site.data.keyword.hscrypto}} to delete an encryption key and its key material if you are a [manager](/docs/hs-crypto?topic=hs-crypto-manage-access) for your {{site.data.keyword.hscrypto}} instance.
{: shortdesc}

In the event that a key is no longer needed, you can delete and ultimately purge keys. This action shreds the key material and makes any of the data encrypted with the keys inaccessible.

When you delete a key, the key moves into a [_Destroyed_ state](/docs/hs-crypto?topic=hs-crypto-key-states). Within 30 days after the deletion, the key can still be viewed and restored. After 90 days, the key is automatically purged and you will no longer able to view the key. The data that is associated with the key is also permanently removed from the {{site.data.keyword.hscrypto}} instance. If you want to purge a key before 90 days, you can also do it manually four hours after it is moved into the _Destroyed_ state.

Once a key is purged, its associated data can no longer be accessed. As a result, it is not recommended to [destroy resources](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#data-deletion) in production environments unless absolutely necessary.
{: important}

The following table lists the time frames in which you can view, restore, and purge the key after you delete a key.

| Time from key deletion  | Name of key state | Can view/access key data? | Can restore? | Can user initiate purge? |
|-------------------------|-------------------|---------------------------|--------------|--------------------------|
| One second - Four hours | Destroyed         | Yes                       | Yes          | No                       |
| 4 hours - 30 days       | Destroyed         | Yes                       | Yes          | Yes                      |
| 30-90 days              | Destroyed         | Yes                       | No           | Yes                      |
| After 90 days           | Purged (not a key state technically)        | No                        | No           | Yes                      |
{: caption="Table 1. Lists how users can interact with keys during certain time intervals after a key has been deleted" caption-side="bottom"}

Because purged keys are completely inaccessible and destroyed, there is technically no key state called _Purged_. However, it can be useful to think of _Purged_ as being a state because nonexistence is part of the lifecycle of a key.
{: note}

The following table lists which APIs you can use to retrieve data related to a deleted key before the key becomes purged.

| API               | Description                                              |
|------------------ |----------------------------------------------------------|
| [Get a key](/docs/hs-crypto?topic=hs-crypto-retrieve-key)                       | Retrieve key details                                     |
| [Get key metadata](/docs/hs-crypto?topic=hs-crypto-view-key-details)     | Retrieve key metadata                                    |
| [Get registrations](/docs/hs-crypto?topic=hs-crypto-view-protected-resources) | Retrieve a list of registrations associated with the key |
{: caption="Table 2. Lists the API that users can use to view details about a key and its registrations." caption-side="bottom"}

Once a key is purged, you receive a 404 HTTP Not Found error when you call any API methods that use the key ID of a purged key. If you are required to retain any data that is associated to a purged key, such as key metadata, registrations, and policies, for an extended period of time, it is recommended to perform the necessary API or CLI calls to retrieve and store that data in your own storage device.
{: tip}

## Considerations before deleting and purging a key
{: #delete-purge-keys-considerations}

{{site.data.keyword.hscrypto}} blocks the deletion of any key that is actively protecting any registered cloud resources. Before you delete a key:

1. [Review the registered IBM resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources) that are associated with the key. If needed, you can [force deletion on a key](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-key-force) that is protecting a registered cloud resource. However, the action won't succeed if the key's associated resource is non-erasable due to a [retention policy](/docs/cloud-object-storage?topic=cloud-object-storage-immutable#immutable-terminology-policy){: external}, which is a Write Once Read Many (WORM) policy set on the customer's relevant cloud resource.
2. Verify whether a key has a retention policy by checking the `preventKeyDeletion` field of the [registration details](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources-api) for the key. You must then contact an account owner to remove the retention policy on each resource that is associated with the key before you can delete the key.
3. Verify the key's deletion authorization policy. By default, keys in {{site.data.keyword.hscrypto}} only require a single deletion authorization by one user with the _Manager_ role. However, if a [dual authorization policy has been set](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy), two users with the _Manager_ role are needed to approve the deletion.

## What's next
{: #delete-purge-keys-next}

- To learn how to delete keys that hold a single authorization policy, see [Deleting keys using a single authorization](/docs/hs-crypto?topic=hs-crypto-delete-keys).
- To learn how to delete keys that hold a dual authorization policy, see [Deleting keys using dual authorization](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys).
- To learn how to manually purge keys, see [Purging keys](/docs/hs-crypto?topic=hs-crypto-purge-keys).
