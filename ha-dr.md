---

copyright:
  years: 2018, 2019
lastupdated: "2019-12-09"

keywords: disaster recovery, High availability, HA, DR, recoverablity

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
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

Provisioning at least two [crypto units](#x9860404){: term} for high availability is suggested. If one available zone that contains your provisioned service instance goes down, {{site.data.keyword.hscrypto}} has automatic in-region data failover in place. The service follows {{site.data.keyword.cloud_notm}} requirements for planning and recovering from disaster events. For more information, see [Disaster recovery](/docs/overview?topic=overview-zero-downtime#disaster-recovery).

## Cross-region disaster recovery
{: #cross-region-disaster-recovery}

IBM also performs cross-region backup for your key resources. Your data is automatically backed up in another supported region daily. If a regional disaster that affects all available zones occurs, you need to open a support ticket so that IBM can restore your data in another supported [{{site.data.keyword.cloud_notm}} region](/docs/hs-crypto?topic=hs-crypto-regions) from the backup. And then, you need to manually load your [master key](#x2908413){: term} to your new service instance again. In this process, you're the only person who owns the master key. IBM administrators or any third-party users can't access your data or keys in the backup or the restored service instance. For the detailed instruction, see [Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data).
