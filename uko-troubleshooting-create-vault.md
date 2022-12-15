---

copyright:
  years: 2022
lastupdated: "2022-12-15"

keywords: troubleshoot, problems, known issues, can't create vaults

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Why can't I create vaults?
{: #troubleshoot-create-vault}
{: troubleshoot}
{: support}

You are not able to create a vault through either the {{site.data.keyword.hscrypto}} user interface or the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

You might receive an error message similar to one of the following messages when you create a vault:
{: tsSymptoms}

>  The service was not able to create vault "vault-name" or the vault "vault-name" is not created.

It might be caused by one of the following reasons:
{: tsCauses}
* You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
* The master key rotation is in progress. 

Try the following solutions: 
{: tsResolve}
* Verify with your administrator that you're assigned the _Vault Administrator_ role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-service-access-roles).
* Try to create the vault again after the master key rotation is complete. For more information, see [Master key rotation](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro).

