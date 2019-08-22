---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-22"

Keywords: release note, new, changelog, what's new, service updates, service bulletin

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:pre: .pre}
{:external: target="_blank" .external}

# What's new
{: #what-new}

Stay up-to-date with the new features that are available for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## August 2019
{: #August-2019}

### Added: {{site.data.keyword.hscrypto}} Cloud HSM now supports EP11 cryptographic operations over gRPC
{: #added-EP11}
New as of: 2019-08-22

The managed cloud Hardware Security Module (HSM) supports Enterprise Public-Key Cryptography Standards (PKCS) #11, so your applications can integrate cryptographic operations like digital signing and validation via Enterprise PKCS#11 (EP11) API. The EP11 library provides an interface very similar to the industry-standard PKCS #11 API.

{{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 (EP11) APIs over gRPC calls (also referred to as *GREP11*), with which, all the Crypto functions are executed in HSM on cloud. GREP11 is designed to be a stateless interface for cloud programs.

For more information on the GREP11 API, see [EP11 introduction](/docs/services/hs-crypto/hs-crypto?topic=hs-crypto-enterprise_PKCS11_overview) and [GREP11 API reference](/docs/services/hs-crypto?topic=hs-crypto-grep11-api-ref).

### Added: {{site.data.keyword.hscrypto}} adds support for private endpoints
{: #added-private-endpoints}
New as of: 2019-08-16

You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the service.

To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using private endpoints](/docs/services/hs-crypto?topic=hs-crypto-private-endpoints).

The private endpoint is currently only available for the key management service.
{: note}

### Added: {{site.data.keyword.hscrypto}} expands into the Frankfurt region
{: #added-frankfurt-region}

New as of: 2019-08-16

You can now create {{site.data.keyword.hscrypto}} resources in the Frankfurt region.

For more information, see [Regions and locations](/docs/services/hs-crypto?topic=hs-crypto-regions).

### Added: {{site.data.keyword.cloud_notm}} service integration
{: #added-service-integration}

New as of: 2019-08-16

{{site.data.keyword.hscrypto}} can now be integrated with several {{site.data.keyword.cloud_notm}} services. For more information, see [Integrating services](/docs/services/hs-crypto?topic=hs-crypto-integrate-services). 

## June 2019
{: #June-2019}

### Added: {{site.data.keyword.hscrypto}} expands into Sydney region
{: #added-sydney-region}
New as of: 2019-06-26

You can now create {{site.data.keyword.hscrypto}} resources in the Sydney region.

For more information, see [Regions and locations](/docs/services/hs-crypto?topic=hs-crypto-regions).

## March 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} is generally available
{: #ga-201903}
New as of: 2019-03-29

As of March 29, 2019, provisioning new Hyper Protect Crypto Services Beta instances will no longer be possible. Existing instances will have support until the End of Beta Support Date (April 30, 2019).

<!-- See [Migrating keys from a Beta service instance](/docs/services/hs-crypto/transition-keys.html) for information on migrating keys to a production service instance. -->

For more information about the {{site.data.keyword.hscrypto}} offering, see the [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} home page](https://www.ibm.com/cloud/hyper-protect-crypto){: external}.

### High availability and disaster recovery
{: #ha-dr-new}
New as of: 2019-03-29

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, which now supports three availability zones in a selected region, is a highly available service with automatic features that help keep your applications secure and operational.

You can create {{site.data.keyword.hscrypto}} resources in the supported [{{site.data.keyword.cloud_notm}} regions](/docs/services/hs-crypto?topic=hs-crypto-regions), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/cloud/blog/announcements/expansion-availability-zones-global-regions) to meet local access, low latency, and security requirements for the region.

For more information, see [High availability and disaster recovery](/docs/services/hs-crypto?topic=hs-crypto-ha-dr).

### Scalability
{: #scalability-new}
New as of: 2019-03-29

The service instance can be scaled out to a maximum of six crypto units to meet your performance requirement. Each crypto unit can crypto-process 5000 keys. In a production environment, it is recommended to select at least two crypto units to enable high availability. By selecting three or more crypto units, these crypto units are distributed among three availability zones in the selected region.

Read [Provisioning the service](/docs/services/hs-crypto?topic=hs-crypto-provision) for more information.

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

For more information, see [Initializing service instances to protect key storage](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm).

### Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API
{: #kp-api}
New as of: 2018-12-19

{{site.data.keyword.keymanagementserviceshort}} API is now integrated with Hyper Protect Crypto Services to generate and protect your keys. You can call the {{site.data.keyword.keymanagementserviceshort}} API directly through {{site.data.keyword.hscrypto}}.

For more information, see [Setting up the key management APIs](/docs/services/hs-crypto?topic=hs-crypto-set-up-kms-api) and [{{site.data.keyword.hscrypto}} key management API reference](https://{DomainName}/apidocs/hs-crypto){: external}.

### Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through ACSP
{: #deprecated-acsp}
New as of: 2018-12-19

At the current stage, accessing {{site.data.keyword.hscrypto}} through an Advanced Cryptography Service Provider (ACSP) client is being deprecated. If you are using a previous service instance, you can still use ACSP to explore {{site.data.keyword.hscrypto}}.
