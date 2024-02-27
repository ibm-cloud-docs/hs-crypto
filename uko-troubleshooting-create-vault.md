---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-27"

keywords: troubleshoot, problems, known issues, can't create vaults

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

# Why can't I create vaults?
{: #troubleshoot-create-vault}
{: troubleshoot}
{: support}

You are not able to create a vault through either the UI or the {{site.data.keyword.uko_full_notm}} API.
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
