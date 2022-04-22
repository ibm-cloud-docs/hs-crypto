---

copyright:
  years: 2022
lastupdated: "2022-04-21"

keywords: troubleshoot, problems, known issues, failed to see azure key changes

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

# Why do I fail to see the changes to my key in Azure Key Vault?
{: #troubleshoot-azure-delay}
{: troubleshoot}
{: support}

After you use {{site.data.keyword.uko_full_notm}} to change the state or installation status of a key in Azure Key Vault, you fail to see the changes in the Azure UI.
{: shortdesc}

The installed key in Azure Key Vault is not updated after you change the key state or installation status in {{site.data.keyword.uko_full_notm}}.
{: tsSymptoms}

When you make changes to a managed key in {{site.data.keyword.uko_full_notm}}, it can take up to 2 minutes to reflect the changes in the Azure UI.
{: tsCauses}

Wait for 2 minutes and refresh the Azure UI to see the changes.
{: tsResolve}


