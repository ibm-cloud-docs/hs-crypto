---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-27"

keywords: import azure key failure, can't import azure key

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I distribute keys to Azure Key Vault?
{: #troubleshoot-import-azure-key}
{: troubleshoot}
{: support}

After I create an Azure Key Vault key using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}, I can't distribute the key to an external keystore of type Azure Key Vault.
{: shortdesc}

After you create a key in {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} and distribute it to a keystore of Azure Key Vault, you cannot find the key that is listed in the connected Key Vault instance in the Azure cloud or use it for encryption.
{: tsSymptoms}

You might have accidentally deleted a key named `EKMF-BYOK-KEK-FOR-IMPORT` in the Azure Key Vault instance that you connect to. You can distribute keys to your Azure Key Vault only if a key named `EKMF-BYOK-KEK-FOR-IMPORT` exists in the Azure Key Vault instance. By default, this key is automatically created when you successfully connect to your Azure Key Vault instance. 
{: tsCauses}

Create a key from the Azure Key Vault UI based on the following key settings. And then, activate and distribute keys that you create from the {{site.data.keyword.hscrypto}} UI to keystores again. For detailed instructions, see [Editing key details with the UI](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
{: tsResolve}

| Parameter | Value |
| --------- | ----- |
| Options   | Generate Key Encryption Key for Importing HSM-protected Keys |
| Name      | `EKMF-BYOK-KEK-FOR-IMPORT` |
| Key type  | RSA-HSM |
| Enabled   | Yes     |
{: caption="Table 1. Key settings" caption-side="bottom"}
