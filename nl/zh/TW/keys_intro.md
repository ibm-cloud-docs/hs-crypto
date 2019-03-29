---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# 金鑰簡介
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 支援數種金鑰類型，包括根金鑰、標準金鑰及主要金鑰。
{:shortdesc}

## 根金鑰

*根金鑰* 是您在 {{site.data.keyword.hscrypto}} 中完全管理的對稱金鑰包裝金鑰。您可以使用根金鑰，以利用進階加密來保護其他加密金鑰。若要進一步瞭解，請參閱<a href="/docs/services/key-protect/concepts/envelope-encryption.html">封套加密</a>。

您可以遵循[管理金鑰](/docs/services/hs-crypto/index.html#manage-keys)中的步驗來管理根金鑰。

## 標準金鑰

*標準金鑰* 是用於加密的對稱金鑰。您可以使用標準金鑰來直接加密及解密資料。

您可以遵循[管理金鑰](/docs/services/hs-crypto/index.html#manage-keys)中的步驗來管理標準金鑰。

## 主要金鑰

*主要金鑰* 用來將加密實例 (HSM) 加密，而該實例可加密處理及管理根金鑰與標準金鑰。有了主要金鑰，您即擁有加密整個「金鑰」（包括根金鑰及標準金鑰）鏈的信任根源。

由於已建立加密實例 (HSM) 的端對端安全通道，因此只有 {{site.data.keyword.hscrypto}} 實例的管理者可以設定及管理主要金鑰。請注意，IBM 不會備份或接觸主要金鑰，也無法將其複製或還原到不同的機器或資料中心。

一個加密實例 (HSM) 只能有一個主要金鑰。如果您刪除 {{site.data.keyword.hscrypto}} 實例的主要金鑰，則可以對使用服務所管理金鑰加密的所有資料有效率地進行加密共用。

在[起始設定加密實例來保護金鑰儲存空間](/docs/services/hs-crypto/initialize_hsm.html)時，您可以管理主要金鑰。

現行階段不支援替換主要金鑰。
{:important}
