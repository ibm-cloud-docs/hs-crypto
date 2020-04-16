---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-10"

keywords: Hyper Protect Crypto Services, Keep Your Own Key, VMware integration, use cases, Bring your Own Keys, KYOK

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:external: target="_blank" .external}
{:term: .term}

# Use cases
{: #use-cases}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} can be used as a key management service to pervasively protect data at rest in the cloud as well as a cloud HSM for cryptographic operations.
{:shortdesc}

## Pervasively protecting data at rest in the cloud
{: #data-at-rest-encryption}

You can use {{site.data.keyword.hscrypto}} to encrypt your data at rest for cloud data and storage services in the highest security level with your own keys. The service uses the same key-provider API as {{site.data.keyword.keymanagementserviceshort}} to provide a consistent approach to adopting {{site.data.keyword.cloud_notm}} services.

 {{site.data.keyword.hscrypto}} support Keep Your Own Key (KYOK) so that you have more control and authority over your data with encryption keys that you can bring, control, and manage.  With {{site.data.keyword.hscrypto}}, you fully leverage the proven technology that is co-developed and operated by large enterprises for managing their most sensitive data.

 Keys are protected by customer-managed dedicated HSMs, which means, only you have access to your data. The cryptographic capabilities of  {{site.data.keyword.hscrypto}} are built on top of the FIPS 140-2 Level 4 Certified Hardware Security Module. You can benefit from the cryptographic capabilities of  {{site.data.keyword.hscrypto}} for both your new and existing workloads. With the introduction of Enterprise PKCS #11 over gRPC, you have access to a full range of cryptographic operations, such as signing, signature validation, message authentication codes, random number generation.

 {{site.data.keyword.keymanagementservicefull_notm}} APIs are integrated for key generation and protection. These keys can be used to provide record or field-level encryption by the application to protect data from other insider threats such as database administrators.

![data at rest encryption with KYOK](/image/byok.svg "Data at rest encryption with KYOK"){: caption="Figure 1. Data at rest encryption with KYOK" caption-side="bottom"}

Organizations that use the VMware&reg; environment in {{site.data.keyword.cloud_notm}} to process and store personal information demands the highest level of security. As a user of {{site.data.keyword.hscrypto}}, you get your own dedicated slot that you set up on your own to ensure that no body else can access. Because {{site.data.keyword.hscrypto}} and VMware do not talk to the same interfaces, the Key Management Interoperability Protocol for VMware acts as an intermediary to allow the VMware environment to store and use keys from {{site.data.keyword.hscrypto}}.

As a single-tenant service, {{site.data.keyword.hscrypto}} offers dedicated control of the Hardware Security Module for VMware images per customer. {{site.data.keyword.hscrypto}} extends the family of key management services in the {{site.data.keyword.cloud_notm}} towards single-tenant instances with dedicated hardware secret control.

Check out the [overview video on IBM Cloud Hyper Protect Crypto Services and VMware on {{site.data.keyword.cloud_notm}} solutions](https://youtu.be/9n8-hQBMYWQ){: external} for more information. For a step-to-step tutorial, see [Use IBM Cloud Hyper Protect Crypto Services to encrypt VMware disks](https://developer.ibm.com/tutorials/use-hyper-protect-crypto-services-to-encrypt-vmware-disks/){: external} and the [demo video](https://youtu.be/huQ5wUfrW4c){: external}.

![VMware image protection with KYOK](/image/byok_vm.svg "VMware image protection with KYOK"){: caption="Figure 2. VMware image protection with KYOK" caption-side="bottom"}

## Using {{site.data.keyword.hscrypto}} as Enterprise PKCS #11 HSMs
{: #ep11_hsm}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 ([EP11](/docs/hs-crypto?topic=hs-crypto-HSM-overview)) APIs. All crypto functions are executed in HSMs at the cloud side. Cloud application needs to call these functions through [gRPC](https://grpc.io).

You as a cloud developer can use standard interfaces from your applications for cryptographic operations with data integrity and confidentiality. {{site.data.keyword.hscrypto}}
supports secure connectivity from cloud application to cloud HSM, and allows for enterprise control of Cloud HSM for application keys.

As IBM is starting to provide a new set of capabilities to support your workloads moving to the cloud, you can benefit from the cryptographic capabilities of {{site.data.keyword.hscrypto}} for both your new and existing workloads. With the introduction of Enterprise PKCS#11 over gRPC, you have access to a full range of cryptographic operations, such as signing, signature validation, message authentication codes, random number generation.

![EP11 HSM](/image/PKCS11.svg "Cryptographic operations with Enterprise PKCS#11"){: caption="Figure 3. Cryptographic operations with Enterprise PKCS#11" caption-side="bottom"}

## What's next
{: #use-case-next}

- You can use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- Use {{site.data.keyword.hscrypto}} to provide highly secured key management capability for your encryption keys, to find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To learn more about using Enterprise PKCS #11 APIs to perform cryptographic operations for your applications, check out [Encrypt your data with Cloud HSM](/docs/hs-crypto?topic=hs-crypto-get-started#encrypt-data-hsm) and the [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
