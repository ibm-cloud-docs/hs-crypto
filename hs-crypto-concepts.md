---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-19"

Keywords: key concepts, HSM concepts，Hyper Protect Crypto Services concepts, terms, terminology

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}

# Components and concepts
{: #understand-concepts}

Before you can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to manage keys and protect data, read this topic to learn the basic components and concepts of {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Key management service
{: #key-management-concepts}

This section covers concepts that are related to the {{site.data.keyword.hscrypto}} [key management feature](/docs/services/hs-crypto?topic=hs-crypto-overview#key-management). The list starts with the most fundamental concepts.

### Root keys
{: #root-key-concept}

Root keys are primary resources in {{site.data.keyword.hscrypto}}. They are symmetric key-wrapping keys that are used as roots of trust for wrapping (encrypting) and unwrapping (decrypting) other keys stored in a data service. With {{site.data.keyword.hscrypto}}, you can create, store, and manage the lifecycle of root keys to achieve full control of other keys stored in the cloud. Unlike a standard key, a root key can never leave the bounds of the {{site.data.keyword.hscrypto}} service. To learn more, see [Introduction to envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) and [Manage your keys](/docs/services/hs-crypto?topic=hs-crypto-get-started#manage-keys).

### Standard keys
{: #standard-key-concept}

Standard keys are another resources in {{site.data.keyword.hscrypto}} to directly encrypt and decrypt data. You can manage standard keys by following steps in [Manage your keys](/docs/services/hs-crypto?topic=hs-crypto-get-started#manage-keys).

### Data encryption keys
{: #dek-concept}

Data encryption keys (DEKs) are cryptographic keys that you use for data encryption. They are provided by user-owned applications and are used to encrypt data stored in applications. Root keys managed in {{site.data.keyword.hscrypto}} serve as wrapping keys to protect DEKs. To learn more, see [Introduction to envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption).

### Envelope encryption
{: #envelope-encryption-concept}

Envelope encryption is the practice of encrypting data with a DEK and then encrypting the DEK with a root key that you can fully manage. To learn more, see [Introduction to envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption).

### Bring Your Own Key
{: #byok-concept}

The Bring Your Own Keys (BYOK) feature allows you to import your existing keys to {{site.data.keyword.hscrypto}} service instances that protect your keys with advanced encryption. With BYOK, you can extend your own keys from internal key management infrastructure to the cloud in a highly secured environment.

<!-- ### Transport Keys
{: #transport-key-concept}

Transport keys are a resource type in {{site.data.keyword.hscrypto}} that enable the secure import of root key material to your service instance. By using a transport key to encrypt your key material on-premises, you protect root keys while they're in flight to {{site.data.keyword.hscrypto}} based on the policies that you specify. For example, you can set a policy on the transport key that limits the use of the key based on time and usage count. -->


## Cloud hardware security module
{: #cloud-hsm-concepts}

This section covers concepts that are related to {{site.data.keyword.hscrypto}} [cloud Hardware Security Module (HSM) feature](/docs/services/hs-crypto?topic=hs-crypto-overview#cloud-hsm). The list starts with the most fundamental concepts.

### Hardware security module
{: #hsm-concept}

Hardware security module (HSM) is a physical device that safeguards and manages digital keys for strong authentication and provides crypto-processing. HSMs of {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} are FIPS 140-2 Level 4 certified, which is the highest level of security for cryptographic hardware. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access.

### Crypto unit
{: #crypto-unit-concept}

A crypto unit is a single unit that represents an HSM and the corresponding software stack dedicated to HSM. Each crypto unit can manage up to 5000 digital keys. If you are setting up a production environment, it is suggested to assign at least two crypto units per service instance for high availability. The two crypto units are located in different [availability zones](https://www.ibm.com/cloud/blog/announcements/expansion-availability-zones-global-regions){: external} within the region that you select when creating the service instance. If one part of availability zones cannot be accessed, the crypto units in a service instance can be used interchangeably. All crypto units in a service instance should be configured the same.

### Administrators
{: #admin-concept}

Administrators can be added to the target crypto units for issuing commands to the crypto units. You can add multiple administrators to one crypto unit to increase security. Each administrator owns one private [signature key](#signature-key-concept) for identity authentication.

### Signature keys
{: #signature-key-concept}

An administrator must sign any commands issued to the crypto unit with a signature. The private part of the signature key file is used to create signatures. The public part is placed in a certificate that is installed in a target crypto unit to define a crypto unit administrator. Commands issued in [imprint mode](#imprint-mode-concept) do not need to be signed.

### Imprint mode
{: #imprint-mode-concept}

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user start in a cleared state known as imprint mode. A crypto unit in imprint mode is not secure. You can only set up crypto unit administrators and signature keys in imprint mode. Commands issued to a crypto unit in imprint mode do not need to be signed. However, the command to exit imprint mode must be signed by one of the added crypto unit administrators using the signature key. Make sure to exit imprint mode before you configure [master keys](#master-key-concept).

### Master keys
{: #master-key-concept}

Master keys are used to encrypt the service instances for key storage. With the master key, you take the full control of the cloud HSM and own the root of trust that encrypts the entire chain of keys including root keys and standard keys. You need to configure the master key first before you can manage root keys and standard keys. {{site.data.keyword.IBM_notm}} does not back up or touch the master key, and has no way to copy it or restore it to a different machine or data center. One service instance can have only one master key. If you delete the master key of the service instance, you can effectively crypto-shred all data that was encrypted with the keys managed in the service.

A master key is composed of several master key parts. For security considerations, each key part can be owned by a different person. The key part owner should be the only person who knows the password associated with the key part file.

### Trusted Key Entry plug-in
{: #tke-concept}

Trusted Key Entry (TKE) plug-in is a CLI plugin working with {{site.data.keyword.cloud_notm}} CLI. The TKE plug-in provides a set of functions for managing crypto units assigned to an {{site.data.keyword.cloud_notm}} user account. Use the TKE plug-in to set up administrators and load the master key.

<!--You can use it for following operations:

- Set up administrators and corresponding signature keys for crypto units.
- Exit imprint mode for further securely managing crypto units.
- Configure master keys to take the full control of cloud HSM.-->

For more information, see [Initializing service instances](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm) and [Trusted Key Entry CLI plug-in reference](/docs/services/hs-crypto?topic=hs-crypto-tke_cli_plugin).

<!-- ### Smart Cards
{: #smart-card-concept}

The smart card is an HSM with encryption capability, and provides the following features to ensure high security:

- Each smart card is protected by a PIN code.
- Each smart card contains the administrator's master key part and signature key.
- Master key parts leaves the smart cards HSM only when it is encrypted.
- The private part of signature keys never leaves the smart card's HSM. -->

### Keep Your Own Key
{: #kyok-concept}

{{site.data.keyword.hscrypto}} supports Keep Your Own Keys (KYOK) feature. It allows you to configure the master key to take the full control of the cloud HSM, so that you have full control and authority over encryption keys that you can bring, control, and manage. No one except you have access to your data.

### PKCS #11
{: #pkcs-concept}

Public-Key Cryptography Standards (PKCS) #11 API defines a platform-independent API to cryptographic tokens, such as HSM and smart cards. Existing applications using PKCS #11 can benefit from enhanced security using secure key cryptography as well as stateless interface, which makes the cryptographic operations much more efficient. For more information, see [PKCS #11 API](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}.

### Enterprise PKCS #11
{: #ep11-concept}

Enterprise PKCS #11 (EP11) is specifically designed for customers seeking support for open standards and enhanced security. The EP11 library provides a stateless interface, which is similar to the industry-standard PKCS #11 API. The HSM that crypto units run on supports EP11 library, so users can call EP11 API through [gRPC](#grpc-concept) for their own key management and data encryption. For more information, see [Introduction to Enterprise PKCS #11](/docs/services/hs-crypto?topic=hs-crypto-enterprise_PKCS11_overview) and [Enterprise PKCS #11 (EP11) Library structure document](https://www.ibm.com/downloads/cas/WXRDPRAN){: external}.

### gRPC
{: #grpc-concept}

gRPC is a modern open source high performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} EP11 library by calling the EP11 API remotely through gRPC. For more information on gRPC, see [the gRPC documentaion](https://grpc.io/docs/guides/index.html){: external}.

### Enterprise PKCS #11 over gRPC
{: #grep11-concept}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 (EP11) APIs over [gRPC](https://grpc.io){: external} calls (also referred to as GREP11), with which all the Crypto functions are executed in a cloud HSM. EP11 over gRPC is designed to be a stateless interface for cryptographic operations on cloud. For more information on the GREP11 API, see [GREP11 API reference](/docs/services/hs-crypto?topic=hs-crypto-grep11-api-ref).

## {{site.data.keyword.hscrypto}} architecture
{: #hs-crypto-architecture}

Refer to the following architectural diagram to see how components of {{site.data.keyword.hscrypto}} co-works to protect your sensitive data and keys.

![Service instance components](/image/hs-crypto-components.png "Service instance components")
*Figure 1. Service instance components*
