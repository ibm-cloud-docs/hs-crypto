<azure-key>
---

copyright:
  years: 2022
lastupdated: "2022-08-24"

keywords: import azure key failure, can't import azure key

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

# Why can't I activate keys in my Azure Key Vault?
{: #troubleshoot-import-azure-key}
{: troubleshoot}
{: support}

After I create a key of the Azure Key Vault type in {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}, I can't set its target keystores to be my Azure Key Vault.
{: shortdesc}

When you set target keystores for your key of the Azure Key Vault, you get an error message similar to the following one:
{: tsSymptoms}

The key is failed to be tagged with a label `EKMF-BYOK-KEK-FOR-IMPORT`.
{: tsCauses}

Create the key directly with the Azure Key Vault UI and labelled it with `EKMF-BYOK-KEK-FOR-IMPORT`.
{: tsResolve}

</azure-key>

