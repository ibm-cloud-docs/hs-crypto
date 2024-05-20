---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-20"

keywords: rotate, rotate master key, rotate encryption key, rotate root key, rotate keys automatically, key rotation, rewrap data

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Root key rotation - Standard Plan 
{: #root-key-rotation-intro}

You can rotate root keys managed in your {{site.data.keyword.hscrypto}} instance on demand or by setting a rotation policy. Key rotation takes place when you retire the original key material and generate a new cryptographic key material for the root key.
{: shortdesc}

Rotating keys regularly helps you meet industry standards and cryptographic best practices. The following table describes the main benefits of key rotation:

| Benefit | Description |
| --- | --- |
| Cryptoperiod management for keys | Key rotation limits how long your information is protected by a single key. By rotating your root keys at regular intervals, you also shorten the cryptoperiod of the keys. The longer the lifetime of an encryption key, the higher the probability for a security breach. |
| Incident mitigation | If your organization detects a security issue, you can immediately rotate the key to mitigate or reduce costs that are associated with key compromise. |
{: caption="Table 1. Describes the benefits of key rotation" caption-side="bottom"}

Key rotation is treated in the NIST Special Publication 800-57, Recommendation for Key Management. To learn more, see [NIST SP 800-57 Pt. 1 Rev. 5](https://csrc.nist.gov/publications/detail/sp/800-57-part-1/rev-5/final){: external}
{: tip}

## Comparing your root key rotation options
{: #compare-key-rotation-options}

In {{site.data.keyword.hscrypto}}, you can [rotate a root key on demand](/docs/hs-crypto?topic=hs-crypto-rotate-keys) or [by setting a rotation policy](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy), without needing to keep track of your retired root key material.


Setting a rotation policy for a key
:   {{site.data.keyword.hscrypto}} helps you simplify rotation for encryption keys by enabling rotation policies for keys that you generate in the service. After you create a root key, you can manage a rotation policy for the key in the UI or with the API. [Choose an automatic rotation interval](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro#rotation-frequency) between 1 - 12 months for your key based on your on-going security needs. When it's time to rotate the key based on the rotation interval that you specify, {{site.data.keyword.hscrypto}} automatically replaces the key with new key material.

Rotating keys on demand
:   As a security admin, you might want to have more control over the frequency of rotation for your keys. If you don't want to set an automatic rotation policy for a key, you can manually create a new key to replace an existing key, and then update your applications so that they reference the new key. To simplify this process, you can use {{site.data.keyword.hscrypto}} to rotate the key on demand. In this scenario, {{site.data.keyword.hscrypto}} creates and replaces the key on your behalf with each rotation request. The key retains the same metadata and key ID.


## How root key rotation works
{: #how-root-key-rotation-works}

Root key rotation works by securely transitioning key material from an *Active* to a *Deactivated* key state. To replace the deactivated or retired key material, new key material moves into the *Active* state and becomes available for cryptographic operations. For more information about different key states, see [Monitoring the lifecycle of encryption keys](/docs/hs-crypto?topic=hs-crypto-key-states).

### Using {{site.data.keyword.hscrypto}} to rotate root keys
{: #use-hs-crypto-rotate-keys}

Keep in mind the following considerations as you prepare to use {{site.data.keyword.hscrypto}} for rotating root keys.

Rotating root keys that are generated in {{site.data.keyword.hscrypto}}
:   You can use {{site.data.keyword.hscrypto}} to rotate a root key that was generated in {{site.data.keyword.hscrypto}} by setting a rotation policy for the key, or by rotating the key on demand. The metadata for the root key, such as the key ID, does not change when you rotate the key.

Rotating root keys that you bring to the service
:   To rotate a root key that you initially imported to the service, you must generate and provide new key material for the key. You can use {{site.data.keyword.hscrypto}} to rotate imported root keys on demand by supplying new key material as part of the rotation request. The metadata for the root key, such as the key ID, does not change when you rotate the key. Because you must provide new key material to rotate an imported key, automatic rotation policies are not available for root keys that have imported key material.

Managing retired root key material
:   {{site.data.keyword.hscrypto}} creates new key material after you rotate a root key. The service retires the old key material and retains the retired versions until the root key is deleted. When you use the root key for envelope encryption, {{site.data.keyword.hscrypto}} uses only the latest key material that is associated with the key. The retired key material can no longer be used to protect keys, but it remains available for unwrap operations. If {{site.data.keyword.hscrypto}} detects that you're using retired key material to unwrap DEKs, the service provides a newly wrapped DEK that's based on the latest root key material.

Enabling root key rotation for {{site.data.keyword.cloud_notm}} data services
:   To enable these root key rotation options for your data service on {{site.data.keyword.cloud_notm}}, the data service must be integrated with {{site.data.keyword.hscrypto}}. Refer to the documentation for your {{site.data.keyword.cloud_notm}} data service, or check out our list of [integrated services to learn more](/docs/hs-crypto?topic=hs-crypto-integrate-services).

When you rotate a root key in {{site.data.keyword.hscrypto}}, you're not charged extra fees. You can continue to unwrap your wrapped data encryption keys (WDEKs) with retired key material at no extra cost. For more information about our pricing options, see the [{{site.data.keyword.hscrypto}} catalog page](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services).
{: tip}

### Understanding the root key rotation process
{: #understand-key-rotation-process}

Behind the scenes, the {{site.data.keyword.hscrypto}} key management service API drives the key rotation process.

The following diagram shows a contextual view of the key rotation functionality.
![The diagram shows a contextual view of key rotation.](/images/key-rotation.svg "Key rotation"){: caption="Figure 1. Key rotation" caption-side="bottom"}

With each rotation request, {{site.data.keyword.hscrypto}} associates new key material with your root key.

![The diagram shows a micro view the root key stack.](/images/root-key-stack.svg "Root key stack"){: caption="Figure 2. Root key stack" caption-side="bottom"}

To learn how to use the {{site.data.keyword.hscrypto}} key management service API to rotate your root keys, see [Rotating keys](/docs/hs-crypto?topic=hs-crypto-rotate-keys).
{: tip}

### Rewrapping data after rotating a root key
{: #rewrap-data-after-key-rotation}

After a root key rotation completes, new root key material becomes available for protecting data encryption keys (DEKs) with [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption). Retired root key material moves to the Deactivated state, where it can only be used to unwrap and access older DEKs that aren't yet protected by the latest root key.

To secure your envelope encryption workflow, [rewrap your DEKs](/docs/hs-crypto?topic=hs-crypto-rewrap-keys) after you rotate a root key so that your at-rest data is protected by the newest root key. Alternatively if {{site.data.keyword.hscrypto}} detects that you're using retired root key material to unwrap a DEK, the service automatically reencrypts the DEK and returns a wrapped data encryption key (WDEK) that's based on the latest root key. Store and use the new WDEK for future unwrap operations that the DEKs are protected with the newest root key material.

To learn how to use the {{site.data.keyword.hscrypto}} key management service API to rewrap data encryption keys, see [Rewrapping keys](/docs/hs-crypto?topic=hs-crypto-rewrap-keys).
{: tip}

## Frequency of root key rotation
{: #rotation-frequency}

After you generate a root key in {{site.data.keyword.hscrypto}}, you decide the frequency of the rotation. You might want to rotate your keys due to personnel turnover, process malfunction, or according to your organization's internal key expiration policy.

Rotate your keys regularly, for example every 30 days, to meet cryptographic best practices.

| Rotation type | Frequency | Description |
| --- | --- | --- |
| [Policy-based root key rotation](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy) | Every 1 - 12 months | Choose a rotation interval between 1 - 12 months for your key based on your on-going security needs. After you set a rotation policy for a key, the clock starts immediately based on the initial creation date for the key. For example, if you set a monthly rotation policy for a key that you created on `2019/02/01`, {{site.data.keyword.hscrypto}} automatically rotates the key on `2019/03/01`.|
| [On-demand root key rotation](/docs/hs-crypto?topic=hs-crypto-rotate-keys) | Up to one rotation per hour | If you're rotating a key on demand, {{site.data.keyword.hscrypto}} allows one rotation per hour for each root key. |
{: caption="Table 2. Rotation frequency options for rotating keys in {{site.data.keyword.hscrypto}}" caption-side="bottom"}



## What's next
{: #root-key-rotation-next}

- To learn how to use {{site.data.keyword.hscrypto}} to set an automatic rotation policy for an individual key, see [Setting a rotation policy](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy).
- To find out more about manually rotating root keys, see [Rotating keys on demand](/docs/hs-crypto?topic=hs-crypto-rotate-keys).
