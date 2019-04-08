---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root key, data encryption key, Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 包裝金鑰
{: #wrap-keys}

如果您是特許使用者，則可以透過 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} API 利用根金鑰來管理及保護加密金鑰。
{: shortdesc}

當您使用根金鑰來包裝資料加密金鑰 (DEK) 時，{{site.data.keyword.hscrypto}} 會結合多種演算法的優勢，用來保護加密資料的隱私及完整性。  

若要瞭解金鑰包裝如何協助您控制雲端中靜置資料的安全，請參閱[封套加密](/docs/services/key-protect/concepts/envelope-encryption.html)。

## 使用 API 包裝金鑰
{: #wrap-keys-api}

您可以使用您在 {{site.data.keyword.hscrypto}} 中管理的根金鑰來保護指定的資料加密金鑰 (DEK)。

當您提供用於包裝的根金鑰時，請確定根金鑰是 128、192 或 256 位元，以讓 wrap 呼叫成功。如果您在服務中建立根金鑰，{{site.data.keyword.hscrypto}} 會從其 HSM 產生 AES-CBC 演算法所支援的 256 位元金鑰。

[在服務中指定根金鑰之後](/docs/services/hs-crypto/create-root-keys.html)，即可對下列端點發出 `POST` 呼叫，以使用進階加密來包裝 DEK。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/hs-crypto/access-api.html)。

2. 複製您要管理及保護之 DEK 的金鑰資料。

    如果您擁有 {{site.data.keyword.hscrypto}} 服務實例的管理員或撰寫者專用權，[您可以發出 `GET /v2/keys/<key_ID>` 要求來擷取指定金鑰的金鑰資料](/docs/services/hs-crypto/view-keys.html#api)。

3. 複製您要用於包裝之根金鑰的 ID。

4. 執行下列 cURL 指令，以使用 wrap 作業來保護金鑰。

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
    }'
    ```
    {: codeblock}
    <!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
        {: tip} -->

    根據下表取代範例要求中的變數。

    <table>
      <tr>
        <th>變數</th>
        <th>說明</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>代表 {{site.data.keyword.hscrypto}} 服務實例所在地理區域的地區縮寫，例如 <code>us-south</code> 或 <code>eu-gb</code>。如需相關資訊，請參閱<a href="/docs/services/hs-crypto/regions.html#endpoints">地區服務端點</a>。</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>您要用於包裝之根金鑰的唯一 ID。</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>您的 {{site.data.keyword.cloud_notm}} 存取記號。請在 cURL 要求中包含 <code>IAM</code> 記號的完整內容，包括 Bearer 值。如需相關資訊，請參閱<a href="/docs/services/hs-crypto/access-api.html#retrieve-token">擷取存取記號</a>。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>指派給您的 {{site.data.keyword.hscrypto}} 服務實例的唯一 ID。如需相關資訊，請參閱<a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">擷取實例 ID</a>。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>選用項目：用來追蹤及關聯交易的唯一 ID。</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>變更 <code>POST</code> 及 <code>DELETE</code> 作業之伺服器行為的標頭。</p><p>當您將 <em>return_preference</em> 變數設為 <code>return=minimal</code> 時，服務在回應實體內文中只會傳回金鑰 meta 資料（例如金鑰名稱及 ID 值）。當您將變數設為 <code>return=representation</code> 時，服務會傳回金鑰資料及金鑰 meta 資料。</p></td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td>選用項目：您要管理及保護之 DEK 的金鑰資料。<code>plaintext</code> 值必須以 base64 編碼。若要產生新的 DEK，請省略 <code>plaintext</code> 屬性。此服務會產生隨機純文字（32 個位元組），並包裝該值。</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>選用項目：用來進一步保護金鑰的其他鑑別資料 (AAD)。每一個字串最多可以保留 255 個字元。如果您在對服務發出 wrap 呼叫時提供 AAD，則必須在後續 unwrap 呼叫期間指定相同的 AAD。<br></br>重要事項：{{site.data.keyword.hscrypto}} 服務不會儲存其他鑑別資料。如果您提供 AAD，請將資料儲存到安全的位置，以確保您可以在後續的 unwrap 要求期間存取及提供相同的 AAD。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明在 {{site.data.keyword.hscrypto}} 中包裝指定金鑰所需的變數。</caption>
    </table>

    已包裝金鑰（包含以 base64 編碼的金鑰資料）會在回應實體內文中傳回。下列 JSON 物件顯示回覆值範例。

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
