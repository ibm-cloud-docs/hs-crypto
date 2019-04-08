---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# 密钥简介
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 支持几种密钥类型，包括根密钥、标准密钥和主密钥。
{:shortdesc}

## 根密钥
{: #introduce-root-keys}

*根密钥*是可在 {{site.data.keyword.hscrypto}} 中进行完全管理的对称密钥打包密钥。可以使用根密钥通过高级加密来保护其他密钥。要了解更多信息，请参阅<a href="/docs/services/key-protect/concepts/envelope-encryption.html">包络加密</a>。

您可以按照[管理密钥](/docs/services/hs-crypto/index.html#manage-keys)中的步骤来管理根密钥。

## 标准密钥
{: #introduce-standard-keys}

*标准密钥*是用于加密的对称密钥。可以使用标准密钥直接对数据进行加密和解密。

您可以按照[管理密钥](/docs/services/hs-crypto/index.html#manage-keys)中的步骤来管理标准密钥。

## 主密钥
{: #introduce-master-keys}

*主密钥*用于对密钥存储器的服务实例进行加密。使用主密钥，您即拥有对包括根密钥和标准密钥在内的整个密钥链进行加密的信任根。

因为已建立与服务实例的端到端安全通道，所以只有服务实例的管理员可以设置和管理主密钥。请注意，IBM 不会备份或改动主密钥，而且无法将其复制或复原到其他机器或数据中心。

一个服务实例只能有一个主密钥。如果删除服务实例的主密钥，就可以有效地对所有已使用服务中管理的密钥加密过的数据进行密码粉碎。

在[初始化服务实例以保护密钥存储器](/docs/services/hs-crypto/initialize_hsm.html)时，可以管理主密钥。

当前阶段不支持轮换主密钥。
{:important}
