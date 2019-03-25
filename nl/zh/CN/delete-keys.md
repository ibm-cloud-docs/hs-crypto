---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: details of the DELETE request, delete encryption key, deleting keys, Variable Description region

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 删除密钥
{: #deleting-keys}

如果您是 {{site.data.keyword.cloud_notm}} 空间或 {{site.data.keyword.hscrypto}} 服务实例的管理员，那么您可以使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 来删除加密密钥及其内容。
{: shortdesc}

**重要信息**：删除密钥时，会永久粉碎其内容和关联的数据。该操作无法撤销。建议不要对生产环境销毁资源，但是对临时环境（如测试或 QA）销毁资源可能很有用。


## 使用 GUI 删除密钥
{: #gui}

如果想要使用图形界面来删除加密密钥，那么可以使用 {{site.data.keyword.hscrypto}} GUI。

[在您创建密钥或将现有密钥导入服务后](/docs/services/hs-crypto/create-root-keys.html)，请完成以下步骤以删除密钥：

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/){: new_window}。
2. 从 {{site.data.keyword.cloud_notm}} 仪表板，选择 {{site.data.keyword.hscrypto}} 的已供应实例。
3. 使用**密钥**表以浏览服务中的密钥。
4. 单击 ⋮ 图标以打开要删除的密钥的选项列表。
5. 从选项菜单中，单击**删除密钥**，然后在下一个屏幕中进行确认。

删除密钥后，该密钥会转变为_已销毁_状态。处于此状态的密钥不再可恢复。与密钥关联的元数据（例如，密钥的删除日期）会保存在 {{site.data.keyword.hscrypto}} 数据库中。

## 使用 API 删除密钥
{: #api}

要删除密钥及其内容，请向以下端点发出 `DELETE` 调用。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

1. [检索服务和认证凭证以与服务中的密钥一起使用](/docs/services/hs-crypto/access-api.html)。

2. 检索要删除的密钥的标识。

    可以发出 `GET /v2/keys/` 请求或在 {{site.data.keyword.hscrypto}} 仪表板中查看密钥，以检索指定密钥的标识。

3. 运行以下 cURL 命令以永久地删除密钥及其内容。

    ```cURL
    curl -X DELETE \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}

    要使用帐户中 Cloud Foundry 组织和空间内的密钥，请将 `Bluemix-Instance` 替换为相应的 `Bluemix-org` 和 `Bluemix-space` 头。[有关更多信息，请参阅 {{site.data.keyword.hscrypto}} API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。
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
        <td>您要删除的密钥的唯一标识。</td>
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
        <td><varname>return_preference</varname></td>
        <td><p>标头，用于更改 <code>POST</code> 和 <code>DELETE</code> 操作的服务器行为。</p><p>将 <em>return_preference</em> 变量设置为 <code>return=minimal</code> 时，服务会返回成功删除响应。在将变量设置为 <code>return=representation</code> 时，服务会返回密钥资料和密钥元数据。</p></td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述使用 {{site.data.keyword.hscrypto}} API 删除密钥所需的变量。</caption>
    </table>

    如果将 _return_preference_ 变量设置为 `return=representation`，那么会在响应的 entity-body 中返回 `DELETE` 请求的详细信息。以下 JSON 对象显示返回值示例。
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    有关可用参数的详细描述，请参阅 {{site.data.keyword.hscrypto}} [REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}。
