---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# 从 Beta 服务实例迁移密钥
{: #migrate-keys}

如果使用了 Beta 服务实例，并希望将您管理的根密钥和标准密钥迁移到 {{site.data.keyword.hscrypto}} 生产服务实例，此处列出了您需要遵循的过程。
{: shortdesc}

由于无法从加密单元抽取主密钥，IBM Cloud 管理员无法迁移主密钥。您需要使用主密钥初始化生产服务实例。
{:important}  

## 开始之前
{: #migrate-prerequisites}

1. 使用 Hyper Protect Crypto Services 套餐[创建服务实例](/docs/services/hs-crypto/provision.html)。

2. 使用 Trusted Key Entry 插件[初始化服务实例](/docs/services/hs-crypto/initialize_hsm.html)。

## 迁移密钥
{: #migrate-keys-steps}  

完成以下步骤，以将根密钥和标准密钥迁移到生产环境。

1. 通过 GUI 或 API [导入根密钥](/docs/services/hs-crypto/import-root-keys.html)。

  您可以将已导入的根密钥从 Beta 服务实例迁移到生产服务实例。
  {:tip}

2. 将 Beta 服务实例中的数据加密密钥 (DEK) 解包，并在生产服务实例中打包 DEK：

  1. 使用 [invoke-an-action-on-a-key API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window}，在 Beta 服务实例中[将数据加密密钥 (DEK) 解包](/docs/services/hs-crypto/unwrap-keys.html)。

  2. 使用 [invoke-an-action-on-a-key API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window})，在生产服务实例中[打包 DEK](/docs/services/hs-crypto/wrap-keys.html)。

3. 通过以下步骤，重新创建标准密钥：

  1. 使用 [retrieve-key-by-id API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window}，[检索标准密钥](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api)。此操作将返回 Beta 实例中用于创建密钥的有效内容。

  2. 通过 GUI 或 [create-a-new-key API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window}，使用上一个步骤中检索的信息，在新服务实例中[创建标准密钥](/docs/services/hs-crypto/create-standard-keys.html)。

## 后续工作
{: #migration-next}

要了解有关以编程方式管理密钥的更多信息，请[查看 {{site.data.keyword.hscrypto}} API 参考文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://{DomainName}/apidocs/hs-crypto){: new_window}。
