---

copyright:
  years: 2021, 2024
lastupdated: "2024-03-07"

keywords: regulated workloads, FS Cloud, IBM Cloud for Financial Services, FS Cloud use cases

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Managing regulated workloads with {{site.data.keyword.hscrypto}}
{: #manage-regulated-workloads}

Because {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is built on FIPS 140-2 Level 4-certified hardware, it provides the same cryptographic technology that financial institutions rely on. By encrypting your workloads with {{site.data.keyword.hscrypto}}, it meets the security requirements of regulatory industries, such as the financial industry.

To help prevent unauthorized access to sensitive data, {{site.data.keyword.hscrypto}} provides the Keep Your Own Key capability for you to retain exclusive access to your encryption keys. Unauthorized parties, including {{site.data.keyword.cloud_notm}} admins, have no access to your encryption keys at any time. In cases where your application encrypts data with those keys, no other parties have access to your data.  

To mitigate risk of stolen private keys, cloud users store the private key of the Transport Layer Security (TLS) certificates that are used for network encryption in the Hardware Security Module (HSM). This approach aligns with Keep Your Own Key that is provided by {{site.data.keyword.hscrypto}}. Private keys never leave the HSM, helping prevent unauthorized access to keys.

## Encrypting your regulated workloads with {{site.data.keyword.hscrypto}}
{: #encrypt-regulated-workloads}

With {{site.data.keyword.hscrypto}}, you have two options to encrypt your workloads:

* Using the key management service
    With the key management service provided, you can benefit from envelope encryption to protect your keys. Envelope encryption is the practice of encrypting data with a data encryption key (DEK) and then wrapping the DEK with a root key that you can fully manage. The root keys in {{site.data.keyword.hscrypto}} instance are also wrapped and protected by the master key that is protected in the hardware security module (HSM) of the {{site.data.keyword.hscrypto}} instance. By leveraging the key management service, your regulated workloads are protected with the envelope encryption mechanism.

    For more information about the key management service, see [Bringing your encryption keys to the cloud](/docs/hs-crypto?topic=hs-crypto-importing-keys) and [Protecting your data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption).
    
* Using the GREP11 and PKCS #11 APIs
    {{site.data.keyword.hscrypto}} provides a set of cryptographic functions that are run in the cloud HSM. You can perform cryptographic operations such as key generation, data encryption, and signature verification. To do so, you can access the cloud HSM with either the PKCS #11 API or the Enterprise PKCS #11 over gRPC (GREP11) API. These operations ensure that your private keys and data are protected by the HSM that meets the regulatory requirements.

    Both the PKCS #11 API and the GREP11 API access the EP11 library that is enabled by the {{site.data.keyword.hscrypto}} cloud HSM to execute cryptographic functions. Comparing with the GREP11 API, the implementation of the standard PKCS #11 API enables portable applications and provides a wider range of cryptographic operations.

    For more information about these two APIs and how they differ, see [Introducing cloud HSM](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm).

## Regulated workloads use cases
{: #regulated-workloads-use-cases}

The following use cases show how {{site.data.keyword.hscrypto}} can work with other {{site.data.keyword.cloud_notm}} services to manage your regulated workloads. For a complete list of {{site.data.keyword.cloud_notm}} services that can integrate with {{site.data.keyword.hscrypto}}, see [Integrating IBM Cloud services with Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

### Managing VMware regulated workloads with {{site.data.keyword.hscrypto}}
{: #vmware-regulated-workloads}

VMware vSphere® encryption is the tool the {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads relies on to secure management and production virtual machines while at-rest or in-transit. {{site.data.keyword.hscrypto}} through the Key Management Interoperability Protocol (KMIP) on the {{site.data.keyword.cloud_notm}} is the KMS required for the vCenter. {{site.data.keyword.hscrypto}} is a mandatory service. On-premises key management service integration is possible through {{site.data.keyword.hscrypto}}.

For more information about how the encryption works, see [the VMware reference doc](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-encryption).

A detailed tutorial on how to encrypt VMware regulated workloads by using {{site.data.keyword.hscrypto}}, see [Tutorial: Configuring KMIP in Hyper Protect Crypto Services for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware). A [demo video](https://mediacenter.ibm.com/media/1_e5gk6ktn){: external} is also available for your reference.

### Managing {{site.data.keyword.cos_full_notm}} regulated workloads with {{site.data.keyword.hscrypto}}
{: #cos-regulated-workloads}

{{site.data.keyword.cos_full_notm}} is an {{site.data.keyword.cloud_notm}} service for you to store unlimited amounts of data in the assigned bucket so that the data can be accessed anywhere from the cloud. {{site.data.keyword.hscrypto}} helps you protect encryption keys for data that is stored in {{site.data.keyword.cos_short}} with the highest security level in the industry and gives only you the access to these keys.

For more information about the integration, see [the {{site.data.keyword.cos_short}} reference doc](/docs/cloud-object-storage?topic=cloud-object-storage-encryption). A [demo video](https://mediacenter.ibm.com/media/0_mgxwp16v){: external} is also available for your reference.

## Getting started to manage your regulated workloads with {{site.data.keyword.hscrypto}}
{: #get-started-regulated-workloads}

To manage your regulated workloads with {{site.data.keyword.hscrypto}}, see the [Getting started tutorial](/docs/hs-crypto?topic=hs-crypto-get-started).

## Reference
{: #reference-regulated-workloads}

For more information about setting up your environment in {{site.data.keyword.cloud_notm}} to manage your regulated workloads, see the following topics:

* [VMware encryption](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-encryption#vrw-encryption-keys).
* [VMware use case 2](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-use-case-2).
* [VMware architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-archi-overview).
