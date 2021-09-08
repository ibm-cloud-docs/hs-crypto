---

copyright:
  years: 2018, 2021
lastupdated: "2021-09-08"

keywords: release note, new, changelog, what's new, service updates, service bulletin

subcollection: hs-crypto

content-type: release-note

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}
{:release-note: data-hd-content-type='release-note'}

# Release notes for {{site.data.keyword.hscrypto}}
{: #what-new}

Stay up to date with the new features that are available for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}





## 30 July 2021
{: #july-2021}
{: release-note}

Added: Exclusive control on the execution of cryptographic operations {: #add-cert-manager}
:   To ensure the exclusive control on the execution of cryptographic operations, you can use the {{site.data.keyword.hscrypto}} certificate manager CLI to enable the second layer of authentication for EP11 (GREP11 or PKCS #11 API) connections. By enabling this function, you enable an extra layer of access control on top of the Identity and Access Management (IAM) token to the EP11 applications. A mutual TLS connection is established to ensure that only EP11 applications with a valid client certificate can perform EP11 operations. For more information, see [Enabling the second layer of authentication for EP11 connections](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11)

Added: {{site.data.keyword.hscrypto}} expands into the Tokyo region {: #add-tokyo-region}
:   You can now create {{site.data.keyword.hscrypto}} instances in the Tokyo (`jp-tok`) region where the infrastructure is based on {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

Added: Using Terraform to initialize the {{site.data.keyword.hscrypto}} instance {: #add-terraform-automation}
:   With the integration with Terraform, now you can initialize your service instance using Terraform, and then automate actions using Terraform. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs) and the [Terraform documentation - Hyper Protect Crypto Services](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs){: external}.

Added: Using a signing service to manage signature keys for instance initialization {: #add-signing-service}
:   If you are using Terraform or key part files to initialize a service instance, you can now choose to use a third-party signing service to create, store, and manage the administrator signature keys that are used by Terraform or the Trusted Key Entry (TKE) CLI plug-in. For more information, see [Using a signing service to manage signature keys for instance initialization](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key).

## 30 June 2021
{: #june-2021}
{: release-note}

Added: Authenticated PKCS #11 keystore {: #add-authenticated-pkcs11-keystore}
:   The PKCS #11 database-backed keystores can now be encrypted and authenticated. For each service instance, a maximum of five authenticated PKCS #11 keystores are supported. You can enable the `sessionauth` parameter to encrypt the generated keys into the keystore or to decrypt the key before you use it. For more information, see [Set up the PKCS #11 configuration file](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file).

Added: Enabling cross-region recovery with failover crypto units {: #add-failover-crypto-units}
:   Failover crypto units back up the operational crypto units and keystores in another region. When a regional disaster occurs, you can use failover crypto units instead to reduce the downtime and data loss. Failover crypto units [charge extra fees](/docs/hs-crypto?topic=hs-crypto-faq-pricing) and this option is now available only in regions of `us-south` and `us-east`. For more information, see [Enabling or adding failover crypto units](/docs/hs-crypto?topic=hs-crypto-enable-add-failover) and [Cross-region disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr#cross-region-disaster-recovery).

Added: {{site.data.keyword.hscrypto}} expands into the London region {: #add-london-region}
:   You can now create {{site.data.keyword.hscrypto}} instances in the London (`eu-gb`) region where the infrastructure is based on {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 30 April 2021
{: #april-2021}
{: release-note}

Added: Rotating your master key by using smart cards and the Management Utilities {: #add-master-key-rotation-smart-cards}
:   Besides rotating your master key [using key part files](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part) and [using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit), you can now also rotate the master key if you are using smart cards and the Management Utilities.

    For detailed instructions, see [Rotating master keys by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards). For more information about how master key rotation works, see [Rotating master keys by using key parts](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro#how-master-key-rotation-works-use-key-parts).

Updated: Restore key API and UI {: #update-restore-key-api-ui}
:   Now you can restore keys that were deleted within 30 days without providing any key materials. All root keys and standard keys, whether generated by {{site.data.keyword.hscrypto}} or imported by you, can be restored. For more information, see [Restoring keys](/docs/hs-crypto?topic=hs-crypto-restore-keys).

## 31 March 2021
{: #march-2021}
{: release-note}

Added: Grouping keys by using key rings {: #add-key-ring}
:   You can now group the keys in your {{site.data.keyword.hscrypto}} instance by creating a key ring. In this case, you can manage keys and control access at the key ring level. For how to use key rings, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings).

Added: Initializing the service instance by using recovery crypto units {: #add-recovery-crypto-units}
:   Besides using smart cards and the Hyper Protect Crypto Services Management Utilities and using key part files, you can now also initialize your service instance by using recover crypto units in the Dallas (`us-south`) and Washington DC (`us-east`) regions.

    When you provision a service instance in either of the Dallas or Washington DC region, two recovery units are automatically assigned without extra costs. A random master key value is automatically generated in a recovery crypto unit and copied to the other crypto units for the service instance. The master key value never appears in the clear outside of the HSMs.

    For more information about the differences between the service instance initialization approaches, see [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit).

    For detailed instructions, see [Initializing service instances with recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit).

    To rotate your master key, see [Rotating master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit).

Added: Managing EP11 keystores and keys with the {{site.data.keyword.cloud_notm}} console {: #add-ep11-keystores-keys-console}
:   Apart from using the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) to manage Enterprise PKCS #11 (EP11) keystores and keys, you can now use the {{site.data.keyword.cloud_notm}} console to view, create, and delete EP11 keystores and keys. For more information, see [Managing EP11 keystores with the {{site.data.keyword.cloud_notm}} console](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui) and [Managing EP11 keys with the {{site.data.keyword.cloud_notm}} console](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui).

Added: Managing key aliases for a key {: #add-key-alias}
:   Key aliases are unique human-readable names that can be used to identify a key. You can now create up to five aliases for a key for easy recognition. For how to use key aliases, see [Managing key aliases](/docs/hs-crypto?topic=hs-crypto-manage-key-alias).

Added: Synchronizing protected resources associated with root keys {: #add-sync-resources}
:   When the state of a root key changes, the protected resources that are associated with the root key are notified of the key lifecycle event and are encouraged to respond accordingly. In the case where the resources do not respond to the key lifecycle notification, you can now manually initiate a renotification to those associated cloud services. For more information, see [Synchronizing associated resources](/docs/hs-crypto?topic=hs-crypto-sync-associated-resources).

Added: Using Virtual Private Endpoints for VPC {: #add-vpe-for-vpc}
:   You can now create virtual private endpoints (VPEs) for your {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance to access {{site.data.keyword.hscrypto}} within your VPC network. For more information, see [Using a virtual private endpoint for VPC](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc).

Updated: The cryptography algorithm that is used to generate signature keys {: #update-signature-key-algorithm}
:   The cryptography algorithm to generate signature keys is updated from Rivest–Shamir–Adleman 2048 (RSA 2048) to P521 Elliptic Curve (P521 EC). The cryptographic strength of P521 EC keys is equivalent to RSA 15360, which means the updated signature keys can provide the higher level of security comparing to the previous signature keys. The previous RSA 2048 signature keys are still valid and can be used.

## 28 February 2021
{: #february-2021}
{: release-note}

Added: Key verification by using the PKCS #11 API {: #add-key-verification}
:   To ensure that no tampering has occurred to the keys that are stored in the {{site.data.keyword.hscrypto}} instance by using the PKCS #11 API, a key verification mechanism is now provided for you to check the key objects that are stored in {{site.data.keyword.hscrypto}}. For instructions on how to verify key objects, see [Verifying that keys are protected by crypto units](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs11-key-verify).

    For an example of how to retrieve checksum values for AES, DES2, and DES3 keys along with the verification of the key checksums, see [the code sample](https://github.com/IBM-Cloud/hpcs-pkcs11/blob/master/samples/pkcs11-checksum.c){: external}.

Added: Support for the Schnorr algorithm {: #add-schnorr}
:   {{site.data.keyword.hscrypto}} now supports the Schnorr algorithm, which can be used as a signing scheme to generate digital signatures. It is proposed as an alternative algorithm to the Elliptic Curve Digital Signature Algorithm (ECDSA) for cryptographic signatures in the Bitcoin system. Before you can use the Schnorr algorithm, make sure to enable this feature by following the instructions in [Enabling the  Schnorr algorithm](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-schnorr).

## 31 January 2021
{: #january-2021}
{: release-note}

Added: Support for a single-tenant KMIP adapter {: #add-support-kmip-adapter}
:   {{site.data.keyword.hscrypto}} now provides a single tenant KMIP adapter to manage the key distribution in the vSphere or vSAN environment. For more information, see [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware).

## 31 December 2020
{: #december-2020}

Added: Managing the key create and import access policy {: #add-key-create-import-access}
:   After you set up your {{site.data.keyword.hscrypto}} instance, you can enable and update the key create and import access policy to control actions permissions for root keys and standard keys. For more information, see [Managing the key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess).

Added: Provisioning and managing service instances with the private-only network {: #add-private-only-network}
:   To achieve increased security, you can now limit the network access to your service instance to the private-only network. You can either [choose the allowed network when you provision the service instance](/docs/hs-crypto?topic=hs-crypto-provision) or [update the network access policy after you set up the instance](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies).

    Before you [update the network access policy](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies), you need to initialize the service instance first. See [Initializing service instances with the IBM Cloud TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) for instructions.
    {: important}

Added: `ReencryptSingle` function in GREP11 API {: #add-reencryptsingle-function-grep11}
:   The GREP11 API now supports the `ReencryptSingle` function, which enables you to decrypt data with the original key and then encrypt the raw data with a different key in a single call within the cloud HSM. This single call is a viable option where a large amount of data needs to be reencrypted with different keys, and bypasses the need to perform a combination of `DecryptSingle` and `EncryptSingle` functions for each data item that needs to be reencrypted. For more information, see [GREP11 API reference - `ReencryptSingle` function](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-ReencryptSingle).

Added: Support for accessing service instances through the Virtual Private Endpoint {: #add-vpe}
:   You can now connect your {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance to your {{site.data.keyword.hscrypto}} instance through a virtual private endpoint (VPE) gateway, so that you can manage your keys by using {{site.data.keyword.hscrypto}} through a private network. For more information, see [Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc).

Added: Support for the SLIP10 mechanism and Edwards-curve algorithm {: #add-slip10-eddsa}
:   {{site.data.keyword.hscrypto}} now supports the SLIP10 mechanism for hierarchical deterministic wallets to derive private and public key pairs. It now also supports the Edwards-curve (ED) 25519 algorithm for digital signatures. Before you can use the ED algorithm, make sure to enable this feature by following the instructions in [Enabling Edwards-curve Digital Signature Algorithm](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-EdDSA).

Added: Using Terraform to manage {{site.data.keyword.hscrypto}} instances and resources {: #add-terraform}
:   Terraform is an open source software to configure and automate cloud resource provisioning and management. Now you can provision and initialize {{site.data.keyword.hscrypto}} instances, as well as managing root keys and standard keys with the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in. For more information, see [Managing key management service resources with Terraform](/docs/terraform?topic=terraform-kms-resources), [Retrieving key management service data with Terraform](/docs/terraform?topic=terraform-kms-data-sources), and the [sample Terraform template for {{site.data.keyword.hscrypto}}](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-hpcs-crypto){: external}.

Updated: Key management API {: #update-kms-api-december}
:   The {{site.data.keyword.hscrypto}} key management API is updated with the following changes:

    - Updated: The API methods for the following key actions are now transferred to individual request paths. The generic path format (except the action of restoring a key) is `/api/v2/keys/<key_ID>/actions/<action>` where `key_ID` is the UUID of the key and `action` is the action name that you want to execute.
        - [Wrap a key](/apidocs/hs-crypto#wrapkey).
        - [Unwrap a key](/apidocs/hs-crypto#unwrapkey).
        - [Rewrap a key](/apidocs/hs-crypto#rewrapkey).
        - [Rotate a key](/apidocs/hs-crypto#rotatekey).
        - [Authorize deletion for a key with a dual authorization policy](/apidocs/hs-crypto#setkeyfordeletion).
        - [Remove an authorization for a key with a dual authorization policy](/apidocs/hs-crypto#unsetkeyfordeletion).
        - [Enable operations for a key](/apidocs/hs-crypto#enablekey).
        - [Disable operations for a key](/apidocs/hs-crypto#disablekey).
        - [Restore a key](/apidocs/hs-crypto#restorekey).

    - Updated: You can now use the following two methods to manage the allowed network policy and the key create and import access policy:
        - [Set instance policies](/apidocs/hs-crypto#putinstancepolicy).
        - [List instance policies](/apidocs/hs-crypto#getinstancepolicy).

    - Deprecated: [Invoke an action on a key](/apidocs/hs-crypto#actiononkey).

        This method is originally used for performing actions on a key, such as wrap, unwrap, and rotate. It is now replaced with individual request path for each action.

    For more information about the API updates, see [{{site.data.keyword.hscrypto}} key management API reference](/apidocs/hs-crypto){: external}.

## 30 November 2020
{: #november-2020}

Added: Support for the BIP32 mechanism {: #add-bip32-mechanism}
:   {{site.data.keyword.hscrypto}} now supports the Bitcoin Improvement Proposal 0032 (BIP32) standard for hierarchical deterministic wallets to define how to derive private and public keys of a digital wallet. To enable BIP 32, follow the instructions in [Enabling BIP32 deterministic wallets](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-BIP32).

Added: TKE activity tracker events {: #add-tke-at-events}
:   {{site.data.keyword.hscrypto}} now supports the Trusted Key Entry (TKE) events auditing. You can now use {{site.data.keyword.at_full_notm}} to monitor TKE activities and analyze failed actions. For more information, see [Auditing events for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-at-events).

## 30 September 2020
{: #september-2020}

Added: Master key rotation {: #added-master-key-rotation}
:   You can now rotate your master key on demand by using the {{site.data.keyword.cloud}} Trusted Key Entry CLI plug-in so as to meet industry standards and cryptographic best practices. For more information about how it works, see [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).

    For the detailed instructions, see [Rotating master keys](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-key-parts).

Added: Support for performing cryptographic operations with the standard PKCS #11 API {: #added-pkcs11}
:   {{site.data.keyword.hscrypto}} now supports performing cryptographic operations with the standard Public-Key Cryptography Standards (PKCS) #11 API.

    With the support of PKCS #11 API, you don not need to change your existing applications that use PKCS #11 standard to make it run in the {{site.data.keyword.hscrypto}} cloud HSM environment. The PKCS #11 library accepts the PKCS #11 API requests from your applications and remotely accesses the cloud HSM to execute the corresponding cryptographic functions.

    For more information about the PKCS #11 API use cases, see [Using Hyper Protect Crypto Services as PKCS #11 HSMs](/docs/hs-crypto?topic=hs-crypto-use-cases#pkcs11_hsm).

    To learn more about the PKCS #11 API, see [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro) and [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).

## 31 August 2020
{: #august-2020}

Added: Support for import tokens to securely upload encryption keys {: #added-import-tokens}
:   If you have *Writer* or *Manager* access permissions, you can now create import tokens to enable added security for encryption keys that you upload to {{site.data.keyword.hscrypto}}.

    To find out more about your options for importing keys, check out [Creating import tokens](/docs/hs-crypto?topic=hs-crypto-create-import-tokens). For a guided tutorial, see [Tutorial: Creating and importing encryption keys](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys).

## 31 July 2020
{: #july-2020}

Added: {{site.data.keyword.hscrypto}} aligns the key management functions with {{site.data.keyword.keymanagementserviceshort}} {: #added-key-protect-concurrency}
:   {{site.data.keyword.hscrypto}}, built on FIPS 140-2 Level 4-compliant HSM, now supports the same level of key management functions as {{site.data.keyword.keymanagementserviceshort}}. The added functions are as follows:

    * [Policy-based key rotation](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy).
    * [Viewing root key versions](/docs/hs-crypto?topic=hs-crypto-view-key-versions).
    * [Disabling and enabling root keys](/docs/hs-crypto?topic=hs-crypto-disable-keys).
    * Dual authorization policies for {{site.data.keyword.hscrypto}} [instances](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) and [keys](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy).
    * [Viewing details about an encryption key](/docs/hs-crypto?topic=hs-crypto-view-key-details).
    * [Viewing associations between root keys and IBM Cloud resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources).
    * [Restoring a deleted key](/docs/hs-crypto?topic=hs-crypto-restore-keys).

Added: {{site.data.keyword.hscrypto}} expands into the Washington DC region {: #added-wdc-region}
:   You can now create {{site.data.keyword.hscrypto}} resources in the Washington DC (US East) region. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 30 June 2020
{: #june-2020}

Added: Support for quorum authentication {: #added-quorum-authentication-202006}
:   Both the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in and the {{site.data.keyword.hscrypto}} Management Utilities now support [quorum authentication](/docs/hs-crypto?topic=hs-crypto-understand-concepts#quorum-authenticaion-concept).

    Quorum authentication is the way to approve an operation by a set number of crypto unit administrators. Some sensitive operations require a sufficient number of crypto unit administrators to enter their credentials. Setting the [signature thresholds](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) to a value greater than one enables quorum authentication.

    For more information about how to initialize a service instance by using the TKE CLI and enable quorum authentication, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

    For more information about how to initialize a service instance by using the Management Utilities and enable quorum authentication, see [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

## 30 April 2020
{: #april-2020}

Added: {{site.data.keyword.hscrypto}} adds support for EP11 private endpoints {: #added-private-endpoints-202004}
:   You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the Enterprise PKCS #11 service.

    To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using private endpoints](/docs/hs-crypto?topic=hs-crypto-secure-connection).

Added: {{site.data.keyword.hscrypto}} adds support for the Management Utilities {: #added-management-utilities-202004}
:   {{site.data.keyword.hscrypto}} now supports loading master key parts and signature keys from smart cards for service instance initialization. It ensures the highest level of protection for master key parts and signature keys.

    The Management Utilities are two applications that use smart cards to configure service instances. The Smart Card Utility Program sets up and manages the smart cards used. The Trusted Key Entry (TKE) application uses those smart cards to configure service instances. To use the Management Utilities, you need to order IBM-supported smart cards and smart card readers.

    For more information, see [Understanding the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#understand-management-utilities) and [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

Updated: {{site.data.keyword.cloud_notm}} service integration {: #added-service-integration-202004}
:   {{site.data.keyword.hscrypto}} can now be integrated with more {{site.data.keyword.cloud_notm}} services:

    - {{site.data.keyword.ihsdbaas_mongodb_full}}
    - {{site.data.keyword.ihsdbaas_postgresql_full}}
    - HyTrust DataControl
    - {{site.data.keyword.containerlong_notm}}
    - {{site.data.keyword.openshiftlong_notm}}

    For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

## 31 August 2019
{: #August-2019}

Added: {{site.data.keyword.hscrypto}} adds support for private endpoints {: #added-private-endpoints}
:   You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the service.

    To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using service endpoints to privately connect to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-secure-connection).

Added: {{site.data.keyword.hscrypto}} Cloud HSM now supports EP11 cryptographic operations over gRPC {: #added-EP11}
:   The managed Cloud Hardware Security Module  (HSM) supports Enterprise Public-Key Cryptography Standards (PKCS) #11, so your applications can integrate cryptographic operations like digital signing and validation through Enterprise PKCS #11 (EP11) API. The EP11 library provides an interface similar to the industry-standard PKCS #11 API.

    {{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 (EP11) over gRPC API calls (also referred to as *GREP11*), with which, all the Crypto functions are executed in HSM on cloud. GREP11 is a stateless interface for cloud programs.

    For more information about the GREP11 API, see [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-grep11_intro) and [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

Added: {{site.data.keyword.hscrypto}} expands into the Frankfurt region {: #added-frankfurt-region}
:   You can now create {{site.data.keyword.hscrypto}} resources in the Frankfurt region. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

Added: {{site.data.keyword.cloud_notm}} service integration {: #added-service-integration}
:   {{site.data.keyword.hscrypto}} can now be integrated with the following {{site.data.keyword.cloud_notm}} services:

    - {{site.data.keyword.cos_full_notm}}
    - {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud
    - {{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud
    - Key Management Interoperability Protocol (KMIP) for VMware&reg; on {{site.data.keyword.cloud_notm}}

    For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

## 30 June 2019
{: #June-2019}

Added: {{site.data.keyword.hscrypto}} expands into Sydney region {: #added-sydney-region}
:   You can now create {{site.data.keyword.hscrypto}} resources in the Sydney region. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 31 March 2019
{: #March-2019}

{{site.data.keyword.hscrypto}} is generally available {: #ga-201903}
:   As of 29 March 2019, provisioning new Hyper Protect Crypto Services Beta instances will no longer be possible. Existing instances will have support until the End of Beta Support Date (30 April 2019).

    For more information about the {{site.data.keyword.hscrypto}} offering, see the [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} home page](https://www.ibm.com/cloud/hyper-protect-crypto){: external}.

High availability and disaster recovery {: #ha-dr-new}
:   {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, which now supports three availability zones in a selected region, is a highly available service with automatic features that help keep your applications secure and operational.

    You can create {{site.data.keyword.hscrypto}} resources in the supported [{{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

    For more information, see [High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr).

Scalability {: #scalability-new}
:   The service instance can be scaled out to a maximum of six crypto units to meet your performance requirement. Each crypto unit can crypto-process 5000 keys. In a production environment, it is suggested to select at least two crypto units to enable high availability. By selecting three or more crypto units, these crypto units are distributed among three availability zones in the selected region.

    Read [Provisioning the service](/docs/hs-crypto?topic=hs-crypto-provision) for more information.

## 28 February 2019
{: #Feb-2019}

{{site.data.keyword.hscrypto}} Beta is available {: #beta-201902}
:   {{site.data.keyword.hscrypto}} Beta version is released. You can now access the {{site.data.keyword.hscrypto}} service through **Catalog** > **Security** directly.

    As of 5 February 2019, provisioning new Hyper Protect Crypto Services Experimental instances will no longer be possible. Existing instances will have support until the End of Experimental Support Date (5 March 2019).

## 31 December 2018
{: #Dec-2018}

Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API {: #kp-api}
:   {{site.data.keyword.keymanagementserviceshort}} API is now integrated with Hyper Protect Crypto Services to generate and protect your keys. You can call the {{site.data.keyword.keymanagementserviceshort}} API directly through {{site.data.keyword.hscrypto}}.

    For more information, see [Setting up the key management API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api) and [{{site.data.keyword.hscrypto}} key management API reference](/apidocs/hs-crypto){: external}.

Added: Support for HSM management with Keep Your own Key {: #hsm-kyok}
:   {{site.data.keyword.hscrypto}} now supports Keep Your Own Key (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. You can initialize and manage your service instance with {{site.data.keyword.cloud}} command-line interface (CLI).

    For more information, see [Initializing service instances to protect key storage](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through Advanced Cryptography Service Provider {: #deprecated-acsp}
:   At the current stage, accessing {{site.data.keyword.hscrypto}} through an Advanced Cryptography Service Provider (ACSP) client is being deprecated. If you are using a previous service instance, you can still use ACSP to explore {{site.data.keyword.hscrypto}}.
