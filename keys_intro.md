---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}

# Introduction to keys
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} supports several key types, including root keys, standard keys, and master keys.
{:shortdesc}

## Root Keys
{: #introduce-root-keys}

*Root keys* are symmetric key-wrapping keys that you fully manage in {{site.data.keyword.hscrypto}}. You can use a root key to protect other cryptographic keys with advanced encryption. To learn more, see <a href="/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption">Envelope encryption</a>.

You can manage root keys by following steps in [Manage your keys](/docs/services/hs-crypto?topic=hs-crypto-get-started#manage-keys).

## Standard keys
{: #introduce-standard-keys}

*Standard keys* are symmetric keys that are used for cryptography. You can use a standard key to directly encrypt and decrypt data.

You can manage standard keys by following steps in [Manage your keys](/docs/services/hs-crypto?topic=hs-crypto-get-started#manage-keys).

## Master keys
{: #introduce-master-keys}

*Master keys* are used to encrypt the service instance for key storage. With the master key, you own the root of trust that encrypts the entire chain of Keys including root keys and standard keys.

Because of the established end-to-end secured channel to the service instance, only the administrators of the service instance can set and manage the master key. Note that IBM does not back up or touch the master key, and has no way to copy it or restore it to a different machine or data center.

One service instance can have only one master key. If you delete the master key of the service instance, you can effectively crypto-shred all data that was encrypted with the keys managed in the service.

You can manage master keys when [Initializing service instances to protect key storage](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm).

Rotating master key is not supported at the current stage.
{:important}
