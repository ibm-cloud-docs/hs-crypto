---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# 從測試版服務實例移轉金鑰
{: #migrate-keys}

如果您使用測試版服務實例，而您想將所管理的根金鑰和標準金鑰移轉至 {{site.data.keyword.hscrypto}} 產品服務實例，則需要遵循這裡所提供的程序。
{: shortdesc}

IBM Cloud 管理者無法移轉主要金鑰，原因是不能從加密單位擷取主要金鑰。您需要使用您的主要金鑰來起始設定正式作業服務實例。
{:important}  

## 開始之前
{: #migrate-prerequisites}

1. 使用 Hyper Protect Crypto Services 方案來[建立服務實例](/docs/services/hs-crypto/provision.html)。

2. 使用「授信金鑰登錄」外掛程式來[起始設定服務實例](/docs/services/hs-crypto/initialize_hsm.html)。

## 移轉金鑰
{: #migrate-keys-steps}  

請完成下列步驟以將根金鑰和標準金鑰移轉至正式作業環境。

1. 透過 GUI 或 API 來[匯入根金鑰](/docs/services/hs-crypto/import-root-keys.html)。

  您可以將從測試版服務實例匯入的根金鑰移轉至正式作業服務實例。
{:tip}

2. 從測試版服務實例中解除包裝資料加密金鑰 (DEK)，並在正式作業服務實例中包裝 DEK：

  1. 從測試版服務實例中使用 [invoke-an-action-on-a-key API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window} [解除包裝資料加密金鑰 (DEK)](/docs/services/hs-crypto/unwrap-keys.html)。

  2. 在正式作業服務實例中使用 [invoke-an-action-on-a-key API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window}) [包裝 DEK](/docs/services/hs-crypto/wrap-keys.html)。

3. 透過下列步驟重建標準金鑰：

  1. 使用 [retrieve-key-by-id API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window} [擷取標準金鑰](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api)。這會傳回在測試版實例中用來建立金鑰的 payload 值。

  2. 使用 GUI 透過前一個步驟所擷取的資訊或使用 [create-a-new-key API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window} 在新的服務實例中[建立標準金鑰](/docs/services/hs-crypto/create-standard-keys.html)。

## 下一步為何？
{: #migration-next}

若要進一步瞭解如何以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto){: new_window}。
