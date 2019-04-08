---

copyright:
  years: 2018, 2019
lastupdated: "2019-33-22"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 常見問題
{: #faqs}

下列常見問題可用來協助您使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}。

## HSM 憑證
{: #HSM-certifications}

### 如何驗證 IBM 加密卡 (HSM) 已經過驗證，符合 FIPS 140-2 Level 4？
{: #FIPS-L4}

FIPS 140-2 Level 4 是市場上尚未廣泛採用的極高保護層次。IBM 是最高層次認證 HSM 的領先供應商，已投入巨資針對每一代的新卡維護這項驗證。從政府需求中收集了高層次保證的需求。為了驗證憑證，會將您指向 NIST 首頁，因為憑證已於該處發佈。

### FIPS 140-2 Level 2、3 與 Level 4 之間的差異為何?
{: #FIPS-levels}

* FIPS 140-2 Level 2：透過密封、可拆卸蓋板及門上的防拆鎖 (pick-resistant lock) 完成的竄改證明需求。防竄改塗層或密封將置於加密模組上，因此必須破壞塗層或密封，才能對模組內的純文字加密金鑰及重要安全參數 (CSP) 進行實體存取。安全層次 2 至少需要以角色為基礎的鑑別，其中加密模組會鑑別要採用特定角色之操作員的授權，並執行相對應的一組服務。
* FIPS 140-2 Level 3：安全層次 3 所需的實體安全機制預期要能偵測及回應加密模組的實體存取、使用與修改嘗試。安全層次 3 需要以身分為基礎的鑑別機制，以加強針對安全層次 2 所指定之以角色為基礎的鑑別機制提供的安全。

* FIPS 140-2 Level 4：在這個安全層次上，實體安全機制會在加密模組周圍提供完整的保護封套，其目的在於偵測及回應實體存取的所有未獲授權嘗試。有很高的機率可偵測到從任何方向滲入加密模組外殼的入侵，進而導致所有純文字 CSP（重要安全參數）立即歸零。安全層次 4 加密模組對於實體無防護環境中的作業非常有用。安全層次 4 也會保護加密模組，以防止因電壓和溫度超出模組正常操作範圍的環境狀況或變動危及安全。攻擊者可能會使用超出正常操作範圍的刻意偏移來阻撓加密模組的防禦。

## 金鑰管理
{: #key-management}

### {{site.data.keyword.hscrypto}} 是否可以與 {{site.data.keyword.keymanagementserviceshort}} 服務一起使用？

 {{site.data.keyword.hscrypto}} 是一種受管理的「加密服務」，隨附有完全相容的 {{site.data.keyword.keymanagementserviceshort}} API，與 Key Protect 具有相同的使用者體驗。主要差異在於，{{site.data.keyword.hscrypto}} 仰賴通過 FIPS 140-2 lvl 4 認證的 HSM。同時，它會利用客戶所管理的 HSM 主要金鑰 (KYOK) 提供完整控制。相較於 {{site.data.keyword.keymanagementserviceshort}} 的多方承租戶設定，此服務專用於每個實例。{{site.data.keyword.hscrypto}} 還提供用於加密作業的 HSM 功能，例如簽署/驗證、金鑰產生、加密雜湊、加密/解密，以及包裝/解除包裝。

### 金鑰名稱可以多長？
{: #key_names}

您可以使用長度最多 50 個字元的金鑰名稱。

### 可以使用語言字元作為金鑰名稱的一部分嗎？
{: #key_chars}

語言字元（例如中文字元）不能作為金鑰名稱的一部分使用。

### 刪除金鑰時會發生什麼情況？
{: #key_destruction}

當您刪除金鑰時，會永久地清除其內容及相關聯的資料。將無法再存取已使用金鑰所加密的資料。

在您刪除金鑰之前，請確定不再需要存取任何與金鑰相關聯的資料。

<!-- ## Pricing
{: #pricing}

### Where can I find the detailed pricing information?
{: #pricing_info}

You can refer to the **Pricing** tab on the [{{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){: new_window} for details.

### Is there a pricing example I can refer to?
{: #pricing_example}

Here is one. If you have a requirement of 5000 keys to be crypto-processed, for high availability, you need to set up two crypto units. The amount is $3140 ($1570 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls). In total, there will be a monthly charge of $3141 ($3140 for the crypto units and $1 for the additional API calls) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1570 |
| Crypto unit 2 | $1570 |
| First 1,000,000 API calls | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) | $1 ($0.01 x 100) |
| End of month charge | $3141  |

*Table 1. Charge of two crypto units with a monthly API calls of 2,000,000* -->
