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

# 管理金鑰的存取
{: #manage-access-api}

使用 {{site.data.keyword.iamlong}}，您可以建立及修改存取原則，為加密金鑰啟用精細的存取控制。
{: shortdesc}

此頁面帶領您查看數個情境，使用[存取管理 API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window} 管理加密金鑰的存取權。

## 在開始之前
{: #prereqs}

若要使用 API，請產生鑑別認證（例如[存取記號](/docs/services/hs-crypto/access-api.html#retrieve-token)及[實例 ID](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID)）。您也需要要管理其存取權的 {{site.data.keyword.hscrypto}} 金鑰 ID。

若要瞭解如何檢視金鑰 ID，請參閱[檢視金鑰](/docs/services/hs-crypto/view-keys.html)。
{: tip}

### 擷取帳戶 ID
{: #retrieve-account-ID}

在您擷取認證之後，請擷取包含 {{site.data.keyword.hscrypto}} 服務實例的帳戶 ID 來判定新存取原則的存取範圍。

若要擷取帳戶 ID，請完成下列步驟：

1. 登入 {{site.data.keyword.cloud_notm}} CLI。
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **附註**：當您使用聯合 ID 登入時，需要 `--sso` 參數。如果使用這個選項，請前往 CLI 輸出中所列的鏈結，以產生一次性的通行碼。

    結果會顯示您帳戶的識別資訊。

    ```sh
    Authenticating...
    OK

    

    Select an account (or press enter to skip):

    

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. 複製帳戶 ID 的值。

    _b6hnh3560ehqjkf89s4ba06i367801e_ 值是範例帳戶 ID。

### 擷取使用者 ID
{: #retrieve-user-ID}

擷取您要修改其存取權的使用者 ID。

若要擷取使用者 ID，請完成下列步驟：

1. [要求使用者提供 IAM 記號](/docs/services/hs-crypto/access-api.html#retrieve-token)。
    IAM 記號結構如下：

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. 複製中間值，並執行下列指令：
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    結果顯示類似於下列範例的 JSON 物件：
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

4. 複製 `id` 內容的值。

## 建立存取原則
{: #create-policy}

若要啟用特定金鑰的存取控制，您可以藉由執行下列指令，傳送要求至 {{site.data.keyword.iamshort}}。請針對每個存取原則重複指令。

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

如果您需要管理所指定 Cloud Foundry 組織及空間內金鑰的存取，請將 `serviceInstance` 取代為 `organizationId` 及 `spaceId`。若要進一步瞭解，請參閱[存取管理 API 參考資料文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}。
{: tip}

在後續指令中，將 `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` 及 `<key_ID>` 取代為適當值。

**選用項目：**確認已順利建立原則。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## 更新存取原則
{: #update-policy}

您可以使用擷取到的原則 ID，以修改使用者的現有原則。藉由執行下列指令，傳送要求至 {{site.data.keyword.iamshort}}：

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

在後續指令中，將 `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` 及 `<key_ID>` 取代為適當值。

**選用項目：**確認已順利更新原則。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## 刪除存取原則
{: #delete-policy}

您可以使用擷取到的原則 ID，以刪除使用者的現有原則。藉由執行下列指令，傳送要求至 {{site.data.keyword.iamshort}}：

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

在後續指令中，將 `<account_ID>`, `<user_ID>`, `<policy_ID>` 及 `<Admin_IAM_token>` 取代為適當值。

**選用項目：**確認已順利刪除原則。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
