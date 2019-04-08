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

# 在 {{site.data.keyword.hscrypto}} 实例上访问 {{site.data.keyword.keymanagementserviceshort}} CLI
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 与 {{site.data.keyword.keymanagementservicelong_notm}} CLI 插件集成，这样就可以使用 {{site.data.keyword.keymanagementservicelong_notm}} CLI 插件来创建、导入和管理加密根密钥和标准密钥。

要能够在 {{site.data.keyword.hscrypto}} 实例（简称服务实例）上使用 {{site.data.keyword.keymanagementserviceshort}} CLI 插件，您需要在工作站上设置 KP_KP_PRIVATE_ADDR 环境变量：

* 对于 Linux 或 MacOS，请运行以下命令：

  ```
export KP_PRIVATE_ADDR=<URL>
```
  {: pre}

  在此命令中，*URL* 是显示在已供应 {{site.data.keyword.hscrypto}} 仪表板的**管理**选项卡上的端点。例如：


  ```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
  {: pre}

* 对于 Windows，在**控制面板**的搜索框中输入`环境变量`，以找到“环境变量”窗口。创建 KP_PRIVATE_ADDR 环境变量，并将值设置为显示在已供应 {{site.data.keyword.hscrypto}} 仪表板的**管理**选项卡上的端点。例如，`https://us-south.hs-crypto.cloud.ibm.com:<port>`。

您也可以通过 API 来检索端点 URL。有关详细信息，[请查看 {{site.data.keyword.hscrypto}} API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto){: new_window}。

- 要了解有关使用 CLI 的更多信息，请查看 [{{site.data.keyword.keymanagementserviceshort}} CLI 参考文档](/docs/services/key-protect/cli-reference.html)。

- 要查找有关访问 CLI 的信息，请查看[设置 {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/services/key-protect/set-up-cli.html)。
