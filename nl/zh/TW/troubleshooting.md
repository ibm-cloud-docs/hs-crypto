---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# 疑難排解
{: #troubleshooting}

使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 的一般問題可能包括當您與 API 互動時提供正確的標頭或認證。在許多情況下，您可以遵照一些簡單的步驟，從這些問題回復。
{: shortdesc}

## 刪除已起始設定的 {{site.data.keyword.hscrypto}} 實例時發生錯誤

當您刪除已起始設定的 {{site.data.keyword.hscrypto}} 實例時，可能會收到類似下列內容的錯誤：

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

在您刪除已起始設定的 {{site.data.keyword.hscrypto}} 實例之前，尚未清除（歸零）該實例。
{: tsCauses}

請在刪除實例之前執行下列指令：
{: tsResolve}

```
ibmcloud tke domain-zeroize
```
{: codeblock}

## 執行與授信金鑰登錄外掛程式相關的指令之後，記號未獲授權

在您執行 `tke` CLI 指令之後，可能會收到類似下列內容的訊息：

```
ibmcloud tke domains
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

記號未重新整理。
{: tsCauses}

請使用 `ibmcloud login` 指令再次登入 {{site.data.keyword.cloud_notm}}，以重新整理記號。
{: tsResolve}

## 使用 CLI 或 API 時收到 `error CKR_IBM_WK_NOT_INITIALIZED`

當您使用 CLI 或 API 時，可能會收到類似下列內容的錯誤訊息：

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

當您執行 `ibmcloud tke domain-compare` 指令時，未在 CURRENT MASTER KEY REGISTER 上取得 `Valid` 配置。
{: tsCauses}

請確定 HSM 主要金鑰已正確設定。
{: tsResolve}

## 無法建立或刪除金鑰
{: #unable-to-create-keys}

當您存取 {{site.data.keyword.hscrypto}} 使用者介面時，看不到新增或刪除金鑰的選項。

從 {{site.data.keyword.cloud_notm}} 儀表板中，選取您的 {{site.data.keyword.hscrypto}} 服務實例。
{: tsSymptoms}

您可以看到金鑰清單，但看不到新增或刪除金鑰的選項。

您沒有正確的授權可執行 {{site.data.keyword.hscrypto}} 動作。
{: tsCauses}

請向管理者確認已將適當資源群組或服務實例中的正確角色指派給您。如需角色的相關資訊，請參閱[角色及許可權](/docs/services/key-protect/manage-access.html#roles)。
{: tsResolve}

## 取得協助與支援
{: #getting-help}

如果您在使用 {{site.data.keyword.hscrypto}} 時有問題或疑問，則可以檢查 {{site.data.keyword.cloud_notm}}，或是搜尋資訊或透過討論區提問來取得協助。您也可以開立支援問題單。
{: shortdesc}

您可以移至[狀態頁面 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/status?tags=platform,runtimes,services)，以檢查 {{site.data.keyword.cloud_notm}} 是否可用。

您可以檢閱討論區，看看是否其他使用者也遇到相同問題。使用討論區提問時，請標記您的問題，以便 {{site.data.keyword.cloud_notm}} 開發團隊能看到它。

- 如果您有 {{site.data.keyword.hscrypto}} 的相關技術問題，請將問題張貼在 [Stack Overflow ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://stackoverflow.com/){: new_window}，並使用 "ibm-cloud" 和 "hyperprotect-crypto" 來標記問題。
- 若為服務及開始使用指示的相關問題，請使用 [IBM developerWorks dW Answers ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/answers/index.html){: new_window} 討論區。請包含 "ibm-cloud" 和 "hyperprotect-crypto" 標籤。

如需使用討論區的詳細資料，請參閱[取得協助 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/docs/support/index.html#getting-help){: new_window}。

如需開立 {{site.data.keyword.IBM_notm}} 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[與支援中心聯絡 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cloud.ibm.com/docs/support/index.html#contacting-support){: new_window}。
