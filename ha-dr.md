---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

Keywords: disaster recovery, High availability, HA, DR, recoverablity,

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

# High availability and disaster recovery
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is a highly available, regional service with automatic features that help keep your applications secure and operational.
{: shortdesc}

Use this page to learn more about availability and disaster recovery strategies of {{site.data.keyword.hscrypto}}.

## Locations, tenancy, and availability
{: #availability}

<!-- {{site.data.keyword.hscrypto}} is a multi-tenant, regional service. -->

You can create {{site.data.keyword.hscrypto}} resources in one of the supported [{{site.data.keyword.cloud_notm}} regions](/docs/services/hs-crypto?topic=hs-crypto-regions), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/cloud/blog/announcements/expansion-availability-zones-global-regions) to meet local access, low latency, and security requirements for the region.

As you plan your encryption at rest strategy with {{site.data.keyword.cloud_notm}}, keep in mind that provisioning {{site.data.keyword.hscrypto}} in a region that is nearest to you is more likely to result in faster, more reliable connections when you interact with the {{site.data.keyword.hscrypto}} APIs. Choose a specific region if the users, apps, or services that depend on a {{site.data.keyword.hscrypto}} resource are geographically concentrated. Remember that users and services who are far away from the region might experience higher latency.

Your encryption keys are confined to the region that you created them in. {{site.data.keyword.hscrypto}} does not copy or export encryption keys to other regions.
{: note}

## Disaster recovery
{: #disaster-recovery}

{{site.data.keyword.hscrypto}} has regional disaster recovery in place with a Recovery Time Objective (RTO) of one hour. The service follows {{site.data.keyword.cloud_notm}} requirements for planning and recovering from disaster events. For more information, see [Disaster recovery](/docs/overview?topic=overview-zero-downtime#disaster-recovery).
