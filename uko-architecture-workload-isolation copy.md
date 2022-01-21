---

copyright:
  years: 2021, 2022
lastupdated: "2022-01-17"

keywords: hyper protect crypto services architecture, service architecture, architecture diagram, workload isolation, crypto units, secure service container, ssc, public isolation for hyper protect crypto services, compute isolation for hyper protect crypto services

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:term: .term}


# Service architecture
{: #uko-architecture-workload-isolation}

Review the service architecture, workload isolation characteristics, and service dependencies for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## {{site.data.keyword.hscrypto}} architecture
{: #uko-architecture}

The following architecture diagram shows how you interact with {{site.data.keyword.hscrypto}} components to protect your sensitive data and keys.

![Service instance components](/images/hs-crypto-components-new.svg "Service instance components"){: caption="Figure 1. Interaction with {{site.data.keyword.hscrypto}} components" caption-side="bottom"}

The following list explains each component in detail.

Key management API
:   The API that you use to interact with the key management service (KMS) module to manage root keys and standard keys.

PKCS #11 API
:   The industry standard API to perform cryptographic operations. {{site.data.keyword.hscrypto}} implements API functions with the PKCS #11 library that interacts with the Enterprise PKCS #11 (EP11) module in the cloud HSM.

GREP11 API
:   The abbreviation of Enterprise PKCS #11 over gRPC API. It is a stateless interface for cryptographic operations, which also leverages the EP11 module in the cloud HSM.

Management Utilities
:   The Management Utilities are composed of the Smart Card Utility Program and the Trusted Key Entry (TKE) application, which provide GUI for you to initialize service instances. With signature keys and master key parts that are stored on smart cards, the Management Utilities provide an approach to initializing service instances with the highest level of security.

TKE CLI plug-in
:   A CLI plug-in working with {{site.data.keyword.cloud_notm}} CLI for you to initialize service instances. Depending on whether recovery crypto units are assigned to your instance, the plug-in provides two ways for instance initialization: by using recovery crypto units and by using key part files.

Operational crypto unit
:   Each service instance is composed of multiple operational crypto units. The operational crypto units are located in different availability zones of the same region for high availability. They are used to manage encryption keys and perform cryptographic operations. The number of crypto units that you specify when you create your instance is the number of operational crypto units.

Recovery crypto unit
:   The purpose of recovery crypto units is to generate a random master key value and to save a backup copy of the master key value. You can use recovery crypto units to load the master key and restore the master key when it is destroyed or lost.

    Currently, recovery crypto units are enabled only in the region of Dallas (`us-south`) and Washington DC (`us-east`). If you create your instance in either of the two regions, two recovery crypto units are automatically assigned to your instance without extra costs: one is in the `us-south`; the other is in the `us-east`.
    {: note}

Failover crypto unit
:   Failover crypto units back up the operational crypto units in another region, which includes keystores that store encryption keys. When a regional disaster occurs, you can use failover crypto units to ensure production workloads and avoid data loss.

    Currently, failover crypto units are available only in the region of Dallas (`us-south`) and Washington DC (`us-east`). If you create your instance in either of the two regions, you can choose whether to enable the failover crypto units with [extra charges](/docs/hs-crypto?topic=hs-crypto-faq-pricing).
    {: note}

For more information about the {{site.data.keyword.hscrypto}} components, see [Components and concepts](/docs/hs-crypto?topic=hs-crypto-understand-concepts).

## {{site.data.keyword.hscrypto}} workload isolation
{: #uko-workload-isolation}

{{site.data.keyword.hscrypto}} is a single-tenant, regional service that supports complete tenant-based workload isolation with the following characteristics:

- Dedicated keystore in {{site.data.keyword.hscrypto}} is provided to ensure data isolation and security.
- You have exclusive control to your hardware security module (HSM) and your master key. Privileged users are locked out for protection against abusive use of system administrator credentials or root user credentials.
- [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external} provides the enterprise level of security and impregnability that enterprise customers expect from [IBM LinuxONE](https://www.ibm.com/it-infrastructure/linuxone){: external} technology.

The following diagram illustrates how {{site.data.keyword.hscrypto}} workload of each tenant is isolated.

![{{site.data.keyword.hscrypto}} workload isolation](/images/workload-isolation.svg "{{site.data.keyword.hscrypto}} workload isolation"){: caption="Figure 2. {{site.data.keyword.hscrypto}} workload isolation" caption-side="bottom"}

## Service dependencies
{: #uko-service_dependencies}

{{site.data.keyword.hscrypto}} has dependencies on the following {{site.data.keyword.cloud_notm}} services:

- [{{site.data.keyword.iamlong}} (IAM)](/docs/account?topic=account-iamoverview)
- [{{site.data.keyword.databases-for-postgresql_full_notm}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started)
- [{{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant)
- [{{site.data.keyword.la_full_notm}}](/docs/log-analysis?topic=log-analysis-getting-started)
- [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started)
- [{{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started)
