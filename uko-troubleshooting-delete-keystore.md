---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-20"

keywords: troubleshoot, problems, known issues, can't delete keystores

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why can't I delete internal keystores?
{: #troubleshoot-delete-keystore}
{: troubleshoot}

You are not able to delete the internal KMS keystore through either UI or API.
{: shortdesc}

You have destroyed all keys in the KMS keystore. However, when you try to delete the keystore, you still receive an error similar to one of the following: 
{: tsSymptoms}

> The service was not able to delete keystore `<keystore_name>` because it still contains some keys.
> Conflict: Key ring could not be deleted: Please see reasons for more details.

The KMS key metadata is to be automatically removed in 90 days. Before that, the key metadata still remains in the keystore and you cannot delete the keystore.
{: tsCauses}

Delete the internal KMS keystore after the key metadata gets removed automatically. Or, you can [manually remove all key metadata using the KMS API](/apidocs/hs-crypto#purgekey){: external} in 4 hours after you destroy the key. Make sure that you have the **KMS Key Purge** role assigned. For more information about roles, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-uko-manage-access).
{: tsResolve}

