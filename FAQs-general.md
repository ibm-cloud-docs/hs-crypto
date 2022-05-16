---

copyright:
  years: 2020, 2022
lastupdated: "2022-05-16"

keywords: general frequently asked questions, cryptographic algorithm, regions, pricing, security compliance, key ceremony, critical security parameters, cryptographic module, security Level, fips

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

# General FAQs
{: #faq-basics}

Read to get answers for general questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## What's {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #faq-what-is-hpcs}
{: faq}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} is a dedicated key management service and cloud [Hardware Security Module (HSM)](#x6704988){: term} service that provides the following features:

- Keep Your Own Key (KYOK) with the FIPS 140-2 Level 4 certified HSM that ensures your full control of the entire key hierarchy where no {{site.data.keyword.cloud_notm}} administrators have access to your keys.
- Single-tenant key management system to create, import, rotate, and manage keys with the standardized API.
- Data-at-rest encryption with customer-owned keys with seamless [integration with other {{site.data.keyword.cloud_notm}} data and storage services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- PKCS #11 library and Enterprise PKCS #11 (EP11) library for cryptographic operations, which is enabled by the {{site.data.keyword.hscrypto}} HSMs with the highest security level in the cloud.

## What is {{site.data.keyword.uko_full_notm}}?
{: #faq-what-is-uko}
{: faq}

{{site.data.keyword.uko_full_notm}} provides the only cloud native single-point-of-control of encryption keys across hybrid multicloud environments of your enterprise. 

* {{site.data.keyword.uko_full_notm}} enables you with both Keep Your Own Key and Bring Your Own Key capabilities from across hybrid multicloud environments that includes on-premises environments.  
* {{site.data.keyword.uko_full_notm}} manages and orchestrates all keys from the multicloud environments on {{site.data.keyword.cloud_notm}}.

## What is a key management service?
{: #faq-what-key-management}
{: faq}

{{site.data.keyword.hscrypto}} provides a single-tenant key management service to create, import, rotate, and manage keys. Once the encryption keys are deleted, you can be assured that your data that is protected by these keys is no longer retrievable. The service is built on FIPS 140-2 Level 4 certified HSM, which offers the highest level of protection in the cloud industry. {{site.data.keyword.hscrypto}} provides the same [key management service API](/apidocs/hs-crypto) as {{site.data.keyword.keymanagementservicefull_notm}} for you to build your applications or leverage {{site.data.keyword.cloud_notm}} data and infrastructure services.

## What is Hardware Security Module?
{: #faq-what-is-hsm}
{: faq}

A Hardware Security Module (HSM) provides secure key storage and cryptographic operations within a tamper-resistant hardware device for sensitive data. HSMs use the key material without exposing it outside the cryptographic boundary of the hardware.

## What is a cloud HSM?
{: #faq-what-is-cloud-hsm}
{: faq}

A cloud HSM is a cloud-based hardware security module to manage your own encryption keys and to perform cryptographic operations in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.hscrypto}} is built on FIPS 140-2 Level 4 certified HSM, which offers the highest level of protection in the cloud industry. With the Keep Your Own Key (KYOK) support, customers can configure the [master key](#x2908413){: term} and take the ownership of the cloud HSM. Customers have full control and authority over the entire key hierarchy, where no {{site.data.keyword.cloud_notm}} administrators have access to your keys.

## How does {{site.data.keyword.hscrypto}} provide a single-tenant cloud service?
{: #faq-single-tenant}

{{site.data.keyword.hscrypto}} is a single-tenant cloud service because each customer has a dedicated software stack and a dedicated HSM domain for every crypto unit. As a customer, you are assured that you are interacting with a dedicated service stack that processes only your data. For more information about the service architecture, see [How does Hyper Protect Crypto Services work](/docs/hs-crypto?topic=hs-crypto-overview#how-hpcs-work).

## What are the responsibilities of users and {{site.data.keyword.cloud_notm}} for {{site.data.keyword.hscrypto}}?
{: #faq-responsibilities-users-cloud}
{: faq}

{{site.data.keyword.hscrypto}} is a platform-as-a-service on {{site.data.keyword.cloud_notm}}. {{site.data.keyword.cloud_notm}} is responsible for management of servers, network, storage, virtualization, middleware, and runtime, which ensures good performance and high availability. Customers are responsible for the management of data and applications, specifically encryption keys that are stored in {{site.data.keyword.hscrypto}} and user applications that use keys or cryptographic functions for cryptographic operations.

## How is this service different from {{site.data.keyword.cloud_notm}} HSM?
{: #faq-differentiators-cloud-hsm}
{: faq}
{: support}

IBM has an IaaS {{site.data.keyword.cloud_notm}} HSM service, which is different from the {{site.data.keyword.hscrypto}}. {{site.data.keyword.cloud_notm}} HSM is FIPS 140-2 Level 3 compliant. {{site.data.keyword.hscrypto}} provides a managed HSM service where no special skills are needed to manage the HSM other than loading of the keys.  {{site.data.keyword.hscrypto}} is the only cloud service that provides HSMs that are built on FIPS 140-2 Level 4 certified hardware and that allow users to have control of the master key.

## How is {{site.data.keyword.hscrypto}} different from {{site.data.keyword.keymanagementserviceshort}}?
{: #faq-differentiators-key-protect}
{: faq}
{: support}

{{site.data.keyword.keymanagementservicefull_notm}} is a shared multi-tenant key management service that supports the Bring Your Own Key (BYOK) capability. The service is built on  FIPS 140-2 Level 3 certified HSMs, which are managed by IBM.

{{site.data.keyword.hscrypto}} is a single-tenant key management service and cloud HSM for you to fully manage your encryption keys and to perform cryptographic operations. This service is built on FIPS 140-2 Level 4 certified HSMs and supports the Keep Your Own Key (KYOK) capability. You can take the ownership to ensure your full control of the entire key hierarchy with no access even from {{site.data.keyword.cloud_notm}} administrators. {{site.data.keyword.hscrypto}} also supports industry standards such as Public-Key Cryptography Standards #11 (PKCS #11) for cryptographic operations like digital signing and Secure Sockets Layer (SSL) offloading.

## How is Keep Your Own Key different from Bring Your Own Key?
{: #faq-differentiators-KYOK}
{: faq}
{: support}

Bring Your Own Key (BYOK) is a way for you to use your own keys to encrypt data. The key management services that provide BYOK are typically multi-tenant services. With these services, you can import your encryption keys from the on-premises hardware security modules (HSM) and then manage the keys.

With Keep Your Own Key (KYOK), IBM brings industry-leading level of control that you can exercise on your own encryption keys. In addition to the BYOK capabilities, KYOK provides technical assurance that IBM cannot access the customer keys. With KYOK, you have exclusive control of the entire key hierarchy, which includes the master key.

The following table details the differences between KYOK and BYOK.

| Cloud key management capabilities                            | BYOK  | KYOK   |
| --------------------------------- | ---------------------------------------------- |---------------------------------------------- |
| Managing encryption key lifecycle                        |                Yes                 |                 Yes                |
| Integrating with other cloud services|           Yes                     |            Yes                     |
| Bringing your own keys from on-premises HSMs                      |                Yes                 |                 Yes                |
| Operational assurance - Cloud service providers cannot access keys. |                Yes                 |                 Yes           |
| Technical assurance - IBM cannot access the keys.          |                No                 |                   Yes                |
| Single tenant, dedicated key management service.          |                No                 |                    Yes              |
| Exclusive control of your master key.                     |                No                  |                   Yes               |
| Highest level security - FIPS 140-2 Level 4 HSM.           |                No                  |                   Yes                |
| Managing your master key with smart cards.                |                No                  |                   Yes                |
| Performing key ceremony.                                  |                No                  |                    Yes               |
{: caption="Table 1. Comparing BYOK with KYOK" caption-side="bottom"}

## What can I do with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #faq-what-do-with-hpcs}
{: faq}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} can be used for key management service and cryptographic operations.

{{site.data.keyword.hscrypto}} can integrate with {{site.data.keyword.cloud_notm}} data and storage services as well as VMware&reg; vSphere&reg; and VSAN, for providing data-at-rest encryption. The managed cloud HSM supports industry standards, such as Enterprise Public-Key Cryptography Standards (PKCS) #11. Your applications can integrate cryptographic operations such as digital signing and validation through Enterprise PKCS #11 (EP11 API). The EP11 library provides an interface similar to the industry-standard PKCS #11 application programming interface (API).

{{site.data.keyword.hscrypto}} leverages frameworks such as gRPC to enable remote application access. gRPC is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} by calling EP11 API remotely over gRPC.

For more information, see [{{site.data.keyword.hscrypto}} use cases](/docs/hs-crypto?topic=hs-crypto-use-cases).

## How do I know whether {{site.data.keyword.hscrypto}} is right for my company?
{: #faq-choose-hs-crypto}
{: faq}

If you are concerned on data security and compliance in the cloud, you are able to maintain complete control over data encryption and [signature keys](#x8250375){: term} in a cloud consumable HSM. The HSM is backed by industry-leading security for cloud data and digital assets. With the security and regulatory compliance support, your data is encrypted and privileged access is controlled. Even {{site.data.keyword.cloud_notm}} administrators have no access to the keys.

With {{site.data.keyword.hscrypto}}, you can ensure regulatory compliance and strengthen data security. Your data is protected with encryption keys in a fully managed, dedicated key management system and cloud HSM service that supports Keep Your Own Key. Keep your own keys for cloud data encryption protected by a dedicated cloud HSM. If you are running regulation intensive applications or applications with sensitive data, this solution is right for you.

Key features are as follows:

* Full control of the entire key hierarchy, including the master keys.
* Tamper-proof hardware device for sensitive data.
* Industry-leading security for cloud data and digital assets.
* Reduced data compromise risk because of in-built protection against privileged access threats.
* Regulatory compliance through data encryption and controls on privileged access.
* Keep Your Own Key (KYOK) that ensures your full control of the entire key hierarchy.

## How does {{site.data.keyword.hscrypto}} work?
{: #faq-how-hpcs-work}
{: faq}

When you use {{site.data.keyword.hscrypto}}, you create a service instance with multiple crypto units that reside in different availability zones in a region. The service instance is built on [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external}, which ensures isolated container runtime environment and provides the enterprise level of security and impregnability. The multiple crypto units in a service instance are automatically synchronized and load balanced across multiple availability zones. If one availability zone cannot be accessed, the crypto units in a service instance can be used interchangeably. 

A crypto unit is a single unit that represents a hardware security module and the corresponding software stack that is dedicated to the hardware security module for cryptography. Encryption keys are generated in the crypto units and stored in the dedicated keystore for you to manage and use through the standard RESTful API. With{{site.data.keyword.hscrypto}}, you take the ownership of the crypto units by loading the master key and assigning your own administrators through CLI or the Management Utilities applications. In this way, you have an exclusive control over your encryption keys. 

{{site.data.keyword.hscrypto}} built on FIPS 140-2 Level 4 HSM supports Enterprise PKCS #11 for cryptographic operations. The functions can be accessed through gRPC API calls.

## What crypto card does {{site.data.keyword.hscrypto}} use?
{: #faq-crypto-card}
{: faq}
{: support}

If you create your instance in [regions](/docs/hs-crypto?topic=hs-crypto-regions) that are based on Virtual Private Cloud (VPC) infrastructure, {{site.data.keyword.hscrypto}} uses the [IBM 4769 crypto card](https://www.ibm.com/security/cryptocards/pciecc4/overview){: external}, also referred to as Crypto Express 7S (CEX7S). If you create your instance in other non-VPC regions, {{site.data.keyword.hscrypto}} uses the [IBM 4768 crypto card](https://www.ibm.com/security/cryptocards/pciecc3/overview){: external}, also referred to as Crypto Express 6S (CEX6S). Both IBM CEX6S and IBM CEX7S are certified at FIPS 140-2 Level 4, the highest level of certification achievable for commercial cryptographic devices. You can check the certificates at the following NIST sites:

- [IBM 4769-001 Cryptographic Coprocessor Security Module](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/4079){: external}
- [IBM 4768 Cryptographic Coprocessor Security Module](https://csrc.nist.gov/projects/cryptographic-module-validation-program/certificate/3410){: external}


## Which IBM regions are {{site.data.keyword.hscrypto}} available in?
{: #faq-hpcs-regions}
{: faq}

Currently, {{site.data.keyword.hscrypto}} is available in Dallas, Sydney, and Frankfurt. For an up-to-date list of supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## I have workloads in a data center where {{site.data.keyword.hscrypto}} is not available. Can I still subscribe to this service?
{: #faq-data-center}
{: faq}

Yes. {{site.data.keyword.hscrypto}} can be accessed remotely worldwide for key management and cloud HSM capabilities.
