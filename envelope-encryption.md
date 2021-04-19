---

copyright:
  years: 2018, 2020
lastupdated: "2020-07-22"

keywords: encryption at rest, envelope encryption, root key, data encryption key, key encryption key, key protect, protect data encryption key, encrypt data encryption key, wrap data encryption key, unwrap data encryption key

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Protecting your data with envelope encryption
{: #envelope-encryption}

Envelope encryption is the practice of encrypting data with a [data encryption key (DEK)](#x4791827){: term} and then wrapping the DEK with a [root key](#x6946961){: term} that you can fully manage. The root keys in {{site.data.keyword.hscrypto}} service instance are also wrapped and protected by the hardware security module (HSM) [master key](#x2908413){: term}.
{: shortdesc}

With envelope encryption, {{site.data.keyword.hscrypto}} protects your at-rest data with advanced encryption and offers several benefits:

<table>
  <th>Benefit</th>
  <th>Description</th>
  <tr>
    <td>Customer-managed encryption keys</td>
    <td>With the service, you can provision root keys to protect the security of your encrypted data in the cloud. Root keys serve as key-wrapping keys, which help you manage and safeguard the data encryption keys (DEKs) provisioned in {{site.data.keyword.cloud_notm}} data services. You decide whether to [import your existing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys), or have {{site.data.keyword.hscrypto}} [generate root keys on your behalf](/docs/hs-crypto?topic=hs-crypto-create-root-keys).</td>
  </tr>
  <tr>
    <td>Confidentiality and integrity protection</td>
    <td>{{site.data.keyword.hscrypto}} uses the Advanced Encryption Standard (AES) algorithm in Cipher Blocker Chaining (CBC) mode to create and protect keys. When you create keys in the service, {{site.data.keyword.hscrypto}} generates them in the {{site.data.keyword.hscrypto}} instance and the master key encrypts the keys to ensure only you have the access.</td>
  </tr>
  <tr>
    <td>Cryptographic shredding of data</td>
    <td>If your organization detects a security issue, or your application no longer needs a set of data, you can choose to shred the data permanently from the cloud. When you delete a root key that protects other DEKs, you ensure that the keys' associated data can no longer be accessed or decrypted.</td>
  </tr>
  <tr>
    <td>Delegated user access control</td>
    <td>By assigning {{site.data.keyword.iamshort}} (IAM) roles, {{site.data.keyword.hscrypto}} supports a centralized access control system to enable granular access for your keys. You can refer to [Granting access to keys](/docs/hs-crypto?topic=hs-crypto-grant-access-keys) for detailed information.</td>
  </tr>
  <caption style="caption-side:bottom;">Table 1. Describes the benefits of customer-managed encryption</caption>
</table>

## Keys in envelope encryption
{: #key-types}

The following keys are used in envelope encryption for the advanced encryption and management of data.

<dl>
  <dt>Master keys</dt>
  <dd>Master keys, also known as HSM master keys, are encryption keys used to protect the {{site.data.keyword.hscrypto}} instances. The master key provides full control of the hardware security module and ownership of the root of trust that encrypts the entire hierarchy of keys, including <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#root-key-concept">root keys</a> and <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept">standard keys</a>.</dd>
  <dt>Root keys</dt>
  <dd>Root keys, also known as customer root keys (CRKs), are primary resources in {{site.data.keyword.hscrypto}}. They are symmetric key-wrapping keys that are used as roots of trust for wrapping (encrypting) and unwrapping (decrypting) other keys that are stored in a data service. With {{site.data.keyword.hscrypto}}, you can create, store, and manage the lifecycle of root keys to achieve full control of other keys stored in the cloud.</dd>
  <dt>Data encryption keys</dt>
  <dd>Data encryption keys (DEKs) are cryptographic keys that you use for data encryption. They are provided by user-owned applications and are used to encrypt data stored in applications. Root keys that are managed in {{site.data.keyword.hscrypto}} serve as wrapping keys to protect DEKs.</dd>
  <!--
  <dt>Standard keys</dt>
    <dd>Standard keys are a way to persist data, such as a password or an encryption key. When you use {{site.data.keyword.hscrypto}} to store standard keys, you enable hardware security module (HSM) storage for data, fine-grained access control to your resources with <a href="/docs/hs-crypto?topic=hs-crypto-manage-access" target="_blank">{{site.data.keyword.iamshort}} (IAM)</a>, and the ability to audit API calls to the service with <a href="/docs/hs-crypto?topic=hs-crypto-at-events" target="_blank">{{site.data.keyword.cloudaccesstrailshort}}</a>.</dd>
  -->
</dl>

After you create a key in {{site.data.keyword.hscrypto}}, the system returns a key ID that is used to uniquely identify the key resource. You can use this ID value to make API calls to the service.

## How it works
{: #envelope-encryption-overview}

Envelope encryption combines the strength of multiple encryption algorithms to protect your sensitive data in the cloud. It works by wrapping one or more data encryption keys (DEKs) with advanced encryption by using a root key that you can fully manage. This key wrapping process creates wrapped DEKs that protect your stored data from unauthorized access or exposure. Unwrapping a DEK reverses the envelope encryption process by using the same root key, resulting in decrypted and authenticated data.

Root keys that are managed in a {{site.data.keyword.hscrypto}} service instance are also encrypted by the master key that ensures you full control of the entire key hierarchy.

The following diagram shows a contextual view of envelope encryption.

![The diagram shows a contextual view of envelope encryption.](/images/envelope-encryption.svg "The diagram shows a contextual view of envelope encryption."){: caption="Figure 1. Contextual view of envelope encryption" caption-side="bottom"}

Envelope encryption is treated briefly in the NIST Special Publication 800-57, Recommendation for Key Management. To learn more, see [NIST SP 800-57 Pt. 1 Rev. 4](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0){: external}

## Wrapping keys
{: #wrapping}

Root keys help you group, manage, and protect data encryption keys (DEKs) stored in the cloud. You can wrap one or more DEKs with advanced encryption by designating a root key in {{site.data.keyword.hscrypto}} that you can fully manage.

After you designate a root key in {{site.data.keyword.hscrypto}}, you can send a key wrap request to the service by using the [{{site.data.keyword.hscrypto}} key management API](/apidocs/hs-crypto#actiononkey){: external}.
The key wrap operation provides both confidentiality and integrity protection for a DEK.

The following diagram shows the key wrapping process in action.

![Wrapping data](/images/wrapping-keys.svg "The diagram shows key wrapping in action."){: caption="Figure 2. Wrapping data" caption-side="bottom"}

<!--
The following table describes the inputs that are needed to perform a key wrap operation:
<table>
  <th>Input</th>
  <th>Description</th>
  <tr>
    <td>Root key ID</td>
    <td>The ID value for the root key that you want to use for wrapping. The root key can be imported into the service, or it can be originated in {{site.data.keyword.hscrypto}} instance. Root keys that are used for wrapping must be 128, 192, or 256 bits so that a wrap request can succeed.</td>
  </tr>
  <tr>
    <td>Plain text</td>
    <td>Optional: The data encryption key (DEK) that you want to use for data encryption. This value must be base64 encoded. To generate a new DEK, you can omit the <code>plaintext</code> property. A random plaintext (32 bytes) that is rooted in an HSM is generated and is then wrapped.</td>
  </tr>
  <caption style="caption-side:bottom;">Table 2. Inputs required for key wrapping in {{site.data.keyword.hscrypto}}</caption>
</table>

If you send a wrap request without specifying the plaintext to encrypt, the AES-CBC encryption algorithm generates and converts a plaintext to an unintelligible form of data called a ciphertext. This process outputs a 256-bit DEK with new key material. The system then uses an AES key-wrapping algorithm, which wraps the DEK and its key material with the specified root key. A successful wrap operation returns a base64 encoded wrapped DEK that you can store in an {{site.data.keyword.cloud_notm}} app or service.
-->

## Unwrapping keys
{: #unwrapping}

Unwrapping a data encryption key (DEK) decrypts and authenticates the contents within the key, returning the original key material to your data service.

If your business application needs to access the contents of your wrapped DEKs, you can use the [{{site.data.keyword.hscrypto}} key management API](/apidocs/hs-crypto#actiononkey){: external} to send an
unwrap request to the service. To unwrap a DEK, you specify the ID value of the root key and the `ciphertext` value returned during the initial wrap request.

The following diagram shows key unwrapping in action.

![Unwrapping data](/images/unwrapping-keys.svg "The diagram shows key unwrapping in action."){: caption="Figure 3. Unwrapping data" caption-side="bottom"}

After you send the unwrap request, the system reverses the key wrapping process by using the same AES algorithms. A successful unwrap operation returns the base64 encoded `plaintext` value to your {{site.data.keyword.cloud_notm}} data at rest service.

## What's next
{: #envelope-encryption-next}

{{site.data.keyword.hscrypto}} supports the integration with other services. With envelope encryption, {{site.data.keyword.hscrypto}} provides advanced protection to your data stored in the integrated services.

- For the full list of supported services for integration, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- For how to create a root key for envelope encryption, see [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
- For how to bring your own root keys for envelope encryption, see [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys).
