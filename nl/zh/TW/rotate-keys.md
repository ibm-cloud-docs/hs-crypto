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

# 替換金鑰
{: #rotating-keys}

您可以使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 依需求替換根金鑰。
{: shortdesc}

目前不支援替換主要金鑰。
{: important}

當您替換根金鑰時，會縮短金鑰的生命期限，並限制該金鑰所保護的資訊數量。   

若要瞭解金鑰替換如何協助您符合業界標準及加密的最佳作法，請參閱[金鑰替換](/docs/services/key-protect/concepts/key-rotation.html)。

替換功能只適用於根金鑰。
{: tip}

## 使用 GUI 替換根金鑰
{: #gui}

如果您偏好使用圖形介面來替換根金鑰，可以使用 {{site.data.keyword.hscrypto}} GUI。

[在建立根金鑰或將現有根金鑰匯入到服務之後](/docs/services/hs-crypto/create-root-keys.html)，請完成下列步驟來替換金鑰：

1. [登入 {{site.data.keyword.cloud_notm}} 主控台 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/){: new_window}。
2. 從 {{site.data.keyword.cloud_notm}} 儀表板，選取已佈建的 {{site.data.keyword.hscrypto}} 實例。
3. 使用**金鑰**表格，以瀏覽服務中的金鑰。
4. 按一下 ⋮ 圖示，以開啟您要替換之金鑰的選項清單。
5. 從選項功能表中，按一下**替換金鑰**，並在下一個畫面中確認替換金鑰。

如果一開始就匯入了根金鑰，則必須提供以 base64 編碼的新金鑰資料來替換該金鑰。如需相關資訊，請參閱[使用 GUI 匯入根金鑰](/docs/services/hs-crypto/import-root-keys.html#gui)。
{: tip}

## 使用 API 替換根金鑰
{: #api}

[在服務中指定根金鑰之後](/docs/services/hs-crypto/create-root-keys.html)，即可對下列端點發出 `POST` 呼叫來替換金鑰。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [擷取服務及鑑別認證以在服務中使用金鑰](/docs/services/hs-crypto/access-api.html)。

2. 複製您要替換之根金鑰的 ID。

4. 執行下列 cURL 指令，將金鑰取代為新的金鑰資料。

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
        <td>您要替換之根金鑰的唯一 ID。</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>您要在服務中儲存及管理並以 base64 編碼的金鑰資料。如果在將金鑰新增至服務時一開始就匯入了金鑰資料，則這個值為必要項目。</p>
          <p>若要替換 {{site.data.keyword.hscrypto}} 最初產生的金鑰，請省略 <code>payload</code> 屬性並傳遞空的要求實體內文。若要替換匯入的金鑰，請提供符合下列需求的金鑰資料：</p>
          <p>
            <ul>
              <li>金鑰必須是 256、384 或 512 位元。</li>
              <li>必須使用 base64 編碼來編碼資料位元組（例如 32 位元組適用於 256 位元）。</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 說明在 {{site.data.keyword.hscrypto}} 中替換指定金鑰所需的變數。</caption>
    </table>

    順利完成的替換要求會傳回 HTTP `204 No Content` 回應，其指出新的金鑰資料已取代您的根金鑰。

4. 選用項目：執行下列呼叫來瀏覽 {{site.data.keyword.hscrypto}} 服務實例中的金鑰，確認已替換金鑰。

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    請檢閱回應實體內文中的 `lastRotateDate` 值，以檢查前次替換金鑰的日期和時間。
