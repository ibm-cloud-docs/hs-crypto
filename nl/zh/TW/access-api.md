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

# 存取 API
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 整合了 {{site.data.keyword.keymanagementserviceshort}} REST API，可搭配任何程式設計語言用來儲存、擷取及產生金鑰。
{: shortdesc}

若要使用 API，您需要產生服務及鑑別認證。

## 擷取存取記號
{: #retrieve-token}

您可以從 {{site.data.keyword.iamshort}} 擷取存取記號，以向 {{site.data.keyword.hscrypto}} 進行鑑別。使用[服務 ID](/docs/iam/serviceid.html#serviceids)，您可以代表 {{site.data.keyword.cloud_notm}} 上或其外的服務或應用程式使用 {{site.data.keyword.hscrypto}} API，而不需要共用您的個人使用者認證。  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

請完成下列步驟，以擷取存取記號：

1. 在 {{site.data.keyword.cloud_notm}} 主控台中，移至**管理** &gt; **安全** &gt; **身分及存取** &gt; **服務 ID**。請遵循[建立服務 ID](/docs/iam/serviceid.html#creating-a-service-id) 的處理程序。
2. 使用**動作**功能表，以[定義新服務 ID 的存取原則](/docs/iam/serviceidaccess.html)。

如需管理 {{site.data.keyword.hscrypto}} 資源存取權的相關資訊，請參閱[角色及許可權](/docs/services/hs-crypto/manage-access.html#roles)。
3. 使用 **API 金鑰**區段，以[建立要與服務 ID 相關聯的 API 金鑰](/docs/iam/serviceid_keys.html#serviceidapikeys)。請將 API 金鑰下載至安全位置來進行儲存。
4. 呼叫 {{site.data.keyword.iamshort}} API 來擷取您的存取記號。

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \ 
    ```
    {: codeblock}

    在要求中，將 `<API_KEY>` 取代為步驟 3 所建立的 API 金鑰。下列的截斷範例會顯示記號輸出：

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

    使用前面加上 _Bearer_ 記號類型的完整 `access_token` 值，以程式設計方式使用 {{site.data.keyword.hscrypto}} API 來管理服務的金鑰。

    存取記號的有效時間為 1 小時，但您可以視需要重新產生它們。若要維護服務存取權，請呼叫 {{site.data.keyword.iamshort}} API 來定期重新整理 API 金鑰的存取記號。   
    {: tip }

## 擷取實例 ID
{: #retrieve-instance-ID}

您可以使用 [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview) 來擷取 {{site.data.keyword.hscrypto}} 服務實例的識別資訊。使用實例 ID 可管理您帳戶中指定 {{site.data.keyword.hscrypto}} 實例內的加密金鑰。

1. 使用 [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview) 登入 {{site.data.keyword.cloud_notm}}。

    ```sh
    ibmcloud login
    ```
    {: pre}

    **附註：**如果登入失敗，請執行 `ibmcloud login --sso` 指令再試一次。當您使用聯合 ID 登入時，需要 `--sso` 參數。如果使用這個選項，請前往 CLI 輸出中所列的鏈結，以產生一次性的通行碼。

2. 選取包含已佈建實例的帳戶。

    您可以執行 `ibmcloud resource service-instances` 來列出帳戶中所佈建的所有服務實例。

3. 擷取可唯一識別 {{site.data.keyword.hscrypto}} 服務實例的「雲端資源名稱 (CRN)」。

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    在後續指令中，將 `<instance_name>` 取代為您指派給 {{site.data.keyword.hscrypto}} 實例的唯一別名。下列截斷範例顯示 CLI 輸出。_42454b3b-5b06-407b-a4b3-34d9ef323901_ 值是範例實例 ID。

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## 擷取連線資訊
{: #retrieve-connection-info}

在您呼叫任何 {{site.data.keyword.keymanagementserviceshort}} API 之前，請先呼叫 **Retrieve the connection info** API 來擷取連線資訊。如需相關資訊，請參閱 [{{site.data.keyword.hscrypto}}API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto){: new_window}。

## 形成 API 要求
{: #form-api-request}

對服務發出 API 呼叫時，會根據最初佈建 {{site.data.keyword.hscrypto}} 實例的方式來建構 API 要求。

若要建置您的要求，請將[地區服務端點](/docs/services/hs-crypto/regions.html)與適當的鑑別認證配對。例如，如果您已建立 `us-south` 地區的服務實例，請使用下列端點及 API 標頭來瀏覽服務中的金鑰：

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### 下一步為何？
{: #api-next}

若要進一步瞭解如何以程式設計方式管理您的金鑰，[請參閱 {{site.data.keyword.hscrypto}} API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://{DomainName}/apidocs/hs-crypto){: new_window}。

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}. -->
