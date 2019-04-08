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

# サービス・インスタンス初期化の開始
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> このチュートリアルは、マスター鍵をロードしてサービス・インスタンスを初期化する方法を示します。この作業は、Trusted Key Entry プラグインを使用して鍵ストレージを保護するために必要です。 サービス・インスタンスを初期化した後に、ルート鍵の管理を開始できます。   
{:shortdesc}

## 前提条件
{: #get-started-hsm-prerequisite}

始める前に、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} インスタンス (略してサービス・インスタンス) をプロビジョンします。詳細な手順については、[{{site.data.keyword.hscrypto}} のプロビジョニング](/docs/services/hs-crypto/provision.html)を参照してください。

2. 以下のコマンドを実行して、正しい API エンドポイントにログインしていることを確認します。

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. {{site.data.keyword.cloud_notm}} コマンド・ライン・インターフェース (CLI) で次のコマンドを使用して、最新の Trusted Key Entry プラグインをインストールします。

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  CLI プラグインをインストールする方法については、[{{site.data.keyword.cloud_notm}} CLI の概説](/docs/cli/index.html)を参照してください。
  {: tip}

4. 環境変数 CLOUDTKEFILES の設定によって、鍵パーツと署名鍵を保管するサブディレクトリーを指定します。

##  ステップ 1: マスター鍵パーツと署名鍵のファイルを作成する
{: #hsm-step1}

1. ランダムなマスター鍵パーツまたは既知の値を持つマスター鍵パーツを作成します。

  * ランダムなマスター鍵パーツを作成するには、次のコマンドを使用します。

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    プロンプトが出されたら、鍵パーツの説明と、鍵パーツ・ファイルのパスワードを入力します。

  * 既知の値を持つマスター鍵パーツを作成するには、次のコマンドを使用します。

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    プロンプトが出されたら、鍵パーツの既知の値を 16 進数ストリングの形式で入力してから、鍵パーツ・ファイルの説明とパスワードを入力します。

  このコマンドを繰り返して、追加の鍵パーツを作成します。

2. 次のコマンドを使用して署名鍵を作成します。
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  プロンプトが出されたら、署名鍵ファイルの管理者名とパスワードを入力します。

## ステップ 2: 作業する暗号装置を選択する
{: #hsm-step2}

1 つのサービス・インスタンスに属するすべての暗号装置は、同じ構成内容にする必要があります。

1. 次のコマンドを使用して、IBM Cloud アカウントに割り当てられたサービス・インスタンスと暗号装置を表示できます。

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. 作業する追加の暗号装置を選択するには、次のコマンドを使用します。

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  プロンプトが出されたら、作業する追加の暗号装置を入力します。

3. 作業するセットから暗号装置を削除するには、次のコマンドを使用します。

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  プロンプトが出されたら、削除する暗号装置を入力します。

## ステップ 3: 暗号装置管理者を追加してインプリント・モードを終了する
{: #hsm-step3}

マスター鍵を暗号装置にロードするには、その前に 1 つ以上の暗号装置管理者を作成して、インプリント・モードを終了する必要があります。

1. 暗号装置管理者をロードします。 暗号装置管理者を作成するには、次のコマンドを使用します。
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  プロンプトが出されたら、管理者が使用する署名鍵の KEYNUM と、署名鍵ファイルのパスワードを入力します。

2. 次のコマンドを使用して、コマンドの署名に使用する署名鍵を選択します。

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  プロンプトが出されたら、コマンドの署名に使用する署名鍵の KEYNUM を入力します。

  これはステップ 3.1 で暗号装置管理者のロードに使用した署名鍵の 1 つと同じでなければなりません。
  {: tip}

3. 次のコマンドを使用して、インプリント・モードを終了します。

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

暗号装置管理者をロードしてインプリント・モードを終了した後、次のコマンドを使用して暗号装置の状態を確認できます。
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## ステップ 4: マスター鍵レジスターをロードする
{: #hsm-step4}

マスター鍵レジスターをロードするには、1 つ以上の暗号装置管理者を定義する必要があり、さらに暗号装置でインプリント・モードを終了しておくことが必要です。

1. 次のコマンドを使用して、新しいマスター鍵レジスターをロードします。

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  プロンプトが出されたら、ロードする鍵パーツの KEYNUM、署名鍵ファイルのパスワード、選択した各鍵パーツのパスワードを入力します。

2. 次のコマンドを使用して、新しいマスター鍵レジスターをコミットします。

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  プロンプトが出されたら、署名鍵ファイルのパスワードを入力します。

3. 次のコマンドを使用して、マスター鍵を現在のマスター鍵レジスターに移動します。

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  プロンプトが出されたら、署名鍵ファイルのパスワードを入力します。

## 次に行うこと
{: #hsm-next}

これで、サービス・インスタンスの使用を開始できるようになりました。 この手順を実稼働環境に実装する方法について詳しくは、[鍵ストレージを保護するためのサービス・インスタンスの初期化](/docs/services/hs-crypto/initialize_hsm.html)を参照してください。
