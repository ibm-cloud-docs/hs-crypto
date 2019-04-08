---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: disaster recovery, High availability, HA, DR

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

# 高可用性和灾难恢复
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 是高可用性区域服务，其中带有自动功能，可帮助使您的应用程序保持安全和正常运作。
{: shortdesc}

使用此页面可了解有关 {{site.data.keyword.hscrypto}} 的可用性和灾难恢复策略的更多信息。

## 位置、租户和可用性
{: #availability}

<!-- {{site.data.keyword.hscrypto}} is a multi-tenant, regional service. -->

您可以在某个受支持的 [{{site.data.keyword.cloud_notm}} 区域](/docs/services/hs-crypto/regions.html)中创建 {{site.data.keyword.hscrypto}} 资源，这些区域表示处理和应对 {{site.data.keyword.hscrypto}} 请求的地理区域。每个 {{site.data.keyword.cloud_notm}} 区域中都包含[多个可用性专区 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/)，可满足该区域的本地访问、低等待时间和安全性需求。

在您使用 {{site.data.keyword.cloud_notm}} 规划静态加密策略时，请记住，如果在距离您最近的区域中供应 {{site.data.keyword.hscrypto}}，那么与 {{site.data.keyword.hscrypto}} API 交互时连接很可能会速度更快、更可靠。如果依赖于 {{site.data.keyword.hscrypto}} 资源的用户、应用程序或服务在地理上比较集中，请选择一个特定区域。请记住，对于距离该区域很远的用户和服务，等待时间可能会比较长。

您的加密密钥限制在创建这些密钥的区域中使用。{{site.data.keyword.hscrypto}} 不会将加密密钥复制或导出到其他区域。
{: note}

## 灾难恢复
{: #disaster-recovery}

{{site.data.keyword.hscrypto}} 已实施了“恢复时间目标”(RTO) 为一小时的区域灾难恢复。该服务遵循 {{site.data.keyword.cloud_notm}} 关于灾难事件规划和恢复的需求。有关更多信息，请参阅[灾难恢复](/docs/overview/zero_downtime.html#disaster-recovery)。
