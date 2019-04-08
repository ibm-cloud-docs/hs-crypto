---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: view keys, key configuration, key type

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 查看密钥
{: #view-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 提供了用于查看、管理和审计加密密钥的集中式系统。审计您的密钥和密钥访问限制，以确保资源安全。
{: shortdesc}

定期审计密钥配置：

- 检查创建密钥的时间并确定是否需要对密钥进行循环。
- 使用 {{site.data.keyword.cloudaccesstrailshort}} 监视对 {{site.data.keyword.hscrypto}} 的 API 调用。
- 检查哪些用户对密钥具有访问权以及访问级别是否正确。

有关审计对资源的访问权的更多信息，请参阅[使用 Cloud IAM 管理用户访问权](/docs/services/hs-crypto/manage-access.html)。

## 使用 GUI 查看密钥
{: #view-key-gui}

如果想要使用图形界面来检查服务中的密钥，那么可以使用 {{site.data.keyword.hscrypto}} 仪表板。

[创建密钥或将现有密钥导入服务后](/docs/services/hs-crypto/create-root-keys.html)，请完成以下步骤以查看密钥。

1. [登录到 {{site.data.keyword.cloud_notm}} 控制台 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/)。
2. 转至**菜单** &gt; **资源列表**，以查看您的资源列表。
3. 从 {{site.data.keyword.cloud_notm}} 资源列表，选择 {{site.data.keyword.hscrypto}} 的已供应实例。
3. 在应用程序详细信息页面中，浏览密钥的常规特征：

    <table>
      <tr>
        <th>列</th>
        <th>描述</th>
      </tr>
      <tr>
        <td>名称</td>
        <td>指定给密钥的人类可读的唯一别名。</td>
      </tr>
      <tr>
        <td>标识</td>
        <td>{{site.data.keyword.hscrypto}} 服务指定给密钥的唯一密钥标识。可以使用标识值通过 [{{site.data.keyword.hscrypto}} API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto) 来调用服务。</td>
      </tr>
      <tr>
        <td>状态</td>
        <td>[密钥状态](/docs/services/key-protect/concepts/key-states.html)，基于 [NIST Special Publication 800-57 Recommendation for Key Management ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf)。这些状态包括<i>预激活</i>、<i>活动</i>、<i>已停用</i>和<i>已销毁</i>。</td>
      </tr>
      <tr>
        <td>类型</td>
        <td>[密钥类型](/docs/services/key-protect/concepts/envelope-encryption.html#key-types)，用于描述服务中密钥的指定用途。</td>
      </tr>
      <caption style="caption-side:bottom;">表 1. 描述<b>密钥</b>表</caption>
    </table>

## 使用 API 查看密钥
{: #view-key-api}

您可以通过使用 {{site.data.keyword.hscrypto}} API 来检索密钥的内容。


### 检索密钥列表
{: #retrieve-keys-api}

对于高级视图，可以通过向以下端点发出 `GET` 调用，浏览在供应的 {{site.data.keyword.hscrypto}} 实例中管理的密钥。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [检索服务和认证凭证以与服务中的密钥一起使用](/docs/services/hs-crypto/access-api.html)。

2. 运行以下 cURL 命令以查看有关密钥的一般特征。

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
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
      <caption style="caption-side:bottom;">表 2. 描述使用 {{site.data.keyword.hscrypto}} API 查看密钥所需的变量</caption>
    </table>

    成功的 `GET /v2/keys` 请求会返回 {{site.data.keyword.hscrypto}} 服务实例中可用的密钥的集合。

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true,
          "imported": false
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {:screen}

    缺省情况下，`GET /keys` 返回前 2000 个密钥，但是可在查询时使用 `limit` 参数调整此限制。要了解有关 `limit` 和 `offset` 的更多信息，请参阅[检索密钥子集](#retrieve_subset_keys_api)。
    {: tip}

### 检索密钥子集
{: #retrieve-subset-keys-api}

通过在查询时指定 `limit` 和 `offset` 参数，可检索密钥子集，从指定的 `offset` 值开始。

例如，可能总共有 3000 密钥存储在 {{site.data.keyword.hscrypto}} 服务实例中，但是在发出 `GET /keys` 请求时可能想要检索密钥 200 - 300。

您可以使用以下示例请求来检索一组不同的密钥。

  ```cURL
  curl -X GET \
  https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys?offset=<offset>&limit=<limit> \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'correlation-id: <correlation_ID>' \
  ```
  {: codeblock}

  根据下表替换请求中的 `limit` 和 `offset` 变量。
  <table>
    <tr>
      <th>变量</th>
      <th>描述</th>
    </tr>
    <tr>
      <td><p><varname>offset</varname></p></td>
      <td>
        <p>可选：要跳过的密钥数。</p>
        <p>例如，如果实例中有 50 个密钥，并且想要列出密钥 26 - 50，请使用 <code>../keys?offset=25</code>。您还可以将 <code>offset</code> 与 <code>limit</code> 配对以翻阅可用资源。</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>limit</varname></p></td>
      <td>
        <p>可选：要检索的密钥数。</p>
        <p>例如，如果实例中有 100 个密钥，并且只想要列出 10 个密钥，那么使用 <code>../keys?limit=10</code>。<code>limit</code> 的最大值为 5000。</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">表 2. 描述 <code>limit</code> 和 <code>offset</code> 变量</caption>
  </table>

要获取用法注释，请查看用于设置 `limit` 和 `offset` 查询参数的以下示例。

<table>
  <tr>
    <th>URL</th>
    <th>描述</th>
  </tr>
  <tr>
    <td><code>.../keys</code></td>
    <td>列出所有可用资源，最多为前 2000 个密钥。</td>
  </tr>
  <tr>
    <td><code>.../keys?limit=10</code></td>
    <td>列出前 10 个密钥。</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=25&limit=50</code></td>
    <td>列出密钥 26 - 50。</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=3000&limit=50</code></td>
    <td>列出密钥 3001 - 3050。</td>
  </tr>
  <caption style="caption-side:bottom;">表 3. 提供 limit 和 offset 查询参数的用法注释</caption>
</table>

Offset 是数据集中特定密钥的位置。`offset` 值从 0 开始，这意味着数据集中的第 10 个加密密钥位于 offset 9。
{: tip}

### 按标识检索密钥
{: #retrieve-key-api}

要查看有关特定密钥的详细信息，可对以下端点发出 `GET` 调用。

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```
{: codeblock}

1. [检索服务和认证凭证以与服务中的密钥一起使用](/docs/services/hs-crypto/access-api.html)。

2. 检索您要访问或管理的密钥的标识。

    标识值用于访问有关密钥的详细信息，例如密钥资料本身。您可以通过发出 `GET /v2/keys` 请求或访问 {{site.data.keyword.hscrypto}} GUI，以检索指定密钥的标识。

3. 运行以下 cURL 命令以获取有关密钥和密钥资料的详细信息。

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
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
        <td><varname>key_ID</varname></td>
        <td>您在[步骤 1](#retrieve-keys-api) 中检索到的密钥的标识。</td>
      </tr>
      <caption style="caption-side:bottom;">表 4. 描述通过使用 {{site.data.keyword.hscrypto}} API 查看指定的密钥所需的变量</caption>
    </table>

    成功的 `GET v2/keys/<key_ID>` 响应会返回有关密钥和密钥资料的详细信息。以下 JSON 对象显示标准密钥的示例返回值。

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
        "resources": [
        {
            "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true,
            "imported": false
        }
      ]
    }
    ```
    {:screen}

    有关可用参数的详细描述，请参阅 {{site.data.keyword.hscrypto}} [REST API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto){: new_window}。
