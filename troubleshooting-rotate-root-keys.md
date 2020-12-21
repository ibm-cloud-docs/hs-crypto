---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: troubleshoot, problems, known issues, can't rotate root keys

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

# Why can't I rotate root keys?
{: #troubleshoot-unable-to-rotate-root-keys}
{: troubleshoot}
{: support}

When you access the {{site.data.keyword.hscrypto}} user interface, you do not see the options to rotate root keys.
{:shortdesc}

From the {{site.data.keyword.cloud_notm}} dashboard, you see a list of keys in the **Key management service keys** table. However, by selecting the key that you want to rotate and clicking the overflow icon, you don't see the **Rotate key** option on the list.
{: tsSymptoms}

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you're assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}
