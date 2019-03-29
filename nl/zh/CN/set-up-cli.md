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

# 设置 CLI
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 与 {{site.data.keyword.keymanagementservicelong_notm}} CLI 插件集成，这样就可以使用 {{site.data.keyword.keymanagementservicelong_notm}} CLI 插件来创建、导入和管理加密根密钥和标准密钥。

- 要了解有关使用 CLI 的更多信息，请查看 [{{site.data.keyword.keymanagementserviceshort}} CLI 参考文档](/docs/services/key-protect/cli-reference.html)。

- 要查找有关访问 CLI 的信息，请查看[设置 {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/services/key-protect/set-up-cli.html)。

要能够在 {{site.data.keyword.hscrypto}} 实例上使用 {{site.data.keyword.keymanagementserviceshort}} CLI 插件，请先运行以下命令：

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

在此命令中，*URL* 是显示在用户界面的**管理**页面上的端点。或者，也可以通过 API 来检索端点 URL。例如：


```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

有关详细信息，[请查看 {{site.data.keyword.hscrypto}} API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。
