---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-06"

Keywords: Hyper Protect Crypto Services, Keep Your Own Keys, VMware integration, use cases, Bring your Own Keys, KYOK,

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:external: target="_blank" .external}

# Use cases
{: #use-cases}

This topic includes the use cases that are currently included in {{site.data.keyword.hscrypto}}. These use cases will be continuously evolving in later releases.
{:shortdesc}

## Pervasive data-at-rest protection in the cloud
{: #data-at-rest-encryption}

You can use {{site.data.keyword.hscrypto}} to encrypt your data at rest in the highest security level with your own keys. {{site.data.keyword.hscrypto}} provides the key management capabilities to generate and manage your keys using {{site.data.keyword.keymanagementservicefull_notm}} APIs.

The following are a few highlights of using {{site.data.keyword.hscrypto}} to protect data at rest:

 * {{site.data.keyword.hscrypto}} enables data at rest encryption for cloud data and storage services.
 * {{site.data.keyword.hscrypto}} support Keep Your Own Keys (KYOK) so that you have more control and authority over your data with encryption keys that you can bring, control, and manage.
 * {{site.data.keyword.keymanagementservicefull_notm}} APIs are integrated for key generation and protection. These keys can be used to provide record or field-level encryption by the application to protect data from other insider threats such as database administrators.
 * Your keys are protected in the highest level of security that is certified to FIPS 140-2 Level 4.
 * Keys are protected by customer-managed dedicated HSMs, which means, only you have access to your data.

![data at rest encryption with KYOK](/image/byok.png "Data at rest encryption with KYOK")
*Figure 1. Data at rest encryption with KYOK*

Similar to data at rest protection, {{site.data.keyword.hscrypto}} can also protect VMware images at rest for encryption and decryption through VMware Key Management Interoperability Protocol.

As a single-tenant service, {{site.data.keyword.hscrypto}} offers dedicated control of the Hardware Security Module for VMware images per customer. {{site.data.keyword.hscrypto}} extends the family of key management services in the {{site.data.keyword.cloud_notm}} towards single-tenant instances with dedicated hardware secret control.

![VMware image protection with KYOK](/image/byok_vm.png "VMware image protection with KYOK")

*Figure 2. VMware image protection with KYOK*

Check out the [overview video on IBM Cloud Hyper Protect Crypto Services and VMware on {{site.data.keyword.cloud_notm}} solutions](https://youtu.be/9n8-hQBMYWQ){: external} for more information. For a step-to-step tutorial, see [Use IBM Cloud Hyper Protect Crypto Services to encrypt VMware disks](https://developer.ibm.com/tutorials/use-hyper-protect-crypto-services-to-encrypt-vmware-disks/){: external} and the [demo video](https://youtu.be/huQ5wUfrW4c){: external}.

## Using {{site.data.keyword.hscrypto}} as Enterprise PKCS #11 HSMs
{: #ep11_hsm}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 ([EP11](/docs/services/hs-crypto?topic=hs-crypto-enterprise_PKCS11_overview)) APIs. All crypto functions are executed in HSMs at the cloud side. User application needs to call these functions through [gRPC](https://grpc.io).

{{site.data.keyword.hscrypto}} provides a single-tenant, dedicated HSM that is controlled by you. IBM Cloud administrators have no access. The service is built on FIPS 140-2 Level 4-certified hardware, the highest offered by any cloud provider in the industry.

Cloud developers can use standard interfaces from their applications for cryptographic operations with data integrity and confidentiality. {{site.data.keyword.hscrypto}}
supports secure connectivity from cloud application to cloud HSM, and allows for enterprise control of Cloud HSM for application keys.

![EP11 HSM](/image/PKCS11.png "Application driven data integrity and confidentiality")

*Figure 3. Application driven data integrity and confidentiality*

## What's next
{: #use-case-next}

- You can use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/services/hs-crypto?topic=hs-crypto-integrate-services).
- Use {{site.data.keyword.hscrypto}} to provide highly-secured key management capability for your encryption keys, to find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To learn more about using Enterprise PKCS #11 APIs to perform cryptographic operations for your applications, check out [Encrypte your data using Cloud HSM](/docs/services/hs-crypto?topic=hs-crypto-get-started#encrypt-data-hsm) and the [GREP11 API reference doc](/docs/services/hs-crypto?topic=hs-crypto-grep11-api-ref).
