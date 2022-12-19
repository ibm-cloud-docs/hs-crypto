---

copyright:
  years: 2022
lastupdated: "2022-11-25"

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

# Why can't I assign keys to Azure Key Vault?
{: #troubleshoot-import-azure-key}
{: troubleshoot}
{: support}

After I create an Azure Key Vault key using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}, I can't assign the key to an external keystore of type Azure Key Vault.
{: shortdesc}

After you create a key in {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} and assign it to a keystore of Azure Key Vault, you cannot find the key listed in the connected Key Vault instance in the Azure cloud or use it for encryption.
{: tsSymptoms}

You might have accidentally deleted a key named `EKMF-BYOK-KEK-FOR-IMPORT` in the Azure Key Vault instance that you connect to. You can assign keys to your Azure Key Vault only if a key named `EKMF-BYOK-KEK-FOR-IMPORT` exists in the Azure Key Vault instance. By default, this key is automatically created when you successfully connect to your Azure Key Vault instance. 
{: tsCauses}

Create a key from the Azure Key Vault UI based on the following key settings. And then, set target keystores for keys that you create from the {{site.data.keyword.hscrypto}} UI again. For detailed instructions, see [Setting target keystores for existing keys](/docs/hs-crypto?topic=hs-crypto-install-key-keystores&interface=ui).
{: tsResolve}

| Parameter | Value |
| --------- | ----- |
| Options   | Generate Key Encryption Key for Importing HSM-protected Keys |
| Name      | `EKMF-BYOK-KEK-FOR-IMPORT` |
| Key type  | RSA-HSM |
| Enabled   | Yes     |
