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

# {{site.data.keyword.hscrypto}} インスタンス上での {{site.data.keyword.keymanagementserviceshort}} CLI へのアクセス
{: #set-up-cli}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} は {{site.data.keyword.keymanagementservicelong_notm}} CLI プラグインと統合しているので、{{site.data.keyword.keymanagementservicelong_notm}} CLI プラグインを使用して暗号のルート鍵と標準鍵を作成、インポート、管理することができます。

{{site.data.keyword.hscrypto}} インスタンス (略してサービス・インスタンス) 上で {{site.data.keyword.keymanagementserviceshort}} CLI プラグインを使用するには、ワークステーション上で KP_KP_PRIVATE_ADDR 環境変数を設定する必要があります。

* Linux または MacOS の場合は、以下のコマンドを実行します。

  ```
  export KP_PRIVATE_ADDR=<URL>
  ```
  {: pre}

  このコマンドで、*URL* は、プロビジョン済みの {{site.data.keyword.hscrypto}} ダッシュボードの**「管理」**タブに表示されるエンドポイントです。以下に例を示します。

  ```
  export KP_PRIVATE_ADDR="https://us-south.hs-crypto.cloud.ibm.com:<port>"
  ```
  {: pre}

* Windows の場合は、**コントロール パネル**で、検索ボックスに `environment variable` と入力して、「環境変数」ウィンドウを見つけます。KP_PRIVATE_ADDR 環境変数を作成し、プロビジョン済みの {{site.data.keyword.hscrypto}} ダッシュボードの**「管理」**タブに表示されるエンドポイントに値を設定します。例えば、`https://us-south.hs-crypto.cloud.ibm.com:<port>` と設定します。

このエンドポイント URL は API で取得することもできます。詳しくは、[{{site.data.keyword.hscrypto}} API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto){: new_window} を確認してください。

- この CLI の使用について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} CLI リファレンス資料](/docs/services/key-protect/cli-reference.html)を確認してください。
- CLI のアクセス方法について詳しくは、[{{site.data.keyword.keymanagementserviceshort}} CLI のセットアップ](/docs/services/key-protect/set-up-cli.html)を参照してください。
