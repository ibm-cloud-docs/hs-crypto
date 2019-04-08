---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: IBM Cloud CLI plug-in, ibmcloud commands, IBM Cloud command-line interface

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# 在 {{site.data.keyword.hscrypto}} 實例上存取 {{site.data.keyword.keymanagementserviceshort}} CLI
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 會與 {{site.data.keyword.keymanagementservicelong_notm}} CLI 外掛程式整合，讓您能夠使用 {{site.data.keyword.keymanagementservicelong_notm}} CLI 外掛程式來建立、匯入及管理加密根金鑰與標準金鑰。

在您能夠於 {{site.data.keyword.hscrypto}} 實例（簡稱為服務實例）上使用 {{site.data.keyword.keymanagementserviceshort}} CLI 外掛程式之前，您需要先設定工作站上的 KP_KP_PRIVATE_ADDR 環境變數：

* 在 Linux 或 MacOS 上，請執行下列指令：

  ```
export KP_PRIVATE_ADDR=<URL>
```
  {: pre}

  在這個指令中，*URL* 是顯示在佈建的 {{site.data.keyword.hscrypto}} 儀表板之**管理**標籤上的端點。例如：

  ```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
  {: pre}

* 在 Windows 上，在**控制台**的搜尋方框中鍵入 `environment variable` 來搜尋「環境變數」視窗。建立 KP_PRIVATE_ADDR 環境變數，並將值設定為在佈建的 {{site.data.keyword.hscrypto}} 儀表板的**管理**標籤上顯示的端點。例如，`https://us-south.hs-crypto.cloud.ibm.com:<port>`.

您也可以透過 API 來擷取端點 URL。如需詳細資料，[請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto){: new_window}。

- 若要進一步瞭解如何使用 CLI，請參閱 [{{site.data.keyword.keymanagementserviceshort}} CLI 參考資料文件](/docs/services/key-protect/cli-reference.html)。
- 若要進一步瞭解如何存取 CLI，請參閱[設定 {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/services/key-protect/set-up-cli.html)。
