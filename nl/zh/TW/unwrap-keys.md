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

# 解除包裝金鑰
{: #unwrap-keys}

如果您是特許使用者，則可以透過 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} API 解除包裝資料加密金鑰 (DEK) 來存取其內容。解除包裝 DEK 會解密其內容並檢查內容完整性，並將原始金鑰資料傳回給 {{site.data.keyword.cloud_notm}} 資料服務。
{: shortdesc}

若要瞭解金鑰包裝如何協助您控制雲端中靜置資料的安全，請參閱[封套加密](/docs/services/key-protect/concepts/envelope-encryption.html)。

## 使用 API 解除包裝金鑰
{: #api}

[對服務發出 wrap 呼叫之後](/docs/services/hs-crypto/wrap-keys.html)，即可對下列端點發出 `POST` 呼叫，以解除包裝指定的資料加密金鑰 (DEK) 來存取其內容。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_id>?action=unwrap
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/hs-crypto/access-api.html)。

2. 複製您用來執行起始 wrap 要求之根金鑰的 ID。

    您可以擷取金鑰的 ID，方法是提出 `GET /v2/keys` 要求，或在 {{site.data.keyword.hscrypto}} GUI 中檢視金鑰。

3. 複製在起始 wrap 要求期間所傳回的 `ciphertext` 值。

4. 執行下列 cURL 指令，以解密及鑑別金鑰資料。

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

    若要在您帳戶的 Cloud Foundry 組織及空間內使用金鑰，請將 `Bluemix-Instance` 取代為適當的 `Bluemix-org` 及 `Bluemix-space` 標頭。[如需相關資訊，請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。
    {: tip}

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
        <td>您用於起始 wrap 要求之根金鑰的唯一 ID。</td>
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
        <td><varname>additional_data</varname></td>
        <td>選用項目：用來進一步保護金鑰的其他鑑別資料 (AAD)。每一個字串最多可以保留 255 個字元。如果您在對服務發出 wrap 呼叫時提供 AAD，則必須在 unwrap 呼叫期間指定相同的 AAD。</td>
      </tr>
      <tr>
        <td><varname>encrypted_data_key</varname></td>
        <td>在 wrap 作業期間所傳回的 <code>ciphertext</code> 值。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明在 {{site.data.keyword.hscrypto}} 中解除包裝金鑰所需的變數。</caption>
    </table>

    原始金鑰資料會在回應實體內文中傳回。下列 JSON 物件顯示回覆值範例。

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg=="
    }
    ```
    {:screen}
