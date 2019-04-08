---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: data encryption key, original key material, unwrap call

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 鍵のアンラッピング
{: #unwrap-keys}

特権ユーザーの場合、{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} API を使用して、データ暗号化鍵 (DEK) をアンラップして、内容にアクセスすることができます。 DEK をアンラップすると、暗号化解除して内容の保全性を確認し、元の鍵素材を {{site.data.keyword.cloud_notm}} データ・サービスに返します。
{: shortdesc}

鍵ラッピングが、クラウド内の保存データのセキュリティー管理にどのように役立つかについては、[エンベロープ暗号化](/docs/services/key-protect/concepts/envelope-encryption.html)を参照してください。

## API を使用した鍵のアンラッピング
{: #unwrap-key-api}

[サービスに対してラップ呼び出しを行った後](/docs/services/hs-crypto/wrap-keys.html)、以下のエンドポイントへの `POST` 呼び出しを行うことにより、指定のデータ暗号化鍵 (DEK) をアンラップして、その内容にアクセスできます。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_id>?action=unwrap
```
{: codeblock}

1. [サービス内で鍵の処理を行うために、サービス資格情報および認証資格情報を取得します](/docs/services/hs-crypto/access-api.html)。

2. 最初のラップ要求を実行するために使用したルート鍵の ID をコピーします。

    `GET /v2/keys` 要求を行うか、{{site.data.keyword.hscrypto}} GUI で鍵を表示することで、鍵の ID を取得できます。

3. 最初のラップ要求時に返された `ciphertext` 値をコピーします。

4. 次の cURL コマンドを実行して、鍵の素材を暗号化解除して認証します。

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=unwrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "ciphertext": "<encrypted_data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
    }'
    ```
    {: codeblock}
    <!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
        {: tip} -->

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
        <td>初期ラップ要求に使用したルート鍵の固有 ID。</td>
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
        <td><varname>return_preference</varname></td>
        <td><p><code>POST</code> および <code>DELETE</code> の操作に関するサーバーの動作を変更するヘッダー。</p><p><em>return_preference</em> 変数を <code>return=minimal</code> に設定すると、サービスは鍵のメタデータ (鍵の名前や ID 値など) のみを応答のエンティティー本体で返します。 変数を <code>return=representation</code> に設定すると、サービスは鍵の素材と鍵のメタデータの両方を返します。</p></td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>オプション: 鍵をさらにセキュアにするために使用される追加認証データ (AAD)。 各ストリングは、最大 255 文字を保持できます。 サービスに対してラップ呼び出しを行ったときに AAD を提供した場合は、アンラップ呼び出し時にも同じ AAD を指定する必要があります。</td>
      </tr>
      <tr>
        <td><varname>encrypted_data_key</varname></td>
        <td>ラップ操作時に返された <code>ciphertext</code> 値。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. {{site.data.keyword.hscrypto}} で鍵をアンラップするために必要な変数についての説明</caption>
    </table>

    元の鍵の素材が、応答のエンティティー本体で返されます。 以下の JSON オブジェクトは、返された値の例を示しています。

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg=="
    }
    ```
    {:screen}
