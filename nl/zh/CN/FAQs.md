---

copyright:
  years: 2018, 2019
lastupdated: "2019-33-22"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# 常见问题
{: #faqs}

您可以使用以下常见问题来帮助使用 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}。

## HSM 证书
{: #HSM-certifications}

### 如何验证 IBM Crypto Card (HSM) 已通过验证，符合 FIPS 140-2 4 级？
{: #FIPS-L4}

FIPS 140-2 4 级属于极高的保护级别，市场上能提供此级别的并不多。IBM 是最高级别认证 HSM 的领先供应商，并且投入大量资金以在每一代新卡中维护这种验证。我们收集了来自政府机构的高级别保障需求。为了进行证书验证，会为您导向 NIST 主页，因为证书已在该主页中发布。

### FIPS 140-2 2 级、3 级、4 级有什么差别？
{: #FIPS-levels}

* FIPS 140-2 2 级：篡改证据的需求由可移除的覆盖物和门上的封条、防撬锁来实现。篡改证据涂层或封条放在加密模块上，这样必须破坏涂层或封条才能对模块中的明文密钥和关键安全性参数 (CSP) 进行物理访问。安全级别 2 至少要求基于角色的认证，即加密模块对操作员拥有特定角色并执行对应服务集的权限进行认证。

* FIPS 140-2 3 级：安全级别 3 所需要的物理安全性机制旨在提高对物理访问、使用或修改加密模块的尝试进行检测和响应的可能性。安全级别 3 需要基于身份的认证机制，从而增强针对安全级别 2 指定的基于角色的认证机制所提供的安全性。

* FIPS 140-2 4 级：在此安全级别，物理安全性机制围绕加密模块提供完整的保护边界，旨在检测所有未授权的物理访问尝试并对其做出响应。从任何方向穿透加密模块外壳都极有可能会被检测到，这将导致全部明文 CSP（关键安全性参数）被立即清零。安全级别 4 加密模块适用于没有物理保护的环境中的操作。安全级别 4 也会防止因为环境状况不利或者模块电压和温度波动到正常运作范围之外而破坏加密模块的安全性。攻击者可能通过故意偏离正常运作范围来突破加密模块的防御机制。

## 密钥管理
{: #key-management}

### {{site.data.keyword.hscrypto}} 可以与 {{site.data.keyword.keymanagementserviceshort}} 服务组合使用吗？

 {{site.data.keyword.hscrypto}} 是受管的 Crypto Service（带有完全兼容的 {{site.data.keyword.keymanagementserviceshort}} API），其用户体验与 Key Protect 完全一致。主要差别是 {{site.data.keyword.hscrypto}} 依赖于已通过 FIPS 140-2 4 级认证的 HSM。此外，它通过客户自行管理 HSM 主密钥 (KYOK) 来提供完全控制。与 {{site.data.keyword.keymanagementserviceshort}} 的多租户设置相比，该服务是每个实例专用的。 {{site.data.keyword.hscrypto}} 还为加密操作（如签名/验证、密钥生成、密码散列、加密/解密和打包/解包）提供 HSM 功能。

### 密钥名称的长度可以为多少？
{: #key_names}

您可以使用长度最多为 50 个字符的密钥名称。

### 可以在密钥名称中使用语言字符吗？
{: #key_chars}

不能在密钥名称中使用语言字符（例如中文字符）。

### 删除密钥时会发生什么？
{: #key_destruction}

删除密钥时，会永久粉碎其内容和关联的数据。使用此密钥加密的数据将不再可访问。

在删除密钥之前，确保不再需要访问与密钥相关联的任何数据。

<!-- ## Pricing
{: #pricing}

### Where can I find the detailed pricing information?
{: #pricing_info}

You can refer to the **Pricing** tab on the [{{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){: new_window} for details.

### Is there a pricing example I can refer to?
{: #pricing_example}

Here is one. If you have a requirement of 5000 keys to be crypto-processed, for high availability, you need to set up two crypto units. The amount is $3140 ($1570 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls). In total, there will be a monthly charge of $3141 ($3140 for the crypto units and $1 for the additional API calls) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1570 |
| Crypto unit 2 | $1570 |
| First 1,000,000 API calls | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) | $1 ($0.01 x 100) |
| End of month charge | $3141  |

*Table 1. Charge of two crypto units with a monthly API calls of 2,000,000* -->
