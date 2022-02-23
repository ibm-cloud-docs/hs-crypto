---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-16"

keywords: troubleshoot, problems, known issues, can't create or import keys

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

# Why can't I create or import keys?
{: #troubleshoot-unable-to-create-keys}
{: troubleshoot}
{: support}

When you access the {{site.data.keyword.hscrypto}} user interface, you do not see the options to add keys or import keys.
{: shortdesc}

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.hscrypto}} service. You can see a list of keys, but you do not see options to add keys or import keys.
{: tsSymptoms}

You do not have the correct authorization to perform {{site.data.keyword.hscrypto}} actions.
{: tsCauses}

Verify with your administrator that you're assigned the correct role in the applicable resource group or service instance. For more information about roles, see [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles).
{: tsResolve}
