---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 新增功能
{: #what-new}

讓您隨時掌握可用於 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 的最新特性。
{: shortdesc}

## 2019 年 3 月
{: #March-2019}

### {{site.data.keyword.hscrypto}} 已正式提供
{: #ga-201903}
文件日期：2019-03-29

如需 {{site.data.keyword.hscrypto}} 供應項目的相關資訊，請參閱 [{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 首頁 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}。

自 2019 年 3 月 31 日開始，將無法再佈建新的 Hyper Protect Crypto Services 測試版實例。於測試版支援結束日期（2019 年 4 月 30 日）之前仍支援現有實例。

請參閱[從測試版服務實例移轉金鑰](/docs/services/hs-crypto/transition-keys.html)，以取得移轉金鑰至正式作業服務實例的相關資訊。

### 高可用性及災難回復
{: #ha-dr-new}
文件日期：2019-03-29

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 現在支援在一個選取的地區中可以有三個可用性區域，這一種含有自動特性的高可用性服務，可協助您確保應用程式安全且可運作。

您可以在支援的 [{{site.data.keyword.cloud_notm}} 地區](/docs/services/hs-crypto/regions.html)中建立 {{site.data.keyword.hscrypto}} 資源，該地區代表處理 {{site.data.keyword.hscrypto}} 要求所在的地理區域。每個 {{site.data.keyword.cloud_notm}} 地區包含[多個可用性區域 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/)，以滿足該地區的本端存取、低延遲及安全需求。

如需相關資訊，請參閱[高可用性及災難回復](/docs/services/hs-crypto/ha-dr.html)。

### 可擴充性
{: #scalability-new}
文件日期：2019-03-29

服務實例可以橫向擴充至最多達 6 個加密單位，以滿足您的效能需求。每一個加密單位可以加密處理 5000 個金鑰。在正式作業環境中，建議您至少要選取兩個加密單位使其具有高可用性。若選取三個以上的加密單位，這些加密單位將會分散在所選地區中的三個可用性區域。

如需相關資訊，請閱讀[佈建服務](/docs/services/hs-crypto/provision.html)。

## 2019 年 2 月
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} 測試版可供使用
{: #beta-201902}
文件日期：2019-02-05

已發行 {{site.data.keyword.hscrypto}} 測試版。您現在可以直接透過**型錄** > **安全及身分** 來存取 {{site.data.keyword.hscrypto}} 服務。

自 2019 年 2 月 5 日開始，再也無法佈建新的 Hyper Protect Crypto Services 實驗性實例。於實驗性支援結束日期（2019 年 3 月 5 日）之前仍支援現有實例。

## 2018 年 12 月
{: #Dec-2018}

### 已新增：支援使用 KYOK 的 HSM 管理
{: #hsm-kyok}
文件日期：2018-12-19

{{site.data.keyword.hscrypto}} 現在支援「自管金鑰 (KYOK)」，讓您能夠利用可保留、控制及管理的加密金鑰，進一步加強對資料的控制和權限。您可以使用 {{site.data.keyword.cloud}} 指令行介面 (CLI) 來起始設定及管理服務實例。

如需相關資訊，請參閱[起始設定服務實例來保護金鑰儲存空間](/docs/services/hs-crypto/initialize_hsm.html)。

### 已新增：{{site.data.keyword.keymanagementserviceshort}} API 的整合
{: #kp-api}
文件日期：2018-12-19

{{site.data.keyword.keymanagementserviceshort}} API 現在會與 Hyper Protect Crypto Services 整合，用來產生及保護您的金鑰。您可以透過 {{site.data.keyword.hscrypto}} 直接呼叫 {{site.data.keyword.keymanagementserviceshort}} API。

如需相關資訊，請參閱[存取 API](/docs/services/hs-crypto/access-api.html) 及 [{{site.data.keyword.hscrypto}} API ![外部鏈結圖示](image/external_link.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto){:new_window}。

### 已淘汰：透過 ACSP 存取 {{site.data.keyword.hscrypto}} 的功能
{: #deprecated-acsp}
文件日期：2018-12-19

在現行階段上，透過「進階加密服務提供者 (ACSP)」用戶端存取 {{site.data.keyword.hscrypto}} 的功能即將淘汰。如果您使用先前的服務實例，仍可使用 ACSP 來探索 {{site.data.keyword.hscrypto}}。
