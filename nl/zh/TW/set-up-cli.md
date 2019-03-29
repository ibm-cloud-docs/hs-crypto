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

# 設定 CLI
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 會與 {{site.data.keyword.keymanagementservicelong_notm}} CLI 外掛程式整合，讓您能夠使用 {{site.data.keyword.keymanagementservicelong_notm}} CLI 外掛程式來建立、匯入及管理加密根金鑰與標準金鑰。

- 若要進一步瞭解如何使用 CLI，請參閱 [{{site.data.keyword.keymanagementserviceshort}} CLI 參考資料文件](/docs/services/key-protect/cli-reference.html)。
- 若要進一步瞭解如何存取 CLI，請參閱[設定 {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/services/key-protect/set-up-cli.html)。

在您能夠於 {{site.data.keyword.hscrypto}} 實例上使用 {{site.data.keyword.keymanagementserviceshort}} CLI 外掛程式之前，請先執行下列指令：

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

在這個指令中，*URL* 是顯示在使用者介面之**管理**頁面上的端點。或者，您可以透過 API 來擷取端點 URL。例如：

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

如需詳細資料，[請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。
