---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root keys, create root keys, Hyper Protect Crypto Services GUI, symmetric key

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 创建根密钥
{: #create-root-keys}

可以使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 通过 {{site.data.keyword.hscrypto}} GUI 来创建根密钥，也可以通过 {{site.data.keyword.hscrypto}} API 以编程方式来创建根密钥。
{: shortdesc}

根密钥是用于保护云中已加密数据的安全性的对称密钥打包密钥。有关根密钥的更多信息，请参阅[包络加密](/docs/services/key-protect/concepts/envelope-encryption.html)。

## 使用 GUI 创建根密钥
{: #root-key-gui}

[创建服务的实例后](/docs/services/hs-crypto/provision.html)，请完成以下步骤以使用 {{site.data.keyword.hscrypto}} GUI 来创建根密钥。

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/){: new_window}。
2. 转至**菜单** &gt; **资源列表**，以查看您的资源列表。
3. 从 {{site.data.keyword.cloud_notm}} 资源列表，选择 {{site.data.keyword.hscrypto}} 的已供应实例。
4. 要创建新密钥，请单击**添加密钥**，然后选择**创建密钥**窗口。

    指定密钥的详细信息：

    <table>
      <tr>
        <th>设置</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>
          <p>密钥的人类可读的唯一别名，以便可轻松识别密钥。</p>
          <p>为保护隐私，请确保密钥名称不包含个人可标识信息 (PII)，例如，姓名或位置。</p>
        </td>
      </tr>
      <tr>
        <td>密钥类型</td>
        <td>要在 {{site.data.keyword.hscrypto}} 中管理的<a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">密钥类型</a>。从密钥类型列表中，选择<b>根密钥</b>。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述<b>生成新密钥</b>设置</caption>
    </table>

5. 填写完密钥详细信息后，单击**创建密钥**以进行确认。

服务中创建的密钥是 AES-CBC 算法支持的 256 位对称密钥。为了提高安全性，密钥通过位于安全 {{site.data.keyword.cloud_notm}} 数据中心且通过 FIPS 140-2 4 级认证的硬件安全模块 (HSM) 生成。

## 使用 API 创建根密钥
{: #root-key-api}

通过对以下端点执行 `POST` 调用来创建根密钥。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [检索服务和认证凭证以与服务中的密钥一起使用](/docs/services/hs-crypto/access-api.html)。

2. 使用以下 cURL 命令调用 [{{site.data.keyword.hscrypto}} API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto){: new_window}。

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
     "metadata": {
"collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "extractable": <key_type>
       }
     ]
    }'
    ```
    {: codeblock}
<!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
    {: tip} -->

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
        <td><varname>IAM_token</varname></td>
        <td>您的 {{site.data.keyword.cloud_notm}} 访问令牌。在 cURL 请求中包含 <code>IAM</code> 令牌的完整内容，包括 Bearer 值。有关更多信息，请参阅<a href="/docs/services/hs-crypto/access-api#retrieve-token">检索访问令牌</a>。</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>指定给您的 {{site.data.keyword.hscrypto}} 服务实例的唯一标识。有关更多信息，请参阅<a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">检索实例标识</a>。</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>用于跟踪和关联事务的唯一标识。</td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>密钥的人类可读的唯一名称，以便可轻松识别密钥。</p>
          <p>重要信息：为保护隐私，请勿将个人数据存储为密钥的元数据。</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>可选：密钥的扩展描述。</p>
          <p>重要信息：为保护隐私，请勿将个人数据存储为密钥的元数据。</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>可选：密钥在系统中到期的日期和时间（RFC 3339 格式）。如果省略了 <code>expirationDate</code> 属性，那么密钥不会到期。</td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>布尔值，用于确定密钥资料是否可以离开服务。</p>
          <p>将 <code>extractable</code> 属性设置为 <code>false</code> 时，服务会创建可用于 <code>wrap</code> 或 <code>unwrap</code> 操作的根密钥。</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">表 2. 描述使用 {{site.data.keyword.hscrypto}} API 添加根密钥所需的变量</caption>
    </table>

    为保护个人数据的机密性，在向服务添加密钥时，避免输入个人可标识信息 (PII)，例如，姓名或位置。有关 PII 的更多示例，请参阅 [NIST Special Publication 800-122 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window} 的第 2.2 节。
    {: tip}

    成功的 `POST /v2/keys` 响应会返回密钥的标识值以及其他元数据。标识是指定给密钥的唯一标识，用于后续调用 {{site.data.keyword.hscrypto}} API。

3. 可选：通过运行以下调用来浏览 {{site.data.keyword.hscrypto}} 服务实例中的密钥，以验证是否创建了密钥。

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**注：**使用该服务创建根密钥后，该密钥会始终位于 {{site.data.keyword.hscrypto}} 的边界内，并且无法检索其密钥资料。

### 后续工作
{: #root-key-next}

- 要了解有关使用包络加密保护密钥的更多信息，请查看[打包密钥](/docs/services/hs-crypto/wrap-keys.html)。
- 要了解有关以编程方式管理密钥的更多信息，请[查看 {{site.data.keyword.hscrypto}} API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto){: new_window}。
