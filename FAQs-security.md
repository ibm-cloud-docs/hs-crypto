---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-21"

keywords: frequently asked questions, cryptographic algorithm, regions, pricing, security compliance, key ceremony, critical security parameters, cryptographic module, security Level, fips, data security, compliance

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:faq: data-hd-content-type='faq'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# FAQs: Security and compliance
{: #faq-security-compliance}

Read to get answers for questions about data security in {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## How can I manage user access to my service instances? Does IBM have access to my instances?
{: #faq-hpcs-ibm-access}
{: faq}
{: support}

IBM or any third-party users do not have access to your service instances or your keys. By loading the master key to your service instance, you take the ownership of the cloud HSM and you have the exclusive control of your resources managed by {{site.data.keyword.hscrypto}}.

{{site.data.keyword.hscrypto}} follows the {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) standard. You can [manage user access by assigning different IAM roles](/docs/hs-crypto?topic=hs-crypto-manage-access) and [grant access to specific keys](/docs/hs-crypto?topic=hs-crypto-grant-access-keys) to enable more granular access control.



## How does IBM offer a unique and secure process for service initialization (key ceremony)?
{: #faq-hpcs-user-access}
{: faq}

{{site.data.keyword.hscrypto}} sets up signature keys for crypto unit administrators during the service initialization process to ensure that the master key parts are loaded to the HSM with no interception.

A master key is composed of two or three master key parts. Each master key custodian owns one encrypted master key part. In most cases, a master key custodian can also be a crypto unit administrator. In order to load the master key to the service instance, master key custodians need to load their key parts separately using their own administrator signature keys.

A signature key is composed of an asymmetric key pair. The private part of the signature key is owned by the crypto unit administrator, while the public part is placed in a certificate that is used to define an administrator and never leaves the crypto unit.

This design ensures that no one can get full access of the master key, even the crypto unit administrators.

## What is a 140-2 FIPS Level 4 Certification and how can I validate it?
{: #faq-fips-level4-meaning}
{: faq}

The Federal Information Processing Standard (FIPS) Publication 140-2 is a US government computer security standard that is used to approve cryptographic modules.

- [Security Requirements for Cryptographic Modules](https://csrc.nist.gov/publications/detail/fips/140/2/final){: external}.
- [Cryptographic Module Validation Program](https://csrc.nist.gov/Projects/cryptographic-module-validation-program){: external}.
- FIPS 140-2 defines four levels of security, including FIPS 140-2 Level 1, 2, 3, and Level 4.

## What is the difference between FIPS 140-2 Level 1, 2, 3, and Level 4?
{: #faq-fips-levels}
{: faq}

- **Level 1**: The lowest level of security. No specific physical security mechanisms are required in a Security Level 1 cryptographic module beyond the basic requirement for production-grade components.
- **Level 2**: Improves the physical security mechanisms of a Level 1 cryptographic module by requiring features that show evidence of tampering including tamper-evident coatings or seals that must be broken to attain physical access to the plaintext cryptographic keys and critical security parameters (CSPs) within the module, or pick-resistant locks on covers or doors to protect against unauthorized physical access. Security Level 2 requires, at minimum, role-based authentication in which a cryptographic module authenticates the authorization of an operator to assume a specific role and perform a corresponding set of services.
- **Level 3**: Provides a high probability of detecting and responding to attempts at physical access, use, or modification of the cryptographic module. The physical security mechanisms can include the use of strong enclosures and tamper-detection and response circuitry that zeroizes all plaintext CSPs when the removable covers or doors of the cryptographic module are opened. Security Level 3 requires identity-based authentication mechanisms, enhancing the security provided by the role-based authentication mechanisms specified for Security Level 2.
- **Level 4**: The highest level of security. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a high probability of being detected, resulting in the immediate zeroization of all plaintext CSPs.

    Security Level 4 cryptographic modules are useful for operation in physically unprotected environments. Security Level 4 also protects a cryptographic module against a security compromise because of environmental conditions or fluctuations outside of the module's normal operating ranges for voltage and temperature. Intentional excursions beyond the normal operating ranges can be used by an attacker to prevent a cryptographic module's defenses.

    A cryptographic module is required to either include special environmental protection features designed to detect fluctuations and delete CSPs, or to undergo environmental failure testing to ensure that the module will not be affected by fluctuations outside of the normal operating range in a manner that can compromise the security of the module. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access.

    {{site.data.keyword.hscrypto}} is the only cloud HSM in the public cloud market that is built on an HSM designed to meet FIPS 140-2 Level 4 certification requirements. The certification is listed on the [Cryptographic Module Validation Program (CVMP) Validated Modules List](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules){: external}.

## How to understand the key hierarchy for {{site.data.keyword.hscrypto}} KYOK?
{: #faq-cryptographic-algorithms}
{: faq}
{: support}

The following table lists the keys that are needed for {{site.data.keyword.hscrypto}} Keep Your Own Key (KYOK) functionality.

| Key types | Algorithms | Functions |
| --------- | --------- | --------- |
| Signature key   | P521 Elliptic Curve (EC) | When you [initialize your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-introduce-service) to load the master key, you need to use signature keys to issue commands to the crypto units. The private part of the signature key is used to create signatures and is stored on the customer side. The public part is placed in a certificate that is stored in the target crypto unit to define a crypto unit administrator. |
| Master key   | 256-bit AES | You need to load your master key to the crypto units to take the ownership of the cloud HSM and own the root of trust that encrypts the entire hierarchy of encryption keys, including root keys and standard keys in the key management keystore and Enterprise PKCS #11 (EP11) keys in the EP11 keystore. Depending on [the method that you use to load the master key](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode), the master key is stored in different locations. |
| Root key   | 256-bit AES  | Root keys are primary resources in {{site.data.keyword.hscrypto}} and are protected by the master key. They are symmetric key-wrapping keys that are used as roots of trust for wrapping (encrypting) and unwrapping (decrypting) other data encryption keys (DEKs) that are stored in a data service. This practice of root key encryption is also called envelope encryption. For more information, see [Protecting your data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption). |
| Data encryption key (DEK)  | Controlled by the data service | Data encryption keys are used to encrypt data that is stored and managed by other customer-owned applications or data services. Root keys that you manage in {{site.data.keyword.hscrypto}} serve as wrapping keys to protect DEKs. For services that support the integration of {{site.data.keyword.hscrypto}} for envelope encryption, see [Integrating {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-integrate-services).  |
{: caption="Table 1. {{site.data.keyword.hscrypto}} key types and algorithms" caption-side="bottom"}

## How does EP11 differ from PKCS #11?
{: #faq-ep11-pkcs11}
{: faq}
{: support}

Enterprise PKCS #11 (EP11) is aligned with PKCS #11 in terms of concepts and functions. An experienced PKCS #11 developer can easily start using EP11 functions. However, they have the following major differences:

- EP11 is built to allow high availability and scalability by design.
- EP11 is a stateless protocol, whereas PKCS #11 is stateful. The stateless design of EP11 allows for the use of external keystores as well as scaling to multiple backends.
- EP11 over gRPC (GREP11) defines a network protocol that can be directly used in cloud applications.

For more information, see [Comparing the PKCS #11 API with the GREP11 API](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm#compare-grep11-pkcs11).

## What EP11 mechanisms are supported by the GREP11 functions?
{: #faq-EP11-mechanisms}
{: faq}

Mechanisms can vary depending on the level of firmware in the IBM 4768 crypto card (also referred to as Crypto Express 6S). For mechanisms that are   supported, see [Supported mechanisms](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-mechanism-list).

For more information about the EP11 mechanisms, see the [Enterprise PKCS #11 (EP11) Library structure guide](https://www.ibm.com/security/cryptocards/pciecc4/library){: external}.

## What compliance standards does {{site.data.keyword.hscrypto}} meet?
{: #faq-compliance-standards}
{: faq}

{{site.data.keyword.hscrypto}} meets controls for global, industry, and regional compliance standards, such as GDPR, HIPAA, and ISO. As the HSM used by {{site.data.keyword.hscrypto}}, the IBM 4768 crypto card is also certified with Common Criteria EAL4 and FIPS 140-2 Level 4. For more information, see [Security and compliance](/docs/hs-crypto?topic=hs-crypto-security-and-compliance).

## Can I monitor my service instance?
{: #faq-monitor-instance}
{: faq}

Yes, you can monitor the status of your service instance through [{{site.data.keyword.cloud_notm}} Activity Tracker](/docs/hs-crypto?topic=hs-crypto-at-events).
