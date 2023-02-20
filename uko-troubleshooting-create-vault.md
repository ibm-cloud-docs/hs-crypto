---

copyright:
  years: 2022, 2023
lastupdated: "2023-02-08"

keywords: troubleshoot, problems, known issues, can't create vaults

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Why can't I create vaults?
{: #troubleshoot-create-vault}
{: troubleshoot}
{: support}

You are not able to create a vault through either the {{site.data.keyword.hscrypto}} user interface or the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

You receive the following message when you try to create a vault:
{: tsSymptoms}

>  The service was not able to create vault "vault-name".

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you're assigned the _Vault Administrator_ role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-service-access-roles).
{: tsResolve}



