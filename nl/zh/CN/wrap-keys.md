---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root key, data encryption key, Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 打包密钥
{: #wrap-keys}

如果您是特权用户，那么可以使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} API 通过根密钥来管理和保护加密密钥。
{: shortdesc}

使用根密钥打包数据加密密钥 (DEK) 时，{{site.data.keyword.hscrypto}} 结合了多种算法的优势来保护加密数据的隐私性和完整性。  

要了解密钥打包如何帮助您控制云中静态数据的安全性，请参阅[包络加密](/docs/services/key-protect/concepts/envelope-encryption.html)。

## 使用 API 打包密钥
{: #api}

可以使用在 {{site.data.keyword.hscrypto}} 中管理的根密钥来保护指定的数据加密密钥 (DEK)。

**重要信息：**提供用于打包的根密钥时，请确保根密钥为 256 位、384 位或 512 位，这样打包调用才能成功。如果在服务中创建根密钥，那么 {{site.data.keyword.hscrypto}} 将从其 HSM 生成 AES-GCM 算法支持的 256 位密钥。

[在服务中指定根密钥后](/docs/services/hs-crypto/create-root-keys.html)，可以通过对以下端点发出 `POST` 调用以高级加密方式来打包 DEK。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [检索服务和认证凭证以与服务中的密钥一起使用](/docs/services/hs-crypto/access-api.html)。

2. 复制要管理和保护的 DEK 的密钥资料。

如果您具有对 {{site.data.keyword.hscrypto}} 服务实例的管理者或写入者特权，那么[可以通过发出 `GET /v2/keys/<key_ID>` 请求来检索特定密钥的密钥资料](/docs/services/hs-crypto/view-keys.html#api)。

3. 复制要用于打包的根密钥的标识。

4. 运行以下 cURL 命令以使用打包操作保护密钥。

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

要使用帐户中 Cloud Foundry 组织和空间内的密钥，请将 `Bluemix-Instance` 替换为相应的 `Bluemix-org` 和 `Bluemix-space` 头。[有关更多信息，请参阅 {{site.data.keyword.hscrypto}} API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
    {: tip}

    根据下表替换示例请求中的变量。

    <table>
      <tr>
        <th>变量</th>
        <th>描述</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>区域缩写（例如，<code>us-south</code> 或 <code>eu-gb</code>），表示 {{site.data.keyword.hscrypto}} 服务实例所在的地理区域。有关更多信息，请参阅<a href="/docs/services/hs-crypto/regions.html#endpoints">区域服务端点</a>。</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>要用于打包的根密钥的唯一标识。</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>您的 {{site.data.keyword.cloud_notm}} 访问令牌。在 cURL 请求中包含 <code>IAM</code> 令牌的完整内容，包括 Bearer 值。有关更多信息，请参阅<a href="/docs/services/hs-crypto/access-api.html#retrieve-token">检索访问令牌</a>。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>指定给您的 {{site.data.keyword.hscrypto}} 服务实例的唯一标识。有关更多信息，请参阅<a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">检索实例标识</a>。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>可选：用于跟踪和关联事务的唯一标识。</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>标头，用于更改 <code>POST</code> 和 <code>DELETE</code> 操作的服务器行为。</p><p>将 <em>return_preference</em> 变量设置为 <code>return=minimal</code> 时，服务在响应的 entity-body 中仅返回密钥元数据，如密钥名称和标识值。在将变量设置为 <code>return=representation</code> 时，服务会返回密钥资料和密钥元数据。</p></td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td>可选：要管理和保护的 DEK 的密钥资料。<code>plaintext</code> 值必须采用 Base64 编码。要生成新的 DEK，请省略 <code>plaintext</code> 属性。服务会生成随机明文（32 个字节）并对该值进行打包。</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>可选：用于进一步确保密钥安全的附加认证数据 (AAD)。每个字符串可含有最多 255 个字符。如果在向服务发出打包调用时提供了 AAD，那么在随后的解包调用期间必须指定同一 AAD。<br></br>重要信息：{{site.data.keyword.hscrypto}} 服务不会保存其他认证数据。如果提供 AAD，请将数据保存到安全位置，以确保您可以在随后的解包请求期间访问并提供同一 AAD。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述对 {{site.data.keyword.hscrypto}} 中的指定密钥进行打包所需的变量
。</caption>
    </table>

    打包的密钥（包含 base64 编码的密钥资料）会在响应的 entity-body 中返回。以下 JSON 对象显示返回值示例。

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
