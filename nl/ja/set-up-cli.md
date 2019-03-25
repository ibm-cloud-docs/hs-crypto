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

# CLI のセットアップ
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} は {{site.data.keyword.keymanagementservicelong_notm}} CLI プラグインと統合しているので、{{site.data.keyword.keymanagementservicelong_notm}} CLI プラグインを使用して暗号のルート鍵と標準鍵を作成、インポート、管理することができます。

- この CLI の使用について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} CLI リファレンス資料](/docs/services/key-protect/cli-reference.html)を確認してください。
- CLI のアクセス方法について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} CLI のセットアップ](/docs/services/key-protect/set-up-cli.html)を参照してください。

{{site.data.keyword.hscrypto}} インスタンス上で {{site.data.keyword.keymanagementserviceshort}} CLI プラグインを使用するには、その前にまず次のコマンドを実行してください。

```
export KP_PRIVATE_ADDR=<URL>
```
{: pre}

このコマンドで、*URL* は、ユーザー・インターフェースの**「管理」**ページに表示されるエンドポイントです。このエンドポイント URL は API で取得することもできます。以下に例を示します。

```
export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
```
{: pre}

詳しくは、[{{site.data.keyword.hscrypto}} API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} を確認してください。
