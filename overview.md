---

copyright:
  years: 2018, 2020
lastupdated: "2020-04-21"

keywords: IBM keys, key management, data security, Hyper Protect Crypto Services, Cloud HSM, hardware security module, PKCS11, openSSL, hsm encryption

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Overview
{: #overview}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is a dedicated key management service and [Hardware Security Module (HSM)](#x6704988){: term} that is built on the {{site.data.keyword.IBM}} LinuxONE platform. {{site.data.keyword.hscrypto}} offers the highest level of protection in the cloud industry for your sensitive data with FIPS 140-2 Level 4 certified hardware.
{: shortdesc}

Watch the following video to learn how {{site.data.keyword.hscrypto}} provides you with exclusive encryption key control and data protection in the cloud:

<iframe class="embed-responsive-item" id="youtubeplayer" title="Initialize Hyper Protect Crypto Services with IBM Cloud TKE CLI" type="text/html" width="640" height="390" src="//www.youtube.com/embed/0LiltyNMwgo?rel=0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen> </iframe>

## Why {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #why_hpcs}

Data and information security is crucial and essential for IT environments. As more data moves to the cloud, keeping data protected becomes a non-trivial challenge. Built on IBM LinuxONE technology, {{site.data.keyword.hscrypto}} helps ensure that only you have access to your keys and data. A single-tenant key management service with key vaulting that is provided by dedicated customer-controlled HSMs helps you easily create and manage your encryption keys. Alternatively, you can bring your own encryption keys to the cloud. The service uses the same key-provider API as {{site.data.keyword.keymanagementserviceshort}}, a multi-tenant key management service, to provide a consistent approach to adopting {{site.data.keyword.cloud_notm}} services.

{{site.data.keyword.hscrypto}} is a dedicated HSM that is controlled by you. {{site.data.keyword.cloud_notm}} administrators have no access. The service is built on FIPS 140-2 Level 4-certified hardware, the highest offered by any cloud provider in the industry. IBM is the first to provide cloud command-line interface (CLI) for HSM [master key](#x2908413){: term} initialization to help enable you to take ownership of the cloud HSM. You can also load the master key with the {{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities. The Management Utilities create and store your master key parts on smart cards and never exposes your secrets to the workstation and cloud, thus ensuring the highest level of protection to your secrets.

{{site.data.keyword.hscrypto}} can integrate with {{site.data.keyword.cloud_notm}} data and storage services as well as VMware&reg; vSphere&reg; and VSAN, for providing data-at-rest encryption. The managed cloud HSM supports industry standards, such as Enterprise Public-Key Cryptography Standards (PKCS) #11, so your applications can integrate cryptographic operations such as digital signing and validation via Enterprise PKCS#11 ([EP11](/docs/hs-crypto?topic=hs-crypto-HSM-overview) API). The EP11 library provides an interface similar to the industry-standard [PKCS #11 application programming interface (API)](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}. For more information about EP11 library structure, see [the EP11 library structure reference guide](https://www.ibm.com/downloads/cas/WXRDPRAN){: external}.

{{site.data.keyword.hscrypto}} leverages frameworks such as gRPC to enable remote application access. [gRPC](https://grpc.io/){: external} is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} by calling EP11 API remotely over gRPC.

With the built-in encryption of {{site.data.keyword.hscrypto}}, you can easily build cloud applications with sensitive data. {{site.data.keyword.hscrypto}} provides you with complete control of your data and encryption keys, including the master key. The service also helps your business meet regulatory compliance with the technology that provides exclusive controls on the external and privileged user access to data and keys.

<!-- With {{site.data.keyword.hscrypto}}, your SSL keys are offloaded to a {{site.data.keyword.hscrypto}} instance to ensure security and protection of those sensitive keys. Besides, the certificate lifecycle management gets common approach to manage certificates and offers the visibility to certificate expiration. -->

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. This cryptography mechanism ensures that the blockchain network is running in a highly protected and isolated environment, and accelerates hashing, sign/verify operations, and node-to-node communications in the network. The success of {{site.data.keyword.blockchainfull_notm}} Platform proves the capability and value of {{site.data.keyword.hscrypto}}. -->

## How does {{site.data.keyword.hscrypto}} work?
{: #how-hpcs-work}

The following architectural diagram shows how {{site.data.keyword.hscrypto}} works.

![{{site.data.keyword.hscrypto}} architecture](/image/architecture.svg "{{site.data.keyword.hscrypto}} architecture"){: caption="Figure 1. {{site.data.keyword.hscrypto}} architecture" caption-side="bottom"}

The following are a few highlights of the {{site.data.keyword.hscrypto}} architecture:
- Applications connect to {{site.data.keyword.hscrypto}} through EP11 API.
- Dedicated keystore in {{site.data.keyword.hscrypto}} is provided to ensure data isolation and security. Privileged users are locked out for protection against abusive use of system administrator credentials or root user credentials.
- [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external} provides the enterprise level of security and impregnability that enterprise customers expect from [IBM LinuxONE](https://www.ibm.com/it-infrastructure/linuxone){: external} technology.
- FIPS 140-2 Level 4 compliant cloud HSM is enabled for highest physical protection of secrets.

## Key features
{: #key-features}

{{site.data.keyword.hscrypto}} provides both key management and cloud HSM functions:

### Key management service
{: #key-management}

* **Key lifecycle management**

  {{site.data.keyword.hscrypto}} provides a single-tenant key management service that allows you to create, import, rotate, and manage keys with standardized APIs. After the encryption keys are deleted, you can be assured that your data is no longer retrievable.

* **Encryption for IBM Cloud services**

  By integrating with other {{site.data.keyword.cloud_notm}} services, {{site.data.keyword.hscrypto}} offers the capability of bringing your own encryption to the cloud. The service provides double-layer protection for your cloud data by wrapping the encryption keys that are associated with your cloud services.

* **Access management and auditing**

  {{site.data.keyword.hscrypto}} integrates with {{site.data.keyword.iamshort}} (IAM) to enable your granular control over user access to service resources. You can also monitor activities of Hyper Protect Crypto Services by using {{site.data.keyword.at_full_notm}}.

### Cloud HSMs
{: #cloud-hsm}

* **Customer-controlled HSM**

  With Keep Your Own Key, {{site.data.keyword.hscrypto}} allows you to take the ownership of the HSM through assigning your own administrators and loading master keys. This ensures your full control of the entire key hierarchy with no access even from {{site.data.keyword.cloud_notm}} administrators.

* **Cryptographic operations**

  {{site.data.keyword.hscrypto}} supports Enterprise PKCS #11 for cryptographic operations. The operations include generating keys, encrypting and decrypting data, signing data, and verifying signatures. The cryptographic functions are executed in HSMs and can be accessed through APIs to provide hardware-based protection for your applications.

* **Security certification**

  The service is built on FIPS 140-2 Level 4-certified hardware, the highest security level that is offered in the industry. The HSM is also certified to meet the Common Criteria Part 3 conformant EAL 4.

<!-- {{site.data.keyword.hscrypto}} also leverages the ACSP solution that enables remote access to the IBM’s cryptographic coprocessors. ACSP allows for utilization of strong hardware-based cryptography as a service in distributed environments where data security cannot be guaranteed. {{site.data.keyword.hscrypto}} utilizes ACSP as a *network hardware security module (NetHSM)* that provides access to HSM via PKCS#11 standard API.-->

## What's next
{: #overview-next}

- To get an overall tutorial about using {{site.data.keyword.hscrypto}}, check out [Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started).
- To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
- For more information about the compliance certificates that {{site.data.keyword.hscrypto}} receives, see [Security and compliance](/docs/hs-crypto?topic=hs-crypto-security-and-compliance).
