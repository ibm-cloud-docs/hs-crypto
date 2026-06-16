---

copyright:
  years: 2022, 2026
lastupdated: "2026-06-16"

keywords: hyper protect crypto services architecture, service architecture, architecture diagram, workload isolation, crypto units, secure service container, ssc, public isolation for hyper protect crypto services, compute isolation for hyper protect crypto services

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Service architecture - Unified Key Orchestrator Plan
{: #uko-architecture-workload-isolation}

Review the service architecture, workload isolation characteristics, and service dependencies for IBM Cloud&reg; Hyper Protect Crypto Services.
{: shortdesc}

## Hyper Protect Crypto Services architecture
{: #uko-architecture}

The following architecture diagram shows how you interact with Hyper Protect Crypto Services components to protect your sensitive data and keys.

![Service instance components](/images/hs-crypto-components-uko.svg "Service instance components"){: caption="Interaction with Hyper Protect Crypto Services components" caption-side="bottom"}

The following list explains each component in detail.

Unified Key Orchestrator API
:   The API that you use to interact with the Unified Key Orchestrator module to manage keys and keystores for multiple clouds. You can interact with Unified Key Orchestrator either with the UI or with the API.

Key management service API
:   The API that you use to interact with the key management service (KMS) module to manage root keys and standard keys.

PKCS #11 API
:   The industry standard API to perform cryptographic operations. Hyper Protect Crypto Services implements API functions with the PKCS #11 library that interacts with the Enterprise PKCS #11 (EP11) module in the cloud HSM.

GREP11 API
:   The abbreviation of Enterprise PKCS #11 over gRPC API. It is a stateless interface for cryptographic operations, which also leverages the EP11 module in the cloud HSM.

Management Utilities
:   The Management Utilities are composed of the Smart Card Utility Program and the Trusted Key Entry (TKE) application, which provide GUI for you to initialize service instances. With signature keys and master key parts that are stored on smart cards, the Management Utilities provide an approach to initializing service instances with the highest level of security.

TKE CLI plug-in
:   A CLI plug-in working with IBM Cloud CLI for you to initialize service instances. Depending on whether recovery crypto units are assigned to your instance, the plug-in provides two ways for instance initialization: by using recovery crypto units and by using key part files.

Operational crypto unit
:   Each service instance is composed of multiple operational crypto units. The operational crypto units are located in different availability zones of the same region for high availability. They are used to manage encryption keys and perform cryptographic operations. The number of crypto units that you specify when you create your instance is the number of operational crypto units.

Recovery crypto unit
:   The purpose of recovery crypto units is to generate a random master key value and to save a backup copy of the master key value. You can use recovery crypto units to load the master key and restore the master key when it is destroyed or lost.

    Currently, service instances in the `eu-es` region don't support recovery crypto units. When a service instance is provisioned in other supported regions, you are by default enabled with the option to back up your master keys in the recovery crypto units located in the disaster recovery region. 

    If smart cards are used to load the master key, the recovery crypto units are not applicable and can be ignored. The backup of the master key relies on the backup of the smart cards in that case.
    {: note}

For more information about the Hyper Protect Crypto Services components, see [Components and concepts](/docs/hs-crypto?topic=hs-crypto-uko-understand-concepts).

## Hyper Protect Crypto Services workload isolation
{: #uko-workload-isolation}

Hyper Protect Crypto Services is a single-tenant, regional service that supports complete tenant-based workload isolation with the following characteristics:

- Dedicated keystore in Hyper Protect Crypto Services is provided to ensure data isolation and security.
- You have exclusive control to your hardware security module (HSM) and your master key. Privileged users are locked out for protection against abusive use of system administrator credentials or root user credentials.
- [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external} provides the enterprise level of security and impregnability that enterprise customers expect from [IBM LinuxONE](https://www.ibm.com/it-infrastructure/linuxone){: external} technology.

The following diagram illustrates how Hyper Protect Crypto Services workload of each tenant is isolated.

![Hyper Protect Crypto Services workload isolation](/images/architecture-workload-isolation.svg "Hyper Protect Crypto Services workload isolation"){: caption="Hyper Protect Crypto Services workload isolation" caption-side="bottom"}

## Service dependencies
{: #uko-service_dependencies}

Hyper Protect Crypto Services has dependencies on the following IBM Cloud services:

- [IBM Cloud&reg; Identity and Access Management (IAM)](/docs/account?topic=account-iamoverview)
- [IBM Cloud Databases for PostgreSQL](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started)
- [IBM Cloudant](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant)
- [IBM Log Analysis](/docs/log-analysis?topic=log-analysis-getting-started)
- [IBM Cloud Activity Tracker](/docs/activity-tracker?topic=activity-tracker-getting-started)
- [IBM Cloud Monitoring](/docs/monitoring?topic=monitoring-getting-started)
