---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: general frequently asked questions, cryptographic algorithm, regions, pricing, security compliance, key ceremony, critical security parameters, cryptographic module, security Level, fips

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

# General FAQs
{: #faq-basics}

This topic can help you with general questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## What's {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #faq-what-is-hpcs}
{: faq}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} is a dedicated key management service and cloud [Hardware Security Module (HSM)](#x6704988){: term} service that provides the following features:

- Keep Your Own Key (KYOK) with the FIPS 140-2 Level 4 certified HSM that ensures your full control of the entire key hierarchy where no {{site.data.keyword.cloud_notm}} administrators have access to your keys.
- Single-tenant key management system that allows you to create, import, rotate, and manage keys with standardized APIs.
- Data-at-rest encryption with customer-owned keys with seamless [integration with other {{site.data.keyword.cloud_notm}} data and storage services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- Enterprise PKCS #11 library for cryptographic operations, which is enabled by the {{site.data.keyword.hscrypto}} HSMs with the highest security level in the cloud.

## What is a key management service?
{: #faq-what-key-management}
{: faq}

{{site.data.keyword.hscrypto}} provides a single-tenant key management service that allows you to create, import, rotate, and manage keys. Once the encryption keys are deleted, you can be assured that your data that is protected by these keys is no longer retrievable. The service is built on FIPS 140-2 Level 4 certified HSM, which offers the highest level of protection in the cloud industry. {{site.data.keyword.hscrypto}} provides the same set of [key management APIs](https://{DomainName}/apidocs/hs-crypto) as [{{site.data.keyword.keymanagementservicefull_notm}}](https://cloud.ibm.com/catalog/services/key-protect){: external} for you to build your applications or leverage {{site.data.keyword.cloud_notm}} data and infrastructure services.

## What is Hardware Security Module?
{: #faq-what-is-hsm}
{: faq}

A Hardware Security Module (HSM) provides secure key storage and cryptographic operations within a tamper-resistant hardware device for sensitive data. HSMs use the key material without exposing it outside the cryptographic boundary of the hardware.

## What is a cloud HSM?
{: #faq-what-is-cloud-hsm}
{: faq}

A cloud HSM is a cloud-based hardware security module that enables you to manage your own encryption keys and to perform cryptographic operations in {{site.data.keyword.cloud_notm}}. {{site.data.keyword.hscrypto}} is built on FIPS 140-2 Level 4 certified HSM, which offers the highest level of protection in the cloud industry. With the Keep Your Own Key (KYOK) support, customers can configure the [master key](#x2908413){: term} and take the ownership of the cloud HSM. Customers have full control and authority over the entire key hierarchy, where no {{site.data.keyword.cloud_notm}} administrators have access to your keys.

## How does {{site.data.keyword.hscrypto}} provide a single-tenant cloud service?
{: #faq-single-tenant}

{{site.data.keyword.hscrypto}} is a single-tenant cloud service because each customer has a dedicated software stack and a dedicated HSM domain for every crypto unit. As a customer, you are assured that you are interacting with a dedicated service stack that only processes your data. For additional information on the service architecture, see [How does Hyper Protect Crypto Services work](/docs/hs-crypto?topic=hs-crypto-overview#how-hpcs-work).

## What are the responsibilities of users and {{site.data.keyword.cloud_notm}} for {{site.data.keyword.hscrypto}}?
{: #faq-responsibilities-users-cloud}
{: faq}

{{site.data.keyword.hscrypto}} is a platform-as-a-service on {{site.data.keyword.cloud_notm}}. {{site.data.keyword.cloud_notm}} is responsible for management of servers, network, storage, virtualization, middleware, and runtime, which ensures good performance and high availability. Customers are responsible for the management of data and applications, specifically encryption keys that are stored in {{site.data.keyword.hscrypto}} and user applications that use keys or cryptographic functions for cryptographic operations.

## How is this service different from {{site.data.keyword.cloud_notm}} HSM?
{: #faq-differentiators-cloud-hsm}
{: faq}
{: support}

IBM has an IaaS {{site.data.keyword.cloud_notm}} HSM service, which is different from the {{site.data.keyword.hscrypto}}. {{site.data.keyword.cloud_notm}} HSM is FIPS 140-2 Level 3 compliant. {{site.data.keyword.hscrypto}} provides a managed HSM service where no special skills are needed to manage the HSM other than loading of the keys. <!--High availability, backup (currently is backed up daily by the service and is not triggered by users), and scaling can all be done by using cloud APIs.--> {{site.data.keyword.hscrypto}} is currently the only cloud service that provides HSMs that are built on FIPS 140-2 Level 4 certified hardware and that allow users to have control of the master key.

## How is {{site.data.keyword.hscrypto}} different from {{site.data.keyword.keymanagementserviceshort}}?
{: #faq-differentiators-key-protect}
{: faq}
{: support}

{{site.data.keyword.keymanagementservicefull_notm}} is a shared multi-tenant key management service with key vaulting that is provided by FIPS 140-2 Level 3 HSMs. The HSMs are managed by IBM and you are not able to take the ownership.

{{site.data.keyword.hscrypto}} is a single-tenant service that is designed for you to look for complete control of your data encryption keys and cloud HSMs that protect these keys. Additionally, this service also supports industry standards such as Public-Key Cryptography Standards #11 (PKCS #11) for cryptographic services like digital signing and Secure Sockets Layer (SSL) offloading.

## What can I do with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #faq-what-do-with-hpcs}
{: faq}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} can be used for key management service and cryptographic operations.

{{site.data.keyword.hscrypto}} can integrate with {{site.data.keyword.cloud_notm}} data and storage services as well as VMware&reg; vSphere&reg; and VSAN, for providing data-at-rest encryption. The managed cloud HSM supports industry standards, such as Enterprise Public-Key Cryptography Standards (PKCS) #11. Your applications can integrate cryptographic operations such as digital signing and validation via Enterprise PKCS#11 (EP11 API). The EP11 library provides an interface similar to the industry-standard PKCS #11 application programming interface (API).

{{site.data.keyword.hscrypto}} leverages frameworks such as gRPC to enable remote application access. gRPC is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} by calling EP11 API remotely over gRPC.

For more information, see [{{site.data.keyword.hscrypto}} use cases](/docs/hs-crypto?topic=hs-crypto-use-cases).

## How do I know whether {{site.data.keyword.hscrypto}} is right for my company?
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

## How does {{site.data.keyword.hscrypto}} work?
{: #faq-how-hpcs-work}
{: faq}

When you use {{site.data.keyword.hscrypto}}, you create a service instance with multiple crypto units that reside in different availability zones in a region. The service instance is built on [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external}, which ensures isolated container runtime environment and provides the enterprise level of security and impregnability. The multiple crypto units in a service instance are automatically synchronized and load balanced across muiltiple availability zones. If one availability zone cannot be accessed, the crypto units in a service instance can be used interchangeably. 

A crypto unit is a single unit that represents a hardware security module and the corresponding software stack that is dedicated to the hardware security module for cryptography. Encryption keys are generated in the crypto units and stored in the dedicated Keystore for you to manage and use via standard RESTful APIs. With{{site.data.keyword.hscrypto}}, you take the ownership of the crypto units by loading the master key and assigning your own administrators through CLI or the Management Utilities applications. In this way, you have an exclusive control over your encryption keys. 

{{site.data.keyword.hscrypto}} built on FIPS 140-2 Level 4 HSM supports Enterprise PKCS #11 for cryptographic operations. The functions can be accessed through gRPC API calls.

## What crypto card does {{site.data.keyword.hscrypto}} use?
{: #faq-crypto-card}
{: faq}
{: support}

{{site.data.keyword.hscrypto}} uses the IBM 4768 crypto card, also referred to as Crypto Express 6S (CEX6S). IBM CEX6S is certified at FIPS 140-2 Level 4, the highest level of certification achievable for commercial cryptographic devices. Here is the [certificate for IBM 4768 Cryptographic Coprocessor Security Module](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3410){: external}.

For  more information, see the [IBM CryptoCards News page](https://www.ibm.com/security/cryptocards/cryptonews){: external} and [IBM CryptoCards CEX6S / 4768 Overview](https://www.ibm.com/security/cryptocards/pciecc3/overview){: external}.

## Which IBM regions are {{site.data.keyword.hscrypto}} available in?
{: #faq-hpcs-regions}
{: faq}

Currently, {{site.data.keyword.hscrypto}} is available in Dallas, Sydney, and Frankfurt. For an up-to-date list of supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## I have workloads in a data center where {{site.data.keyword.hscrypto}} is not available. Can I still subscribe to this service?
{: #faq-data-center}
{: faq}
{: support}

Yes. {{site.data.keyword.hscrypto}} can be accessed remotely worldwide for key management and cloud HSM capabilities.
