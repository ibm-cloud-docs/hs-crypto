---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root keys, Rotate key, key rotation

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# 鍵のローテート
{: #rotating-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} を使用して、ルート鍵をオンデマンドでローテートできます。
{: shortdesc}

マスター鍵のローテートは、現在サポートされていません。
{: important}

ルート鍵をローテートすると、鍵の存続期間が短くなり、その鍵で保護される情報量が制限されます。   

鍵のローテーションがどのように業界標準や暗号のベスト・プラクティスへの準拠に役立つのかについては、『[鍵のローテーション](/docs/services/key-protect/concepts/key-rotation.html)』を参照してください。

ローテーションは、ルート鍵に対してのみ使用可能です。
{: tip}

## GUI を使用したルート鍵のローテート
{: #gui}

グラフィカル・インターフェースを使用してルート鍵をローテートする場合は、{{site.data.keyword.hscrypto}} GUI を使用できます。

[サービス内にルート鍵を作成するか、既存のルート鍵をインポートした後](/docs/services/hs-crypto/create-root-keys.html)、鍵をローテートするには以下のステップを実行します。

1. [{{site.data.keyword.cloud_notm}} コンソール ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン") にログインします](https://cloud.ibm.com/){: new_window}。
2. {{site.data.keyword.cloud_notm}} ダッシュボードで、{{site.data.keyword.hscrypto}} のプロビジョン済みインスタンスを選択します。
3. **「鍵 (Keys)」**テーブルを使用して、サービス内の鍵を表示します。
4. 「⋮」アイコンをクリックして、ローテートする鍵に関するオプションのリストを開きます。
5. オプション・メニューで**「鍵のローテート (Rotate key)」**をクリックし、次の画面でローテーションを確認します。

ルート鍵を最初にインポートした場合、鍵をローテートするには、 新しい Base64 エンコードの鍵素材を指定する必要があります。 詳しくは、[GUI を使用したルート鍵のインポート](/docs/services/hs-crypto/import-root-keys.html#gui)を参照してください。
{: tip}

## API を使用したルート鍵のローテート
{: #api}

[サービス内でルート鍵を指定した後](/docs/services/hs-crypto/create-root-keys.html)、以下のエンドポイントへの `POST` 呼び出しを行うことにより、鍵をローテートできます。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービスおよび認証の資格情報を取得します。](/docs/services/hs-crypto/access-api.html)

2. ローテートするルート鍵の ID をコピーします。

4. 以下の cURL コマンドを実行して、鍵を新しい鍵素材に置き換えます。

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <key_material>'
      }'
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
        <td>{{site.data.keyword.hscrypto}} サービス・インスタンスが存在している地理的領域を表す、地域の省略形 (例: <code>us-south</code> または <code>eu-gb</code>)。 詳しくは、<a href="/docs/services/hs-crypto/regions.html#endpoints">地域のサービス・エンドポイント</a>を参照してください。</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>ローテートするルート鍵の固有 ID。</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>サービスで保管および管理する、base64 エンコードの鍵素材。 この値は、サービスへの鍵の追加時に鍵素材を最初にインポートした場合に必要になります。</p>
          <p>{{site.data.keyword.hscrypto}} によって最初に生成された鍵をローテートする場合は、<code>payload</code> 属性を省略し、空の要求エンティティー本体を渡します。 インポートした鍵をローテートする場合は、以下の要件を満たしている鍵素材を指定します。</p>
          <p>
            <ul>
              <li>鍵は 256 ビット、384 ビット、または 512 ビットでなければならない。</li>
              <li>データのバイト数 (例えば、256 ビットの場合は 32 バイト) は、base64 エンコードを使用してエンコードされていなければならない。</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.hscrypto}} で指定の鍵をローテートするために必要な変数についての説明</caption>
    </table>

    ローテーション要求が成功すると、HTTP `204 No Content` 応答が返されます。これは、ルート鍵が新しい鍵素材に置き換えられたことを示しています。

4. オプション: 次の呼び出しを実行して {{site.data.keyword.hscrypto}} サービス・インスタンス内の鍵を表示し、鍵がローテートされたことを確認します。

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    応答エンティティー本体内の `lastRotateDate` の値を確認して、鍵が最後にローテートされた日時を調べます。
