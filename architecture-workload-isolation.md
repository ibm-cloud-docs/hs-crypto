---

copyright:
  years: 2021
lastupdated: "2021-05-12"

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
{: #architecture-workload-isolation}

Review the service architecture, workload isolation characteristics, and service dependencies for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## {{site.data.keyword.hscrypto}} architecture
{: #architecture}

The following architecture diagram shows how you interact with {{site.data.keyword.hscrypto}} components to protect your sensitive data and keys.

![Service instance components](/images/hs-crypto-components.svg "Service instance components"){: caption="Figure 1. Interaction with {{site.data.keyword.hscrypto}} components" caption-side="bottom"}



For more information about the {{site.data.keyword.hscrypto}} components, see [Components and concepts](/docs/hs-crypto?topic=hs-crypto-understand-concepts).

## {{site.data.keyword.hscrypto}} workload isolation
{: #workload-isolation}

{{site.data.keyword.hscrypto}} is a single-tenant, regional service that supports complete tenant-based workload isolation with the following characteristics:

- Dedicated keystore in {{site.data.keyword.hscrypto}} is provided to ensure data isolation and security.
- You have exclusive control to your hardware security module (HSM) and your master key. Privileged users are locked out for protection against abusive use of system administrator credentials or root user credentials.
- [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external} provides the enterprise level of security and impregnability that enterprise customers expect from [IBM LinuxONE](https://www.ibm.com/it-infrastructure/linuxone){: external} technology.

The following diagram illustrates how {{site.data.keyword.hscrypto}} workload of each tenant is isolated.

![{{site.data.keyword.hscrypto}} workload isolation](/images/workload-isolation.svg "{{site.data.keyword.hscrypto}} workload isolation"){: caption="Figure 2. {{site.data.keyword.hscrypto}} workload isolation" caption-side="bottom"}

## Service dependencies
{: #service_dependencies}

{{site.data.keyword.hscrypto}} has dependencies on the following {{site.data.keyword.cloud_notm}} services:

- [{{site.data.keyword.iamlong}} (IAM)](/docs/account?topic=account-iamoverview)
- [{{site.data.keyword.databases-for-postgresql_full_notm}}](/docs/databases-for-postgresql?topic=databases-for-postgresql-getting-started)
- [{{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant)
- [{{site.data.keyword.la_full_notm}}](/docs/log-analysis?topic=log-analysis-getting-started)
- [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started)
- [{{site.data.keyword.mon_full_notm}}](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-getting-started)
