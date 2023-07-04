---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-04"

keywords: rotate managed key, rotate key, managed key rotation, key rotation, key rewrap

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Managed key rotation
{: #managed-key-rotation-intro}

You can manually rotate managed keys in your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} instance on demand. Key rotation takes place when you retire the original key material of the managed key, and you re-key it by generating a new cryptographic key material.
{: shortdesc}

Rotating keys regularly helps you meet industry standards and cryptographic best practices. The following table describes the main benefits of key rotation:

| Benefit | Description |
| --- | --- |
| Cryptoperiod management for keys | Key rotation limits how long your information is protected by a single key. By rotating your managed keys at regular intervals, you also shorten the cryptoperiod of the keys. The longer the lifetime of an encryption key, the higher the probability for a security breach. |
| Incident mitigation | If your organization detects a security issue, you can immediately rotate the key to mitigate or reduce costs that are associated with key compromise. |
{: caption="Table 1. Describes the benefits of key rotation" caption-side="bottom"}

Key rotation is treated in the NIST Special Publication 800-57, Recommendation for Key Management. To learn more, see [NIST SP 800-57 Pt. 1 Rev. 5](https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final){: external}
{: tip}

Note that key rotation might charge extra fees depending on the type of your managed key. For the pricing details, refer to the following links:

- AWS Key Management Service keys: [AWS Key Management Service Pricing](https://aws.amazon.com/kms/pricing/){: external}
- Azure Key Vault keys: [Azure Key Vault pricing](https://azure.microsoft.com/en-us/pricing/details/key-vault/){: external}
- Google Cloud KMS keys: [Google Cloud Key Management Service Pricing](https://cloud.google.com/security-key-management#section-11){: external}.
- {{site.data.keyword.cloud_notm}} KMS keys: No extra fees. For more information, see [{{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-how-charge-hpcs-uko).
- IBM {{site.data.keyword.keymanagementserviceshort}} keys: No extra fees. For more information, see [{{site.data.keyword.keymanagementserviceshort}} pricing](https://cloud.ibm.com/docs/key-protect?topic=key-protect-pricing-plan){: external}. 

## How managed key rotation works
{: #how-managed-key-rotation-works}

When you rotate a managed key, new key material is automatically generated and replaces the previous key material. It moves into the *Active* state and becomes available for cryptographic operations. When you use the managed key to perform encryption, {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} uses only the latest key material. Key rotation changes the key material. The key ID can also change, depending on the keystore type.

The following diagram shows a contextual view of the key rotation functionality.
![Manage key rotation](/images/uko-key-rotation.svg "Managed key rotation"){: caption="Figure 1. Managed key rotation" caption-side="bottom"}

Depending on the key type, managed keys in certain states are not eligible for key rotation. Before you rotate a managed key, make sure to check the following table. The **Checkmark** icon ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") indicates that the managed key in this state is eligible for rotation. For more information about the different key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states).

| Key type | Pre-active | Active | Deactivated | Destroyed |
| ------ | ------ | ---------- | ----------- | --------- |
| AWS Key Management Service keys |N/A  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | N/A|
| Azure Key Vault keys | N/A | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | N/A  |
| Google Cloud KMS keys | N/A | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")  | N/A  |
| {{site.data.keyword.cloud_notm}} KMS keys |  N/A   |  ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")   |N/A | N/A  |
| IBM {{site.data.keyword.keymanagementserviceshort}} keys | N/A | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | N/A | N/A  |
{: caption="Table 2. Manage key rotation eligibility" caption-side="bottom"}

### What happens to the previous key versions?
{: #previous-managed-key-versions}

After key rotation, the service retains the previous key versions and materials until the managed key is deleted, but you can no longer edit these key materials and the key state might change. The following table lists the detailed changes and the corresponding actions that are available for previous key versions.

| Key type | Key state changes | Available for encryption | Available for decryption | Description |
| ------ | ------------------- | --------------------- | --------------------- | --------------------- |
| AWS Key Management Service keys | Remain the same. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | For more information, see [Rotating AWS KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/rotate-keys.html){: external}. |
| Azure Key Vault keys | Remain the same. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | For more information, see [Configure cryptographic key auto-rotation in Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/keys/how-to-configure-key-rotation){: external} |
| Google Cloud KMS keys - Other key types except AES keys | Remain the same. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | For more information, see [Key rotation](https://cloud.google.com/kms/docs/key-rotation){: external} and [Rotating keys](https://cloud.google.com/kms/docs/rotating-keys){: external}. |
| Google Cloud KMS keys - AES keys | Automatically move to *Deactivated* state.  | N/A | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | For more information, see [Key rotation](https://cloud.google.com/kms/docs/key-rotation){: external} and [Rotating keys](https://cloud.google.com/kms/docs/rotating-keys){: external}.  |
| {{site.data.keyword.cloud_notm}} KMS keys | Automatically move to *Deactivated* state.   | N/A | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | The previous key material can no longer be used for encryption, but it remains available for unwrap operations. When you use the rotated manage key to decrypt data, the service uses the same version of the key material that was used for encryption, and then rewraps data by using the latest key material. |
| IBM {{site.data.keyword.keymanagementserviceshort}} keys | Automatically move to *Deactivated* state.   | N/A | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | The previous key material can no longer be used for encryption, but it remains available for unwrap operations. When you use the rotated manage key to decrypt data, the service uses the same version of the key material that was used for encryption before, and then rewraps data by using the latest key material. For more information, see [Rotating your keys](/docs/key-protect?topic=key-protect-key-rotation){: external}. |
{: caption="Table 3. Previous key versions changes" caption-side="bottom"}

### How often should keys be rotated?
{: #managed-key-rotation-frequency}

The best practice is to rotate your manage keys regularly. {{site.data.keyword.uko_full_notm}} allows no more than one key rotation per hour for each key.

### Rewrapping data after rotating a managed key
{: #rewrap-data-after-managed-key-rotation}

After a managed key rotation is complete, new key material becomes available for cryptographic operations. To ensure that your data is protected by the latest version of a managed key, rewrap your data after you rotate a managed key. Depending on your key type, refer to the following table for corresponding instructions.

| Key type | Instructions for rewrapping data | 
| ------ | ------------------- |
| AWS Key Management Service keys | [Rewrapping data with AWS Key Management Service](https://docs.aws.amazon.com/kms/latest/APIReference/API_ReEncrypt.html){: external}. |
| Azure Key Vault keys | [Azure key vault documentation](https://learn.microsoft.com/en-us/azure/key-vault/){: external}. |
| Google Cloud KMS keys | [Rewrapping data with Google Cloud KMS](https://cloud.google.com/kms/docs/re-encrypt-data){: external}.  |
| {{site.data.keyword.cloud_notm}} KMS keys | [Rewrapping data with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-rewrap-keys). |
| IBM {{site.data.keyword.keymanagementserviceshort}} keys | [Rewrapping data with IBM {{site.data.keyword.keymanagementserviceshort}}](https://cloud.ibm.com/docs/key-protect?topic=key-protect-rewrap-keys). |
{: caption="Table 4. Rewrapping data after key rotation" caption-side="bottom"}

## What's next
{: #managed-key-rotation-next}

- For more information about how to manually rotate a managed key, see [Rotating managed keys](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys).
- For more information about how to edit managed keys, see [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).

