---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# Introduction to keys
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} supports several key types, including root keys, standard keys, and master keys.
{:shortdesc}

## Root Keys

*Root keys* are symmetric key-wrapping keys that you fully manage in {{site.data.keyword.hscrypto}}. You can use a root key to protect other cryptographic keys with advanced encryption. To learn more, see <a href="/docs/services/key-protect/concepts/envelope-encryption.html">Envelope encryption</a>.

You can manage root keys by following steps in [Manage your keys](index.html#manage-keys).

## Standard keys

*Standard keys* are symmetric keys that are used for cryptography. You can use a standard key to directly encrypt and decrypt data.

You can manage standard keys by following steps in [Manage your keys](index.html#manage-keys).

## Master keys

*Master keys* are used to encrypt the crypto instance (HSM) that crypto-processes and manages root keys and standard keys. With the master key, you own the root of trust that encrypts the entire chain of Keys including root keys and standard keys.

Because of the established end-to-end secured channel to the crypto instance (HSM), only the administrators of the {{site.data.keyword.hscrypto}} instance can set and manage the master key. Note that IBM does not back up or touch the master key, and has no way to copy it or restore it to a different machine or data center.

One crypto instance (HSM) can have only one master key. If you delete the master key of the {{site.data.keyword.hscrypto}} instance, you can effectively crypto-shred all data that was encrypted with the keys managed in the service.

You can manage master keys when [Initializing crypto instances to protect key storage](initialize_hsm.html).

Rotating master key is not supported in the current stage.
{:important}
