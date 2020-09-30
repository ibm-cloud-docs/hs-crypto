---

copyright:
  years: 2020
lastupdated: "2020-07-22"

keywords: rotate, rotate master key, rotate encryption key, rotate root key, rotate keys automatically, key rotation, rewrap data

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Rotating your master keys and root keys
{: #key-rotation}

With envelope encryption, both master keys and root keys can be rotated. Key rotation takes place when you retire the original key material of the master key or root key, and you re-key it by generating new, cryptographic key material.
{: shortdesc}

Rotating keys on a regular basis helps you meet industry standards and cryptographic best practices. The following table describes the main benefits of key rotation:

| Benefit | Description |
| --- | --- |
| Cryptoperiod management for keys | Key rotation limits how long your information is protected by a single key. By rotating your root keys at regular intervals, you also shorten the cryptoperiod of the keys. The longer the lifetime of an encryption key, the higher the probability for a security breach. |
| Incident mitigation | If your organization detects a security issue, you can immediately rotate the key to mitigate or reduce costs that are associated with key compromise. |
{: caption="Table 1. Describes the benefits of key rotation" caption-side="bottom"}

Key rotation is treated in the NIST Special Publication 800-57, Recommendation for Key Management. To learn more, see [NIST SP 800-57 Pt. 1 Rev. 4](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0){: external}
{: tip}

## Master key rotation
{: #master-key-rotation-intro}

With envelope encryption, a master key is used to wrap root keys managed in the service instance. After you have a master key loaded to your service instance, you need to regularly [rotate your master key](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli).

### How master key rotation works
{: #how-master-key-rotation-works}

A master key is composed of at least two master key parts. Before you rotate the master key, you need to have the master key parts prepared on your workstation. To be able to rotate a master key, the Current Master Key Register should be in `Valid` state with the current master key loaded and the New Master Key Register is empty.

The following flow shows how master key rotation works:

1. The master key parts are loaded to the New Master Key Register, so that the New Master Key Register is in `Full uncommitted` state with the new master key loaded.

2. The new master key is committed, and the New Master Key Register state is changed to `Full committed`.

3. After the master key rotation takes place, the new master key is activated and loaded to the Current Master Key Register in `Valid` state, and the New Master Key Register is cleared. All root keys and encryption keys managed in the crypto units are rewrapped with the new master key.

The following flow chart illustrates how the master key register state changes during the master key rotation.

![Rotating master keys](/image/rotate_master_key.svg "How to load a master key"){: caption="Figure 1. Loading master key" caption-side="bottom"}

## Root key rotation
{: #root-key-rotation-intro}

### Comparing your root key rotation options in {{site.data.keyword.hscrypto}}
{: #compare-key-rotation-options}

In {{site.data.keyword.hscrypto}}, you can rotate a root key  [on-demand](/docs/hs-crypto?topic=hs-crypto-rotate-keys) or [by setting a rotation policy](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy), without needing to keep track of your retired root key material.

<dl>
  <dt>Setting a rotation policy for a key</dt>
    <dd>{{site.data.keyword.hscrypto}} helps you simplify rotation for encryption keys by enabling rotation policies for keys that you generate in the service. After you create a root key, you can manage a rotation policy for the key in the {{site.data.keyword.hscrypto}} GUI or with the API. <a href="/docs/hs-crypto?topic=hs-crypto-key-rotation#rotation-frequency">Choose an automatic rotation interval between 1 - 12 months for your key</a> based on your on-going security needs. When it's time to rotate the key based on the rotation interval that you specify, {{site.data.keyword.hscrypto}} automatically replaces the key with new key material.</dd>
  <dt>Rotating keys on-demand</dt>
    <dd>As a security admin, you might want to have more control over the frequency of rotation for your keys. If you don't want to set an automatic rotation policy for a key, you can manually create a new key to replace an existing key, and then update your applications so that they reference the new key. To simplify this process, you can use {{site.data.keyword.hscrypto}} to rotate the key on-demand. In this scenario, {{site.data.keyword.hscrypto}} creates and replaces the key on your behalf with each rotation request. The key retains the same metadata and key ID.</dd>
</dl>

### How root key rotation works
{: #how-root-key-rotation-works}

Root key rotation works by securely transitioning key material from an *Active* to a *Deactivated* key state. To replace the deactivated or retired key material, new key material moves into the *Active* state and becomes available for cryptographic operations. For more information about different key states, refer to [Monitoring the lifecycle of encryption keys](/docs/hs-crypto?topic=hs-crypto-key-states).

#### Using {{site.data.keyword.hscrypto}} to rotate root keys
{: #use-hs-crypto-rotate-keys}

Keep in mind the following considerations as you prepare to use {{site.data.keyword.hscrypto}} for rotating root keys.

<dl>
  <dt>Rotating root keys that are generated in {{site.data.keyword.hscrypto}}</dt>
    <dd>You can use {{site.data.keyword.hscrypto}} to rotate a root key that was generated in {{site.data.keyword.hscrypto}} by setting a rotation policy for the key, or by rotating the key on-demand. The metadata for the root key, such as its key ID, does not change when you rotate the key.</dd>
  <dt>Rotating root keys that you bring to the service</dt>
    <dd>To rotate a root key that you initially imported to the service, you must generate and provide new key material for the key. You can use {{site.data.keyword.hscrypto}} to rotate imported root keys on-demand by supplying new key material as part of the rotation request. The metadata for the root key, such as its key ID, does not change when you rotate the key. Because you must provide new key material to rotate an imported key, automatic rotation policies are not available for root keys that have imported key material.</dd>
  <dt>Managing retired root key material</dt>
    <dd>{{site.data.keyword.hscrypto}} creates new key material after you rotate a root key. The service retires the old key material and retains the retired versions until the root key is deleted. When you use the root key for envelope encryption, {{site.data.keyword.hscrypto}} uses only the latest key material that is associated with the key. The retired key material can no longer be used to protect keys, but it remains available for unwrap operations. If {{site.data.keyword.hscrypto}} detects that you're using retired key material to unwrap DEKs, the service provides a newly wrapped DEK that's based on the latest root key material.</dd>
 <dt>Enabling root key rotation for {{site.data.keyword.cloud_notm}} data services</dt>
    <dd>To enable these root key rotation options for your data service on {{site.data.keyword.cloud_notm}}, the data service must be integrated with {{site.data.keyword.hscrypto}}. Refer to the documentation for your {{site.data.keyword.cloud_notm}} data service, or <a href="/docs/hs-crypto?topic=hs-crypto-integrate-services">check out our list of integrated services to learn more</a>.</dd>
</dl>

When you rotate a root key in {{site.data.keyword.hscrypto}}, you're not charged additional fees. You can continue to unwrap your wrapped data encryption keys (WDEKs) with retired key material at no extra cost. For more information about our pricing options, see the [{{site.data.keyword.hscrypto}} catalog page](https://{DomainName}/catalog/services/hs-crypto).
{: tip}

#### Understanding the root key rotation process
{: #understand-key-rotation-process}

Behind the scenes, the {{site.data.keyword.hscrypto}} key management API drives the key rotation process.

The following diagram shows a contextual view of the key rotation functionality.
![The diagram shows a contextual view of key rotation.](/image/key_rotation_min.svg "Key rotation"){: caption="Figure 1. Key rotation" caption-side="bottom"}

With each rotation request, {{site.data.keyword.hscrypto}} associates new key material with your root key.

![The diagram shows a micro view the root key stack.](/image/root_key_stack_min.svg "Root key stack"){: caption="Figure 2. Root key stack" caption-side="bottom"}

To learn how to use the {{site.data.keyword.hscrypto}} key management API to rotate your root keys, see [Rotating keys](/docs/hs-crypto?topic=hs-crypto-rotate-keys).
{: tip}

#### Rewrapping data after rotating a root key
{: #rewrap-data-after-key-rotation}

After a root key rotation completes, new root key material becomes available for protecting data encryption keys (DEKs) with [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption). Retired root key material moves to the _Deactivated_ state, where it can only be used to unwrap and access older DEKs that aren't yet protected by the latest root key.

To secure your envelope encryption workflow, [rewrap your DEKs](/docs/hs-crypto?topic=hs-crypto-rewrap-keys) after you rotate a root key so that your at-rest data is protected by the newest root key. Alternatively if {{site.data.keyword.hscrypto}} detects that you're using retired root key material to unwrap a DEK, the service automatically reencrypts the DEK and returns a wrapped data encryption key (WDEK) that's based on the latest root key. Store and use the new WDEK for future unwrap operations that the DEKs are protected with the newest root key material.

To learn how to use the {{site.data.keyword.hscrypto}} key management API to rewrap data encryption keys, see [Rewrapping keys](/docs/hs-crypto?topic=hs-crypto-rewrap-keys).
{: tip}

### Frequency of root key rotation
{: #rotation-frequency}

After you generate a root key in {{site.data.keyword.hscrypto}}, you decide the frequency of its rotation. You might want to rotate your keys due to personnel turnover, process malfunction, or according to your organization's internal key expiration policy.

Rotate your keys regularly, for example every 30 days, to meet cryptographic best practices.

| Rotation type | Frequency | Description |
| --- | --- | --- |
| [Policy-based root key rotation](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy) | Every 1 - 12 months | Choose a rotation interval between 1 - 12 months for your key based on your on-going security needs. After you set an rotation policy for a key, the clock starts immediately based on the initial creation date for the key. For example, if you set a monthly rotation policy for a key that you created on `2019/02/01`, {{site.data.keyword.hscrypto}} automatically rotates the key on `2019/03/01`.|
| [On-demand root key rotation](/docs/hs-crypto?topic=hs-crypto-rotate-keys) | Up to one rotation per hour | If you're rotating a key on-demand, {{site.data.keyword.hscrypto}} allows one rotation per hour for each root key. |
{: caption="Table 2. Rotation frequency options for rotating keys in {{site.data.keyword.hscrypto}}" caption-side="bottom"}

## What's next
{: #rotation-next-steps}

- To learn how to rotate a master key, see [Rotating your master key with the Trusted Key Entry (TKE) CLI](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli).
- To learn how to use {{site.data.keyword.hscrypto}} to set an automatic rotation policy for an individual key, see [Setting a rotation policy](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy).
- To find out more about manually rotating root keys, see [Rotating keys on-demand](/docs/hs-crypto?topic=hs-crypto-rotate-keys).
