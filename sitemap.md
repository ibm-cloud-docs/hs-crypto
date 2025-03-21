---

copyright:
  years: 2021, 2024
lastupdated: "2024-08-22"

keywords: site map, doc structure, information architecture

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Site map
{: #sitemap}

Find what you are looking for in the compilation of topics that are available in this documentation set.
{: shortdesc}







## Getting started
{: #sitemap_getting_started}


[Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started#get-started)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-get-started#get-started-prerequisites)

* [Step 1: Initialize your service instance](/docs/hs-crypto?topic=hs-crypto-get-started#initialize-crypto)

* [Step 2 (Standard Plan only): Create keys](/docs/hs-crypto?topic=hs-crypto-get-started#create-key-standard)

* [Step 2 ({{site.data.keyword.uko_full_notm}} Plan only): Manage your encryption keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-uko-key)

* [Step 3: Encrypt your data with cloud HSM](/docs/hs-crypto?topic=hs-crypto-get-started#encrypt-data-hsm)


## Understanding Hyper Protect Crypto Services Standard Plan
{: #sitemap_understanding_hyper_protect_crypto_services_standard_plan}


[Overview - Standard Plan](/docs/hs-crypto?topic=hs-crypto-overview#overview)

* [Why {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-overview#why_hpcs)

* [How does {{site.data.keyword.hscrypto}} work?](/docs/hs-crypto?topic=hs-crypto-overview#how-hpcs-work)

* [Key features](/docs/hs-crypto?topic=hs-crypto-overview#key-features)

* [What's next](/docs/hs-crypto?topic=hs-crypto-overview#overview-next)

[Service architecture - Standard Plan](/docs/hs-crypto?topic=hs-crypto-architecture-workload-isolation#architecture-workload-isolation)

* [{{site.data.keyword.hscrypto}} architecture](/docs/hs-crypto?topic=hs-crypto-architecture-workload-isolation#architecture)

* [{{site.data.keyword.hscrypto}} workload isolation](/docs/hs-crypto?topic=hs-crypto-architecture-workload-isolation#workload-isolation)

* [Service dependencies](/docs/hs-crypto?topic=hs-crypto-architecture-workload-isolation#service_dependencies)

[Use cases - Standard Plan](/docs/hs-crypto?topic=hs-crypto-use-cases#use-cases)

* [Pervasively protecting data at rest in the cloud](/docs/hs-crypto?topic=hs-crypto-use-cases#data-at-rest-encryption)

* [Using {{site.data.keyword.hscrypto}} as a cloud HSM](/docs/hs-crypto?topic=hs-crypto-use-cases#cloud_hsm)

* [What's next](/docs/hs-crypto?topic=hs-crypto-use-cases#use-case-next)

[Components and concepts - Standard Plan](/docs/hs-crypto?topic=hs-crypto-understand-concepts#understand-concepts)

* [Key management service](/docs/hs-crypto?topic=hs-crypto-understand-concepts#key-management-concepts)

* [Cloud hardware security module](/docs/hs-crypto?topic=hs-crypto-understand-concepts#cloud-hsm-concepts)


### About service instance initialization - Standard Plan
{: #sitemap_about_service_instance_initialization_standard_plan}


[Initializing your service instance - Standard Plan](/docs/hs-crypto?topic=hs-crypto-introduce-service#introduce-service)

* [Understanding administrators and signature keys](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-crypto-unit-admin)

* [Understanding imprint mode and signature thresholds](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-imprint-mode)

* [Understanding the master key](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-key-ceremony)

* [What's next](/docs/hs-crypto?topic=hs-crypto-introduce-service#introduce-instance-initialization-next)

[Introducing service instance initialization approaches - Standard Plan](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#initialize-instance-mode)

* [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-management-utilities)

* [Initializing service instances by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit)

* [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-key-files)

* [What's next](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#initialize-instance-mode-next)


### About key management service - Standard Plan
{: #sitemap_about_key_management_service_standard_plan}


[Bringing your encryption keys to the cloud - Standard Plan](/docs/hs-crypto?topic=hs-crypto-importing-keys#importing-keys)

* [Planning ahead for importing key material](/docs/hs-crypto?topic=hs-crypto-importing-keys#plan-ahead)

* [Using import tokens](/docs/hs-crypto?topic=hs-crypto-importing-keys#using-import-tokens)

* [What's next](/docs/hs-crypto?topic=hs-crypto-importing-keys#importing-keys-next)

[Protecting your data with envelope encryption - Standard Plan](/docs/hs-crypto?topic=hs-crypto-envelope-encryption#envelope-encryption)

* [Keys in envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption#key-types)

* [How it works](/docs/hs-crypto?topic=hs-crypto-envelope-encryption#envelope-encryption-overview)

* [Wrapping keys](/docs/hs-crypto?topic=hs-crypto-envelope-encryption#wrapping)

* [Unwrapping keys](/docs/hs-crypto?topic=hs-crypto-envelope-encryption#unwrapping)

* [What's next](/docs/hs-crypto?topic=hs-crypto-envelope-encryption#envelope-encryption-next)

[Monitoring the lifecycle of encryption keys - Standard Plan](/docs/hs-crypto?topic=hs-crypto-key-states#key-states)

* [Key states and transitions](/docs/hs-crypto?topic=hs-crypto-key-states#key-transitions)

* [Key states and service actions](/docs/hs-crypto?topic=hs-crypto-key-states#key-states-service-actions)

* [Monitoring for lifecycle changes](/docs/hs-crypto?topic=hs-crypto-key-states#monitor-lifecycle-changes)


### About cloud hardware security module - Standard Plan
{: #sitemap_about_cloud_hardware_security_module_standard_plan}


[Introducing cloud HSM - Standard Plan](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm#introduce-cloud-hsm)

* [What is cloud HSM?](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm#what-is-cloud-hsm)

* [Performing cryptographic operations by accessing the cloud HSM](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm#cryptography-cloud-hsm)

[Introducing PKCS #11 - Standard Plan](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro#pkcs11-intro)

* [PKCS #11 implementation components](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro#pkcs11-components)

* [Post-quantum cryptography support](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro#pkcs11-support-post-quantum)

[Introducing EP11 over gRPC - Standard Plan](/docs/hs-crypto?topic=hs-crypto-grep11-intro#grep11-intro)

* [Post-quantum cryptography support](/docs/hs-crypto?topic=hs-crypto-grep11-intro#grep11-support-post-quantum)


### About key rotation - Standard Plan
{: #sitemap_about_key_rotation_standard_plan}


[Master key rotation - Standard Plan](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro#master-key-rotation-intro)

* [How master key rotation works](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro#how-master-key-rotation-works)

* [What's next](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro#master-key-rotation-next)

[Root key rotation - Standard Plan](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro#root-key-rotation-intro)

* [Comparing your root key rotation options](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro#compare-key-rotation-options)

* [How root key rotation works](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro#how-root-key-rotation-works)

* [Frequency of root key rotation](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro#rotation-frequency)

* [What's next](/docs/hs-crypto?topic=hs-crypto-root-key-rotation-intro#root-key-rotation-next)


### About Bring Your Own HSM  - Standard Plan
{: #sitemap_about_bring_your_own_hsm_standard_plan}


[Introducing Bring Your Own HSM](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm#introduce-bring-your-own-hsm)

* [What is Bring Your Own HSM?](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm#what-is-byohsm)

* [How to enable Bring Your Own HSM?](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm#how-to-enable-byohsm)

* [Limitations and scope](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm#byohsm-limitation-scope)

* [Responsibilities](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm#byohsm-responsibility)


## Understanding Hyper Protect Crypto Services with Unified Key Orchestrator Plan
{: #sitemap_understanding_hyper_protect_crypto_services_with_unified_key_orchestrator_plan}


[Overview - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-overview#uko-overview)

* [Why {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-uko-overview#uko-why_hpcs)

* [Why {{site.data.keyword.uko_full_notm}}?](/docs/hs-crypto?topic=hs-crypto-uko-overview#why-uko)

* [Key features](/docs/hs-crypto?topic=hs-crypto-uko-overview#uko-key-features)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-overview#uko-overview-next)

[Service architecture - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-architecture-workload-isolation#uko-architecture-workload-isolation)

* [{{site.data.keyword.hscrypto}} architecture](/docs/hs-crypto?topic=hs-crypto-uko-architecture-workload-isolation#uko-architecture)

* [{{site.data.keyword.hscrypto}} workload isolation](/docs/hs-crypto?topic=hs-crypto-uko-architecture-workload-isolation#uko-workload-isolation)

* [Service dependencies](/docs/hs-crypto?topic=hs-crypto-uko-architecture-workload-isolation#uko-service_dependencies)

[Use cases - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-use-cases#uko-use-cases)

* [Pervasively protecting data at rest in the cloud](/docs/hs-crypto?topic=hs-crypto-uko-use-cases#uko-data-at-rest-encryption)

* [Using {{site.data.keyword.uko_full_notm}} for multicloud key orchestration](/docs/hs-crypto?topic=hs-crypto-uko-use-cases#uko-use-case)

* [Using {{site.data.keyword.hscrypto}} as a cloud HSM](/docs/hs-crypto?topic=hs-crypto-uko-use-cases#uko-cloud_hsm)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-use-cases#uko-use-case-next)

[Components and concepts](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-understand-concepts)

* [Key management service](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-key-management-concepts)

* [Cloud hardware security module](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-cloud-hsm-concepts)

* [{{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts#uko-unified-key-orchestrator-concepts)


### About service instance initialization - Unified Key Orchestrator Plan
{: #sitemap_about_service_instance_initialization_unified_key_orchestrator_plan}


[Initializing your service instance - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-introduce-service#uko-introduce-service)

* [Understanding administrators and signature keys](/docs/hs-crypto?topic=hs-crypto-uko-introduce-service#uko-understand-crypto-unit-admin)

* [Understanding imprint mode and signature thresholds](/docs/hs-crypto?topic=hs-crypto-uko-introduce-service#uko-understand-imprint-mode)

* [Understanding the master key](/docs/hs-crypto?topic=hs-crypto-uko-introduce-service#uko-understand-key-ceremony)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-introduce-service#uko-introduce-instance-initialization-next)

[Introducing service instance initialization approaches - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-initialize-instance-mode#uko-initialize-instance-mode)

* [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-uko-initialize-instance-mode#uko-instance-initialization-management-utilities)

* [Initializing service instances by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-uko-initialize-instance-mode#uko-instance-initialization-recovery-crypto-unit)

* [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-uko-initialize-instance-mode#uko-instance-initialization-key-files)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-initialize-instance-mode#uko-initialize-instance-mode-next)


### About Unified Key Orchestrator
{: #sitemap_about_unified_key_orchestrator}


[Introducing {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-introduce-uko#introduce-uko)

* [Use case example](/docs/hs-crypto?topic=hs-crypto-introduce-uko#uko-use-case-example)

* [Components](/docs/hs-crypto?topic=hs-crypto-introduce-uko#Components)

* [What's next](/docs/hs-crypto?topic=hs-crypto-introduce-uko#uko-next)

[Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states#uko-key-states)

* [Key states and transitions](/docs/hs-crypto?topic=hs-crypto-uko-key-states#uko-key-transitions)

* [Key states and service actions](/docs/hs-crypto?topic=hs-crypto-uko-key-states#uko-key-states-service-actions)

* [Monitoring for lifecycle changes](/docs/hs-crypto?topic=hs-crypto-uko-key-states#uko-monitor-lifecycle-changes)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-key-states#uko-key-states-next)


### About cloud hardware security module - Unified Key Orchestrator Plan
{: #sitemap_about_cloud_hardware_security_module_unified_key_orchestrator_plan}


[Introducing cloud HSM - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-introduce-cloud-hsm#uko-introduce-cloud-hsm)

* [What is cloud HSM?](/docs/hs-crypto?topic=hs-crypto-uko-introduce-cloud-hsm#uko-what-is-cloud-hsm)

* [Performing cryptographic operations by accessing the cloud HSM](/docs/hs-crypto?topic=hs-crypto-uko-introduce-cloud-hsm#uko-cryptography-cloud-hsm)

[Introducing PKCS #11 - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-pkcs11-intro#uko-pkcs11-intro)

* [PKCS #11 implementation components](/docs/hs-crypto?topic=hs-crypto-uko-pkcs11-intro#uko-pkcs11-components)

* [Post-quantum cryptography support](/docs/hs-crypto?topic=hs-crypto-uko-pkcs11-intro#uko-pkcs11-support-post-quantum)

[Introducing EP11 over gRPC - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-grep11-intro#uko-grep11-intro)

* [Post-quantum cryptography support](/docs/hs-crypto?topic=hs-crypto-uko-grep11-intro#uko-grep11-support-post-quantum)


### About key rotation - Unified Key Orchestrator Plan
{: #sitemap_about_key_rotation_unified_key_orchestrator_plan}


[Master key rotation - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro#uko-master-key-rotation-intro)

* [How master key rotation works](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro#uko-how-master-key-rotation-works)

* [How keys are protected during master key rotation](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro#uko-how-master-key-protect-rotation)

* [How the UI reflects master key rotation](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro#uko-how-console-display-progress)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro#uko-master-key-rotation-next)

[Managed key rotation](/docs/hs-crypto?topic=hs-crypto-managed-key-rotation-intro#managed-key-rotation-intro)

* [How managed key rotation works](/docs/hs-crypto?topic=hs-crypto-managed-key-rotation-intro#how-managed-key-rotation-works)

* [What's next](/docs/hs-crypto?topic=hs-crypto-managed-key-rotation-intro#managed-key-rotation-next)


## Managing regulated workloads with {{site.data.keyword.hscrypto}}
{: #sitemap_managing_regulated_workloads_with_}


[Managing regulated workloads with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-manage-regulated-workloads#manage-regulated-workloads)

* [Encrypting your regulated workloads with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-manage-regulated-workloads#encrypt-regulated-workloads)

* [Regulated workloads use cases](/docs/hs-crypto?topic=hs-crypto-manage-regulated-workloads#regulated-workloads-use-cases)

* [Getting started to manage your regulated workloads with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-manage-regulated-workloads#get-started-regulated-workloads)

* [Reference](/docs/hs-crypto?topic=hs-crypto-manage-regulated-workloads#reference-regulated-workloads)


## Integrating {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.hscrypto}}
{: #sitemap_integrating_services_with_}


[Integrating {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-integrate-services#integrate-services)

* [Storage service integrations](/docs/hs-crypto?topic=hs-crypto-integrate-services#storage-integration)

* [Database service integrations](/docs/hs-crypto?topic=hs-crypto-integrate-services#database-integration)

* [Compute service integrations](/docs/hs-crypto?topic=hs-crypto-integrate-services#compute-integration)

* [Container service integrations](/docs/hs-crypto?topic=hs-crypto-integrate-services#container-integration)

* [Ingestion service integrations](/docs/hs-crypto?topic=hs-crypto-integrate-services#Ingestion-integrations)

* [Security service integrations](/docs/hs-crypto?topic=hs-crypto-integrate-services#security-service-integrations)

* [Developer tools service integrations](/docs/hs-crypto?topic=hs-crypto-integrate-services#devtools-integrations)

* [Understanding your integration](/docs/hs-crypto?topic=hs-crypto-integrate-services#understand-integration)

* [What's next](/docs/hs-crypto?topic=hs-crypto-integrate-services#integration-next-steps)


## Security and compliance
{: #sitemap_security_and_compliance}


[Security and compliance](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#security-and-compliance)

* [Security readiness](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#security-ready)

* [Compliance readiness](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#compliance-ready)


## Release notes
{: #sitemap_release_notes}


[Release notes](/docs/hs-crypto?topic=hs-crypto-what-new#what-new)

* [18 July 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-july182024)

    * Updated: Transition to VPC data centers in Dallas, Washington D.C, and Frankfurt

* [15 July 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-july152024)

    * Updated: New API endpoints in Frankfurt

* [2 July 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-july22024)

    * Updated: New API endpoints in Madrid

* [19 June 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-june192024)

    * Updated: New API endpoints in Tokyo

* [5 June 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-june2024)

    * Updated: New API endpoints in London

* [29 May 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-may292024)

    * Updated: New API endpoints in Toronto

* [15 May 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-may152024)

    * Updated: New API endpoints in S&atilde;o-Paulo

* [8 May 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-may2024)

    * Updated: New API endpoints in Dallas

* [12 April 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-apr2024)

    * Updated: New API endpoints in Washington DC

* [29 February 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-feb2024)

    * Added: New key state `pending destruction` 

    * Added: Connecting to Azure Key Vault through private endpoint

* [18 January 2024](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-jan2024)

    * Added: Azure software-protected key support for {{site.data.keyword.cloud_notm}}

* [09 November 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-nov2023)

    * Added: {{site.data.keyword.hscrypto}} adds support for Bring Your Own HSM (BYOHSM)

* [26 October 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-26oct2023)

    * Deprecated: {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} in Sydney

* [22 Sept 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-sept2023)

    * Added: {{site.data.keyword.hscrypto}} expands into the Madrid region 

* [3 August 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-august2023)

    * Added: Key template support for {{site.data.keyword.uko_full_notm}} 

* [1 June 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-june2023)

    * Updated: Pricing plan for {{site.data.keyword.uko_full_notm}} 

* [24 May 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-may2023)

    * Updated: Master key rotation support for all regions

* [24 March 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-march2023)

    * Added: Master key rotation for {{site.data.keyword.uko_full_notm}}

    * Added: Master key rotation for EP11 keystores

* [1 Feb 2023](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-feb2023)

    * Added: {{site.data.keyword.hscrypto}} key management functions 

    * Added: Activity Tracker event names

* [19 December 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-dec2022)

    * Added: Managed key rotation support for {{site.data.keyword.uko_full_notm}}

* [21 November 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-nov2022)

    * Added: Management Utilities support for Red Hat Enterprise Linux 9.0 and Ubuntu 22.04.1 LTS

* [31 October 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-31oct2022)

    * Added: Google Cloud KMS support

* [20 October 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-20oct2022)

    * Added: EP11 activity tracker events

* [24 June 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-24june2022)

    * Added: Go SDK and Terraform support for {{site.data.keyword.uko_full_notm}}

* [8 June 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-8june2022)

    * [Added: Post-quantum cryptography support](/docs/hs-crypto?topic=hs-crypto-what-new#add-pqc)

* [3 June 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-3june2022)

    * [Added: {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} CLI plug-in](/docs/hs-crypto?topic=hs-crypto-what-new#add-uko-cli)

* [1 April 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-1april2022)

    * [Updated: Pricing model of the {{site.data.keyword.hscrypto}} standard plan](/docs/hs-crypto?topic=hs-crypto-what-new#update-pricing-model)

    * [Updated: Process of ordering smart cards and smart card readers](/docs/hs-crypto?topic=hs-crypto-what-new#update-smartcard-procurement)

* [25 March 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-25mar2022)

    * [Added: {{site.data.keyword.hscrypto}} expands into the Toronto region](/docs/hs-crypto?topic=hs-crypto-what-new#add-toronto-region)

* [22 March 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-march2022)

    * General availability: Using {{site.data.keyword.uko_full_notm}} to manage and orchestrate keys in a multicloud environment 

* [28 February 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-28feb2022)

    * [Limited availability: Using {{site.data.keyword.uko_full_notm}} to manage and orchestrate keys in a multicloud environment](/docs/hs-crypto?topic=hs-crypto-what-new#add-uko})

* [23 February 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-23feb2022)

    * [Added: Using {{site.data.keyword.mon_full_notm}} to measure {{site.data.keyword.hscrypto}} metrics](/docs/hs-crypto?topic=hs-crypto-what-new#add-monitoring-metrics)

* [15 February 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-15feb2022)

    * [Added: {{site.data.keyword.hscrypto}} expands into the S&atilde;o-Paulo region](/docs/hs-crypto?topic=hs-crypto-what-new#add-sao-region)

* [21 January 2022](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-jan2022)

    * [Updated: {{site.data.keyword.hscrypto}} key management functions](/docs/hs-crypto?topic=hs-crypto-what-new#update-kms-api-v282)

* [30 July 2021](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-july2021)

    * [Added: Exclusive control on the execution of cryptographic operations](/docs/hs-crypto?topic=hs-crypto-what-new#add-cert-manager)

    * [Added: {{site.data.keyword.hscrypto}} expands into the Tokyo region](/docs/hs-crypto?topic=hs-crypto-what-new#add-tokyo-region)

    * [Added: Using Terraform to initialize the {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-what-new#add-terraform-automation)

    * [Added: Using a signing service to manage signature keys for instance initialization](/docs/hs-crypto?topic=hs-crypto-what-new#add-signing-service)

* [30 June 2021](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-june2021)

    * [Added: Authenticated PKCS #11 keystore](/docs/hs-crypto?topic=hs-crypto-what-new#add-authenticated-pkcs11-keystore)

    * [Added: Enabling cross-region recovery with failover crypto units](/docs/hs-crypto?topic=hs-crypto-what-new#add-failover-crypto-units)

    * [Added: {{site.data.keyword.hscrypto}} expands into the London region](/docs/hs-crypto?topic=hs-crypto-what-new#add-london-region)

* [30 April 2021](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-april2021)

    * [Added: Rotating your master key by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-what-new#add-master-key-rotation-smart-cards)

    * [Updated: Restore key API and UI](/docs/hs-crypto?topic=hs-crypto-what-new#update-restore-key-api-ui)

* [31 March 2021](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-march2021)

    * [Added: Grouping keys by using key rings](/docs/hs-crypto?topic=hs-crypto-what-new#add-key-ring)

    * [Added: Initializing the service instance by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-what-new#add-recovery-crypto-units)

    * [Added: Managing EP11 keystores and keys with the UI](/docs/hs-crypto?topic=hs-crypto-what-new#add-ep11-keystores-keys-console)

    * [Added: Managing key aliases for a key](/docs/hs-crypto?topic=hs-crypto-what-new#add-key-alias)

    * [Added: Synchronizing protected resources associated with root keys](/docs/hs-crypto?topic=hs-crypto-what-new#add-sync-resources)

    * [Added: Using Virtual Private Endpoints for VPC](/docs/hs-crypto?topic=hs-crypto-what-new#add-vpe-for-vpc)

    * [Updated: The cryptography algorithm that is used to generate signature keys](/docs/hs-crypto?topic=hs-crypto-what-new#update-signature-key-algorithm)

* [28 February 2021](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-february2021)

    * [Added: Key verification by using the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-what-new#add-key-verification)

    * [Added: Support for the Schnorr algorithm](/docs/hs-crypto?topic=hs-crypto-what-new#add-schnorr)

* [31 January 2021](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-january2021)

    * [Added: Support for a single-tenant KMIP adapter](/docs/hs-crypto?topic=hs-crypto-what-new#add-support-kmip-adapter)

* [31 December 2020](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-december2020)

    * [Added: Managing the key create and import access policy](/docs/hs-crypto?topic=hs-crypto-what-new#add-key-create-import-access)

    * [Added: Provisioning and managing service instances with the private-only network](/docs/hs-crypto?topic=hs-crypto-what-new#add-private-only-network)

    * [Added: `ReencryptSingle` function in GREP11 API](/docs/hs-crypto?topic=hs-crypto-what-new#add-reencryptsingle-function-grep11)

    * [Added: Support for accessing service instances through the Virtual Private Endpoint](/docs/hs-crypto?topic=hs-crypto-what-new#add-vpe)

    * [Added: Support for the SLIP10 mechanism and Edwards-curve algorithm](/docs/hs-crypto?topic=hs-crypto-what-new#add-slip10-eddsa)

    * [Added: Using Terraform to manage {{site.data.keyword.hscrypto}} instances and resources](/docs/hs-crypto?topic=hs-crypto-what-new#add-terraform)

    * [Updated: key management service API](/docs/hs-crypto?topic=hs-crypto-what-new#update-kms-api-december)

* [30 November 2020](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-november2020)

    * [Added: Support for the BIP32 mechanism](/docs/hs-crypto?topic=hs-crypto-what-new#add-bip32-mechanism)

    * [Added: TKE activity tracker events](/docs/hs-crypto?topic=hs-crypto-what-new#add-tke-at-events)

* [30 September 2020](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-september2020)

    * [Added: Master key rotation](/docs/hs-crypto?topic=hs-crypto-what-new#added-master-key-rotation)

    * [Added: Support for performing cryptographic operations with the standard PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-what-new#added-pkcs11)

* [31 August 2020](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-august2020)

    * [Added: Support for import tokens to securely upload encryption keys](/docs/hs-crypto?topic=hs-crypto-what-new#added-import-tokens)

* [31 July 2020](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-july2020)

    * [Added: {{site.data.keyword.hscrypto}} aligns the key management functions with {{site.data.keyword.keymanagementserviceshort}}](/docs/hs-crypto?topic=hs-crypto-what-new#added-key-protect-concurrency)

    * [Added: {{site.data.keyword.hscrypto}} expands into the Washington DC region](/docs/hs-crypto?topic=hs-crypto-what-new#added-wdc-region)

* [30 June 2020](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-june2020)

    * [Added: Support for quorum authentication](/docs/hs-crypto?topic=hs-crypto-what-new#added-quorum-authentication-202006)

* [30 April 2020](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-april2020)

    * [Added: {{site.data.keyword.hscrypto}} adds support for EP11 private endpoints](/docs/hs-crypto?topic=hs-crypto-what-new#added-private-endpoints-202004)

    * [Added: {{site.data.keyword.hscrypto}} adds support for the Management Utilities](/docs/hs-crypto?topic=hs-crypto-what-new#added-management-utilities-202004)

    * [Updated: {{site.data.keyword.cloud_notm}} service integration](/docs/hs-crypto?topic=hs-crypto-what-new#added-service-integration-202004)

* [31 August 2019](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-August2019)

    * [Added: {{site.data.keyword.hscrypto}} adds support for private endpoints](/docs/hs-crypto?topic=hs-crypto-what-new#added-private-endpoints)

    * [Added: {{site.data.keyword.hscrypto}} Cloud HSM now supports EP11 cryptographic operations over gRPC](/docs/hs-crypto?topic=hs-crypto-what-new#added-EP11)

    * [Added: {{site.data.keyword.hscrypto}} expands into the Frankfurt region](/docs/hs-crypto?topic=hs-crypto-what-new#added-frankfurt-region)

    * [Added: {{site.data.keyword.cloud_notm}} service integration](/docs/hs-crypto?topic=hs-crypto-what-new#added-service-integration)

* [30 June 2019](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-June2019)

    * [Added: {{site.data.keyword.hscrypto}} expands into Sydney region](/docs/hs-crypto?topic=hs-crypto-what-new#added-sydney-region)

* [31 March 2019](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-March2019)

    * [{{site.data.keyword.hscrypto}} is generally available](/docs/hs-crypto?topic=hs-crypto-what-new#ga-201903)

    * [High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-what-new#ha-dr-new)

    * [Scalability](/docs/hs-crypto?topic=hs-crypto-what-new#scalability-new)

* [28 February 2019](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-Feb2019)

    * [{{site.data.keyword.hscrypto}} Beta is available](/docs/hs-crypto?topic=hs-crypto-what-new#beta-201902)

* [31 December 2018](/docs/hs-crypto?topic=hs-crypto-what-new#hs-crypto-Dec2018)

    * [Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API](/docs/hs-crypto?topic=hs-crypto-what-new#kp-api)

    * [Added: Support for HSM management with Keep Your own Key](/docs/hs-crypto?topic=hs-crypto-what-new#hsm-kyok)

    * [Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through Advanced Cryptography Service Provider](/docs/hs-crypto?topic=hs-crypto-what-new#deprecated-acsp)


## Tutorials on key management service
{: #sitemap_tutorials_on_key_management_service}


[Creating and importing encryption keys](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-keys)

* [Objectives](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-objectives)

* [Task flow](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-flow)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-prereqs)

* [Create an import token](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-create-token)

* [Retrieve the import token](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-retrieve-token)

* [Create an encryption key](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-create-key)

* [Set the encryption key as an environment variable](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-env-variable)

* [Encrypt the nonce with the encryption key](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-encrypt-nonce)

* [Encrypt the created encryption key](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-encrypt-key)

* [Import the encrypted key](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-encrypted-key)

* [Clean up](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-clean-up)

* [Next steps](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys#tutorial-import-next-steps)

[Configuring KMIP for key management and distribution in {{site.data.keyword.hscrypto}} Standard Plan](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-vmware)

* [Objectives](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-objectives)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-prerequisites)

* [Task flow](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-steps)

* [Grant the service-to-service authorization in IAM](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-s2s)

* [Configure KMIP for VMWare with {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-vmware-configure)

* [Configure a trusted connection between the vCenter Server and KMIP adapter](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-verify)

* [What's next](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-next)


## Tutorials on cloud hardware security module
{: #sitemap_tutorials_on_cloud_hardware_security_module}


[Using {{site.data.keyword.hscrypto}} PKCS #11 for Oracle Transparent Database Encryption](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-tde-pkcs11)

* [Objectives](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-tde-objectives)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-tde-prerequisites)

* [Task flow](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-tde-steps)

* [Initialize your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-tde-initialize)

* [Set up the {{site.data.keyword.hscrypto}} PKCS #11 library in your Oracle Database environment](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-tde-pkcs11-setup)

* [Set up Oracle Database TDE and encrypt your data](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-dte-encrypt)

* [Next steps](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11#tutorial-tde-summary)

[Using {{site.data.keyword.hscrypto}} PKCS #11 for IBM Db2 native encryption](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-pkcs11)

* [Objectives](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-objectives)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-prerequisites)

* [Task flow](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-steps)

* [Initialize your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-initialize)

* [Set up the {{site.data.keyword.hscrypto}} PKCS #11 library](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-pkcs11-setup)

* [Set up Db2 native encryption](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-encrypt)

* [Next steps](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11#tutorial-db2-summary)


## Tutorials on Unified Key Orchestrator
{: #sitemap_tutorials_on_unified_key_orchestrator}


[Using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} to manage keys in {{site.data.keyword.keymanagementserviceshort}} on Satellite](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite)

* [Objectives](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite-objectives)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite-prerequisites)

* [Task flow](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite-steps)

* [Deploy {{site.data.keyword.keymanagementserviceshort}} on Satellite](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite-deploy-kp)

* [Connect {{site.data.keyword.uko_full_notm}} to {{site.data.keyword.keymanagementserviceshort}} on Satellite](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite-connect-uko-kp)

* [Manage {{site.data.keyword.keymanagementserviceshort}} keys through {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite-manage-kp-keys)

* [Next steps](/docs/hs-crypto?topic=hs-crypto-tutorial-uko-satellite#tutorial-uko-satellite-next-step)


## Tutorials on Bring Your Own HSM
{: #sitemap_tutorials_on_bring_your_own_hsm}


[Managing your keys with BYOHSM in {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm)

* [Objectives](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-objectives)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-prerequisites)

* [Task flow](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-steps)

* [Purchase and set up your on-premises HSMs](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-step1)

* [Configure and deploy your HSMs to work with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-step2)

* [Contact IBM to get the required information](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-step3)

* [Provision a {{site.data.keyword.hscrypto}} instance with BYOHSM](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-step4)

* [Use your {{site.data.keyword.hscrypto}} instance with BYOHSM](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-step5)

* [What's next](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm#tutorial-byohsm-next)


## Provisioning service instances
{: #sitemap_provisioning_service_instances}


[Provisioning service instances](/docs/hs-crypto?topic=hs-crypto-provision#provision)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-provision#provision-prerequisites)

* [Provisioning an instance of {{site.data.keyword.hscrypto}} Standard Plan](/docs/hs-crypto?topic=hs-crypto-provision#provision-standard)

* [Provisioning an instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-provision#provision-uko)

* [What's next](/docs/hs-crypto?topic=hs-crypto-provision#provision-next)


## Initializing service instances
{: #sitemap_initializing_service_instances}


[Before you begin](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite#initialize-hsm-prerequisite)

* [What's next](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite#initialize-hsm-prerequisite-whats-next)


### Initializing service instances using smart cards and the Management Utilities
{: #sitemap_initializing_service_instances_using_smart_cards_and_the_management_utilities}


[Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#prepare-management-utilities)

* [Step 1: Order smart cards and smart card readers](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#order-smart-card-and-reader)

* [Step 2: Install the smart card reader driver on your local workstation](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver)

* [Step 3: Install the Management Utilities on your local workstation](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-management-utility-application)

* [Step 4: Configure smart cards with the Smart Card Utility Program](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#configure-smart-card-utility)

* [What's next](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#prepare-management-utilities-next)

[Initializing service instances with smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#initialize-hsm-management-utilities)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#initialize-hsm-management-utilities-prerequisites)

* [Loading the master key from the smart cards](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#load-master-key-management-utilities)

* [What's next](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#initialize-crypto-utilities-management-utilities-next)

[Initializing service instances using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit#initialize-hsm-recovery-crypto-unit)

* [Initializing service instances](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit#initialize-hsm-recovery-crypto-unit-steps)

* [What's next](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit#initialize-hsm-recovery-crypto-unit-whats-next)

[Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-hsm)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-hsm-cli-prerequisite)

* [Selecting target crypto units for service initialization](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#identify_crypto_units)

* [Loading master keys](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#load-master-keys)

* [What's next](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-crypto-cli-next)

[Using a signing service to manage signature keys for instance initialization](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key#signing-service-signature-key)

* [Signing service prerequisites](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key#signing-service-requirements)

* [Configuring the TKE CLI plug-in to use the signing service](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key#configure-tke-cli-for-signing-service)

* [What's next](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key#signing-service-whats-next)


## Retrieving an access token
{: #sitemap_retrieving_an_access_token}


[Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token#retrieve-access-token)

* [Retrieving an access token with the CLI](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token&interface=cli#retrieve-token-cli)

* [Retrieving an access token with the API](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token&interface=api#retrieve-token-api)


## Retrieving your instance ID
{: #sitemap_retrieving_your_instance_id}


[Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID#retrieve-instance-ID)

* [Viewing your instance ID with the UI](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID&interface=ui#view-instance-ID)

* [Retrieving an instance ID with the CLI](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID&interface=cli#retrieve-instance-ID-cli)

* [Retrieving an instance ID with the API](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID&interface=api#retrieve-instance-ID-api)


## Setting up API calls
{: #sitemap_setting_up_api_calls}


[Managing your keys with the key management service API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api#set-up-kms-api)

* [Retrieving your IBM Cloud credentials](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api#retrieve-kms-credentials)

* [Forming your key management service API request](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api#form-kms-api-request)

* [What's next](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api#set-up-kms-api-next-steps)

[Setting up {{site.data.keyword.uko_full_notm}} API calls - {{site.data.keyword.uko_full_notm}} Plan](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api#set-up-uko-api)

* [Retrieving your IBM Cloud credentials](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api#retrieve-uko-credentials)

* [Forming your {{site.data.keyword.uko_full_notm}} API request](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api#form-uko-api-request)

* [What's next](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api#set-up-uko-api-next-steps)

[Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#set-up-pkcs-api)

* [Prerequisites](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#prerequisite-pkcs-api)

* [Step 1: Set up the PKCS #11 library](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step1-setup-pkcs-library)

* [Step 2: (Optional) Verify the integrity and authenticity of the PKCS #11 library](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step2-verify-pkcs-library)

* [Step 3: Set up the PKCS #11 configuration file](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file)

* [Step 4: Use the PKCS #11 library to make PKCS #11 API calls](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step4-use-pkcs-library)

* [What's next](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#set-up-pkcs-api-next-steps)

[Performing cryptographic operations with the GREP11 API](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api#set-up-grep11-api)

* [Retrieving your IBM Cloud credentials](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api#retrieve-grep11-credentials)

* [Generating a GREP11 API request](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api#form-grep11-api-request)

* [What's next](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api#set-up-grep11-api-next-steps)

[Enabling the second layer of authentication for EP11 connections - Standard Plan only](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11)

* [Security and availability best practices for enabling mutual TLS authentication](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11-security-best-practices)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11-prerequisites)

* [Step 1: Configure the administrator signature key](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11-step1-signature)

* [Step 2: Set up the client CA certificate for authentication](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11-step2-certificate)

* [Step 3: Establish mutual TLS connections for EP11 applications](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11-step3-enable-tls)

* [(Optional) Disabling mutual TLS connections](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11-disable-tls)

* [What's next](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11#enable-authentication-ep11-whats-next)


## Performing key management operations with the CLI - Standard Plan only
{: #sitemap_performing_key_management_operations_with_the_cli_standard_plan_only}


[Performing key management operations with the CLI - Standard Plan only](/docs/hs-crypto?topic=hs-crypto-set-up-cli#set-up-cli)

* [What's next](/docs/hs-crypto?topic=hs-crypto-set-up-cli#cli-next-steps)


## Setting up Terraform
{: #sitemap_setting_up_terraform}


[Setting up Terraform for {{site.data.keyword.hscrypto}} Standard Plan](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs#terraform-setup-for-hpcs)

* [Example: Provisioning and initializing service instances by using Terraform](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs#terraform-provision-initialize-instance-hpcs)

* [What's next?](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs#terraform-setup-hpcs-next)

[Setting up Terraform for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-terraform-setup-for-hpcs#uko-terraform-setup-for-hpcs)

* [Example: Provisioning and initializing service instances by using Terraform](/docs/hs-crypto?topic=hs-crypto-uko-terraform-setup-for-hpcs#uko-terraform-provision-initialize-instance-hpcs)

* [What's next?](/docs/hs-crypto?topic=hs-crypto-uko-terraform-setup-for-hpcs#uko-terraform-setup-hpcs-next)


## Setting up BYOHSM
{: #sitemap_setting_up_byohsm}


[Setting up BYOHSM](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-hsm-for-byohsm)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-prerequisites)

* [Creating partitions](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-partition)

* [Creating keys](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-key)

* [Network connectivity best practice](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-network-connection)

* [Preparing information for HSM connection](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-prepare-info)

* [What's next](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-hsm-next)


## Managing keys, keystores, and KMIP adapters - Standard Plan
{: #sitemap_managing_keys_keystores_and_kmip_adapters_standard_plan}



### Managing instance policies - Standard Plan
{: #sitemap_managing_instance_policies_standard_plan}


[Managing the network access policy](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies#managing-network-access-policies)

* [Updating the network access policy for your {{site.data.keyword.hscrypto}} instance with the UI](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies&interface=ui#update-network-access-policy-ui)

* [Updating the network access policy for your {{site.data.keyword.hscrypto}} instance with the key management service API](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies&interface=api#update-network-access-policy-api)

* [Updating the network access policy for your {{site.data.keyword.hscrypto}} instance with the CLI](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies&interface=cli#update-network-access-policy-cli)

* [Disabling the network access policy for your {{site.data.keyword.hscrypto}} instance with the key management service API](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies&interface=api#disable-network-access-policy-api)

[Managing dual authorization of your service instance](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth#manage-dual-auth)

* [Understanding dual authorization of your service instance](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth#understand-daul-auth-policy)

* [Enabling dual authorization for your service instance with the UI](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth&interface=ui#enable-dual-auth-instance-policy-ui)

* [Enabling dual authorization for your service instance with the API](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth&interface=api#enable-dual-auth-instance-policy-api)

* [Disabling dual authorization for your service instance with the UI](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth&interface=ui#disable-dual-auth-instance-policy-ui)

* [Disabling dual authorization for your service instance with the key management service API](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth&interface=api#disable-dual-auth-instance-policy-api)

[Managing the key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess#manage-keyCreateImportAccess)

* [Understanding the key create and import access settings](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess#understand-keyCreateImportAccess-instance-policy)

* [Enabling or updating the key create and import access policy for your service instance with the UI](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess&interface=ui#enable-keyCreateImportAccess-policy-console)

* [Enabling and updating the key create and import access policy for your service instance with the API](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess&interface=api#enable-keyCreateImportAccess-policy-api)

* [Disabling the key create and import access policy for your service instance with the key management service API](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess&interface=api#disable-key-create-import-policy-api)


### Managing key management service keys - Standard Plan
{: #sitemap_managing_key_management_service_keys_standard_plan}


[Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys#create-root-keys)

* [Creating root keys with the UI](/docs/hs-crypto?topic=hs-crypto-create-root-keys&interface=ui#root-key-gui)

* [Creating root keys with the API](/docs/hs-crypto?topic=hs-crypto-create-root-keys&interface=api#root-key-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-create-root-keys&interface=api#root-key-next)

[Creating standard keys](/docs/hs-crypto?topic=hs-crypto-create-standard-keys#create-standard-keys)

* [Creating standard keys with the UI](/docs/hs-crypto?topic=hs-crypto-create-standard-keys&interface=ui#standard-key-gui)

* [Creating standard keys with the API](/docs/hs-crypto?topic=hs-crypto-create-standard-keys&interface=api#create-standard-key-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-create-standard-keys&interface=api#standard-key-next)

[Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings#managing-key-rings)

* [Creating key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings#create-key-ring)

* [Transferring a key to a different key ring](/docs/hs-crypto?topic=hs-crypto-managing-key-rings#transfer-key-key-ring)

* [Granting access to a key ring](/docs/hs-crypto?topic=hs-crypto-managing-key-rings&interface=ui#grant-access-key-ring)

* [Listing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings&interface=ui#list-key-ring)

* [Deleting key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings&interface=ui#delete-key-ring)

[Managing key aliases](/docs/hs-crypto?topic=hs-crypto-manage-key-alias#manage-key-alias)

* [Creating key aliases](/docs/hs-crypto?topic=hs-crypto-manage-key-alias#create-key-alias)

* [Deleting key aliases](/docs/hs-crypto?topic=hs-crypto-manage-key-alias#delete-key-alias)

* [APIs that use key alias](/docs/hs-crypto?topic=hs-crypto-manage-key-alias&interface=api#key-alias-apis)

[Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys#import-root-keys)

* [Importing root keys with the UI](/docs/hs-crypto?topic=hs-crypto-import-root-keys&interface=ui#import-root-key-gui)

* [Importing root keys with the API](/docs/hs-crypto?topic=hs-crypto-import-root-keys&interface=api#import-root-key-api)

* [Importing root keys with the CLI](/docs/hs-crypto?topic=hs-crypto-import-root-keys&interface=cli#import-root-key-cli)

* [Base64 encoding your key material](/docs/hs-crypto?topic=hs-crypto-import-root-keys&interface=cli#encode-key-material-root-key)

* [What's next](/docs/hs-crypto?topic=hs-crypto-import-root-keys&interface=cli#import-root-key-next)

[Importing standard keys](/docs/hs-crypto?topic=hs-crypto-import-standard-keys#import-standard-keys)

* [Importing standard keys with the UI](/docs/hs-crypto?topic=hs-crypto-import-standard-keys&interface=ui#import-standard-key-gui)

* [Importing standard keys with the API](/docs/hs-crypto?topic=hs-crypto-import-standard-keys&interface=api#import-standard-key-api)

* [Importing standard keys with the CLI](/docs/hs-crypto?topic=hs-crypto-import-standard-keys&interface=cli#import-standard-key-cli)

* [Base64 encoding your key material](/docs/hs-crypto?topic=hs-crypto-import-standard-keys&interface=cli#encode-key-material-standard-key)

* [What's next](/docs/hs-crypto?topic=hs-crypto-import-standard-keys&interface=cli#import-standard-key-next)

[Creating import tokens](/docs/hs-crypto?topic=hs-crypto-create-import-tokens#create-import-tokens)

* [Creating an import token with the API](/docs/hs-crypto?topic=hs-crypto-create-import-tokens&interface=api#create-import-token-api)

* [Creating an import token with the CLI](/docs/hs-crypto?topic=hs-crypto-create-import-tokens&interface=cli#create-import-token-cli)

* [Retrieving an import token with the API](/docs/hs-crypto?topic=hs-crypto-create-import-tokens&interface=api#retrieve-import-token-api)

* [Retrieving an import token with the CLI](/docs/hs-crypto?topic=hs-crypto-create-import-tokens&interface=cli#retrieve-import-token-cli)

* [What's next](/docs/hs-crypto?topic=hs-crypto-create-import-tokens&interface=cli#create-import-token-next-steps)

[Viewing a list of root keys or standard keys](/docs/hs-crypto?topic=hs-crypto-view-keys#view-keys)

* [Viewing root keys or standard keys with the UI](/docs/hs-crypto?topic=hs-crypto-view-keys&interface=ui#view-key-gui)

* [Viewing root keys or standard keys with the key management service API](/docs/hs-crypto?topic=hs-crypto-view-keys&interface=api#view-key-api)

[Viewing details about a root key or a standard key](/docs/hs-crypto?topic=hs-crypto-view-key-details#view-key-details)

* [Viewing key details with the UI](/docs/hs-crypto?topic=hs-crypto-view-key-details&interface=ui#view-key-details-ui)

* [Viewing key details with the key management service API](/docs/hs-crypto?topic=hs-crypto-view-key-details&interface=api#view-key-details-api)

[Retrieving a root key or a standard key](/docs/hs-crypto?topic=hs-crypto-retrieve-key#retrieve-key)

* [Retrieving a key with the key management service API](/docs/hs-crypto?topic=hs-crypto-retrieve-key#get-key-api)

[Wrapping data encryption keys with root keys](/docs/hs-crypto?topic=hs-crypto-wrap-keys#wrap-keys)

* [Wrapping keys by using the API](/docs/hs-crypto?topic=hs-crypto-wrap-keys#wrap-keys-api)

[Unwrapping data encryption keys with root keys](/docs/hs-crypto?topic=hs-crypto-unwrap-keys#unwrap-keys)

* [Unwrapping keys by using the API](/docs/hs-crypto?topic=hs-crypto-unwrap-keys#unwrap-key-api)

* [Decoding your key material](/docs/hs-crypto?topic=hs-crypto-unwrap-keys#how-to-decode-key-material)

[Rewrapping data encryption keys with root keys](/docs/hs-crypto?topic=hs-crypto-rewrap-keys#rewrap-keys)

* [Rewrapping keys by using the API](/docs/hs-crypto?topic=hs-crypto-rewrap-keys#rewrap-key-api)

[Rotating root keys based on the rotation policy](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy#set-rotation-policy)

* [Managing rotation policies in the UI](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy&interface=ui#manage-policies-gui)

* [Managing rotation policies with the API](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy&interface=api#manage-rotation-policies-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy&interface=api#set-rotation-policy-next)

[Rotating root keys manually](/docs/hs-crypto?topic=hs-crypto-rotate-keys#rotate-keys)

* [Rotating root keys in the UI](/docs/hs-crypto?topic=hs-crypto-rotate-keys&interface=ui#rotate-root-key-gui)

* [Rotating root keys with the API](/docs/hs-crypto?topic=hs-crypto-rotate-keys&interface=api#rotate-root-key-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-rotate-keys&interface=api#rotate-key-next)

[Viewing root key versions](/docs/hs-crypto?topic=hs-crypto-view-key-versions#view-key-versions)

* [Viewing root key versions with the key management service API](/docs/hs-crypto?topic=hs-crypto-view-key-versions#view-key-versions-api)

[Disabling root keys](/docs/hs-crypto?topic=hs-crypto-disable-keys#disable-keys)

* [Disabling and enabling root keys with the UI](/docs/hs-crypto?topic=hs-crypto-disable-keys&interface=ui#disable-enable-ui)

* [Disabling and enabling root keys with the API](/docs/hs-crypto?topic=hs-crypto-disable-keys&interface=api#disable-enable-api)

[About deleting and purging keys](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys#delete-purge-keys)

* [Considerations before you delete and purge a key](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys#delete-purge-keys-considerations)

* [What's next](/docs/hs-crypto?topic=hs-crypto-delete-purge-keys#delete-purge-keys-next)

[Deleting keys by using a single authorization](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-keys)

* [Deleting keys with the UI](/docs/hs-crypto?topic=hs-crypto-delete-keys&interface=ui#delete-keys-gui)

* [Deleting keys with the API](/docs/hs-crypto?topic=hs-crypto-delete-keys&interface=api#delete-keys-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-delete-keys&interface=api#delete-key-next)

[Deleting keys by using dual authorization](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys#delete-dual-auth-keys)

* [Considerations for deleting a key using dual authorization](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys#dual-auth-deletion-considerations)

* [Authorize deletion for a key with the UI](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys&interface=ui#set-key-deletion-console)

* [Authorize deletion for a key with the API](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys&interface=api#set-key-deletion-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys&interface=api#delete-daul-auth-keys-next)

[Setting dual authorization policies for keys](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy#set-dual-auth-key-policy)

* [Managing dual authorization policies with the key management service API](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy#manage-dual-auth-key-policies-api)

[Purging keys manually](/docs/hs-crypto?topic=hs-crypto-purge-keys#purge-keys)

* [Purging keys in the UI](/docs/hs-crypto?topic=hs-crypto-purge-keys&interface=ui#purge-keys-gui)

* [Purging keys with the API](/docs/hs-crypto?topic=hs-crypto-purge-keys&interface=api#purge-keys-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-purge-keys&interface=api#purge-keys-next)

[Restoring keys](/docs/hs-crypto?topic=hs-crypto-restore-keys#restore-keys)

* [How do I know whether a key can be restored?](/docs/hs-crypto?topic=hs-crypto-restore-keys#restore-keys-eligibility)

* [Restoring a deleted key with the UI](/docs/hs-crypto?topic=hs-crypto-restore-keys&interface=ui#restore-keys-ui)

* [Restoring a deleted key with the API](/docs/hs-crypto?topic=hs-crypto-restore-keys&interface=api#restore-keys-api)

[Viewing associations between root keys and encrypted {{site.data.keyword.cloud_notm}} resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources)

* [Viewing protected resources with the UI](/docs/hs-crypto?topic=hs-crypto-view-protected-resources&interface=ui#view-protected-resources-gui)

* [Viewing protected resources with the API](/docs/hs-crypto?topic=hs-crypto-view-protected-resources&interface=api#view-protected-resources-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-view-protected-resources&interface=api#view-protected-resources-next-steps)

[Synchronizing associated resources](/docs/hs-crypto?topic=hs-crypto-sync-associated-resources#sync-associated-resources)

* [Syncing associated resources with the UI](/docs/hs-crypto?topic=hs-crypto-sync-associated-resources&interface=ui#sync-associated-resources-ui)

* [Syncing associated resources with the API](/docs/hs-crypto?topic=hs-crypto-sync-associated-resources&interface=api#sync-associated-resources-api)


### Managing EP11 keys, keystores, and certificates  - Standard Plan
{: #sitemap_managing_ep11_keys_keystores_and_certificates_standard_plan}


[Managing EP11 keystores with the UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui#manage-ep11-keystores-ui)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui#manage-ep11-keystores-ui-before)

* [Viewing EP11 keystores](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui#view-ep11-keystore-ui)

* [Creating EP11 keystores](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui#create-ep11-keystore-ui)

* [Deleting EP11 keystores](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui#delete-ep11-keystore-ui)

* [What's next](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui#manage-ep11-keystore-ui-next)

[Managing EP11 keys with the UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui#manage-ep11-key-ui)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui#manage-ep11-key-ui-before)

* [Viewing EP11 keys](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui#view-ep11-key-ui)

* [Creating EP11 keys](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui#create-ep11-key-ui)

* [Deleting EP11 keys](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui#delete-ep11-key-ui)

* [What's next](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui#manage-ep11-key-ui-next)

[Managing EP11 certificates with the UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-certificate-ui#manage-ep11-certificate-ui)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-manage-ep11-certificate-ui#manage-ep11-certificate-ui-before)

* [Viewing EP11 certificates](/docs/hs-crypto?topic=hs-crypto-manage-ep11-certificate-ui#view-ep11-certificate-ui)

* [Downloading EP11 certificates](/docs/hs-crypto?topic=hs-crypto-manage-ep11-certificate-ui#download-ep11-certificate-ui)

* [Deleting EP11 certificates](/docs/hs-crypto?topic=hs-crypto-manage-ep11-certificate-ui#delete-ep11-certificate-ui)

* [What's next](/docs/hs-crypto?topic=hs-crypto-manage-ep11-certificate-ui#manage-ep11-certificate-ui-next)


## Managing keys and keystores - Unified Key Orchestrator Plan
{: #sitemap_managing_keys_and_keystores_unified_key_orchestrator_plan}



### Managing vaults - Unified Key Orchestrator Plan
{: #sitemap_managing_vaults_unified_key_orchestrator_plan}


[Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults#create-vaults)

* [Creating vaults with the UI](/docs/hs-crypto?topic=hs-crypto-create-vaults&interface=ui#create-vaults-ui)

* [Creating vaults through the API](/docs/hs-crypto?topic=hs-crypto-create-vaults&interface=api#create-vaults-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-create-vaults&interface=api#create-vaults-next)

[Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults#edit-vaults)

* [Editing vault details with the UI](/docs/hs-crypto?topic=hs-crypto-edit-vaults&interface=ui#edit-vaults-ui)

* [Editing vault details with the API](/docs/hs-crypto?topic=hs-crypto-edit-vaults&interface=api#edit-vaults-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-edit-vaults&interface=api#edit-vaults-next)

[Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults#delete-vaults)

* [Deleting vaults with the UI](/docs/hs-crypto?topic=hs-crypto-delete-vaults&interface=ui#delete-vaults-ui)

* [Deleting vaults with the API](/docs/hs-crypto?topic=hs-crypto-delete-vaults&interface=api#delete-vaults-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-delete-vaults&interface=api#delete-vaults-next)


### Managing key templates - Unified Key Orchestrator Plan
{: #sitemap_managing_key_templates_unified_key_orchestrator_plan}


[Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template#create-template)

* [Creating key templates from scratch with the UI](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#create-template-ui)

* [Creating key templates from scratch through the API](/docs/hs-crypto?topic=hs-crypto-create-template&interface=api#create-template-api)

* [Creating a copy of an existing key template with the UI](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#copy-template-ui)

* [Creating key templates from an existing key template through the API](/docs/hs-crypto?topic=hs-crypto-create-template&interface=api#copy-template-api)

* [Defining key naming schemes](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#define-naming-scheme)

* [What's next](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#create-template-next)

[Viewing a list of key templates](/docs/hs-crypto?topic=hs-crypto-view-key-template#view-key-template)

* [Viewing a list of key templates with the UI](/docs/hs-crypto?topic=hs-crypto-view-key-template&interface=ui#view-key-template-ui)

* [Viewing a list of key templates with the API](/docs/hs-crypto?topic=hs-crypto-view-key-template&interface=api#view-key-template-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-view-key-template&interface=api#view-key-template-next)

[Editing key template details](/docs/hs-crypto?topic=hs-crypto-edit-template#edit-template)

* [Editing key templates with the UI](/docs/hs-crypto?topic=hs-crypto-edit-template&interface=ui#edit-key-template-ui)

* [Editing key templates with the API](/docs/hs-crypto?topic=hs-crypto-edit-template&interface=api#edit-key-template-api)

* [Editing keystores for key templates with the API](/docs/hs-crypto?topic=hs-crypto-edit-template&interface=api#assign-keystores-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-edit-template&interface=api#edit-key-template-next)

[Archiving and unarchiving key templates](/docs/hs-crypto?topic=hs-crypto-archive-template#archive-template)

* [Archiving key templates with the UI](/docs/hs-crypto?topic=hs-crypto-archive-template&interface=ui#archive-key-template-ui)

* [Archiving key templates with the API](/docs/hs-crypto?topic=hs-crypto-archive-template&interface=api#archive-key-template-api)

* [Unarchiving key templates with the UI](/docs/hs-crypto?topic=hs-crypto-archive-template&interface=ui#unarchive-key-template-ui)

* [Unarchiving key templates with the API](/docs/hs-crypto?topic=hs-crypto-archive-template&interface=api#unarchive-key-template-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-archive-template&interface=api#archive-key-template-next)

[Deleting key templates](/docs/hs-crypto?topic=hs-crypto-delete-template#delete-template)

* [Deleting key templates with the UI](/docs/hs-crypto?topic=hs-crypto-delete-template&interface=ui#delete-key-template-ui)

* [Deleting key templates with the API](/docs/hs-crypto?topic=hs-crypto-delete-template&interface=api#delete-key-template-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-delete-template&interface=api#delete-key-template-next)


### Managing keys - Unified Key Orchestrator Plan
{: #sitemap_managing_keys_unified_key_orchestrator_plan}


[Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys#create-managed-keys)

* [Creating managed keys with a key template in the UI](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=ui#create-managed-keys-template-ui)

* [Creating managed keys with a key template through the API](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=api#create-managed-keys-template-api)

* [Creating managed keys with custom properties in the UI](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=ui#create-managed-keys-ui)

* [Creating managed keys with custom properties through the API](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=api#create-managed-keys-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=api#create-managed-keys-next)

[Viewing a list of managed keys](/docs/hs-crypto?topic=hs-crypto-view-key-list#view-key-list)

* [Viewing a list of managed keys with the UI](/docs/hs-crypto?topic=hs-crypto-view-key-list&interface=ui#view-key-list-ui)

* [Viewing a list of keys with the API](/docs/hs-crypto?topic=hs-crypto-view-key-list&interface=api#view-key-list-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-view-key-list&interface=api#view-key-list-next)

[Filtering and searching managed keys](/docs/hs-crypto?topic=hs-crypto-search-key-list#search-key-list)

* [Filtering managed keys with the UI](/docs/hs-crypto?topic=hs-crypto-search-key-list&interface=ui#filter-key-list-ui)

* [ Searching for keys with the UI](/docs/hs-crypto?topic=hs-crypto-search-key-list&interface=ui#search-key-list-ui)

* [Searching keys with the API](/docs/hs-crypto?topic=hs-crypto-search-key-list&interface=api#search-key-list-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-search-key-list&interface=api#search-key-list-next)

[Editing managed key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys#edit-kms-keys)

* [Editing managed key details with the  UI](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys&interface=ui#edit-kms-keys-ui)

* [Editing key details with the API](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys&interface=api#edit-kms-keys-api)

* [Editing keystores for keys with the API](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys&interface=api#assign-key-keystores-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys&interface=api#edit-kms-keys-next)

[Rotating managed keys manually](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys#uko-rotate-keys)

* [Rotating managed keys with the UI](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys&interface=ui#uko-rotate-managed-key-gui)

* [Rotating managed keys with the API](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys&interface=api#uko-rotate-managed-key-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys&interface=api#uko-rotate-keys-next)

[Syncing keys in keystores with managed keys manually](/docs/hs-crypto?topic=hs-crypto-uko-sync-keys#uko-sync-keys)

* [Syncing keys with the UI](/docs/hs-crypto?topic=hs-crypto-uko-sync-keys&interface=ui#uko-sync-managed-key-gui)

* [Syncing with the API](/docs/hs-crypto?topic=hs-crypto-uko-sync-keys&interface=api#uko-sync-managed-key-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-sync-keys&interface=api#uko-sync-keys-next)

[Realigning managed keys with key templates](/docs/hs-crypto?topic=hs-crypto-align-key#align-key)

* [Realigning managed keys with key templates through the UI](/docs/hs-crypto?topic=hs-crypto-align-key&interface=ui#align-key-ui)

* [Realigning keys with key templates through the API](/docs/hs-crypto?topic=hs-crypto-align-key&interface=api#align-key-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-align-key&interface=api#align-key-next)

[Viewing managed key versions](/docs/hs-crypto?topic=hs-crypto-uko-view-key-versions#uko-view-key-versions)

* [Viewing manage key versions with the UI](/docs/hs-crypto?topic=hs-crypto-uko-view-key-versions&interface=ui#uko-view-key-versions-gui)

* [Viewing managed key versions with the API](/docs/hs-crypto?topic=hs-crypto-uko-view-key-versions&interface=api#uko-view-key-versions-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-view-key-versions&interface=api#uko-view-key-versions-next)

[Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys#delete-managed-keys)

* [Deleting managed keys with the UI](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys&interface=ui#delete-managed-keys-ui)

* [Deleting managed keys with the API](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys&interface=api#delete-managed-keys-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys&interface=api#delete-managed-keys-next)


### Managing keystores - Unified Key Orchestrator Plan
{: #sitemap_managing_keystores_unified_key_orchestrator_plan}


[Creating internal KMS keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores#create-internal-keystores)

* [Creating internal KMS keystores with the UI](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores&interface=ui#create-internal-keystores-ui)

* [Creating internal KMS keystores with the API](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores&interface=api#create-internal-keystores-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores&interface=api#create-internal-keystores-next)

[Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores#connect-external-keystores)

* [Setting up required user access in external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores#connect-external-keystores-access)

* [Connecting to external keystores with the UI](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores&interface=ui#connect-external-keystores-ui)

* [Connecting to external keystores with the API](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores&interface=api#connect-external-keystores-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores&interface=api#connect-external-keystores-next)

[Editing internal keystores](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores#edit-internal-keystores)

* [Editing internal keystores with the UI](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores&interface=ui#edit-internal-keystores-ui)

* [Editing internal keystores with the API](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores&interface=api#edit-internal-keystores-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores&interface=api#edit-internal-keystores-next)

[Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection#edit-external-keystore-connection)

* [Editing connection to external keystores with the UI](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection&interface=ui#edit-external-keystore-connection-ui)

* [Editing connection to external keystores with the API](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection&interface=api#edit-external-keystore-connection-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection&interface=api#edit-external-keystore-connection-next)

[Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores#delete-internal-keystores)

* [Deleting internal keystores with the UI](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores&interface=ui#delete-internal-keystores-ui)

* [Deleting internal keystores with the API](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores&interface=api#delete-internal-keystores-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores&interface=api#delete-internal-keystores-next)

[Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores#disconnect-external-keystores)

* [Disconnecting from external keystores with the UI](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores&interface=ui#disconnect-external-keystores-ui)

* [Disconnecting from external keystores with the API](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores&interface=api#disconnect-external-keystores-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores&interface=api#disconnect-external-keystores-next)

[Connecting to Azure Key Vault through private endpoint](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint#connect-azure-key-vault-private-endpoint)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint&interface=ui#prerequisite)

* [Step 1: Create a private endpoint in Azure portal](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint&interface=ui#step1-create-private-endpoint-ui)

* [Step 2: Create and manage connector endpoint](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint&interface=ui#step2-create-manage-endpoint-ui)

* [Step 3: Connect Azure Key Vault to the UI](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint&interface=ui#step3-connect-azure-key-vault-ui)

* [Connecting to Azure Key Vault with API](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint&interface=api#connect-azure-key-vault-api)

* [What's next](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint&interface=api#connect-azure-key-vault-private-endpoint-next)


## Managing master keys
{: #sitemap_managing_master_keys}


[Rotating master keys by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards#rotate-master-key-smart-cards)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards#rotate-master-key-smart-cards-prerequisites)

* [Rotating master keys using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards#rotate-master-key-smart-cards-steps)

* [What's next](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards#rotate-master-key-smart-cards-next)

[Rotating master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit#rotate-master-key-cli-recovery-crypto-unit)

* [Rotating master keys](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit#rotate-master-key-cli-recovery-crypto-unit-steps)

* [What's next](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit#rotate-master-key-cli-recovery-crypto-unit-next)

[Rotating master keys by using key part files](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part#rotate-master-key-cli-key-part)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part#rotate-master-key-cli-key-part-prerequisites)

* [Rotating master keys by using key part files](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part#rotate-master-key-cli-key-part-steps)

* [What's next](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part#rotate-master-key-cli-key-part-next)

[Recovering a master key from a recovery crypto unit](/docs/hs-crypto?topic=hs-crypto-recover-master-key-recovery-crypto-unit#recover-master-key-recovery-crypto-unit)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-recover-master-key-recovery-crypto-unit#recover-master-key-prerequisites)

* [Recovering master keys](/docs/hs-crypto?topic=hs-crypto-recover-master-key-recovery-crypto-unit#recover-master-key-step)

* [What's next](/docs/hs-crypto?topic=hs-crypto-recover-master-key-recovery-crypto-unit#recover-master-key-next)


## Enabling crypto mechanisms
{: #sitemap_enabling_crypto_mechanisms}


[Enabling crypto mechanisms](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-mechanisms)

* [Enabling BIP32 deterministic wallets](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-BIP32)

* [Enabling Edwards-curve Digital Signature Algorithm](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-EdDSA)

* [Enabling the Schnorr algorithm](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-schnorr)

* [What's next](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#next-enable-mechanisms)


## Adding or removing crypto units
{: #sitemap_adding_or_removing_crypto_units}


[Adding or removing crypto units](/docs/hs-crypto?topic=hs-crypto-add-remove-crypto-units#add-remove-crypto-units)

* [Adding crypto units to an existing service instance](/docs/hs-crypto?topic=hs-crypto-add-remove-crypto-units#add-crypto-units)

* [Removing crypto units from an existing service instance](/docs/hs-crypto?topic=hs-crypto-add-remove-crypto-units#remove-crypto-units)

* [What's next](/docs/hs-crypto?topic=hs-crypto-add-remove-crypto-units#add-remove-crypto-units-next)


## Enabling or adding failover crypto units after you provision a service instance
{: #sitemap_enabling_or_adding_failover_crypto_units_after_you_provision_a_service_instance}


[Enabling or adding failover crypto units after you provision a service instance](/docs/hs-crypto?topic=hs-crypto-enable-add-failover#enable-add-failover)

* [Step 1: Add failover crypto units](/docs/hs-crypto?topic=hs-crypto-enable-add-failover#add-failover-cu)

* [Step 2: Raise a support ticket](/docs/hs-crypto?topic=hs-crypto-enable-add-failover#raise-support-ticket)

* [What's next](/docs/hs-crypto?topic=hs-crypto-enable-add-failover#enable-add-failover-next)


## Deleting service instances
{: #sitemap_deleting_service_instances}


[Deleting service instances](/docs/hs-crypto?topic=hs-crypto-delete-instance#delete-instance)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-delete-instance#delete-instance-prerequisite)

* [Step 1: Delete keys](/docs/hs-crypto?topic=hs-crypto-delete-instance#delete-all-key-step)

* [Step 2: Select the crypto units to be deleted](/docs/hs-crypto?topic=hs-crypto-delete-instance#select-crypto-unit-step)

* [Step 3: Zeroize crypto units](/docs/hs-crypto?topic=hs-crypto-delete-instance#zeroize-crypto-unit-step)

* [Step 4: Optional - Uninstall the {{site.data.keyword.hscrypto}} utilities](/docs/hs-crypto?topic=hs-crypto-delete-instance#uninstall-utilities-step)

* [Step 5: Delete your service instance](/docs/hs-crypto?topic=hs-crypto-delete-instance#delete-instance-step)


## Restoring your data from another region
{: #sitemap_restoring_your_data_from_another_region}


[Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data#restore-data)

* [Restoring your data by using failover crypto units](/docs/hs-crypto?topic=hs-crypto-restore-data#restore-data-failover-crypto-units)

* [Restoring your data by opening an IBM support ticket](/docs/hs-crypto?topic=hs-crypto-restore-data#restore-data-open-support-ticket)

* [What's next](/docs/hs-crypto?topic=hs-crypto-restore-data#restore-data-next)


## Enhancing security - Standard Plan
{: #sitemap_enhancing_security_standard_plan}


[Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access#manage-access)

* [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access#roles)

* [Managing access to multiple instances](/docs/hs-crypto?topic=hs-crypto-manage-access#manage-multiple-instances)

* [What's next](/docs/hs-crypto?topic=hs-crypto-manage-access#manage-access-next)

[Granting access to keys](/docs/hs-crypto?topic=hs-crypto-grant-access-keys#grant-access-keys)

* [Granting access to all keys in an instance](/docs/hs-crypto?topic=hs-crypto-grant-access-keys#grant-access-instance-level)

* [Granting access to a single key in an instance](/docs/hs-crypto?topic=hs-crypto-grant-access-keys#grant-access-key-level)

* [Granting access to key rings in an instance](/docs/hs-crypto?topic=hs-crypto-grant-access-keys#grant-access-key-ring-level)


### Granting users access to manage EP11 keystores and keys
{: #sitemap_granting_users_access_to_manage_ep11_keystores_and_keys}


[Granting users access to manage EP11 keystores and keys through UI](/docs/hs-crypto?topic=hs-crypto-grant-pkcs11-ui-access#grant-pkcs11-ui-access)

* [(Optional) Step 1: Create custom IAM roles](/docs/hs-crypto?topic=hs-crypto-grant-pkcs11-ui-access#step1-create-custom-roles-pkcs11-ui)

* [Step 2: Assign IAM roles to users](/docs/hs-crypto?topic=hs-crypto-grant-pkcs11-ui-access#step2-assign-iam-roles-pkcs-ui)

* [ What's next](/docs/hs-crypto?topic=hs-crypto-grant-pkcs11-ui-access#pkcs11-ui-best-practices-next)

[Setting up PKCS #11 API user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access#best-practice-pkcs11-access)

* [ PKCS #11 user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access#pkcs11-user-types)

* [Step 1: Create custom IAM roles](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access#step1-create-custom-roles)

* [ Step 2: Create service IDs and API keys for the SO user, normal user, and anonymous user](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access#step2-create-service-id-api-key)

* [Step 3: Assign IAM roles to the service IDs](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access#step3-assign-iam-roles)

* [ What's next](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access#pkcs11-best-practices-next)


### Privately connecting to Hyper Protect Crypto Services
{: #sitemap_privately_connecting_to_hyper_protect_crypto_services}


[Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc#virtual-private-endpoints-for-vpc)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc#virtual-private-endpoints-for-vpc-prereqs)

* [Setting up a VPE for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc#virtual-private-endpoints-for-vpc-setup)

* [Using your VPE for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc#use-vpe-for-hpcs)

[Using service endpoints to privately connect to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-secure-connection#secure-connection)

* [Understanding the network access policy](/docs/hs-crypto?topic=hs-crypto-secure-connection#understand-network-access-policies)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-secure-connection#private-endpoint-prereqs)

* [Step 1: Configure the private network of {{site.data.keyword.cloud_notm}} on your virtual server](/docs/hs-crypto?topic=hs-crypto-secure-connection#configure-network)

* [Step 2: Provision a service instance and select the network access](/docs/hs-crypto?topic=hs-crypto-secure-connection#service-endpoint-private-endpoints)

* [Step 3:  Target the {{site.data.keyword.hscrypto}} private endpoint for the TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-secure-connection#target-tke-private-endpoint)

* [Step 4: Initialize the service instance](/docs/hs-crypto?topic=hs-crypto-secure-connection#secure-connection-key-ceremony)

* [Step 5: Target the {{site.data.keyword.hscrypto}} private endpoint for key management service](/docs/hs-crypto?topic=hs-crypto-secure-connection#target-internal-endpoint)

* [Step 6: Test your private network connection](/docs/hs-crypto?topic=hs-crypto-secure-connection#Test-private-connection)

* [What's next](/docs/hs-crypto?topic=hs-crypto-secure-connection#secure-connection-next)

[Auditing events for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-at-events#at-events)

* [Historical information regarding events](/docs/hs-crypto?topic=hs-crypto-at-events#historical-mapping-events)

* [Supported events](/docs/hs-crypto?topic=hs-crypto-at-events#at-supported-events)

* [Viewing events](/docs/hs-crypto?topic=hs-crypto-at-events#at-ui)

* [Analyzing successful events](/docs/hs-crypto?topic=hs-crypto-at-events#at-events-analyze)

* [Analyzing failed events](/docs/hs-crypto?topic=hs-crypto-at-events#at-events-analyze-failed)

* [Event severity](/docs/hs-crypto?topic=hs-crypto-at-events#event-severity)

[Managing security and compliance with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-manage-security-compliance#manage-security-compliance)

* [Governing {{site.data.keyword.hscrypto}} resource configuration with config rules](/docs/hs-crypto?topic=hs-crypto-manage-security-compliance#govern-crypto)


## Enhancing security - Unified Key Orchestrator Plan
{: #sitemap_enhancing_security_unified_key_orchestrator_plan}


[Managing user access](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-manage-access)

* [Roles and permissions](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-roles)

* [Assigning access to {{site.data.keyword.hscrypto}} in the UI](/docs/hs-crypto?topic=hs-crypto-uko-manage-access&interface=ui#assign-access-console)

* [Assigning access to {{site.data.keyword.hscrypto}} in the CLI](/docs/hs-crypto?topic=hs-crypto-uko-manage-access&interface=cli#assign-access-cli)

* [Assigning access to {{site.data.keyword.hscrypto}} by using the API](/docs/hs-crypto?topic=hs-crypto-uko-manage-access&interface=api#assign-access-api)

* [Assigning access to {{site.data.keyword.hscrypto}} by using Terraform](/docs/hs-crypto?topic=hs-crypto-uko-manage-access&interface=terraform#assign-access-terraform)

* [Managing access to multiple instances](/docs/hs-crypto?topic=hs-crypto-uko-manage-access&interface=terraform#uko-manage-multiple-instances)

* [What's next](/docs/hs-crypto?topic=hs-crypto-uko-manage-access&interface=terraform#uko-manage-access-next)

[Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults#grant-access-vaults)

* [Step 1. Retrieve the vault ID](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults#access-vault-retrieve-ID)

* [Step 2. Grant access to vaults from the UI](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults#grant-access-vault-console)

* [What's next](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults#grant-access-vaults-next)

[Setting up custom roles for {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-role-best-practices#uko-role-best-practices)

* [Step 1: Create custom IAM roles](/docs/hs-crypto?topic=hs-crypto-uko-role-best-practices#step1-create-custom-roles-uko)

* [Step 2: Assign IAM roles to users](/docs/hs-crypto?topic=hs-crypto-uko-role-best-practices#step2-assign-iam-roles-uko)

* [ What's next](/docs/hs-crypto?topic=hs-crypto-uko-role-best-practices#uko-role-best-practices-next)

[Auditing events for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-at-events#uko-at-events)

* [Supported events](/docs/hs-crypto?topic=hs-crypto-uko-at-events#uko-at-supported-events)

* [Viewing events](/docs/hs-crypto?topic=hs-crypto-uko-at-events#uko-at-ui)

* [Analyzing successful events](/docs/hs-crypto?topic=hs-crypto-uko-at-events#uko-at-events-analyze)

* [Analyzing failed events](/docs/hs-crypto?topic=hs-crypto-uko-at-events#uko-at-events-analyze-failed)

* [Event severity](/docs/hs-crypto?topic=hs-crypto-uko-at-events#uko-event-severity)


## Logging and monitoring
{: #sitemap_logging_and_monitoring}


[Managing metrics](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics#manage-monitoring-metrics)

* [Managing metrics settings](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics#manage-metrics-policy)

* [What's next](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics#monitor-metrics-next-steps)

[{{site.data.keyword.mon_short}} operational metrics](/docs/hs-crypto?topic=hs-crypto-operational-metrics#operational-metrics)

* [What metrics are available for {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-operational-metrics#hpcs-metrics-available)

* [Before you begin](/docs/hs-crypto?topic=hs-crypto-operational-metrics#operational-metrics-considerations)

* [Connecting {{site.data.keyword.mon_short}} with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-operational-metrics#connect-monitoring-hpcs)

* [{{site.data.keyword.hscrypto}} Metrics Details](/docs/hs-crypto?topic=hs-crypto-operational-metrics#hpcs-metrics)

* [Latency](/docs/hs-crypto?topic=hs-crypto-operational-metrics#latency)

* [Attributes for Segmentation](/docs/hs-crypto?topic=hs-crypto-operational-metrics#attributes-for-segmentation)

* [Default Dashboards](/docs/hs-crypto?topic=hs-crypto-operational-metrics#default-dashboards)

* [Setting Alerts](/docs/hs-crypto?topic=hs-crypto-operational-metrics#set-monitor-alerts)


## API reference
{: #sitemap_api_reference}



### Key management service API
{: #sitemap_key_management_service_api}


[{{site.data.keyword.hscrypto}} key management service API change log](/docs/hs-crypto?topic=hs-crypto-kms-api-change-log#kms-api-change-log)

* [API versioning](/docs/hs-crypto?topic=hs-crypto-kms-api-change-log#kms-api-versioning)

* [February 2024](/docs/hs-crypto?topic=hs-crypto-kms-api-change-log#kms-api-feb-2024)

* [February 2023](/docs/hs-crypto?topic=hs-crypto-kms-api-change-log#kms-api-feb-2023)

* [January 2022](/docs/hs-crypto?topic=hs-crypto-kms-api-change-log#kms-api-jan-2022)

* [April 2021](/docs/hs-crypto?topic=hs-crypto-kms-api-change-log#kms-api-april-2021)


### Unified Key Orchestrator API
{: #sitemap_unified_key_orchestrator_api}


[{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API change log](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-change-log)

* [API versioning](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-versioning)

* [August 2023](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-aug-2023)

* [December 2022](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-december-2022)

* [October 2022](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-october-2022)

* [July 2022](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-july-2022)

* [June 2022](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-june-2022)

* [March 2022](/docs/hs-crypto?topic=hs-crypto-uko-api-change-log#uko-api-march-2022)

[Cryptographic operations: PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs11-api-ref)

* [Installing and configuring PKCS #11 library](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#setup-pkcs11-library)

* [Error handling](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs11-error-handling)

* [Verifying that keys are protected by crypto units](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs11-key-verify)

* [PKCS #11 function list](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs11_function_list)

* [Supported mechanisms](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs-mechanism-list)

* [Supported attributes and key types](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs-attribute-list)

* [Supported curves](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#supported-pkcs11-curve-name)

* [Standard PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs11-standard-api-ref)

[Cryptographic operations: GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-api-ref)

* [Accessing the API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#access-grep11-functions)

* [Error handling](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-error-handling)

* [GREP11 function list](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11_function_list)

* [Supported mechanisms](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-mechanism-list)

* [Supported attributes and key types](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-attribute-list)

* [Supported curves](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#supported-grep11-curve-name)

* [Performing cryptographic operations with GREP11 functions](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-functions)

* [Retrieving supported crypto algorithms](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-retrieve-mechanisms)

* [Generating and deriving keys](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-generate-keys)

* [Protecting keys](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-manage-keys)

* [Retrieving and modifying attributes for keys](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-attribute-value)

* [Generating random data](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-generate-random-data)

* [Encrypting and decrypting data](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-encrypt-decrypt-data)

* [Signing and verifying data](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-sign-verify-data)

* [Protecting data integrity through message digests](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-operation-digest-data)

* [Code examples](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#code-example)


## CLI reference
{: #sitemap_cli_reference}


[{{site.data.keyword.hscrypto}} CLI change log](/docs/hs-crypto?topic=hs-crypto-cli-change-log#cli-change-log)

* [{{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-cli-change-log#tke-cli-change-log)

* [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} certificate manager CLI plug-in](/docs/hs-crypto?topic=hs-crypto-cli-change-log#cert-manager-cli-change-log)

* [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} CLI plug-in](/docs/hs-crypto?topic=hs-crypto-cli-change-log#uko-cli-change-log)

[{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} CLI](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#hpcs-cli-plugin)

* [{{site.data.keyword.hscrypto}} key management CLI plug-in](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#kp-cli-plugin)

* [{{site.data.keyword.hscrypto}} Trusted Key Entry CLI plug-in](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#tke-cli-plugin)

* [{{site.data.keyword.hscrypto}} certificate manager CLI plug-in](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#cert-manager-cli-plugin)

* [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} CLI plug-in](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#uko-cli-plugin)


## Terraform reference
{: #sitemap_terraform_reference}


[Provisioning and initializing service instances with Terraform](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs){: external}

[Managing keys with Terraform - Key management service](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/kms_key){: external}

[Managing keys with Terraform - Unified Key Orchestrator](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs_managed_key){: external}


## Regions and locations
{: #sitemap_regions_and_locations}


[Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#regions)

* [Available regions](/docs/hs-crypto?topic=hs-crypto-regions#available-regions)

* [Connectivity options](/docs/hs-crypto?topic=hs-crypto-regions#connectivity-options)

* [Service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints)


## {{site.data.keyword.hscrypto}} cloud TKE procedures
{: #sitemap__cloud_tke_procedures}


[{{site.data.keyword.hscrypto}} cloud TKE procedures](/docs/hs-crypto?topic=hs-crypto-tke-procedures#tke-procedures)


## Security considerations for initializing a service instance
{: #sitemap_security_considerations_for_initializing_a_service_instance}


[Security considerations for initializing a service instance](/docs/hs-crypto?topic=hs-crypto-initialization-security-policy#initialization-security-policy)

* [Considerations for storing signature keys and master key parts](/docs/hs-crypto?topic=hs-crypto-initialization-security-policy#consideration-key-parts)

* [Considerations for defining the Management Utilities security policy](/docs/hs-crypto?topic=hs-crypto-initialization-security-policy#smart-card-security-plan)

* [Considerations for defining the file security policy](/docs/hs-crypto?topic=hs-crypto-initialization-security-policy#file-security-plan)


## Understanding your responsibilities when using {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #sitemap_understanding_your_responsibilities_when_using_}


[Understanding your responsibilities when using {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-shared-responsibilities#shared-responsibilities)

* [Incident and operations management](/docs/hs-crypto?topic=hs-crypto-shared-responsibilities#incident-and-ops)

* [Change management](/docs/hs-crypto?topic=hs-crypto-shared-responsibilities#change-management)

* [Identity and access management](/docs/hs-crypto?topic=hs-crypto-shared-responsibilities#iam-responsibilities)

* [Security and regulation compliance](/docs/hs-crypto?topic=hs-crypto-shared-responsibilities#security-compliance)

* [Disaster recovery](/docs/hs-crypto?topic=hs-crypto-shared-responsibilities#disaster-recovery)


## High availability and disaster recovery
{: #sitemap_high_availability_and_disaster_recovery}


[High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr#ha-dr)

* [Locations, tenancy, and availability](/docs/hs-crypto?topic=hs-crypto-ha-dr#availability)

* [In-region data redundancy and failover](/docs/hs-crypto?topic=hs-crypto-ha-dr#data-failover)

* [Cross-region disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr#cross-region-disaster-recovery)


## Open-source licenses
{: #sitemap_open-source_licenses}


[Open-source licenses](/docs/hs-crypto?topic=hs-crypto-open-source-licenses#open-source-licenses)

* [{{site.data.keyword.hscrypto}} notices and information](/docs/hs-crypto?topic=hs-crypto-open-source-licenses#notice)

* [Hosting appliance notices and information](/docs/hs-crypto?topic=hs-crypto-open-source-licenses#hosting-appliance-notice)


## Resource links
{: #sitemap_resource_links}


[Resource links](/docs/hs-crypto?topic=hs-crypto-resources#resources)

* [Videos](/docs/hs-crypto?topic=hs-crypto-resources#videos)

* [blogs](/docs/hs-crypto?topic=hs-crypto-resources#blogs)


## FAQs
{: #sitemap_faqs}


[General FAQs](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-basics)

* [What's {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-what-is-hpcs)

* [What is {{site.data.keyword.uko_full_notm}}?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-what-is-uko)

* [What is a key management service?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-what-key-management)

* [What is Hardware Security Module?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-what-is-hsm)

* [What is a cloud HSM?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-what-is-cloud-hsm)

* [How does {{site.data.keyword.hscrypto}} provide a single-tenant cloud service?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-single-tenant)

* [What are the responsibilities of users and {{site.data.keyword.cloud_notm}} for {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-responsibilities-users-cloud)

* [How is this service different from {{site.data.keyword.cloud_notm}} HSM?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-differentiators-cloud-hsm)

* [How is {{site.data.keyword.hscrypto}} different from {{site.data.keyword.keymanagementserviceshort}}?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-differentiators-key-protect)

* [How is Keep Your Own Key different from Bring Your Own Key?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-differentiators-KYOK)

* [What can I do with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-what-do-with-hpcs)

* [How do I know whether {{site.data.keyword.hscrypto}} is right for my company?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-choose-hs-crypto)

* [How does {{site.data.keyword.hscrypto}} work?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-how-hpcs-work)

* [What crypto card does {{site.data.keyword.hscrypto}} use?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-crypto-card)

* [Which IBM regions are {{site.data.keyword.hscrypto}} available in?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-hpcs-regions)

* [I have workloads in a data center where {{site.data.keyword.hscrypto}} is not available. Can I still subscribe to this service?](/docs/hs-crypto?topic=hs-crypto-faq-basics#faq-data-center)

[FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-pricing)

* [How am I charged for my use of {{site.data.keyword.hscrypto}} standard plan?](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-how-charge-hpcs)

* [How am I charged for my use of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}?](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-how-charge-hpcs-uko)

* [Is there a free trial for {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-free-trial)

[FAQs: Provisioning and operations](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-provisioning-operations)

* [Are there any prerequisites for using {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-hpcs-prerequisites)

* [How to initialize {{site.data.keyword.hscrypto}} service instances?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-how-to-initialize)

* [Can I initialize my service instance through the TKE CLI plug-in by using a proxy?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-tke-proxy)

* [Are there any recommendations on how to set up smart cards?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-smart-card-setup)

* [How can I procure smart cards and smart card readers?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-procure-smart-card)

* [How many crypto units shall I set up in my service instance?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-crypto-units-number)

* [Can I use {{site.data.keyword.hscrypto}} along with other {{site.data.keyword.cloud_notm}} services?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-hpcs-with-cloud-services)

* [How does my application connect to a {{site.data.keyword.hscrypto}} service instance?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-application-connection)

* [Can I generate master key on-premises and store the master key parts in the smart cards?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-generate-master-key-on-premises)

* [Can I import root keys from an on-premises HSM?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-import-key-on-premises)

* [Can I use {{site.data.keyword.hscrypto}} only for cryptographic operations, but use other {{site.data.keyword.cloud_notm}} services such as {{site.data.keyword.keymanagementserviceshort}} for key management?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-hpcs-with-key-protect)

* [Can I use {{site.data.keyword.hscrypto}} for applications hosted in other cloud service providers such as AWS, Azure, and GCP?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-hpcs-other-cloud-vendor)

* [How can I know whether the {{site.data.keyword.cloud_notm}} services that I adopt can integrate with {{site.data.keyword.hscrypto}} for key encryption?](/docs/hs-crypto?topic=hs-crypto-faq-provisioning-operations#faq-hpcs-service-integration)

[FAQs: {{site.data.keyword.hscrypto}} Standard Plan](/docs/hs-crypto?topic=hs-crypto-faq-performance-capacity#faq-performance-capacity)

* [How many keys can be stored in a Standard Plan instance of {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-performance-capacity#faq-keys-number)

* [How many key rings can be created for a {{site.data.keyword.hscrypto}} service instance?](/docs/hs-crypto?topic=hs-crypto-faq-performance-capacity#faq-keyrings-number)

* [Can I add or remove crypto units after I provision a service instance?](/docs/hs-crypto?topic=hs-crypto-faq-performance-capacity#faq-add-remove-crypto-unit)

* [Is there a Service Level Agreement (SLA) specifically for {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-performance-capacity#faq-hpcs-sla)

[FAQs: {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko)

* [How many keys can be stored in a {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} instance?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-keys-number-uko)

* [What is the difference between key management, key orchestration, and key governance?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-differences)

* [Does {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} provide key management, governance, and orchestration at the same time?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-functions)

* [Is {{site.data.keyword.uko_full_notm}} a separate offering?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-offering)

* [How is {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} different from the {{site.data.keyword.hscrypto}} Standard Plan?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-hpcs)

* [What type of HSM is used for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-fips)

* [Which cloud vendors or providers are supported by {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} as connected external keystores?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-vendor-cloud)

* [How is {{site.data.keyword.uko_full_notm}} different from EKMF Web?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-ekmf)

* [What multizone regions is {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} available in?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-mzr)

* [Can I still use {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} for key management even if {{site.data.keyword.hscrypto}} is not available in the {{site.data.keyword.cloud_notm}} region that my service resides in?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-region)

* [How many keystores can be created for an instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}?](/docs/hs-crypto?topic=hs-crypto-faq-uko#faq-uko-keystore-number)

[FAQs: Security and compliance](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-security-compliance)

* [How can I manage user access to my service instances? Does IBM have access to my instances?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-hpcs-ibm-access)

* [How does IBM offer a unique and secure process for service initialization (key ceremony)?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-hpcs-user-access)

* [What is a 140-2 FIPS Level 4 Certification and how can I validate it?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-fips-level4-meaning)

* [What is the difference between FIPS 140-2 Level 1, 2, 3, and Level 4?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-fips-levels)

* [How to understand the key hierarchy for {{site.data.keyword.hscrypto}} KYOK?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-cryptographic-algorithms)

* [How does EP11 differ from PKCS #11?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-ep11-pkcs11)

* [What EP11 mechanisms are supported by the GREP11 functions?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-EP11-mechanisms)

* [What compliance standards does {{site.data.keyword.hscrypto}} meet?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-compliance-standards)

* [Can I monitor my service instance?](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-monitor-instance)

[FAQs: High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-ha-dr)

* [How do I set up a high availability configuration?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-ha-configuration)

* [Can I back up my service instance manually?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-backup-manually)

* [What happens if my service instance fails?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-instance-fail)

* [How can I restore the content from backups?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-store-backup)

* [What happens if I delete my service instances?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-delete-instance)

* [Can I back up the keys before I delete a service instance?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-backup-keys)

* [What happens when I delete a key?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-delete-a-key)

* [What happens if I lose the signature key or the master key parts?](/docs/hs-crypto?topic=hs-crypto-faq-ha-dr#faq-lose-signature-key)

[FAQs: Support and maintenance](/docs/hs-crypto?topic=hs-crypto-faq-support-maintenance#faq-support-maintenance)

* [How is routine maintenance performed on {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-support-maintenance#faq-routine-maintenance)

* [How do I get support for {{site.data.keyword.hscrypto}}?](/docs/hs-crypto?topic=hs-crypto-faq-support-maintenance#faq-hpcs-support)

* [After the service initialization is done, are there any best practices for managing smart cards or key part files?](/docs/hs-crypto?topic=hs-crypto-faq-support-maintenance#faq-manage-smartcards)


## Troubleshooting key management service
{: #sitemap_troubleshooting_key_management_service}


[Why am I not authorized to make key management service API request?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-authenticate-api#troubleshoot-unable-to-authenticate-api)

[Why am I receiving a `CKR_IBM_WK_NOT_INITIALIZED` error when I use CLI or API?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-error-CLI-API#troubleshoot-error-CLI-API)

[Why can't I create a standard key after I load another master key?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-create-standard-keys#troubleshoot-unable-to-create-standard-keys)

[Why can't I create or import keys?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-create-keys#troubleshoot-unable-to-create-keys)

[Why can't I delete an initialized service instance?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-delete-instance#troubleshoot-delete-instance)

[Why can't I delete keys?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-delete-keys#troubleshoot-unable-to-delete-keys)

[Why can't I perform any actions by using the UI?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-ui-session-timeout#troubleshoot-ui-session-timeout)

[Why can't I rotate root keys?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-rotate-root-keys#troubleshoot-unable-to-rotate-root-keys)

[Why can't I view or list keys?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-list-keys-api#troubleshoot-unable-to-list-keys-api)

[Why can't I view or list specific keys?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-list-specific-keys#troubleshoot-unable-to-list-specific-keys)


## Troubleshooting master key rotation
{: #sitemap_troubleshooting_master_key_rotation}


[Why can't I rotate master keys by using key part files?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation-key-part-files#troubleshoot-master-key-rotation-key-part-files)

[Why can't I rotate master keys by using recovery crypto units?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation-recovery-crypto-units#troubleshoot-master-key-rotation-recovery-crypto-units)

[Why can't I rotate master keys by using smart cards?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation-key-smart-cards#troubleshoot-master-key-rotation-key-smart-cards)

[Why do I fail to load the new master key during the master key rotation process?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation#troubleshoot-master-key-rotation)


## Troubleshooting smart cards and the Management Utilities
{: #sitemap_troubleshooting_smart_cards_and_the_management_utilities}


[Why am I not authorized when I start the Trusted Key Entry application?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unauthorized-token-tke-application#troubleshoot-unauthorized-token-tke-application)

[Why am I receiving a blocked PIN on EP11 smart card error?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-block-smart-card#troubleshoot-block-smart-card)

[Why am I receiving a no smart card readers found error when I use the Management Utilities?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-no-smart-card#troubleshoot-no-smart-card)


## Troubleshooting Trusted Key Entry
{: #sitemap_troubleshooting_trusted_key_entry}


[Why am I not authorized when running TKE CLI plug-in commands?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unauthorized-token#troubleshoot-unauthorized-token)

[Why can't I change signature thresholds?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-unable-to-change-signature-thresholds#troubleshoot-unable-to-change-signature-thresholds)

[Why can't I list crypto units?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-list-crypto-units#troubleshoot-list-crypto-units)


## Troubleshooting Unified Key Orchestrator
{: #sitemap_troubleshooting_unified_key_orchestrator}


[Why can't I distribute keys to Azure Key Vault?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-import-azure-key#troubleshoot-import-azure-key)

[Why can't I create internal keystores?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-create-internal-keystores#troubleshoot-create-internal-keystores)

[Why can't I create vaults?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-create-vault#troubleshoot-create-vault)

[Why can't I delete vaults?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-delete-vault#troubleshoot-delete-vault)

[Why can't I delete internal keystores?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-delete-keystore#troubleshoot-delete-keystore)

[Why do I fail to see the changes to my key in Azure Key Vault?](/docs/hs-crypto?topic=hs-crypto-troubleshoot-azure-delay#troubleshoot-azure-delay)


## Getting help and support for {{site.data.keyword.hscrypto}}
{: #sitemap_getting_help_and_support_for_}


[Getting help and support for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-getting-help#getting-help)

* [Providing support case details](/docs/hs-crypto?topic=hs-crypto-getting-help#support-case-details)

