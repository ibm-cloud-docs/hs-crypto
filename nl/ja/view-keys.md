---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: view keys, key configuration, key type

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 鍵の表示
{: #view-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} により、
暗号鍵を表示、管理、監査する集中システムが提供されます。 鍵と鍵へのアクセス制限を監査して、リソースのセキュリティーを確保します。
{: shortdesc}

定期的に鍵の構成を監査するために、以下を行います。

- いつ鍵が作成されたかを調べ、鍵をローテートする時期かどうかを判断します。
- [{{site.data.keyword.cloudaccesstrailshort}} を使用して、{{site.data.keyword.hscrypto}} への API 呼び出しをモニターします](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html)。
- どのユーザーが鍵へのアクセス権限を持っているか、アクセス権限のレベルは適切かどうかを検査します。

リソースへのアクセス権限の監査について詳しくは、[Cloud IAM を使用したユーザーのアクセス権限の管理](/docs/services/hs-crypto/manage-access.html)を参照してください。

## GUI を使用した鍵の表示
{: #gui}

グラフィカル・インターフェースを使用してサービス内の鍵を検査したい場合は、{{site.data.keyword.hscrypto}} ダッシュボードを使用できます。

[サービス内に鍵を作成するか、既存の鍵をインポートした後](/docs/services/hs-crypto/create-root-keys.html)、以下の手順を実行して、鍵を表示します。

1. [{{site.data.keyword.cloud_notm}} コンソール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") にログインします](https://cloud.ibm.com/)。
2. {{site.data.keyword.cloud_notm}} ダッシュボードで、{{site.data.keyword.hscrypto}} のプロビジョン済みインスタンスを選択します。
3. {{site.data.keyword.hscrypto}} ダッシュボードで、以下のような鍵の一般的な特性を参照します。

    <table>
      <tr>
        <th>列</th>
        <th>説明</th>
      </tr>
      <tr>
        <td>名前</td>
        <td>鍵に割り当てられた、人間が理解できる固有の別名。</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>{{site.data.keyword.hscrypto}} サービスによって鍵に割り当てられた固有の鍵 ID。 この ID 値を使用して、[{{site.data.keyword.hscrypto}} API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/hs-crypto)でサービスを呼び出すことができます。</td>
      </tr>
      <tr>
        <td>状態</td>
        <td>[NIST Special Publication 800-57, Recommendation for Key Management ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf) に基づく[鍵の状態](/docs/services/key-protect/concepts/key-states.html)。 状態には、<i>アクティブ化前</i>、<i>アクティブ</i>、<i>非アクティブ化</i>、および <i>破棄</i> があります。</td>
      </tr>
      <tr>
        <td>タイプ</td>
        <td>サービス内の鍵の指定された目的を説明する、[鍵のタイプ](/docs/services/key-protect/concepts/envelope-encryption.html#key-types)。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. <b>「鍵 (Keys)」</b>テーブルの説明</caption>
    </table>

## API を使用した鍵の表示
{: #api}

{{site.data.keyword.hscrypto}} API を使用して、鍵の内容を取得できます。

### 鍵のリストの取得
{: #retrieve-keys-api}

概要を参照するために、次のエンドポイントへの `GET` 呼び出しを行って、{{site.data.keyword.hscrypto}} のプロビジョン済みインスタンスで管理されている鍵を表示できます。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービス資格情報および認証資格情報を取得します](/docs/services/hs-crypto/access-api.html)。

2. 次の cURL コマンドを実行して、鍵に関する一般的な特性を表示します。

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    ご使用のアカウントの Cloud Foundry 組織およびスペース内で鍵の処理を行うには、`Bluemix-Instance` を、適切な `Bluemix-org` および `Bluemix-space` のヘッダーに置き換えます。 [詳しくは、{{site.data.keyword.hscrypto}} API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} を参照してください。
    {: tip}

    次の表に従って、例の要求内の変数を置き換えてください。
    <table>
      <tr>
        <th>変数</th>
        <th>説明</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>{{site.data.keyword.hscrypto}} サービス・インスタンスが存在している地理的領域を表す、地域の省略形 (例: <code>us-south</code> または <code>eu-gb</code>)。 詳しくは、<a href="/docs/services/hs-crypto/regions.html#endpoints">地域のサービス・エンドポイント</a>を参照してください。</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>{{site.data.keyword.cloud_notm}} アクセス・トークン。 Bearer 値を含む、<code>IAM</code> トークンの全コンテンツを cURL 要求に組み込みます。 詳しくは、<a href="/docs/services/hs-crypto/access-api.html#retrieve-token">アクセス・トークンの取得</a>を参照してください。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>{{site.data.keyword.hscrypto}} サービス・インスタンスに割り当てられた固有 ID。 詳しくは、<a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">インスタンス ID の取得</a>を参照してください。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>オプション: トランザクションを追跡し、相互に関連付けるために使用される固有 ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 2. {{site.data.keyword.hscrypto}} API を使用して鍵を表示するために必要な変数についての説明</caption>
    </table>

    `GET /v2/keys` 要求が成功すると、{{site.data.keyword.hscrypto}} サービス・インスタンス内の使用可能な鍵の集合が返されます。

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true,
          "imported": false
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {:screen}

    デフォルトでは、`GET /keys` は最初の 2000 個の鍵を返しますが、照会時に `limit` パラメーターを使用してこの制限を調整できます。 `limit` および `offset` について詳しくは、[鍵のサブセットの取得](#retrieve_subset_keys_api)を参照してください。
    {: tip}

### 鍵のサブセットの取得
{: #retrieve-subset-keys-api}

照会時に `limit` パラメーターおよび `offset` パラメーターを指定することによって、指定した `offset` 値から始まる、鍵のサブセットを取得できます。

例えば、{{site.data.keyword.hscrypto}} サービス・インスタンスに合計 3000 個の鍵を保管しているが、`GET /keys` 要求を行うときに 200 から 300 までの鍵を取得したい場合が考えられます。

以下の要求例を使用して、さまざまな鍵セットを取得できます。

  ```cURL
  curl -X GET \
  https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys?offset=<offset>&limit=<limit> \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'correlation-id: <correlation_ID>' \
  ```
  {: codeblock}

  次の表に従って、要求内の `limit` 変数と `offset` 変数を置き換えてください。
  <table>
    <tr>
      <th>変数</th>
      <th>説明</th>
    </tr>
    <tr>
      <td><p><varname>offset</varname></p></td>
      <td>
        <p>オプション: スキップする鍵の数。</p>
        <p>例えば、インスタンスに 50 個の鍵があって、26 個から 50 個までの鍵をリストしたい場合、<code>../keys?offset=25</code> を使用します。 <code>offset</code> を <code>limit</code> と組み合わせて、使用可能なリソースの一部を取り出すこともできます。</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>limit</varname></p></td>
      <td>
        <p>オプション: 取得する鍵の数。</p>
        <p>例えば、インスタンスに 100 個の鍵があって、10 個のみの鍵をリストしたい場合、<code>../keys?limit=10</code> を使用します。 <code>limit</code> の最大値は 5000 です。</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">表 2. <code>limit</code> 変数および <code>offset</code> 変数についての説明</caption>
  </table>

照会パラメーター `limit` および `offset` を設定する以下の例で、使用上の注意点を確認してください。

<table>
  <tr>
    <th>URL</th>
    <th>説明</th>
  </tr>
  <tr>
    <td><code>.../keys</code></td>
    <td>使用可能なリソースをすべてリストしますが、最初から 2000 個までの鍵が最大限です。</td>
  </tr>
  <tr>
    <td><code>.../keys?limit=10</code></td>
    <td>最初の 10 個の鍵をリストします。</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=25&limit=50</code></td>
    <td>26 から 50 までの鍵をリストします。</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=3000&limit=50</code></td>
    <td>3001 から 3050 までの鍵をリストします。</td>
  </tr>
  <caption style="caption-side:bottom;">表 3. 照会パラメーター limit および offset の使用上の注意</caption>
</table>

オフセットは、データ・セット内の特定の鍵の位置です。 `offset` 値はゼロが基準です。つまり、データ・セット内の 10 番目の暗号鍵はオフセット 9 の位置にあります。
{: tip}

### ID による鍵の取得
{: #retrieve-key-api}

特定の鍵に関する詳細情報を表示するには、次のエンドポイントに対して `GET` 呼び出しを行います。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービス資格情報および認証資格情報を取得します](/docs/services/hs-crypto/access-api.html)。

2. アクセスまたは管理する鍵の ID を取得します。

    この ID 値を使用して、鍵に関する詳細な情報 (鍵の素材自体など) にアクセスします。 `GET /v2/keys` 要求を行うか、{{site.data.keyword.hscrypto}} GUI にアクセスすることによって、指定された鍵の ID を取得できます。

3. 次の cURL コマンドを実行して、鍵と鍵の素材に関する詳細を取得します。

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    次の表に従って、例の要求内の変数を置き換えてください。

    <table>
      <tr>
        <th>変数</th>
        <th>説明</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>{{site.data.keyword.hscrypto}} サービス・インスタンスが存在している地理的領域を表す、地域の省略形 (例: <code>us-south</code> または <code>eu-gb</code>)。 詳しくは、<a href="/docs/services/hs-crypto/regions.html#endpoints">地域サービス・エンドポイント</a>を参照してください。</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>{{site.data.keyword.cloud_notm}} アクセス・トークン。 Bearer 値を含む、<code>IAM</code> トークンの全コンテンツを cURL 要求に組み込みます。 詳しくは、<a href="/docs/services/hs-crypto/access-api.html#retrieve-token">アクセス・トークンの取得</a>を参照してください。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>{{site.data.keyword.hscrypto}} サービス・インスタンスに割り当てられた固有 ID。 詳しくは、<a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">インスタンス ID の取得</a>を参照してください。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>オプション: トランザクションを追跡し、相互に関連付けるために使用される固有 ID。</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>[ステップ 1](#retrieve-keys-api) で取得した鍵の ID。</td>
      </tr>
      <caption style="caption-side:bottom;">表 4. {{site.data.keyword.hscrypto}} API を使用して指定の鍵を表示するために必要な変数についての説明</caption>
    </table>

    正常な `GET v2/keys/<key_ID>` 応答は、鍵と鍵の素材に関する詳細を返します。 以下の JSON オブジェクトは、標準鍵の戻り値の例を示しています。

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
            "mode": "GCM"
            },
            "extractable": true,
            "imported": false
        }
      ]
    }
    ```
    {:screen}

    使用可能なパラメーターについて詳しくは、{{site.data.keyword.hscrypto}} [REST API リファレンス資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} を参照してください。
