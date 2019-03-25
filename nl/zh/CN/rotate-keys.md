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

# 轮换密钥
{: #rotating-keys}

您可以使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 按需轮换根密钥。
{: shortdesc}

当前不支持轮换主密钥。
{: important}

轮换根密钥可缩短密钥的生命周期，并限制受密钥保护的信息量。   

要了解密钥轮换如何帮助您符合行业标准和加密最佳实践，请参阅[密钥轮换](/docs/services/key-protect/concepts/key-rotation.html)。

轮换仅适用于根密钥。
{: tip}

## 使用 GUI 轮换根密钥
{: #gui}

如果想要使用图形界面来轮换根密钥，那么可以使用 {{site.data.keyword.hscrypto}} GUI。

[在创建根密钥或将现有根密钥导入到服务后](/docs/services/hs-crypto/create-root-keys.html)，请完成以下步骤来轮换密钥：

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/){: new_window}。
2. 从 {{site.data.keyword.cloud_notm}} 仪表板，选择 {{site.data.keyword.hscrypto}} 的已供应实例。
3. 使用**密钥**表以浏览服务中的密钥。
4. 单击 ⋮ 图标以打开要轮换的密钥的选项列表。
5. 从选项菜单中，单击**轮换密钥**，然后在下一个屏幕中进行确认。

如果最初导入的是根密钥，那么必须提供新的 Base64 编码的密钥资料，才能轮换密钥。有关更多信息，请参阅[使用 GUI 导入根密钥](/docs/services/hs-crypto/import-root-keys.html#gui)。
{: tip}

## 使用 API 轮换根密钥
{: #api}

[在服务中指定根密钥后](/docs/services/hs-crypto/create-root-keys.html)，可以通过对以下端点发出 `POST` 调用来轮换密钥。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [检索服务和认证凭证以与服务中的密钥一起使用](/docs/services/hs-crypto/access-api.html)。

2. 复制要轮换的根密钥的标识。

4. 运行以下 cURL 命令，将密钥替换为新的密钥资料。

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
        <td>要轮换的根密钥的唯一标识。</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>要在服务中存储和管理的 Base64 编码的密钥资料。如果最初在将密钥添加到服务时导入了密钥资料，那么此值是必需的。</p>
          <p>要轮换最初由 {{site.data.keyword.hscrypto}} 生成的密钥，请省略 <code>payload</code> 属性并传递空请求 entity-body。要轮换已导入的密钥，请提供满足以下需求的密钥资料：</p>
          <p>
            <ul>
              <li>密钥必须为 256 位、384 位或 512 位。</li>
              <li>数据字节（例如，对于 256 位，为 32 个字节）必须使用 Base64 编码进行编码。</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述在 {{site.data.keyword.hscrypto}} 中轮换指定密钥时所需的变量。</caption>
    </table>

    成功的轮换请求会返回 HTTP `204 No Content` 响应，这表示根密钥已替换为新的密钥资料。

4. 可选：通过运行以下调用来浏览 {{site.data.keyword.hscrypto}} 服务实例中的密钥，以验证是否轮换了密钥。

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    查看响应 entity-body 中的 `lastRotateDate` 值，以检查密钥的上次轮换日期和时间。
