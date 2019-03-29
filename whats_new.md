---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# What's new
{: #what-new}

Stay up-to-date with the new features that are available for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## March 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} is generally available
{: #ga-201903}
New as of: 2019-03-29

As of March 29, 2019, provisioning new Hyper Protect Crypto Services Beta instances will no longer be possible. Existing instances will have support until the End of Beta Support Date (April 30, 2019).

See [Migrating keys from a Beta service instance](/docs/services/hs-crypto/transition-keys.html) for information on migrating keys to a production service instance.

For more information about the {{site.data.keyword.hscrypto}} offering, see the [{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}.

### High availability and disaster recovery
{: #ha-dr-new}
New as of: 2019-03-29

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, which now supports three availability zones in a selected region, is a highly available service with automatic features that help keep your applications secure and operational.

You can create {{site.data.keyword.hscrypto}} resources in the supported [{{site.data.keyword.cloud_notm}} regions](/docs/services/hs-crypto/regions.html), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) to meet local access, low latency, and security requirements for the region.

For more information, see [High availability and disaster recovery](/docs/services/hs-crypto/ha-dr.html).

### Scalability
{: #scalability-new}
New as of: 2019-03-29

The service instance can be scaled out to a maximum of six crypto units to meet your performance requirement. Each crypto unit can crypto-process 5000 keys. In a production environment, it is recommended to select at least two crypto units to enable high availability. By selecting three or more crypto units, these crypto units are distributed among three availability zones in the selected region.

Read [Provisioning the service](/docs/services/hs-crypto/provision.html) for more information.

## February 2019
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} Beta is available
{: #beta-201902}
New as of: 2019-02-05

{{site.data.keyword.hscrypto}} Beta version is released. You can now access the {{site.data.keyword.hscrypto}} service through **Catalog** > **Security and Identity** directly.

As of February 5, 2019, provisioning new Hyper Protect Crypto Services Experimental instances will no longer be possible. Existing instances will have support until the End of Experimental Support Date (March 5, 2019).

## December 2018
{: #Dec-2018}

### Added: Support for HSM management with KYOK
{: #hsm-kyok}
New as of: 2018-12-19

{{site.data.keyword.hscrypto}} now supports Keep Your Own Keys (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. You can initialize and manage your service instance with {{site.data.keyword.cloud}} command-line interface (CLI).

For more information, see [Initializing service instances to protect key storage](/docs/services/hs-crypto/initialize_hsm.html).

### Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API
{: #kp-api}
New as of: 2018-12-19

{{site.data.keyword.keymanagementserviceshort}} API is now integrated with Hyper Protect Crypto Services to generate and protect your keys. You can call the {{site.data.keyword.keymanagementserviceshort}} API directly through {{site.data.keyword.hscrypto}}.

For more information, see [Accessing the API](/docs/services/hs-crypto/access-api.html) and [{{site.data.keyword.hscrypto}} API ![External link icon](image/external_link.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){:new_window}.

### Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through ACSP
{: #deprecated-acsp}
New as of: 2018-12-19

At the current stage, accessing {{site.data.keyword.hscrypto}} through an Advanced Cryptography Service Provider (ACSP) client is being deprecated. If you are using a previous service instance, you can still use ACSP to explore {{site.data.keyword.hscrypto}}.
