---

copyright:
  years: 2022, 2025
lastupdated: "2025-03-17"

keywords: troubleshoot, problems, known issues, can't delete vaults

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




## Why can't I delete vaults?
{: #troubleshoot-delete-vault}
{: troubleshoot}

You are not able to delete vaults by using either UI or API.
{: shortdesc}

You try to delete a vault, but it fails with the following message:
{: tsSymptoms}

> The service was not able to delete vault `<vault_name>` because it still contains some keys or keystores.

If you want to delete a vault, you need to delete all managed keys, and delete or disconnect from all keystores that are managed in the vault first. The Delete function is available for empty vaults only. 
{: tsCauses}

Verify with your administrator that you're assigned [the correct role](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) in the applicable resource group or service instance. And then, delete all managed keys, and delete or disconnect from all keystores that are managed in the vault, and try again.
{: tsResolve}
