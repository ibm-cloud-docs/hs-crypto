---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

Keywords: key storage, service instance, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}  
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# 開始使用服務實例起始設定
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> 本指導教學教您如何使用「授信金鑰登錄」外掛程式載入主要金鑰，保護金鑰儲存空間，藉以起始設定服務實例。起始設定服務實例之後，您就可以開始管理根金鑰。   
{:shortdesc}

## 必要條件
{: #get-started-hsm-prerequisite}

在開始之前，請執行下列步驟：

1. 佈建 {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 實例（簡稱為服務實例）。如需詳細步驟，請參閱[佈建 {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/provision.html)。

2. 執行下列指令以確定您已登入至正確的 API 端點：

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. 透過 {{site.data.keyword.cloud_notm}} 指令行介面 (CLI)，使用下列指令安裝最新的「授信金鑰登錄」外掛程式。

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  若要安裝 CLI 外掛程式，請參閱[開始使用 {{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html)。
  {: tip}

4. 設定環境變數 CLOUDTKEFILES，以指出您要儲存金鑰部分及簽章金鑰的子目錄

##  步驟 1：建立主要金鑰部分及簽章金鑰檔
{: #hsm-step1}

1. 建立隨機主要金鑰部分或含已知值的主要金鑰部分。

  * 若要建立隨機主要金鑰部分，請使用下列指令：

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    收到提示時，請輸入金鑰部分的說明及金鑰部分檔案的密碼。

  * 若要建立含已知值的主要金鑰部分，請使用下列指令：

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    收到提示時，請以十六進位字串輸入已知的金鑰部分值，然後輸入說明及金鑰部分檔案的密碼。

  重複任一指令來建立其他的金鑰部分。

2. 使用下列指令建立簽章金鑰：
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  收到提示時，請輸入管理者名稱及簽章金鑰檔的密碼。

## 步驟 2：選取您要使用的加密單位
{: #hsm-step2}

在一個服務實例中的所有加密單元必須有相同的配置。

1. 您可以使用下列指令來顯示指派給 IBM Cloud 帳戶的服務實例及加密單位：

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. 若要選取要使用的其他加密單位，請使用下列指令：

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  收到提示時，請輸入要使用的其他加密單位。

3. 若要從將使用的集合中移除加密單位，請使用下列指令：

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  收到提示時，請輸入要移除的加密單位。

## 步驟 3：新增加密單位管理者並結束印記模式
{: #hsm-step3}

您必須建立一個以上的加密單位管理者並結束印記模式，才能在加密單位中載入主要金鑰。

1. 載入加密單位管理者。若要建立加密單位管理者，請使用下列指令：
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  收到提示時，請輸入要用於管理者之簽章金鑰的 KEYNUM 及簽章金鑰檔的密碼。

2. 使用下列指令，選取要用於簽署指令的簽章金鑰：

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  收到提示時，請輸入要用於簽署指令之簽章金鑰的 KEYNUM。

  這必須與步驟 3.1 中用來載入加密單位管理者的其中一個簽章金鑰相同。
  {: tip}

3. 使用下列指令，結束印記模式：

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

載入加密單位管理者並結束印記模式之後，您可以使用下列指令來檢查加密單位的狀態：
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## 步驟 4：載入主要金鑰登錄
{: #hsm-step4}

若要載入主要金鑰登錄，必須定義一個以上的加密單位管理者，而且該加密單位必須離開印記模式。

1. 使用下列指令，載入新的主要金鑰登錄：

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  收到提示時，請輸入要載入之金鑰部分的 KEYNUM、簽章金鑰檔的密碼，以及每個已選取金鑰部分的密碼。

2. 使用下列指令，確定新的主要金鑰登錄：

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  收到提示時，請輸入簽章金鑰檔的密碼。

3. 使用下列指令，將主要金鑰移至現行的主要金鑰登錄：

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  收到提示時，請輸入簽章金鑰檔的密碼。

## 下一步為何？
{: #hsm-next}

現在，您可以開始使用服務實例。如需在正式作業環境中實作程序的詳細資料，請參閱[起始設定服務實例來保護金鑰儲存空間](/docs/services/hs-crypto/initialize_hsm.html)。
