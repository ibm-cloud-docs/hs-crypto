---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What's new
{: #what's-new}

Stay up-to-date with the new features that are available for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## January 2019
{: #Jan-2019}

{{site.data.keyword.hscrypto}} Beta version is released. You can now access the {{site.data.keyword.hscrypto}} service through **Catalog** > **Security and Identity** directly.

As of January 21, 2019, provisioning new Hyper Protect Crypto Services Experimental instances will no longer be possible. Existing instances will have support until the End of Experimental Support Date (February 22, 2019).

## December 2018
{: #Dec-2018}

### Added: Support for HSM management with KYOK
New as of: 2018-12-19

{{site.data.keyword.hscrypto}} now supports Keep Your Own Keys (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. You can initialize and manage your crypto instance (HSM) with {{site.data.keyword.cloud}} command-line interface (CLI).

For more information, see [Initializing crypto instances to protect key storage](initialize_hsm.html).

### Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API
New as of: 2018-12-19

{{site.data.keyword.keymanagementserviceshort}} API is now integrated with Hyper Protect Crypto Services to generate and protect your keys. You can call the {{site.data.keyword.keymanagementserviceshort}} API directly through {{site.data.keyword.hscrypto}}.

For more information, see [Accessing the API](access-api.html) and [{{site.data.keyword.hscrypto}} API ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/apidocs/hp-crypto){:new_window}.

### Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through ACSP
New as of: 2018-12-19

At the current stage, accessing {{site.data.keyword.hscrypto}} through an Advanced Cryptography Service Provider (ACSP) client is being deprecated. If you are using a previous service instance, you can still use ACSP to explore {{site.data.keyword.hscrypto}}.
