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

# 管理对密钥的访问权
{: #manage-access-api}

使用 {{site.data.keyword.iamlong}} 可以通过创建和修改访问策略，对加密密钥启用精确的访问控制。
{: shortdesc}

此页面将引导您完成几个方案，以使用[访问管理 API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window} 来管理加密密钥的访问权。

## 开始之前
{: #prereqs}

要使用 API，请生成认证凭证，例如，[访问令牌](/docs/services/hs-crypto/access-api.html#retrieve-token)和[实例标识](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID)。您还需要想要管理其访问权的 {{site.data.keyword.hscrypto}} 密钥的标识。

要了解如何查看密钥标识，请参阅[查看密钥](/docs/services/hs-crypto/view-keys.html)。
{: tip}

### 检索帐户标识
{: #retrieve-account-ID}

在检索凭证后，通过检索包含 {{site.data.keyword.hscrypto}} 服务实例的帐户的标识，确定新访问策略的访问权作用域。

要检索帐户标识，请完成以下步骤：

1. 登录到 {{site.data.keyword.cloud_notm}} CLI。
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **注**：使用联合标识登录时需要 `--sso` 参数。如果使用此选项，请转至 CLI 输出中列出的链接以生成一次性密码。

    结果显示帐户的识别信息。

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

2. 复制帐户标识的值。

    _b6hnh3560ehqjkf89s4ba06i367801e_ 值是示例帐户标识。

### 检索用户标识
{: #retrieve-user-ID}

检索要修改其访问权的用户的用户标识。

要检索用户标识，请完成以下步骤：

1. [要求用户提供 IAM 令牌](/docs/services/hs-crypto/access-api.html#retrieve-token)。
    IAM 令牌结构如下：

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. 复制中间值并运行以下命令：
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    结果显示类似于以下示例的 JSON 对象：
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

4. 复制 `id` 属性的值。

## 创建访问策略
{: #create-policy}

要启用特定密钥的访问控制，您可以通过运行以下命令，向 {{site.data.keyword.iamshort}} 发送请求。针对每个访问策略，重复该命令。

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

如果需要管理对指定 Cloud Foundry 组织和空间内密钥的访问权，请将 `serviceInstance` 替换为 `organizationId` 和 `spaceId`。要了解更多信息，请参阅 [Access Management API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}。
{: tip}

将 `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` 和 `<key_ID>` 替换为相应的值。

**可选：**验证是否已成功创建策略。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## 更新访问策略
{: #update-policy}

您可以使用检索到的策略标识，为用户修改现有策略。通过运行以下命令，向 {{site.data.keyword.iamshort}} 发送请求：

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

将 `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` 和 `<key_ID>` 替换为相应的值。

**可选：**验证是否已成功更新策略。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## 删除访问策略
{: #delete-policy}

您可以使用检索到的策略标识，为用户删除现有策略。通过运行以下命令，向 {{site.data.keyword.iamshort}} 发送请求：

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

将 `<account_ID>`, `<user_ID>`, `<policy_ID>` 和 `<Admin_IAM_token>` 替换为相应的值。

**可选：**验证是否已成功删除策略。

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
