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

# 故障诊断
{: #troubleshooting}

使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 的常见问题可能包括在与 API 交互时提供正确的头或凭证。在多种情况下，可通过执行几个简单步骤以解决这些问题。
{: shortdesc}

## 删除已初始化的 {{site.data.keyword.hscrypto}} 实例时发生错误

在删除已初始化的 {{site.data.keyword.hscrypto}} 实例时，您可能会收到类似以下内容的错误：

```
失败
来自服务器的错误响应。状态码：400；描述：400 删除 https://zCryptoBroker.mybluemix.net/v2/service_instances/ 失败，错误状态为 409。冲突。
```
{: codeblock}
{: tsSymptoms}

您在删除已初始化的 {{site.data.keyword.hscrypto}} 实例之前并未将其清除（清零）。
{: tsCauses}

在删除实例前，先运行以下命令：
{: tsResolve}

```
ibmcloud tke cryptounit-zeroize
```
{: codeblock}

## 运行与 Trusted Key Entry 插件相关的命令之后未授权的令牌

在运行 `tke` CLI 命令之后，您可能会收到类似以下内容的消息：

```
ibmcloud tke cryptounits
失败
查询加密实例时出错。
状态码：401
消息：未授权
您的访问令牌无效、已到期或没有访问此实例所需的许可权。`
```
{: codeblock}
{: tsSymptoms}

令牌未刷新。
{: tsCauses}

使用 `ibmcloud login` 命令再次登录到 {{site.data.keyword.cloud_notm}} 以刷新令牌。
{: tsResolve}

## 在使用 CLI 或 API 时收到 `error CKR_IBM_WK_NOT_INITIALIZED`

在使用 CLI 或 API 时，您可能会收到类似以下内容的错误消息：

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
正在合并密钥...
失败
请求错误：rpc 错误：代码 = 未知 描述 = GRPC 返回码：[0X434B525F484F53545F4D454D4F5259]  GRPC 消息：[Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

在运行 `ibmcloud tke cryptounit-compare` 命令时，您未在当前主密钥寄存器上收到`有效`确认。
{: tsCauses}

确保 HSM 主密钥设置正确。
{: tsResolve}

## 无法创建或删除密钥
{: #unable-to-create-keys}

访问 {{site.data.keyword.hscrypto}} 用户界面时，看不到添加密钥或删除密钥选项。

从 {{site.data.keyword.cloud_notm}} 仪表板，选择 {{site.data.keyword.hscrypto}} 服务的实例。
{: tsSymptoms}

您可以查看密钥列表，但是看不到用于添加或删除密钥的选项。

您没有正确的权限来执行 {{site.data.keyword.hscrypto}} 操作。
{: tsCauses}

与您的管理员确认是否已在适用的资源组或服务实例中为您分配了正确的角色。有关角色的更多信息，请参阅[角色和许可权](/docs/services/key-protect/manage-access.html#roles)。
{: tsResolve}

## 获取帮助和支持
{: #getting-help}

如果您在使用 {{site.data.keyword.hscrypto}} 时有任何疑问或遇到任何问题，可以检查 {{site.data.keyword.cloud_notm}}，或者在论坛中搜索相关信息或进行提问来获取帮助。还可以开具支持凭单。
{: shortdesc}

您可以通过转至[状态页面 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/status?tags=platform,runtimes,services)，来检查 {{site.data.keyword.cloud_notm}} 是否可用。

可以查看论坛以了解是否有其他用户遇到相同问题。使用论坛进行提问时，请标记您的问题，以便 {{site.data.keyword.cloud_notm}} 开发团队可以看到。

- 如果有关于 {{site.data.keyword.hscrypto}} 的技术问题，请将您的问题发布到 [Stack Overflow ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://stackoverflow.com/){: new_window} 上，并使用“ibm-cloud”和“hyperprotect-crypto”标记问题。
- 有关服务的问题和入门指示信息，请使用 [IBM developerWorks dW Answers ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://developer.ibm.com/answers/index.html){: new_window} 论坛。请包括“ibm-cloud”和“hyperprotect-crypto”标记。

有关使用论坛的更多详细信息，请参阅[获取帮助 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/docs/support/index.html#getting-help){: new_window}。

有关提交 {{site.data.keyword.IBM_notm}} 支持凭单或支持级别和凭单严重性的更多信息，请参阅[联系支持人员 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://cloud.ibm.com/docs/support/index.html#contacting-support){: new_window}。
