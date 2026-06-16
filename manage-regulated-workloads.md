---

copyright:
  years: 2021, 2026
lastupdated: "2026-06-16"

keywords: regulated workloads, FS Cloud, IBM Cloud for Financial Services, FS Cloud use cases

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Managing regulated workloads with Hyper Protect Crypto Services
{: #manage-regulated-workloads}

Because IBM Cloud&reg; Hyper Protect Crypto Services is built on FIPS 140-2 Level 4-certified hardware, it provides the same cryptographic technology that financial institutions rely on. By encrypting your workloads with Hyper Protect Crypto Services, it meets the security requirements of regulatory industries, such as the financial industry.

To help prevent unauthorized access to sensitive data, Hyper Protect Crypto Services provides the Keep Your Own Key capability for you to retain exclusive access to your encryption keys. Unauthorized parties, including IBM Cloud admins, have no access to your encryption keys at any time. In cases where your application encrypts data with those keys, no other parties have access to your data.  

To mitigate risk of stolen private keys, cloud users store the private key of the Transport Layer Security (TLS) certificates that are used for network encryption in the Hardware Security Module (HSM). This approach aligns with Keep Your Own Key that is provided by Hyper Protect Crypto Services. Private keys never leave the HSM, helping prevent unauthorized access to keys.

## Encrypting your regulated workloads with Hyper Protect Crypto Services
{: #encrypt-regulated-workloads}

With Hyper Protect Crypto Services, you have two options to encrypt your workloads:

* Using the key management service
    With the key management service provided, you can benefit from envelope encryption to protect your keys. Envelope encryption is the practice of encrypting data with a data encryption key (DEK) and then wrapping the DEK with a root key that you can fully manage. The root keys in Hyper Protect Crypto Services instance are also wrapped and protected by the master key that is protected in the hardware security module (HSM) of the Hyper Protect Crypto Services instance. By leveraging the key management service, your regulated workloads are protected with the envelope encryption mechanism.

    For more information about the key management service, see [Bringing your encryption keys to the cloud](/docs/hs-crypto?topic=hs-crypto-importing-keys) and [Protecting your data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).
    
* Using the GREP11 and PKCS #11 APIs
    Hyper Protect Crypto Services provides a set of cryptographic functions that are run in the cloud HSM. You can perform cryptographic operations such as key generation, data encryption, and signature verification. To do so, you can access the cloud HSM with either the PKCS #11 API or the Enterprise PKCS #11 over gRPC (GREP11) API. These operations ensure that your private keys and data are protected by the HSM that meets the regulatory requirements.

    Both the PKCS #11 API and the GREP11 API access the EP11 library that is enabled by the Hyper Protect Crypto Services cloud HSM to execute cryptographic functions. Comparing with the GREP11 API, the implementation of the standard PKCS #11 API enables portable applications and provides a wider range of cryptographic operations.

    For more information about these two APIs and how they differ, see [Introducing cloud HSM](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm).

## Regulated workloads use cases
{: #regulated-workloads-use-cases}

The following use cases show how Hyper Protect Crypto Services can work with other IBM Cloud services to manage your regulated workloads. For a complete list of IBM Cloud services that can integrate with Hyper Protect Crypto Services, see [Integrating IBM Cloud services with Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

### Managing VMware regulated workloads with Hyper Protect Crypto Services
{: #vmware-regulated-workloads}

VMware vSphere® encryption is the tool the IBM Cloud for VMware® Regulated Workloads relies on to secure management and production virtual machines while at-rest or in-transit. Hyper Protect Crypto Services through the Key Management Interoperability Protocol (KMIP) on the IBM Cloud is the KMS required for the vCenter. Hyper Protect Crypto Services is a mandatory service. On-premises key management service integration is possible through Hyper Protect Crypto Services.

For more information about how the encryption works, see [the VMware reference doc](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-encryption).

A detailed tutorial on how to encrypt VMware regulated workloads by using Hyper Protect Crypto Services, see [Tutorial: Configuring KMIP in Hyper Protect Crypto Services for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware). A [demo video](https://mediacenter.ibm.com/media/1_e5gk6ktn){: external} is also available for your reference.

### Managing IBM Cloud Object Storage regulated workloads with Hyper Protect Crypto Services
{: #cos-regulated-workloads}

IBM Cloud Object Storage is an IBM Cloud service for you to store unlimited amounts of data in the assigned bucket so that the data can be accessed anywhere from the cloud. Hyper Protect Crypto Services helps you protect encryption keys for data that is stored in Object Storage with the highest security level in the industry and gives only you the access to these keys.

For more information about the integration, see [the Object Storage reference doc](/docs/cloud-object-storage?topic=cloud-object-storage-encryption). A [demo video](https://mediacenter.ibm.com/media/0_mgxwp16v){: external} is also available for your reference.

## Getting started to manage your regulated workloads with Hyper Protect Crypto Services
{: #get-started-regulated-workloads}

To manage your regulated workloads with Hyper Protect Crypto Services, see the [Getting started tutorial](/docs/hs-crypto?topic=hs-crypto-get-started).

## Reference
{: #reference-regulated-workloads}

For more information about setting up your environment in IBM Cloud to manage your regulated workloads, see the following topics:

* [VMware encryption](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-encryption#vrw-encryption-keys).
* [VMware use case 2](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-use-case-2).
* [VMware architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-archi-overview).
