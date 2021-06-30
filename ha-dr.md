---

copyright:
  years: 2018, 2021
lastupdated: "2021-06-30"

keywords: disaster recovery, high availability, ha, dr, recoverablity, availability, failover

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is a highly available, regional service with automatic features that help keep your applications secure and operational.
{: shortdesc}

Learn more about availability and disaster recovery strategies of {{site.data.keyword.hscrypto}}.

## Locations, tenancy, and availability
{: #availability}

You can create {{site.data.keyword.hscrypto}} resources in one of the supported [{{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

As you plan your encryption at rest strategy with {{site.data.keyword.cloud_notm}}, keep in mind that provisioning {{site.data.keyword.hscrypto}} in a region that is nearest to you is more likely to result in faster, more reliable connections when you interact with the {{site.data.keyword.hscrypto}} APIs. Choose a specific region if the users, apps, or services that depend on a {{site.data.keyword.hscrypto}} resource are geographically concentrated. Users and services who are far away from the region might experience higher latency.

Your encryption keys are confined to the region that you created them in. {{site.data.keyword.hscrypto}} does not copy or export encryption keys to other regions.
{: note}

## In-region data redundancy and failover
{: #data-failover}

Multiple [crypto units](#x9860404){: term} in a service instance are automatically synchronized and load balanced across multiple availability zones. If one available zone that contains your provisioned service instance cannot be accessed, {{site.data.keyword.hscrypto}} has automatic in-region data failover in place. The service follows {{site.data.keyword.cloud_notm}} requirements for planning and recovering from disaster events. For more information, see [Disaster recovery](/docs/overview?topic=overview-zero-downtime#disaster-recovery).

## Cross-region disaster recovery
{: #cross-region-disaster-recovery}

IBM also performs cross-region backup for your key resources. Your data is automatically backed up in another supported region daily. Depending on the region that you create your service instance in and whether you enable failover crypto units, you can restore your data in case of a regional disaster with the following options:

- If you create your instance in Dallas (`us-south`) or Washington DC (`us-east`) and you enable failover crypto units, the failover crypto units back up the operational crypto units and keystores in another region. When a regional disaster occurs, your data is restored automatically with the failover crypto units to reduce the downtime and data loss. For more information about how to use failover crypto units to restore data, see [Restoring your data by using failover crypto units](/docs/hs-crypto?topic=hs-crypto-restore-data#restore-data-failover-crypto-units).
- If you don't enable failover crypto units, you can use the default daily backup to restore your data. In this case, you need to open a support ticket so that IBM can create a new service instance in another supported region to restore your data from the backup. Then, you need to manually load your master key to the new instance again to make it work. In this process, you're the only person who owns the master key. IBM administrators or any third-party users can't access your data or keys in the backup or the restored service instance. For more information about the recovery process, see [Restoring your data by opening an IBM support ticket](/docs/hs-crypto?topic=hs-crypto-restore-data#restore-data-open-support-ticket).
