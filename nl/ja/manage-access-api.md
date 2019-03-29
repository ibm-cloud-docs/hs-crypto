---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: instance ID, account ID, Access Management

subcollection: hs-crypto


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 鍵へのアクセス権限の管理
{: #manage-access-api}

{{site.data.keyword.iamlong}} を使用すると、アクセス・ポリシーを作成および変更することによって、暗号鍵に対する細分化されたアクセス制御を有効にすることができます。
{: shortdesc}

このページでは、[Access Management API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window} を使用して暗号鍵へのアクセス権限を管理するためのシナリオをいくつか紹介します。

## 始めに
{: #prereqs}

この API を使用して処理を行うために、認証資格情報 (例えば、[アクセス・トークン](/docs/services/hs-crypto/access-api.html#retrieve-token)および[インスタンス ID](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID)) を生成してください。また、アクセス権限を管理したい {{site.data.keyword.hscrypto}} 鍵の ID も必要です。

鍵 ID の表示について詳しくは、[鍵の表示](/docs/services/hs-crypto/view-keys.html)を参照してください。
{: tip}

### アカウント ID の取得
{: #retrieve-account-ID}

資格情報を取得した後、{{site.data.keyword.hscrypto}} サービス・インスタンスを含んでいるアカウントの ID を取得することによって、新規アクセス・ポリシーのアクセス権限の範囲を判別します。

アカウント ID を取得するには、以下のステップを実行します。

1. {{site.data.keyword.cloud_notm}} CLI にログインします。
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **注:** フェデレーテッド ID を使用してログインする場合は、`--sso` パラメーターが必要です。 このオプションを使用する場合、CLI 出力にリストされたリンクにアクセスして、ワンタイム・パスコードを生成します。

    結果に、アカウントの ID 情報が表示されます。

    ```sh
    Authenticating...
    OK

    アカウントを選択します (または Enter キーを押してスキップします):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. アカウント ID の値をコピーします。

    値 _b6hnh3560ehqjkf89s4ba06i367801e_ は、アカウント ID の例です。

### ユーザー ID の取得
{: #retrieve-user-ID}

アクセス権限を変更するユーザーのユーザー ID を取得します。

ユーザー ID を取得するには、以下のステップを実行します。

1. [ユーザーに IAM トークンを提供するように依頼します](/docs/services/hs-crypto/access-api.html#retrieve-token)。
    IAM トークンの構造は次のとおりです。

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. 中央の値をコピーして、次のコマンドを実行します。
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    結果に、以下の例のような JSON オブジェクトが表示されます。
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. `id` プロパティーの値をコピーします。

## アクセス・ポリシーの作成
{: #create-policy}

特定の鍵に対するアクセス制御を有効にするには、以下のコマンドを実行して、{{site.data.keyword.iamshort}} に要求を送信します。 アクセス・ポリシーごとにコマンドを繰り返します。

```cURL
curl -X POST \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

指定された Cloud Foundry 組織およびスペース内の鍵へのアクセス権限を管理する必要がある場合は、`serviceInstance` を `organizationId` および `spaceId` に置き換えます。 詳しくは、[Access Management API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window} を参照してください。
{: tip}

`<user_ID>`、`<Admin_IAM_token>`、`<IAM_role>`、`<region>`、`<account_ID>`、`<instance_ID>`、および `<key_ID>` を、適切な値に置き換えてください。

**オプション:** ポリシーが正常に作成されたことを確認します。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## アクセス・ポリシーの更新
{: #update-policy}

取得したポリシー ID を使用して、ユーザーの既存のポリシーを変更できます。 以下のコマンドを実行して、{{site.data.keyword.iamshort}} に要求を送信します。

```cURL
curl -X PUT \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

`<user_ID>`、`<Admin_IAM_token>`、`<IAM_role>`、`<region>`、`<account_ID>`、`<instance_ID>`、および `<key_ID>` を、適切な値に置き換えてください。

**オプション:** ポリシーが正常に更新されたことを確認します。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## アクセス・ポリシーの削除
{: #delete-policy}

取得したポリシー ID を使用して、ユーザーの既存のポリシーを削除できます。 以下のコマンドを実行して、{{site.data.keyword.iamshort}} に要求を送信します。

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

`<account_ID>`、`<user_ID>`、`<policy_ID>`、および `<Admin_IAM_token>` を、適切な値に置き換えます。

**オプション:** ポリシーが正常に削除されたことを確認します。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
