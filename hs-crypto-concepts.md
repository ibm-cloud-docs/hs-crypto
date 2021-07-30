---

copyright:
  years: 2018, 2021
lastupdated: "2021-07-30"

keywords: concept, keep your own key, encryption key management, kyok, smart card, master key, root key, smart card utility program, trusted key entry application, key concepts, hsm concepts, terms, terminology

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
{:term: .term}

# Components and concepts
{: #understand-concepts}

Before you can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to manage encryption keys and protect data, learn the basic components and concepts of {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Key management service
{: #key-management-concepts}

Learn concepts that are related to the {{site.data.keyword.hscrypto}} [key management feature](/docs/hs-crypto?topic=hs-crypto-overview#key-management) to manage encryption keys. The list starts with the most fundamental concepts.

### Root keys
{: #root-key-concept}

Root keys, also known as customer root keys (CRKs), are primary resources in {{site.data.keyword.hscrypto}}. They are symmetric key-wrapping keys that are used as roots of trust for wrapping (encrypting) and unwrapping (decrypting) other data encryption keys (DEKs) that are stored in a data service. With {{site.data.keyword.hscrypto}}, you can create, store, and manage the lifecycle of root keys. Root keys that are created in {{site.data.keyword.hscrypto}} are symmetric 256-bit AES keys. Unlike a standard key, a root key can never leave the bounds of the {{site.data.keyword.hscrypto}} service. To learn more, see [Introduction to envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) and [Manage your keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys).

### Standard keys
{: #standard-key-concept}

Standard keys are another resources in {{site.data.keyword.hscrypto}} to directly encrypt and decrypt data. You can manage standard keys by following steps in [Manage your keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys).

### Data encryption keys
{: #dek-concept}

Data encryption keys (DEKs) are cryptographic keys that you use for data encryption. They are provided by user-owned applications and are used to encrypt data stored in applications. Root keys that you manage in {{site.data.keyword.hscrypto}} serve as wrapping keys to protect DEKs. To learn more, see [Introduction to envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).

### Envelope encryption
{: #envelope-encryption-concept}

Envelope encryption is the practice of encrypting data with a DEK and then encrypting the DEK with a root key that you can fully manage. To learn more, see [Introduction to envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).






## Cloud hardware security module
{: #cloud-hsm-concepts}

This section covers concepts that are related to {{site.data.keyword.hscrypto}} [Cloud Hardware Security Module (HSM) feature](/docs/hs-crypto?topic=hs-crypto-overview#cloud-hsm). The list starts with the most fundamental concepts.

### Hardware security module
{: #hsm-concept}

A hardware security module (HSM) is a physical device that safeguards and manages digital keys for strong authentication and provides crypto-processing. HSMs of {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} are FIPS 140-2 Level 4 certified, which is the highest level of security for cryptographic hardware. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access.

### Crypto units
{: #crypto-unit-concept}

A crypto unit is a single unit that represents an HSM and the corresponding software stack that is dedicated to the HSM for cryptography. In {{site.data.keyword.hscrypto}}, the following types of crypto unit are available:

- Operational crypto unit

  When you create a {{site.data.keyword.hscrypto}} instance, the number of crypto units that you specify is the number of operational crypto units. For high availability and disaster recovery, you need to set up at least two operational crypto units. These operational crypto units are located in different [availability zones](https://www.ibm.com/cloud/data-centers/){: external} of the same region where your service instance resides. Operational crypto units are used to manage encryption keys and perform cryptographic operations. Each operational crypto unit can manage up to 5000 digital keys.

- Recovery crypto unit

  If you create your service instance in Dallas (`us-south`) or Washington DC (`us-east`), two recovery crypto units are automatically assigned to your service instance without extra costs. A recovery crypto unit is used to generate the random master key which is then securely exported to operational crypto units and the other recovery crypto unit to [initialize the service instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit).

  Recovery crypto units can also be used as backup crypto units that save a copy of the master key value used by the operational crypto units. If the master key is lost or destroyed, you can [recover the master key from a recovery crypto unit](/docs/hs-crypto?topic=hs-crypto-recover-master-key-recovery-crypto-unit) using signed TKE administrative commands.

- Failover crypto unit

  Failover crypto units back up the operational crypto units and keystores in another region. When a regional disaster occurs, you can use failover crypto units to ensure production workloads and avoid data loss. Failover crypto units [charge extra fees](/docs/hs-crypto?topic=hs-crypto-faq-pricing) and this option is now available only in regions of `us-south` and `us-east`, which means if you create your instance in either of the two regions, the failover crypto units are located in the other region. For more information about using failover crypto units in a regional disaster, see [Restoring your data by using failover crypto units](/docs/hs-crypto?topic=hs-crypto-restore-data#restore-data-failover-crypto-units).

### Administrators
{: #admin-concept}

Administrators can be added to the target crypto units for issuing commands to the crypto units. You can add up to eight administrators to one crypto unit to increase security. Each administrator owns one private [signature key](#signature-key-concept) for identity authentication.

### Signature keys
{: #signature-key-concept}

An administrator must sign any commands that are issued to the crypto unit with a signature key. The signature keys that are created in {{site.data.keyword.hscrypto}} are P521 Elliptic Curve (EC) keys. The private part of the signature key is used to create signatures. The public part is placed in a certificate that is installed in a target crypto unit to define a crypto unit administrator. Commands issued in [imprint mode](#imprint-mode-concept) do not need to be signed with any signature keys.

### Imprint mode
{: #imprint-mode-concept}

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user start in a cleared state that is known as *imprint mode*. Most crypto unit operations are disabled in imprint mode, and a crypto unit in imprint mode is not secure. You can add administrators in imprint mode and exit imprint mode by using a signed command. After the crypto unit exits imprint mode, all commands to configure a crypto unit must be signed. You must exit imprint mode before you can load [master keys](#master-key-concept).

### Quorum authentication
{: #quorum-authenticaion-concept}

Quorum authentication is the way to approve an operation by a set number of crypto unit administrators. Some sensitive operations require a sufficient number of crypto unit administrators to enter their credentials. Quorum authentication assures that no single person can make a critical change on the crypto unit. Instead, a minimum number of crypto unit administrators (at least two) must cooperate to do these operations. Quorum authentication requires more than one crypto unit administrator to approve an operation, which enables an extra layer of protection on the crypto unit.

### Signature thresholds
{: #signature-thresholds-concept}

The signature thresholds of a crypto unit control how many administrative signatures are needed to run a command. In imprint mode, the signature thresholds are set to zero. To exit imprint mode, set the signature thresholds to a value greater than zero. When a crypto unit is zeroized, the signature thresholds are reset to zero.

There are two types of signature thresholds on a crypto unit. The main signature threshold controls how many signatures are needed to run most administrative commands. The revocation signature threshold controls how many signatures are needed to remove an administrator. Some commands need only one signature, regardless of how the signature threshold is set.

Setting the signature thresholds to a value greater than one enables quorum authentication from multiple administrators for sensitive operations. The maximum value that you can set the signature threshold and revocation signature threshold is eight, which is also the maximum number of administrators that can be added to a crypto unit.

### Master key
{: #master-key-concept}

The master key, also known as HSM master key, is used to encrypt the service instance for key storage. It is a symmetric 256-bit AES key. With the master key, you take the ownership of the cloud HSM and own the root of trust that encrypts the entire hierarchy of encryption keys, including root keys and standard keys in the key management keystore and Enterprise PKCS #11 (EP11) keys in the EP11 keystore. You need to configure the master key first before you can manage encryption keys. One service instance can have only one master key. If you delete the master key of the service instance, you can effectively crypto-shred all data that was encrypted with the keys that are managed in the service.

### Master key part
{: #master-key-part-concept}

If you initialize your service instance using key part files, or using smart cards together with the Management Utilities, a master key is composed of several master key parts. Master key parts that are created in {{site.data.keyword.hscrypto}} are symmetric 256-bit AES keys. For security considerations, each key part can be owned by a different person. Key parts are stored in workstation key part files when the [{{site.data.keyword.cloud_notm}} TKE CLI plug-in](#tke-concept) is used to load the master key. Key parts are stored on [smart cards](#smart-card-concept) when the [{{site.data.keyword.hscrypto}} Management Utilities](#management-utilities-concept) are used to load the master key. The key part owner needs to be the only person who knows the file password or the smart card personal identification number (PIN) for the key part.

### {{site.data.keyword.cloud_notm}} Trusted Key Entry CLI plug-in
{: #tke-concept}

Trusted Key Entry (TKE) command-line interface (CLI) plug-in is a CLI plug-in working with {{site.data.keyword.cloud_notm}} CLI. The TKE plug-in provides a set of functions for managing crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user account. You can use the TKE plug-in to set up administrators and load the master key with the requirements of a medium level of security. The TKE CLI plug-in provides two approaches to initializing service instances: [Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) and [Initializing service instances using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit). For the complete command reference, see [Trusted Key Entry CLI plug-in reference](/docs/hs-crypto?topic=hs-crypto-cli-plugin-hpcs-cli-plugin#tke-cli-plugin).

### Management Utilities
{: #management-utilities-concept}

The Management Utilities provide an alternate way of configuring service instances with signature keys and master key parts that are stored on smart cards with the highest level of security. To use the Management Utilities, you must order IBM-supported smart card readers and smart cards. For detailed instructions on installing and configuring the Management Utilities, see [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

### Smart cards
{: #smart-card-concept}

A smart card looks like a credit card with an embedded chip. The chip can perform a limited set of cryptographic operations and is loaded with custom software. In the Management Utilities, the Smart Card Utility Program loads custom software on the smart card to create two types of smart cards:

- Certificate authority smart cards - Establish a set of smart cards that can work together, called a smart card zone.
- Enterprise PKCS #11 (EP11) smart cards - Hold an administrator signature key and up to 85 master key parts. With EP11 smart cards, you can sign a command by using a private signature key that is stored on the smart card and encrypt a master key part for delivery to a crypto unit.

Smart cards are protected by a personal identification number (PIN) that must be entered on a smart card reader PIN pad before the smart card performs the operations. The EP11 smart card has a single PIN. The certificate authority smart card has two PINs and both must be entered to enable operations.

On an EP11 smart card, if an incorrect PIN is entered three times, the smart card becomes blocked and can't be used for operations that require PIN entry. An EP11 smart card can be unblocked by using the Smart Card Utility Program. You need the certificate authority smart card that is used to initialize the EP11 smart card to unblock an EP11 smart card. To unblock an EP11 smart card, select **EP11 Smart Card** > **Unblock EP11 smart card** from the menu, and follow the prompts.

A certificate authority smart card becomes blocked if an incorrect PIN is entered five times. If a certificate authority smart card becomes blocked, it can't be unblocked.

### Smart card readers
{: #smart-card-reader-concept}

A smart card reader is a device that attaches to a workstation and allows the workstation to communicate with a smart card. To access a smart card, the smart card must be inserted in the smart card reader. Most smart card operations require the smart card PIN to be entered on the smart card reader PIN pad.

A driver for the smart card reader must be installed on the workstation before the smart card reader can be used. For more information, see [Installing the smart card reader driver](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver).

### Smart Card Utility Program
{: #smart-card-utility-concept}

The Smart Card Utility Program is one of the two applications that are installed as part of the Management Utilities. It sets up and manages the smart cards that are used by the Trusted Key Entry (TKE) application.

### Trusted Key Entry application
{: #tke-client-concept}

The Trusted Key Entry (TKE) application is one of the two applications that are installed as part of the Management Utilities. It uses smart cards to load master keys in service instances and to perform other configuration tasks for service instances.

### Keep Your Own Key
{: #kyok-concept}

{{site.data.keyword.hscrypto}} supports the Keep Your Own Key (KYOK) feature. You can configure the master key to take the full control of the cloud HSM, so that you have full control and authority over encryption keys that you can bring, control, and manage. No one except you have access to your encryption keys.

### PKCS #11
{: #pkcs-concept}

Public-Key Cryptography Standards (PKCS) #11 API defines a platform-independent API to cryptographic tokens, such as HSM and smart cards. Existing applications that use PKCS #11 can benefit from enhanced security by using secure key cryptography as well as stateless interface, which makes the cryptographic operations much more efficient. For more information, see [PKCS #11 API](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}.

### Cryptoki
{: #cryptoki-concept}

The Cryptographic Token Interface defined in the PKCS #11 standard. Cryptoki follows a simple object based approach, addressing the goals of technology independence and resource sharing.

### PKCS #11 library
{: #pkcs11-library-concept}

A PKCS #11 library that implements the Cryptoki API functions that are specified in the PKCS #11 standard. With the PKCS #11 library, your applications can use the PKCS #11 API to access the {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations. To learn more about how to set up the library, see [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api).

### Cryptoki token
{: #cryptoki-token-concept}

The logical view of a cryptographic device that is defined by Cryptoki. For more information, see [PKCS #11 Cryptographic Token Interface Usage Guide Version 2.40 - Logical view of a token](http://docs.oasis-open.org/pkcs11/pkcs11-ug/v2.40/cn02/pkcs11-ug-v2.40-cn02.html#_Toc406759983){: external}.

### Cryptoki session
{: #cryptoki-session-concept}

A logical connection between an application and a token. Cryptoki requires that an application open one or more sessions with a token to gain access to the objects and functions of the token. A session can be a read/write (R/W) session or a read-only (R/O) session. For more information, see [Introducing PKCS #11 - Session](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro#pkcs11-session-intro).

### Cryptoki object
{: #cryptoki-object-concept}

An item that is stored on a token. An object can be data, a certificate, or a key. A data object is defined by an application. A certificate object stores a certificate. A key object stores a cryptographic key. Each characteristic of the object is defined in an *attribute*. For more information, see [Introducing PKCS #11 - Key object](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro#pkcs11-object-intro).

### Mechanism
{: #mechanism-concept}

A process for implementing a cryptographic operation.

### Enterprise PKCS #11
{: #ep11-concept}

Enterprise PKCS #11 (EP11) is designed for customers that are seeking support for open standards and enhanced security. The EP11 library provides a stateless interface, which is similar to the industry-standard PKCS #11 API. The HSM that crypto units run on supports EP11 library, so users can call EP11 API through [gRPC](#grpc-concept) for their own key management and data encryption. For more information, see [Enterprise PKCS #11 (EP11) Library structure document](https://www.ibm.com/security/cryptocards/pciecc4/library){: external}.

### gRPC
{: #grpc-concept}

gRPC is a modern open source high performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} EP11 library by calling the EP11 API remotely through gRPC. For more information about gRPC, see [the gRPC documentation](https://grpc.io/docs/guides/index.html){: external}.

### Enterprise PKCS #11 over gRPC
{: #grep11-concept}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a set of the Enterprise PKCS #11 (EP11) over [gRPC](https://grpc.io){: external} API calls (also referred to as GREP11), with which all the Crypto functions are executed in a cloud HSM. EP11 over gRPC is a stateless interface for cryptographic operations on cloud. For more information about the GREP11 API, see [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-grep11_intro) and [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
