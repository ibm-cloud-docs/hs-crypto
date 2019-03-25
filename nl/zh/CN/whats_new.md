---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 新增内容
{: #what-new}

及时获取适用于 {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 的新功能。
{: shortdesc}

## 2019 年 3 月
{: #March-2019}

### {{site.data.keyword.hscrypto}} 已一般可用
最新更新日期：2019 年 3 月 29 日

有关 {{site.data.keyword.hscrypto}} 产品的更多信息，请参阅 [{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} 主页 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}。

### 高可用性和灾难恢复
最新更新日期：2019 年 3 月 29 日

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 是高可用性区域服务，具有可帮助保护应用程序安全和可操作的自动功能。


您可以在受支持的 [{{site.data.keyword.cloud_notm}} 区域](/docs/services/hs-crypto/regions.html)中创建 {{site.data.keyword.hscrypto}} 资源，这些区域表示处理和应对 {{site.data.keyword.hscrypto}} 请求的地理区域。每个 {{site.data.keyword.cloud_notm}} 区域中都包含[多个可用性专区 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/)，可满足该区域的本地访问、低等待时间和安全性需求。

有关更多信息，请参阅[高可用性和灾难恢复](/docs/services/hs-crypto/ha-dr.html)。

## 2019 年 2 月
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} Beta 已可用
最新更新日期：2019 年 2 月 05 日

{{site.data.keyword.hscrypto}} Beta 版本已发布。现在您可以通过**目录** > **安全性和身份**直接访问 {{site.data.keyword.hscrypto}} 服务。

从 2019 年 2 月 5 日起，将无法再供应新的 Hyper Protect Crypto Services Experimental 实例。对现有实例的支持截止到实验支持结束日期（2019 年 3 月 5 日）。

## 2018 年 12 月
{: #Dec-2018}

### 新增：支持使用 KYOK 管理 HSM
最新更新日期：2018 年 12 月 19 日

{{site.data.keyword.hscrypto}} 现在支持“保管自己的密钥”(KYOK)，这样您就可以利用您可以保管、控制和管理的加密密钥实现对数据更高的控制和权限。您可以使用 {{site.data.keyword.cloud}} 命令行界面 (CLI) 来初始化并管理加密实例 (HSM)。

有关更多信息，请参阅[初始化加密实例以保护密钥存储器](/docs/services/hs-crypto/initialize_hsm.html)。

### 新增：集成 {{site.data.keyword.keymanagementserviceshort}} API
最新更新日期：2018 年 12 月 19 日

{{site.data.keyword.keymanagementserviceshort}} API 现在与 Hyper Protect Crypto Services 集成以生成并保护密钥。您可以通过 {{site.data.keyword.hscrypto}} 直接调用 {{site.data.keyword.keymanagementserviceshort}} API。

有关更多信息，请参阅[访问 API](/docs/services/hs-crypto/access-api.html) 和 [{{site.data.keyword.hscrypto}} API ![外部链接图标](image/external_link.svg "外部链接图标")](https://cloud.ibm.com/apidocs/hs-crypto){:new_window}。

### 不推荐：通过 ACSP 访问 {{site.data.keyword.hscrypto}} 的功能
最新更新日期：2018 年 12 月 19 日

在当前阶段，不推荐通过 Advanced Cryptography Service Provider (ACSP) 客户机访问 {{site.data.keyword.hscrypto}}。如果您要使用先前的服务实例，那么仍可以使用 ACSP 来探索 {{site.data.keyword.hscrypto}}。
