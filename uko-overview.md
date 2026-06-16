---

copyright:
  years: 2022, 2026
lastupdated: "2026-06-16"

keywords: key management, dedicated key management, hsm, hardware security module, cloud hsm, dedicated hsm, keep your own key, kyok, cryptographic operation, key storage, encryption key, cloud encryption, encryption at rest, secure service container, ssc

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}






# Overview - Unified Key Orchestrator Plan
{: #uko-overview}

IBM Cloud&reg; Hyper Protect Crypto Services is a dedicated key management service and [Hardware Security Module (HSM)](#x6704988){: term} that provides you with the Keep Your Own Key capability for cloud data encryption. Built on FIPS 140-2 Level 4 certified hardware, Hyper Protect Crypto Services provides you with exclusive control of your encryption keys. With Unified Key Orchestrator, you can connect your service instance to keystores in IBM Cloud and third-party cloud providers, back up and manage keys by using a unified system, and orchestrate keys across multiple clouds.
{: shortdesc}

Watch the following video to learn how Hyper Protect Crypto Services with Unified Key Orchestrator provides you with exclusive encryption key control and unified key management in the cloud:

![IBM Cloud Hyper Protect Crypto Services Overview](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_1ipwq52p){: video output="iframe" data-script="none" id="mediacenterplayer" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}

## Why IBM Cloud Hyper Protect Crypto Services?
{: #uko-why_hpcs}

Data and information security is crucial and essential for IT environments. As more data moves to the cloud, keeping data protected becomes a nontrivial challenge. Built on IBM LinuxONE technology, Hyper Protect Crypto Services helps ensure that only you have access to your keys and data.

A single-tenant key management service that is provided by dedicated customer-controlled HSMs helps you easily create and manage your encryption keys. Alternatively, you can bring your own encryption keys to the cloud. The service uses the same key-provider API as Key Protect, a multi-tenant key management service, to provide a consistent approach to adopting IBM Cloud services.

Hyper Protect Crypto Services offers a dedicated HSM that is controlled by you. IBM Cloud administrators have no access. The service is built on FIPS 140-2 Level 4-certified hardware, the highest offered by any cloud provider in the industry. IBM is the first to provide cloud command-line interface (CLI) for HSM [master key](#x2908413){: term} initialization to help enable you to take ownership of the cloud HSM. You can also load the master key with the IBM Hyper Protect Crypto Services Management Utilities. The Management Utilities create and store your master key parts on smart cards and never exposes your secrets to the workstation and cloud, thus ensuring the highest level of protection to your secrets.

Hyper Protect Crypto Services can integrate with IBM Cloud data and storage services as well as VMware&reg; vSphere&reg; and VSAN, for providing data-at-rest encryption.

The managed cloud HSM supports the industry-standard cryptographic operations by using the Public-Key Cryptography Standards (PKCS) #11. You don't need to change your existing applications that use PKCS #11 standard to make it run in the Hyper Protect Crypto Services environment. The PKCS #11 library accepts the PKCS #11 API requests from your applications and remotely accesses the cloud HSM to execute the corresponding cryptographic functions, such as digital signing and validation.

Enterprise PKCS #11 over gRPC (GREP11) is also supported by Hyper Protect Crypto Services. The EP11 library provides an interface similar to the industry-standard [PKCS #11 application programming interface (API)](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}.

With the built-in encryption of Hyper Protect Crypto Services, you can easily build cloud applications with sensitive data. Hyper Protect Crypto Services provides you with complete control of your data and encryption keys, including the master key. The service also helps your business meet regulatory compliance with the technology that provides exclusive controls on the external and privileged user access to data and keys.




## Why Unified Key Orchestrator?
{: #why-uko}

Many enterprises have the legal obligation to bring their own cryptographic keys when they move sensitive workloads to the cloud. Enterprises are adopting native encryption and key management offerings from cloud providers.

Dealing with multiple clouds means to deal with cryptographic keys in multiple key management services. This presents the following challenges:
- High manual effort and susceptibility to errors when enterprises operate different key management systems
- No control over the master key in external cloud key management systems
- Shortage of data centers and skilled staff to operate hardware security modules (HSMs) for KYOK or BYOK

Unified Key Orchestrator alleviates the complexity of maintaining encryption across hybrid environments. You can integrate all your key management use cases into one consistent approach, backed by a trusted IBM zSystems HSM. It provides you with the following features:
- Consistent user experience
- Seamless integration into the existing cloud framework
- One point of control for multiple keys in multiple clouds
- Secure backup of all keys and easy restoration across multiple clouds




For an architectural diagram of Hyper Protect Crypto Services, see [Service architecture](/docs/hs-crypto?topic=hs-crypto-uko-architecture-workload-isolation).

Watch the following video to learn how to manage compliance of a Microsoft Office 365 environment using Hyper Protect Crypto Services with Unified Key Orchestrator:

![Managing compliance of a Microsoft Office 365 environment using IBM Cloud Hyper Protect Crypto Services with Unified Key Orchestrator](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_1pzzhrb8){: video output="iframe" data-script="none" id="mediacenterplayer1" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}

Watch the following video to learn how to securely manage AWS S3 encryption keys using Hyper Protect Crypto Services with Unified Key Orchestrator:

![Securely managing AWS S3 encryption keys using Hyper Protect Crypto Services with Unified Key Orchestrator](https://www.kaltura.com/p/1773841/sp/177384100/embedIframeJs/uiconf_id/27941801/partner_id/1773841?iframeembed=true&entry_id=1_1a6c6vub){: video output="iframe" data-script="none" id="mediacenterplayer2" frameborder="0" width="560" height="315" allowfullscreen webkitallowfullscreen mozAllowFullScreen}

## Key features
{: #uko-key-features}

Hyper Protect Crypto Services provides the following features:

### Unified Key Orchestrator
{: #hpcs-uko-overview}

* **Connection to external keystores**

    Unified Key Orchestrator, as part of Hyper Protect Crypto Services, provides key lifecycle management according to NIST recommendations and secure transfer of keys to internal keystores in the service instance or external keystores. With Unified Key Orchestrator, you can push your keys to third-party cloud keystores, such as Azure Key Vault, AWS Key Management Service (KMS), Google Cloud KMS, or IBM Key Protect for IBM Cloud, distribute keys across keystores, and manage keys and keystores through both the UI and REST API.

* **Unified key backup and management system**

   Unified Key Orchestrator enables you to back up all keys in IBM Cloud with your Hyper Protect Crypto Services instance. You can redistribute keys through your Hyper Protect Crypto Services instance to quickly recover from fatal cloud errors. And at the same time, you own the root trust of your key hierarchy.

* **Key orchestration across multiple clouds**

    You can orchestrate keys through a single and unified user experience across multiple clouds with an auditable key lifecycle orchestration mechanism. For more information, see [Monitoring the lifecycle of encryption keys in Unified Key Orchestrator](/docs/hs-crypto?topic=hs-crypto-uko-key-states) and [Auditing events for Hyper Protect Crypto Services Hyper Protect Crypto Services with Unified Key Orchestrator](/docs/hs-crypto?topic=hs-crypto-uko-at-events).

For more information about Unified Key Orchestrator, see [Introducing Unified Key Orchestrator](/docs/hs-crypto?topic=hs-crypto-introduce-uko).

### Key management service
{: #uko-key-management}


In the Hyper Protect Crypto Services with Unified Key Orchestrator plan, currently you can manage key management service (KMS) root keys and standard keys only through the API. For more information about the KMS API, see the [KMS API reference](/apidocs/hs-crypto){: external}.
{: note}

* **Key lifecycle management**

    Hyper Protect Crypto Services provides a single-tenant key management service to create, import, rotate, and manage keys with the standardized API. After the encryption keys are deleted, you can be assured that your data is no longer retrievable.

* **Encryption for IBM Cloud data and workload services**

    By integrating with other IBM Cloud services, Hyper Protect Crypto Services offers the capability of bringing your own encryption to the cloud. The service provides double-layer protection for your cloud data by wrapping the encryption keys that are associated with your cloud services.

* **Access management and auditing**

    Hyper Protect Crypto Services integrates with Cloud Identity and Access Management (IAM) to enable your granular control over user access to service resources. For more information, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-uko-manage-access).

    You can also monitor and audit events and activities of Hyper Protect Crypto Services by using IBM Cloud Activity Tracker. For more information, see [Auditing events for Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-at-events).

### Cloud hardware security module
{: #uko-cloud-hsm}

* **Customer-controlled HSM**

    With Keep Your Own Key, you can take the ownership of the HSM through assigning your own administrators and loading master keys with Hyper Protect Crypto Services. This ensures your full control of the entire key hierarchy with no access even from IBM Cloud administrators.

* **Cryptographic operations**

    Hyper Protect Crypto Services supports the standard PKCS #11 API and the Enterprise PKCS #11 over gRPC (GREP11) API for cryptographic operations. The operations include generating keys, encrypting and decrypting data, signing data, and verifying signatures. The cryptographic functions are executed in HSMs and can be accessed through APIs to provide hardware-based protection for your applications.

    
    In the Hyper Protect Crypto Services with Unified Key Orchestrator plan, currently you can perform the cryptographic operations only through the APIs. For more information about the APIs, see the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and the [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
    {: note}



* **Security certification**

    The service is built on FIPS 140-2 Level 4-certified hardware, the highest security level that is offered in the industry. The HSM is also certified to meet the Common Criteria Part 3 conformant EAL 4.



## What's next
{: #uko-overview-next}

- To get an overall tutorial about using Hyper Protect Crypto Services, check out [Getting started with IBM Cloud Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-get-started).
- To find out more about managing your Unified Key Orchestrator keys and keystores, check out the [Unified Key Orchestrator API reference doc](/apidocs/uko){: external}.
- To find out more about programmatically managing your KMS keys, check out the [Hyper Protect Crypto Services key management service API reference doc](/apidocs/hs-crypto){: external}.
- To find out more about the PKCS #11 API, see [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-uko-pkcs11-intro) and [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
- To find out more about the GREP11 API, see [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-uko-grep11-intro) and [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
- For more information about the compliance certificates that Hyper Protect Crypto Services receives, see [Security and compliance](/docs/hs-crypto?topic=hs-crypto-security-and-compliance).
- To find more about available IBM Cloud services for integration, see [Integrating IBM Cloud services with Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- To find the differences between Hyper Protect Crypto Services with Unified Key Orchestrator and Hyper Protect Crypto Services Standard Plan , see [How is Hyper Protect Crypto Services with Unified Key Orchestrator different from the Hyper Protect Crypto Services Standard Plan?](/docs/hs-crypto?topic=hs-crypto-faq-uko&interface=ui#faq-uko-hpcs) 
