---

copyright:
  years: 2018, 2020
lastupdated: "2020-05-06"

keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level，questions and answers

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:faq: data-hd-content-type='faq'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}

# FAQs
{: #faqs}

You can use the following FAQs to help you with {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## General
{: #faq-basics}

### What's {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #faq-what-is-hpcs}
{: faq}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} is a dedicated key management service and cloud [Hardware Security Module (HSM)](#x6704988){: term} service that provides the following features:

- Keep Your Own Key (KYOK) with the FIPS 140-2 Level 4 certified HSM that ensures your full control of the entire key hierarchy where no {{site.data.keyword.cloud_notm}} administrators have access to your keys.
- Single-tenant key management system that allows you to create, import, rotate, and manage keys with standardized APIs.
- Data-at-rest encryption with customer-owned keys with seamless [integration with other {{site.data.keyword.cloud_notm}} data and storage services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- Enterprise PKCS #11 library for cryptographic operations, which is enabled by the {{site.data.keyword.hscrypto}} HSMs with the highest security level in the cloud.

### What is a key management service?
{: #faq-what-key-management}
{: faq}

{{site.data.keyword.hscrypto}} provides a single-tenant key management service that allows you to create, import, rotate, and manage keys. Once the encryption keys are deleted, you can be assured that your data that is protected by these keys is no longer retrievable. The service is built on FIPS 140-2 Level 4 certified HSM, which offers the highest level of protection in the cloud industry. {{site.data.keyword.hscrypto}} provides the same set of [key management APIs](https://{DomainName}/apidocs/hs-crypto) as [{{site.data.keyword.keymanagementservicefull_notm}}](https://cloud.ibm.com/catalog/services/key-protect){: external} for you to build your applications or leverage {{site.data.keyword.cloud_notm}} data and infrastructure services.

### What is Hardware Security Module?
{: #faq-what-is-hsm}
{: faq}

A Hardware Security Module (HSM) provides secure key storage and cryptographic operations within a tamper-resistant hardware device for sensitive data. HSMs use the key material without exposing it outside the cryptographic boundary of the hardware.

### What is a cloud HSM?
{: #faq-what-is-cloud-hsm}
{: faq}

A cloud HSM is a cloud-based hardware security module that enables you to manage your own encryption keys and to perform cryptographic operations in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.hscrypto}} is built on FIPS 140-2 Level 4 certified HSM, which offers the highest level of protection in the cloud industry. With the Keep Your Own Key (KYOK) support, customers can configure the [master key](#x2908413){: term} and take the ownership of the cloud HSM. Customers have full control and authority over the entire key hierarchy, where no {{site.data.keyword.cloud_notm}} administrators have access to your keys.

### What are the responsibilities of users and {{site.data.keyword.cloud_notm}} for {{site.data.keyword.hscrypto}}?
{: #faq-responsibilities-users-cloud}
{: faq}

{{site.data.keyword.hscrypto}} is a platform-as-a-service on {{site.data.keyword.cloud_notm}}. {{site.data.keyword.cloud_notm}} is responsible for management of servers, network, storage, virtualization, middleware, and runtime, which ensures good performance and high availability. Customers are responsible for the management of data and applications, specifically encryption keys that are stored in {{site.data.keyword.hscrypto}} and user applications that use keys or cryptographic functions for cryptographic operations.

### How is this service different from {{site.data.keyword.cloud_notm}} HSM?
{: #faq-differentiators-cloud-hsm}
{: faq}
{: support}

IBM has an IaaS {{site.data.keyword.cloud_notm}} HSM service, which is different from the {{site.data.keyword.hscrypto}}. {{site.data.keyword.cloud_notm}} HSM is FIPS 140-2 Level 3 compliant. {{site.data.keyword.hscrypto}} provides a managed HSM service where no special skills are needed to manage the HSM other than loading of the keys. <!--High availability, backup (currently is backed up daily by the service and is not triggered by users), and scaling can all be done by using cloud APIs.--> {{site.data.keyword.hscrypto}} is currently the only cloud service that provides HSMs that are built on FIPS 140-2 Level 4 certified hardware and that allow users to have control of the master key.

### How is {{site.data.keyword.hscrypto}} different from {{site.data.keyword.keymanagementserviceshort}}?
{: #faq-differentiators-key-protect}
{: faq}
{: support}

{{site.data.keyword.keymanagementservicefull_notm}} is a shared multi-tenant key management service with key vaulting that is provided by FIPS 140-2 Level 3 HSMs. The HSMs are managed by IBM and you are not able to take the ownership.

{{site.data.keyword.hscrypto}} is a single-tenant service that is designed for you to look for complete control of your data encryption keys and cloud HSMs that protect these keys. Additionally, this service also supports industry standards such as Public-Key Cryptography Standards #11 (PKCS #11) for cryptographic services like digital signing and Secure Sockets Layer (SSL) offloading.

### What can I do with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #faq-what-do-with-hpcs}
{: faq}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} can be used for key management service and cryptographic operations.

{{site.data.keyword.hscrypto}} can integrate with {{site.data.keyword.cloud_notm}} data and storage services as well as VMware&reg; vSphere&reg; and VSAN, for providing data-at-rest encryption. The managed cloud HSM supports industry standards, such as Enterprise Public-Key Cryptography Standards (PKCS) #11. Your applications can integrate cryptographic operations such as digital signing and validation via Enterprise PKCS#11 (EP11 API). The EP11 library provides an interface similar to the industry-standard PKCS #11 application programming interface (API).

{{site.data.keyword.hscrypto}} leverages frameworks such as gRPC to enable remote application access. gRPC is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} by calling EP11 API remotely over gRPC.

For more information, see [{{site.data.keyword.hscrypto}} use cases](/docs/hs-crypto?topic=hs-crypto-use-cases).

### How do I know whether {{site.data.keyword.hscrypto}} is right for my company?
{: #faq-choose-hs-crypto}
{: faq}

If you are concerned on data security and compliance in the cloud, you are able to maintain complete control over data encryption and [signature keys](#x8250375){: term} in a cloud consumable HSM with industry-leading security for cloud data and digital assets, regulatory compliance support through data encryption and controls on privileged access. {{site.data.keyword.cloud_notm}} administrators have no access to the keys.

With {{site.data.keyword.hscrypto}}, you can ensure regulatory compliance and strengthen data security. Your data is protected with encryption keys in a fully managed, dedicated key management system and cloud HSM service that supports Keep Your Own Key. Keep your own keys for cloud data encryption protected by a dedicated cloud HSM. If you are running regulation intensive applications or applications with sensitive data, this solution is right for you.

Key features include the following:

* Full control of the entire key hierarchy, including the HSM master keys
* Tamper-proof hardware device for sensitive data
* Industry-leading security for cloud data and digital assets
* Reduced data compromise risk because of in-built protection against privileged access threats
* Regulatory compliance through data encryption and controls on privileged access
* Keep Your Own Key (KYOK) that ensures your full control of the entire key hierarchy

### How does {{site.data.keyword.hscrypto}} work?
{: #faq-how-hpcs-work}
{: faq}

When you use {{site.data.keyword.hscrypto}}, you create a service instance with multiple crypto units that reside in different availability zones in a region. The service instance is built on [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external}, which ensures isolated container runtime environment and provides the enterprise level of security and impregnability. The multiple crypto units in a service instance are automatically synchronized and load balanced across muiltiple availability zones. If one availability zone cannot be accessed, the crypto units in a service instance can be used interchangeably. 

A crypto unit is a single unit that represents a hardware security module and the corresponding software stack that is dedicated to the hardware security module for cryptography. Encryption keys are generated in the crypto units and stored in the dedicated Keystore for you to manage and use via standard RESTful APIs. With{{site.data.keyword.hscrypto}}, you take the ownership of the crypto units by loading the master key and assigning your own administrators through CLI or the Management Utilities applications. In this way, you have an exclusive control over your encryption keys. 

{{site.data.keyword.hscrypto}} built on FIPS 140-2 Level 4 HSM supports Enterprise PKCS #11 for cryptographic operations. The functions can be accessed through gRPC API calls.

### What crypto card does {{site.data.keyword.hscrypto}} use?
{: #faq-crypto-card}
{: faq}
{: support}

{{site.data.keyword.hscrypto}} uses the IBM 4768 crypto card, also referred to as Crypto Express 6S (CEX6S). IBM CEX6S is certified at FIPS 140-2 Level 4, the highest level of certification achievable for commercial cryptographic devices. Here is the [certificate for IBM 4768 Cryptographic Coprocessor Security Module](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3410){: external}.

For  more information, see the [IBM CryptoCards News page](https://www.ibm.com/security/cryptocards/cryptonews){: external} and [IBM CryptoCards CEX6S / 4768 Overview](https://www.ibm.com/security/cryptocards/pciecc3/overview){: external}.

### Which IBM regions are {{site.data.keyword.hscrypto}} available in?
{: #faq-hpcs-regions}
{: faq}

Currently, {{site.data.keyword.hscrypto}} is available in Dallas, Sydney, and Frankfurt. For an up-to-date list of supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

### I have workloads in a data center where {{site.data.keyword.hscrypto}} is not available. Can I still subscribe to this service?
{: #faq-data-center}
{: faq}
{: support}

Yes. {{site.data.keyword.hscrypto}} can be accessed remotely worldwide for key management and cloud HSM capabilities.

## Pricing
{: #faq-pricing}

### How am I charged for my use of {{site.data.keyword.hscrypto}}?
{: #faq-how-charge-hpcs}
{: faq}
{: support}

A monthly charge for each provisioned crypto unit and API calls is billed at a rate of $0.01 USD per 10,000 API calls over 1 million API calls. The detailed [pricing plan](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external} is available for your reference.

For example, if you want to crypto-process 5000 keys by using {{site.data.keyword.hscrypto}}, for high availability, you need to set up two crypto units. The amount is $3120 ($1560 per crypto unit) per month. The first 1,000,000 API calls per crypto unit are free of charge. However, if you perform 2,000,000 API calls per month per crypto unit, you are charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls) per crypto unit. In total, there is a monthly charge of $3142 ($3140 for the crypto units and $2 for the additional API calls on both crypto units) for your service instance. The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1560 |
| Crypto unit 2 | $1560 |
| First 1,000,000 API calls for Crypto unit 1 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 1 | $1 ($0.01 x 100) |
| First 1,000,000 API calls for Crypto unit 2 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 2 | $1 ($0.01 x 100) |
| End of month charge | $3122  |
{: caption="Table 1. A billing example of two crypto units with monthly API calls of 2,000,000 per crypto unit" caption-side="bottom"}

<!--
### Is there a free trial for {{site.data.keyword.hscrypto}}?
{: #faq-free-trial}
{: faq}

Yes, a free trial period of 60 days is available for {{site.data.keyword.hscrypto}}. 
-->

## Provisioning and operations
{: #faq-provisioning-operations}

### Are there any prerequisites for using {{site.data.keyword.hscrypto}}?
{: #faq-hpcs-prerequisites}
{: faq}

There are no prerequisites for using {{site.data.keyword.hscrypto}}. The service can be provisioned quickly by following instructions in [Provisioning service instances](/docs/hs-crypto?topic=hs-crypto-provision). However, in order to perform key management and cryptographic operations, you need to initialize service instances first by using [{{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or the [Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) by using smart cards.

### How to initialize {{site.data.keyword.hscrypto}} service instances?
{: #faq-how-to-initialize}
{: faq}
{: support}

To initialize the service instance, you need to create administrator signature keys, exit the imprint mode, and load the master key to the instance. To meet various security requirements of your enterprises, IBM offers you the following options to load the master key: 

- Using the [IBM {{site.data.keyword.hscrypto}} Management Utilities](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-management-utilities) for the highest level of security. This solution uses smart cards to store signature keys and master key parts. Signature keys and master key parts never appear in the clear outside the smart card.

- Using the [{{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-tke-plugin) for a solution that does not require the procurement of smart card readers and smart cards. This solution uses workstation files encrypted with a key that is derived from a file password to store signature keys and master key parts. When the keys are used, file contents are decrypted and appear temporarily in the clear in workstation memory.

### Are there any recommendations on how to set up smart cards?
{: #faq-smart-card-setup}
{: faq}
{: support}

It is recommended to procure eight or 10 smart cards and two smart card readers. The smart cards can be set up to contain a primary set and a backup set. For details of the recommendations, see [Smart card setup recommendations](/docs/hs-crypto?topic=hs-crypto-introduce-service#smart-card-considerations). To find out details on how to procure and set up smart cards and other Management Utilities components, see [Setting up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities).

### How can I procure smart cards and smart card readers?
{: #faq-procure-smart-card}
{: faq}

If you are in the United States, you can order smart cards and smart card readers online. For details, see [Order smart cards and smart card readers](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#order-smart-card-and-reader).

For procurement from other countries, contact IBM Part Sales through the following email addresses. For countries that are not listed, contact `ppricing@de.ibm.com`. In the email, provide the Field Replaceable Unit (FRU) number, 00RY790, for the smart card.

|Country| Email address |
|--------------|-----------------------|
|Belgium  | parts@be.ibm.com|
|Denmark  | reservedele@dk.ibm.com|
|Germany | partsale@de.ibm.com|
|France | vtepce@fr.ibm.com|
|Ireland | emeapart@ie.ibm.com|
|Israel | psale@il.ibm.com|
|Poland | parts@pl.ibm.com|
|Portugal | ptsales@pt.ibm.com|
|South Africa    |autoship@za.ibm.com |
|Spain    | ventadepiezas@es.ibm.com|
|Switzerland | pasa@ch.ibm.com|
|UK | parts_sales@uk.ibm.com|
{: caption="Table 2. IBM Part Sales contacts" caption-side="top"}

### How many crypto units should I set up in my service instance?
{: #faq-crypto-units-number}
{: faq}

You need to set up at least two crypto units for high availability. {{site.data.keyword.hscrypto}} currently sets the upper limit of crypto unit to three.

### Can I use {{site.data.keyword.hscrypto}} along with other {{site.data.keyword.cloud_notm}} services?
{: #faq-hpcs-with-cloud-services}
{: faq}

Yes. {{site.data.keyword.hscrypto}} can be integrated with many {{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cos_full_notm}}, {{site.data.keyword.vmwaresolutions_short}}, {{site.data.keyword.containerlong_notm}}, and {{site.data.keyword.openshiftlong_notm}}. For a complete list of services and instructions on integrations, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

### How does my application connect to a {{site.data.keyword.hscrypto}} service instance?
{: #faq-application-connection}
{: faq}

{{site.data.keyword.hscrypto}} provides the standard APIs for users to access. Your applications can connect to a {{site.data.keyword.hscrypto}} service instance by using the APIs directly over the public internet. If a more secured and isolated connection is needed, you can also use [private endpoints](/docs/hs-crypto?topic=hs-crypto-private-endpoints). You can connect your service instance through {{site.data.keyword.cloud_notm}} service endpoints over the {{site.data.keyword.cloud_notm}} private network.

<!--
### Can I use language characters as part of the key name?
{: #faq-key-name-rules}
{: faq}
{: support}

Language characters, such as Chinese characters, cannot be used as part of the key name.
-->

### Can I generate master key on-premises and store the master key parts in the smart cards?
{: #faq-generate-master-key-on-premises}

Generating master key on-premises is currently not supported.

### Can I import root keys from an on-premises HSM?
{: #faq-import-key-on-premises}
{: faq}

Importing root keys from an on-premises HSM is currently not supported.

### Can I use {{site.data.keyword.hscrypto}} only for cryptographic operations, but use other {{site.data.keyword.cloud_notm}} services such as {{site.data.keyword.keymanagementserviceshort}} for key management?
{: #faq-hpcs-with-key-protect}
{: faq}

Yes. {{site.data.keyword.hscrypto}} can be used with {{site.data.keyword.keymanagementserviceshort}} for key management. In this way, {{site.data.keyword.hscrypto}} is responsible for only cryptographic operations, while {{site.data.keyword.keymanagementserviceshort}} provides key management service secured by multi-tenant FIPS 140-2 Level 3 certified cloud-based HSM.

<!--
### Can I use {{site.data.keyword.hscrypto}} only for cryptographic operations, but use my existing on-premises key management system for key storage?
{: #faq-hpcs-cryptography-only}
{: faq}

Integration with on-premises key management system is currently not supported.
-->

### Can I use {{site.data.keyword.hscrypto}} in conjunction with other cloud provider services such as AWS and Azure?
{: #faq-hpcs-other-cloud-vendor}
{: faq}

Yes. Any application can connect to {{site.data.keyword.hscrypto}} and use our APIs from anywhere on the internet.

## Performance and capacity
{: #faq-performance-capacity}

### How many keys can be stored in a {{site.data.keyword.hscrypto}} service instance?
{: #faq-keys-number}
{: faq}

A {{site.data.keyword.hscrypto}} service instance can hold a maximum of 5000 keys.

<!--
### How many cryptographic operations per second can {{site.data.keyword.hscrypto}} perform?
{: #faq-cryptographic-operations-number}
{: faq}

*Answers needed*
-->

### Can I add or remove crypto units after I provision a service instance?
{: #faq-add-remove-crypto-unit}
{: faq}

Adding or removing crypto units is currently not supported.

### Is there a Service Level Agreement (SLA) specifically for {{site.data.keyword.hscrypto}}?
{: #faq-hpcs-sla}
{: faq}

Yes, you can find the [SLA](https://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-8506-01){: external} for detailed terms.

## Security and compliance
{: #faq-security-compliance}

### What level of access does IBM have to my service instances?
{: #faq-hpcs-ibm-access}
{: faq}

IBM or any third-party users do not have access to your service instances or your keys. You are the only person who has access to your service instance and keys managed.

### Can I share my service instance with other users? How can I manage the user's access?
{: #faq-hpcs-user-access}
{: faq}

{{site.data.keyword.hscrypto}} follows the {{site.data.keyword.cloud_notm}} Identity and Access Management standard. You can share the service instance access through adding users in the access group. For more information, see [Managing access in {{site.data.keyword.cloud_notm}}](/docs/iam?topic=iam-cloudaccess).

### What is a 140-2 FIPS Level 4 Certification and how can I validate it?
{: #faq-fips-level4-meaning}
{: faq}

The Federal Information Processing Standard (FIPS) Publication 140-2 is a US government computer security standard that is used to approve cryptographic modules.

- [Security Requirements for Cryptographic Modules](https://csrc.nist.gov/publications/detail/fips/140/2/final){: external}.
- [Cryptographic Module Validation Program](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Standards){: external}.
- FIPS 140-2 defines four levels of security, including FIPS 140-2 Level 1, 2, 3, and Level 4.

### What is the difference between FIPS 140-2 Level 1, 2, 3, and Level 4?
{: #faq-fips-levels}
{: faq}

- **Level 1**: The lowest level of security. No specific physical security mechanisms are required in a Security Level 1 cryptographic module beyond the basic requirement for production-grade components.
- **Level 2**: Improves the physical security mechanisms of a Level 1 cryptographic module by requiring features that show evidence of tampering including tamper-evident coatings or seals that must be broken to attain physical access to the plaintext cryptographic keys and critical security parameters (CSPs) within the module, or pick-resistant locks on covers or doors to protect against unauthorized physical access. Security Level 2 requires, at minimum, role-based authentication in which a cryptographic module authenticates the authorization of an operator to assume a specific role and perform a corresponding set of services.
- **Level 3**: Provides a high probability of detecting and responding to attempts at physical access, use, or modification of the cryptographic module. The physical security mechanisms can include the use of strong enclosures and tamper-detection and response circuitry that zeroizes all plaintext CSPs when the removable covers or doors of the cryptographic module are opened. Security Level 3 requires identity-based authentication mechanisms, enhancing the security provided by the role-based authentication mechanisms specified for Security Level 2.
- **Level 4**: The highest level of security. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a high probability of being detected, resulting in the immediate zeroization of all plaintext CSPs.

  Security Level 4 cryptographic modules are useful for operation in physically unprotected environments. Security Level 4 also protects a cryptographic module against a security compromise because of environmental conditions or fluctuations outside of the module's normal operating ranges for voltage and temperature. Intentional excursions beyond the normal operating ranges can be used by an attacker to prevent a cryptographic module's defenses.

  A cryptographic module is required to either include special environmental protection features designed to detect fluctuations and delete CSPs, or to undergo environmental failure testing to ensure that the module will not be affected by fluctuations outside of the normal operating range in a manner that can compromise the security of the module. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access.

  {{site.data.keyword.hscrypto}} is the only cloud HSM in the public cloud market that is built on an HSM designed to meet FIPS 140-2 Level 4 certification requirements. The certification is listed on the [Cryptographic Module Validation Program (CVMP) Validated Modules List](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules){: external}.

### What cryptographic algorithms are used and supported by {{site.data.keyword.hscrypto}}?
{: #faq-cryptographic-algorithms}
{: faq}

{{site.data.keyword.hscrypto}} supports the Advanced Encryption Standard of Cipher Blocker Chaining (AES-CBC) algorithm for cryptographic operations.

### What EP11 mechanisms are supported by the GREP11 functions?
{: #faq-EP11-mechanisms}
{: faq}

The following table includes the EP11 mechanisms that are categorized by GREP11 function groups:

|Function group| Supported mechanisms |
|--------------|-----------------------|
|Encrypt | CKM_AES_CBC CKM_AES_CBC_PAD CKM_AES_ECB CKM_DES3_CBC CKM_DES3_CBC_PAD CKM_DES3_ECB CKM_IBM_EC_MULTIPLY CKM_RSA_PKCS CKM_RSA_PKCS_OAEP|
|Decrypt | CKM_AES_CBC CKM_AES_CBC_PAD CKM_AES_ECB CKM_DES3_CBC CKM_DES3_CBC_PAD CKM_DES3_ECB CKM_RSA_PKCS CKM_RSA_PKCS_OAEP|
|Digest  | CKM_IBM_SHA512_224 CKM_IBM_SHA512_256 CKM_SHA224 CKM_SHA256 CKM_SHA384 CKM_SHA512 CKM_SHA512_224 CKM_SHA512_256 CKM_SHA_1|
|Sign    | CKM_DSA CKM_DSA_SHA1 CKM_ECDSA CKM_ECDSA_SHA1 CKM_ECDSA_SHA224 CKM_ECDSA_SHA256 CKM_ECDSA_SHA384 CKM_ECDSA_SHA512 CKM_IBM_CMAC CKM_IBM_ECDSA_SHA224 CKM_IBM_ECDSA_SHA256 CKM_IBM_ECDSA_SHA384 CKM_IBM_ECDSA_SHA512 CKM_IBM_SHA512_224_HMAC CKM_IBM_SHA512_256_HMAC CKM_RSA_PKCS CKM_RSA_PKCS_PSS CKM_RSA_X9_31 CKM_SHA1_RSA_PKCS CKM_SHA1_RSA_PKCS_PSS CKM_SHA1_RSA_X9_31 CKM_SHA224_HMAC CKM_SHA224_RSA_PKCS CKM_SHA224_RSA_PKCS_PSS CKM_SHA256_HMAC CKM_SHA256_RSA_PKCS CKM_SHA256_RSA_PKCS_PSS CKM_SHA384_HMAC CKM_SHA384_RSA_PKCS CKM_SHA384_RSA_PKCS_PSS CKM_SHA512_224_HMAC CKM_SHA512_256_HMAC CKM_SHA512_HMAC CKM_SHA512_RSA_PKCS CKM_SHA512_RSA_PKCS_PSS CKM_SHA_1_HMAC|
|Verify | CKM_DSA CKM_DSA_SHA1 CKM_ECDSA CKM_ECDSA_SHA1 CKM_ECDSA_SHA224 CKM_ECDSA_SHA256 CKM_ECDSA_SHA384 CKM_ECDSA_SHA512 CKM_IBM_CMAC CKM_IBM_ECDSA_SHA224 CKM_IBM_ECDSA_SHA256 CKM_IBM_ECDSA_SHA384 CKM_IBM_ECDSA_SHA512 CKM_IBM_SHA512_224_HMAC CKM_IBM_SHA512_256_HMAC CKM_RSA_PKCS CKM_RSA_PKCS_PSS CKM_RSA_X9_31 CKM_SHA1_RSA_PKCS CKM_SHA1_RSA_PKCS_PSS CKM_SHA1_RSA_X9_31 CKM_SHA224_HMAC CKM_SHA224_RSA_PKCS CKM_SHA224_RSA_PKCS_PSS CKM_SHA256_HMAC CKM_SHA256_RSA_PKCS CKM_SHA256_RSA_PKCS_PSS CKM_SHA384_HMAC CKM_SHA384_RSA_PKCS CKM_SHA384_RSA_PKCS_PSS CKM_SHA512_224_HMAC CKM_SHA512_256_HMAC CKM_SHA512_HMAC CKM_SHA512_RSA_PKCS CKM_SHA512_RSA_PKCS_PSS CKM_SHA_1_HMAC|
|Generate | CKM_AES_KEY_GEN CKM_DES2_KEY_GEN CKM_DES3_KEY_GEN CKM_DH_PKCS_KEY_PAIR_GEN CKM_DH_PKCS_PARAMETER_GEN CKM_DSA_KEY_PAIR_GEN CKM_DSA_PARAMETER_GEN CKM_EC_KEY_PAIR_GEN CKM_GENERIC_SECRET_KEY_GEN CKM_PBE_SHA1_DES3_EDE_CBC CKM_RSA_PKCS_KEY_PAIR_GEN CKM_RSA_X9_31_KEY_PAIR_GEN|
|Wrap | CKM_AES_CBC CKM_AES_CBC_PAD CKM_DES3_CBC CKM_DES3_CBC_PAD CKM_IBM_ATTRIBUTEBOUND_WRAP CKM_IBM_RETAINKEY CKM_RSA_PKCS CKM_RSA_PKCS_OAEP|
|Unwrap | CKM_AES_CBC CKM_AES_CBC_PAD CKM_DES3_CBC CKM_DES3_CBC_PAD CKM_IBM_ATTRIBUTEBOUND_WRAP CKM_RSA_PKCS CKM_RSA_PKCS_OAEP|
|Derive | CKM_DH_PKCS_DERIVE CKM_ECDH1_DERIVE CKM_GENERIC_SECRET_KEY_GEN CKM_IBM_DH_PKCS_DERIVE_RAW CKM_IBM_EAC CKM_IBM_ECDH1_DERIVE_RAW CKM_SHA1_KEY_DERIVATION CKM_SHA224_KEY_DERIVATION CKM_SHA256_KEY_DERIVATION CKM_SHA384_KEY_DERIVATION CKM_SHA512_KEY_DERIVATION|
{: caption="Table 3. Mechanisms supported by GREP11" caption-side="top"}

For more information on the EP11 mechanisms, see the [Enterprise PKCS#11 (EP11) Library structure guide](https://www.ibm.com/common/ssi/cgi-bin/ssialias?htmlfid=15022415USEN&dd=yes&){: external}.

### What compliance standards does {{site.data.keyword.hscrypto}} meet?
{: #faq-compliance-standards}
{: faq}

{{site.data.keyword.hscrypto}} meets controls for global, industry, and regional compliance standards, such as GDPR, HIPAA,<!-- IRAP,--> and ISO. As the HSM used by {{site.data.keyword.hscrypto}}, the IBM 4768 crypto card is also certified with Common Criteria EAL4 and FIPS 140-2 Level 4. For more information, see [Security and compliance](/docs/hs-crypto?topic=hs-crypto-security-and-compliance).

### Can I monitor my service instance?
{: #faq-monitor-instance}
{: faq}

Yes, you can monitor the status of your service instance through [Activity Tracker with LogDNA](/docs/hs-crypto?topic=hs-crypto-at-events).

## High availability and disaster recovery
{: #faq-ha-dr}

### How do I set up a high availability configuration?
{: #faq-ha-configuration}
{: faq}

It is recommended that you provision at least two crypto units for high availability. If one available zone that contains your provisioned service instance goes down, {{site.data.keyword.hscrypto}} has automatic in-region data failover in place.

### Can I back up my service instance manually?
{: #faq-backup-manually}
{: faq}

You need to only back up your master key parts and signature keys for service initialization. Your data in {{site.data.keyword.hscrypto}} is backed up automatically by {{site.data.keyword.cloud_notm}} daily.

### What happens if my service instance fails?
{: #faq-instance-fail}
{: faq}

{{site.data.keyword.cloud_notm}} has automatic in-region failover plan in place. Currently, your data is backed up daily by the service  and you don't need to do anything to enable it. For [cross-region data restores](/docs/hs-crypto?topic=hs-crypto-ha-dr), you need to open an IBM support ticket so that IBM can restore the service instance for you.

### How can I restore the content from backups?
{: #faq-store-backup}
{: faq}

For cross-region data restores, you need to open an IBM support ticket so that IBM can restore the service instance for you. For more information, see [Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data).

### What happens if I delete my service instances?
{: #faq-delete-instance}
{: faq}

If you delete your service instance, your keys that are managed are not accessible.

### Can I back up the keys before I delete a service instance?
{: #faq-backup-keys}
{: faq}

Backing up the keys manually is currently not supported.

### What happens when I delete a key?
{: #faq-delete-a-key}
{: faq}
{: support}

When you delete a key, the key is no longer recoverable and the cloud services that use the key can no longer decrypt data that is associated with the key. Your data remains in those services in its encrypted form. Before you delete a key, ensure that you no longer require access to any data that is associated with the key. This action currently cannot be reversed.

### What happens if I lose the signature key or the master key parts?
{: #faq-lose-signature-key}
{: faq}

If your signature key or master key part is lost, you are not able to initialize your service instance, and your service instance is not accessible. You need to back up you key files on your workstation or back up your smart cards that hold your signature key or master key parts depending on how to store your keys. 

## Support and maintenance
{: #faq-support-maintenance}

### How is routine maintenance performed on {{site.data.keyword.hscrypto}}?
{: #faq-routine-maintenance}
{: faq}

If one available zone that contains your provisioned service instance goes down, {{site.data.keyword.hscrypto}} has automatic in-region data failover in place if you have 2 or 3 crypto units provisioned. IBM also performs cross-region backup for your key resources. Your data is automatically backed up in another supported region daily. If a regional disaster that affects all available zones occurs, you need to open a support ticket so that IBM can restore your data in another supported [{{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions) from the backup. And then, you need to manually load your master key to your new service instance. For more information, see [Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data).

### How do I get support for {{site.data.keyword.hscrypto}}?
{: #faq-hpcs-support}
{: faq}

If you have technical questions about {{site.data.keyword.hscrypto}}, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/hyper-protect-crypto){: external} and tag your question with `ibm-cloud` and `hyper-protect-crypto`. For questions about the service and getting started instructions, use the [IBM Developer Answers](https://developer.ibm.com/answers/topics/hyper-protect-crypto/){: external}. Include the `ibm-cloud` and `hyper-protect-crypto` tags. See [Getting help](/docs/get-support?topic=get-support-getting-customer-support) for more details about using the forums.

For more information about opening an IBM support ticket, or about support levels and ticket severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support).
