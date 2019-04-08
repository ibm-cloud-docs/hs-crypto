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

# 高可用性及災難回復
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 是一種含有自動特性的高可用性地區服務，可協助您確保應用程式安全且可運作。
{: shortdesc}

請利用這個頁面來進一步瞭解 {{site.data.keyword.hscrypto}} 的可用性及災難回復策略。

## 位置、承租戶及可用性
{: #availability}

<!-- {{site.data.keyword.hscrypto}} is a multi-tenant, regional service. -->

您可以在其中一個支援的 [{{site.data.keyword.cloud_notm}} 地區](/docs/services/hs-crypto/regions.html)中建立 {{site.data.keyword.hscrypto}} 資源，該地區代表處理 {{site.data.keyword.hscrypto}} 要求所在的地理區域。每個 {{site.data.keyword.cloud_notm}} 地區包含[多個可用性區域 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/)，以滿足該地區的本端存取、低延遲及安全需求。

在您使用 {{site.data.keyword.cloud_notm}} 規劃靜態加密策略時，請記住，當您與 {{site.data.keyword.hscrypto}} API 互動時，在最接近您的地區佈建 {{site.data.keyword.hscrypto}} 更可能產生更快、更可靠的連線。如果取決於 {{site.data.keyword.hscrypto}} 資源之使用者、應用程式或服務的地理位置集中，請選擇特定地區。請記住，遠離該地區的使用者及服務可能會遭遇較高的延遲。

您的加密金鑰侷限於您在其中建立這些金鑰的地區。{{site.data.keyword.hscrypto}} 不會將加密金鑰複製或匯出到其他地區。
{: note}

## 災難回復
{: #disaster-recovery}

{{site.data.keyword.hscrypto}} 具有適當的地區災難回復，其「回復時間目標 (RTO)」為一個小時。此服務會遵循 {{site.data.keyword.cloud_notm}} 對於規劃及從災難事件回復的需求。如需相關資訊，請參閱[災難回復](/docs/overview/zero_downtime.html#disaster-recovery)。
