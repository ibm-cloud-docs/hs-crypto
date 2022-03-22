---

copyright:
  years: 2022
lastupdated: "2022-03-22"

keywords: troubleshoot, problems, known issues, can't delete vaults

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}

# Why can't I delete vaults?
{: #troubleshoot-delete-vault}
{: troubleshoot}

You are not able to delete vaults using either UI or API.
{: shortdesc}

You try to delete a vault, but it fails with the following message:
{: tsSymptoms}

```
The service was not able to delete vault `<vault_name>` because it still contains some keys or keystores.
```
{: screen}

If you want to delete a vault, you need to delete all managed keys, and delete or disconnect from all target keystores that are managed in the vault first. The Delete function is available for empty vaults only. 
{: tsCauses}

Verify with your administrator that you're assigned [the correct role](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) in the applicable resource group or service instance. And then, delete all managed keys, and delete or disconnect from all target keystores that are managed in the vault, and try again.
{: tsResolve}

