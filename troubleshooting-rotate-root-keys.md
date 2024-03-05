---

copyright:
  years: 2020, 2024
lastupdated: "2024-02-27"

keywords: troubleshoot, problems, known issues, can't rotate root keys

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I rotate root keys?
{: #troubleshoot-unable-to-rotate-root-keys}
{: troubleshoot}
{: support}

When you access the UI, you do not see the options to rotate root keys.
{: shortdesc}

From the {{site.data.keyword.cloud_notm}} dashboard, you see a list of keys in the **Keys** table. However, by selecting the key that you want to rotate and clicking the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), you don't see the **Rotate key** option on the list.
{: tsSymptoms}

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you're assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}
