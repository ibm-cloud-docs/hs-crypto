---

copyright:
  years: 2018, 2020
lastupdated: "2020-06-02"

keywords: release note, new, changelog, what's new, service updates, service bulletin

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

## June 2020
{: #june-2020}

### Added: Support for multiple signatures for administrative commands
{: #added-multiple-signature-202006}

Both the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in and the {{site.data.keyword.hscrypto}} Management Utilities now support signature thresholds greater than one.

The signature thresholds of a crypto unit control how many administrative signatures are required for a command to be executed. With this change, you can set as many as eight signatures for an administrative command to be executed during service instance initialization. Eight is also the maximum number of administrators that can be added to a crypto unit. For detailed information, see [Signature thresholds](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept).

For information on how to initialize a service instance using the TKE CLI, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

For information on how to initialize a service instance using the Management Utilities, see [Setting up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

## April 2020
{: #april-2020}

### Added: {{site.data.keyword.hscrypto}} adds support for the Management Utilities
{: #added-management-utilities-202004}

{{site.data.keyword.hscrypto}} now supports loading master key parts and signature keys from smart cards for service instance initialization. It ensures the highest level of protection for master key parts and signature keys.

The Management Utilities are two applications that use smart cards to configure service instances. The Smart Card Utility Program sets up and manages the smart cards used. The Trusted Key Entry (TKE) application uses those smart cards to configure service instances. To use the Management Utilities, you need to order IBM-supported smart cards and smart card readers.

For more information, see [Understanding the Management Utilities](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-management-utilities) and [Loading master keys with the Management Utilities](/docs/key-protect?topic=key-protect-grant-access-keys).

<!-- ### Added: {{site.data.keyword.hscrypto}} aligns the key management functions with {{site.data.keyword.keymanagementserviceshort}}
{: #added-key-protect-concurrency}

{{site.data.keyword.hscrypto}} now supports the same level of key management functions as {{site.data.keyword.keymanagementserviceshort}} with FIPS 140-2 Level 4-compliant HSM. The added functions include the following:

* [Support for import token to securely upload keys](/docs/hs-crypto?topic=hs-crypto-create-import-tokens)
* [Support for policy-based key rotation](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy)
* [Support for key rewrapping](/docs/hs-crypto?topic=hs-crypto-rewrap-keys) -->

### Updated: {{site.data.keyword.cloud_notm}} service integration
{: #added-service-integration-202004}

{{site.data.keyword.hscrypto}} can now be integrated with additional {{site.data.keyword.cloud_notm}} services:

- {{site.data.keyword.ihsdbaas_mongodb_full}}
- {{site.data.keyword.ihsdbaas_postgresql_full}}
- HyTrust DataControl
- {{site.data.keyword.containerlong_notm}}
- {{site.data.keyword.openshiftlong_notm}}

For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

### Added: {{site.data.keyword.hscrypto}} adds support for EP11 private endpoints
{: #added-private-endpoints-202004}

You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the Enterprise PKCS #11 service.

To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using private endpoints](/docs/hs-crypto?topic=hs-crypto-private-endpoints).

<!-- ### Changed: Platform and service access roles
{: #changed-access-roles}

{{site.data.keyword.hscrypto}} is updating its user access roles and how they correspond to {{site.data.keyword.hscrypto}} service actions. {{site.data.keyword.hscrypto}} updates access roles according to the following table:

| Service action | Current role assignments | New role assignments |
| --- | --- | --- |
| Create keys | Administrator, Editor, Writer, Manager | Writer, Manager |
| Retrieve a key by ID | Administrator, Editor, Writer, Manager | Writer, Manager |
| Retrieve a list of keys | Administrator, Editor, Writer, Manager, Viewer, Reader | Reader, Writer, Manager |
| Wrap keys | Administrator, Editor, Writer, Manager, Viewer, Reader | Reader, Writer, Manager |
| Unwrap keys | Administrator, Editor, Writer, Manager, Viewer, Reader | Reader, Writer, Manager |
| Rewrap keys | Administrator, Editor, Writer, Manager, Viewer, Reader | Reader, Writer, Manager |
| Rotate keys | Administrator, Editor, Writer, Manager | Writer, Manager |
| Set rotation policies | Administrator, Manager | Manager |
| Retrieve rotation policies | Administrator, Manager | Manager |
| Delete a key by ID | Administrator, Manager | Manager |
{: caption="Table 1. Lists upcoming changes to {{site.data.keyword.hscrypto}} service access roles" caption-side="top"}

As an account owner or admin, review the existing access policies for all {{site.data.keyword.hscrypto}} users in your account to ensure that they are assigned the appropriate levels of access.

To learn more about {{site.data.keyword.hscrypto}} roles and permissions, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access). -->

## August 2019
{: #August-2019}

### Added: {{site.data.keyword.hscrypto}} Cloud HSM now supports EP11 cryptographic operations over gRPC
{: #added-EP11}

The managed cloud Hardware Security Module (HSM) supports Enterprise Public-Key Cryptography Standards (PKCS) #11, so your applications can integrate cryptographic operations like digital signing and validation via Enterprise PKCS#11 (EP11) API. The EP11 library provides an interface similar to the industry-standard PKCS #11 API.

{{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 (EP11) APIs over gRPC calls (also referred to as *GREP11*), with which, all the Crypto functions are executed in HSM on cloud. GREP11 is a stateless interface for cloud programs.

For more information about the GREP11 API, see [EP11 introduction](/docs/hs-crypto/hs-crypto?topic=hs-crypto-HSM-overview) and [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

### Added: {{site.data.keyword.hscrypto}} adds support for private endpoints
{: #added-private-endpoints}

You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the service.

To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using private endpoints](/docs/hs-crypto?topic=hs-crypto-private-endpoints).

### Added: {{site.data.keyword.hscrypto}} expands into the Frankfurt region
{: #added-frankfurt-region}

You can now create {{site.data.keyword.hscrypto}} resources in the Frankfurt region.

For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

### Added: {{site.data.keyword.cloud_notm}} service integration
{: #added-service-integration}

{{site.data.keyword.hscrypto}} can now be integrated with the following {{site.data.keyword.cloud_notm}} services:

- {{site.data.keyword.cos_full_notm}}
- {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud
- {{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud
- Key Management Interoperability Protocol (KMIP) for VMware&reg; on {{site.data.keyword.cloud_notm}}

For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

## June 2019
{: #June-2019}

### Added: {{site.data.keyword.hscrypto}} expands into Sydney region
{: #added-sydney-region}

You can now create {{site.data.keyword.hscrypto}} resources in the Sydney region.

For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## March 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} is generally available
{: #ga-201903}

As of 29 March 2019, provisioning new Hyper Protect Crypto Services Beta instances will no longer be possible. Existing instances will have support until the End of Beta Support Date (30 April 2019).

<!-- See [Migrating keys from a Beta service instance](/docs/hs-crypto/transition-keys.html) for information on migrating keys to a production service instance. -->

For more information about the {{site.data.keyword.hscrypto}} offering, see the [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} home page](https://www.ibm.com/cloud/hyper-protect-crypto){: external}.

### High availability and disaster recovery
{: #ha-dr-new}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, which now supports three availability zones in a selected region, is a highly available service with automatic features that help keep your applications secure and operational.

You can create {{site.data.keyword.hscrypto}} resources in the supported [{{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

For more information, see [High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr).

### Scalability
{: #scalability-new}

The service instance can be scaled out to a maximum of six crypto units to meet your performance requirement. Each crypto unit can crypto-process 5000 keys. In a production environment, it is recommended to select at least two crypto units to enable high availability. By selecting three or more crypto units, these crypto units are distributed among three availability zones in the selected region.

Read [Provisioning the service](/docs/hs-crypto?topic=hs-crypto-provision) for more information.

## February 2019
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} Beta is available
{: #beta-201902}

{{site.data.keyword.hscrypto}} Beta version is released. You can now access the {{site.data.keyword.hscrypto}} service through **Catalog** > **Security and Identity** directly.

As of 5 February 2019, provisioning new Hyper Protect Crypto Services Experimental instances will no longer be possible. Existing instances will have support until the End of Experimental Support Date (5 March 2019).

## December 2018
{: #Dec-2018}

### Added: Support for HSM management with Keep Your own Key
{: #hsm-kyok}

{{site.data.keyword.hscrypto}} now supports Keep Your Own Key (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. You can initialize and manage your service instance with {{site.data.keyword.cloud}} command-line interface (CLI).

For more information, see [Initializing service instances to protect key storage](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

### Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API
{: #kp-api}

{{site.data.keyword.keymanagementserviceshort}} API is now integrated with Hyper Protect Crypto Services to generate and protect your keys. You can call the {{site.data.keyword.keymanagementserviceshort}} API directly through {{site.data.keyword.hscrypto}}.

For more information, see [Setting up the key management APIs](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api) and [{{site.data.keyword.hscrypto}} key management API reference](https://{DomainName}/apidocs/hs-crypto){: external}.

### Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through Advanced Cryptography Service Provider
{: #deprecated-acsp}

At the current stage, accessing {{site.data.keyword.hscrypto}} through an Advanced Cryptography Service Provider (ACSP) client is being deprecated. If you are using a previous service instance, you can still use ACSP to explore {{site.data.keyword.hscrypto}}.
