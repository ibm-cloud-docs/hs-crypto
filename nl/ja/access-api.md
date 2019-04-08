---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: REST API, RESTful API, access token, instance ID

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# API へのアクセス
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} は、鍵の保管、取得、生成を行うために、{{site.data.keyword.keymanagementserviceshort}} REST API と統合されています。この API は任意のプログラミング言語で使用できます。
{: shortdesc}

API で作業するには、サービス資格情報と認証資格情報を生成する必要があります。

## アクセス・トークンの取得
{: #retrieve-token}

{{site.data.keyword.iamshort}} からアクセス・トークンを取得して、{{site.data.keyword.hscrypto}} で認証できます。 [サービス ID](/docs/iam/serviceid.html#serviceids) を使用して、{{site.data.keyword.cloud_notm}} 上または外部にあるサービスまたはアプリケーションの代わりに、{{site.data.keyword.hscrypto}} API で作業できます。個人のユーザー資格情報を共有する必要はありません。  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

アクセス・トークンを取得するには、以下の手順を実行します。

1. {{site.data.keyword.cloud_notm}} コンソールで、**「管理」** &gt; **「セキュリティー」** &gt; **「ID およびアクセス」** &gt; **「サービス ID」**に移動します。 [サービス ID の作成](/docs/iam/serviceid.html#creating-a-service-id)のプロセスに従います。
2. **「アクション」**メニューを使用して、[新しいサービス ID のアクセス・ポリシーを定義します。](/docs/iam/serviceidaccess.html)

    {{site.data.keyword.hscrypto}} リソースに対するアクセス権限の管理について詳しくは、[役割と許可](/docs/services/hs-crypto/manage-access.html#roles)を参照してください。
3. **「API キー」**セクションを使用して、[サービス ID に関連付ける API キーを作成します](/docs/iam/serviceid_keys.html#serviceidapikeys)。 API キーをダウンロードして、安全な場所に保存します。
4. {{site.data.keyword.iamshort}} API を呼び出して、アクセス・トークンを取得します。

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    要求内の `<API_KEY>` を、ステップ 3 で作成した API キーに置き換えます。以下の省略された例は、トークンの出力を示しています。

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    完全な `access_token` 値 (接頭部に _Bearer_ トークン・タイプが付いている) を使用して、サービス用の鍵を {{site.data.keyword.hscrypto}} API を使ってプログラムで管理します。

    アクセス・トークンが有効なのは 1 時間ですが、必要に応じて再生成できます。 サービスへのアクセス権限を維持するには、{{site.data.keyword.iamshort}} API を呼び出すことによって、定期的に API 鍵のアクセス・トークンをリフレッシュしてください。   
    {: tip }

## インスタンス ID の取得
{: #retrieve-instance-ID}

{{site.data.keyword.hscrypto}} サービス・インスタンスの識別情報を、[{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview) を使用して取得できます。 インスタンス ID を使用して、アカウントの {{site.data.keyword.hscrypto}} の指定インスタンス内の暗号鍵を管理します。

1. [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview) を使用して、{{site.data.keyword.cloud_notm}} にログインします。

    ```sh
    ibmcloud login
    ```
    {: pre}

    **注:** ログインに失敗した場合は、`ibmcloud login --sso` コマンドを実行して、再試行してください。 フェデレーテッド ID を使用してログインする場合は、`--sso` パラメーターが必要です。 このオプションを使用する場合、CLI 出力にリストされたリンクにアクセスして、ワンタイム・パスコードを生成します。

2. プロビジョン済みインスタンスを含むアカウントを選択します。

    `ibmcloud resource service-instances` を実行すると、アカウント内でプロビジョンされたすべてのサービス・インスタンスをリストできます。

3. {{site.data.keyword.hscrypto}} サービス・インスタンスを一意的に識別するクラウド・リソース名 (CRN) を取得します。

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    `<instance_name>` を、{{site.data.keyword.hscrypto}} のインスタンスに割り当てた固有の別名に置き換えます。 以下の省略された例は、CLI 出力を示しています。 値 _42454b3b-5b06-407b-a4b3-34d9ef323901_ は、インスタンス ID の例です。

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## 接続情報の取得
{: #retrieve-connection-info}

いずれかの {{site.data.keyword.keymanagementserviceshort}} API を呼び出す前に、まず**接続情報の取得** API を呼び出して接続情報を取得します。 詳しくは、[the {{site.data.keyword.hscrypto}} API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto){: new_window} を参照してください。

## API 要求の作成
{: #form-api-request}

サービスに対して API 呼び出しを行う場合、{{site.data.keyword.hscrypto}} のインスタンスを最初にプロビジョンした方法に応じて、API 要求を構成します。

要求を作成するには、[地域のサービス・エンドポイント](/docs/services/hs-crypto/regions.html)と適切な認証資格情報を組み合わせます。 例えば、`us-south` 地域のサービス・インスタンスを作成した場合は、以下のエンドポイントと API ヘッダーを使用して、サービス内の鍵を表示します。

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### 次に行うこと
{: #api-next}

プログラムでの鍵の管理について詳しくは、[{{site.data.keyword.hscrypto}} API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/hs-crypto){: new_window} を確認してください。

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}. -->
