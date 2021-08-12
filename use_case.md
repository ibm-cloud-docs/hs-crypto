---

copyright:
  years: 2018, 2021
lastupdated: "2021-08-12"

keywords: encryption at rest, keep your own key, kyok, vmware, cryptographic operation, digital signing, use cases

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:external: target="_blank" .external}
{:term: .term}

# Use cases
{: #use-cases}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} can be used as a key management service to pervasively protect data at rest in the {{site.data.keyword.cloud_notm}} as well as a cloud HSM for general-purpose cryptographic operations.
{: shortdesc}

## Pervasively protecting data at rest in the cloud
{: #data-at-rest-encryption}

With the integration in the {{site.data.keyword.cloud_notm}} Security Architecture, you can use {{site.data.keyword.hscrypto}} encrypt your data at rest for cloud data and storage services in the highest security level with your own keys. The service uses the same key-provider API as {{site.data.keyword.keymanagementserviceshort}} to provide a consistent envelope encryption and file system encryption approach to adopting {{site.data.keyword.cloud_notm}} services.

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} supports Keep Your Own Key (KYOK) so that you have more control and authority over your data with encryption keys that you can bring, control, and manage. At the same time, you still maintain the control over the HSM that the encryption key is located in. With {{site.data.keyword.hscrypto}}, you fully leverage the proven technology that is co-developed and operated by large enterprises for managing their most sensitive data.

Encryption keys that are generated and protected by {{site.data.keyword.hscrypto}} can be used to provide application record-level or field-level encryption to protect data from other insider threats such as from database administrators.

###  Data at rest encryption with KYOK
{: #data-at-rest-encryption-kyok}

Keys are protected by customer-managed dedicated HSMs, which means, only you have access to your data. The cryptographic capabilities of  {{site.data.keyword.hscrypto}} are built on top of a FIPS 140-2 Level 4 Certified Hardware Security Module. You can benefit from the cryptographic capabilities of {{site.data.keyword.hscrypto}} for both your new and existing workloads. The {{site.data.keyword.keymanagementservicefull_notm}} API is integrated for generating and protecting encryption keys.

Refer to [Apply end to end security to a cloud application](/docs/solution-tutorials?topic=solution-tutorials-cloud-e2e-security) and [Create secure microservices that write to a consolidated database](https://developer.ibm.com/patterns/create-a-secured-microservices-and-deploy-it-to-a-consolidated-database/){: external} for tutorials on how to encrypt cloud applications by using the key management API of {{site.data.keyword.hscrypto}}.

![data at rest encryption with KYOK](/images/byok.svg "Data at rest encryption with KYOK"){: caption="Figure 1. Data at rest encryption with KYOK" caption-side="bottom"}

###  VMware image protection with KYOK
{: #vmware-encryption-kyok}

Organizations that use the VMware&reg; environment in {{site.data.keyword.cloud_notm}} to process and store personal information demands the highest level of security. As a user of {{site.data.keyword.hscrypto}}, you get your own dedicated slot that you set up on your own to ensure that no body else can access. Because {{site.data.keyword.hscrypto}} and VMware do not talk to the same interfaces, the Key Management Interoperability Protocol for VMware component acts as an intermediary to allow the VMware environment to store and use keys from {{site.data.keyword.hscrypto}}.

As a single-tenant service, {{site.data.keyword.hscrypto}} offers dedicated control of the Hardware Security Module for VMware images for each customer. {{site.data.keyword.hscrypto}} extends the family of key management services in the {{site.data.keyword.cloud_notm}} toward single-tenant instances with dedicated hardware secret control.

Check out the [overview video on {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} and VMware on {{site.data.keyword.cloud_notm}} solutions](https://youtu.be/9n8-hQBMYWQ){: external} for more information. For a step-to-step tutorial, see [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware) and the [demo video](https://mediacenter.ibm.com/media/1_e5gk6ktn){: external}.

![VMware image protection and vSAN encryption with KYOK](/images/byok_vm.svg "VMware image protection with KYOK"){: caption="Figure 2. VMware image protection with KYOK" caption-side="bottom"}

## Using {{site.data.keyword.hscrypto}} as PKCS #11 HSMs
{: #pkcs11_hsm}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} provides the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref). PKCS #11 is defined as one of the Public-Key Cryptography Standards. Cryptographic operations are executed inside the HSMs at the cloud side. This allows for schemes where a cryptographic key is never in the clear outside the HSM, and all corresponding sensitive cryptographic operations are handled inside the HSM boundary as well.

### Application-level encryption using the PKCS #11 API
{: #app-encryption-pkcs11}

{{site.data.keyword.hscrypto}} allows application programmers to design and develop applications with a standard PKCS #11 API to request encryption or to sign the application data. It means that you can invoke security without having programmers to become encryption experts. Now you can enable and improve data integrity through digital signing and confidentiality through data encryption. Applications can use the {{site.data.keyword.hscrypto}} PKCS #11 library to perform cryptographic operations. This capability helps you to modernize business processes through building applications that have a digital workflow with private data and digital reviews, approvals, and signatures that are secure and trustworthy.

You can use the PKCS #11 API to encrypt applications between clouds. With the support of PKCS #11, you have access to a full range of advanced cryptographic operations, such as signing, signature validation, message authentication codes, and more advanced encryption schemes.



![Application encryption by using PKCS #11](/images/application-encryption-pkcs11.svg "Application encryption by using PKCS #11"){: caption="Figure 3. Application encryption by using PKCS #11" caption-side="bottom"}

### Databases encryption by using the PKCS #11 API
{: #database_encryption_pkcs11}

With {{site.data.keyword.hscrypto}}, you can encrypt Oracle® Database by using Transparent Data Encryption (TDE) and encrypt IBM Db2® Database by using Db2 default encryption.

* With TDE, you can encrypt sensitive data on database storage media, such as table spaces and files, and on backup media. Transparent Data Encryption ensures that sensitive data is encrypted, meets compliance, and provides functionality that streamlines encryption operations. The database system automatically and transparently encrypts and decrypts data when it is used by authorized users and applications. Database users do not need to be aware of TDE and database applications do not need to be adapted specifically for TDE.

    TDE uses a two-tiered key hierarchy that is composed of a TDE master encryption key and a TDE data encryption key. The TDE data encryption key is used to encrypt and decrypt data, while the TDE master encryption key is used to encrypt and decrypt the TDE data encryption key.

    ![Transparent Database Encryption by using the standard PKCS #11 API](/images/pkcs_database.svg "Transparent Database Encryption by using the standard PKCS #11 API"){: caption="Figure 4. Transparent Database Encryption by using the standard PKCS #11 API" caption-side="bottom"}

* IBM Db2 default encryption protects key database files and database backup images from inappropriate access while they are stored on external storage media. The database system automatically encrypts and decrypts data when it is used by authorized users and applications. Typically, database users do not need to be aware of default encryption and database client applications do not need to be adapted specifically.

    Db2 default encryption uses a two-tiered key hierarchy: Data is encrypted with a data encryption key (DEK). The DEK is encrypted with a master key and is stored in encrypted form with the database or the backup image. A unique DEK is generated by Db2 for each encrypted database and for each encrypted backup. A master key is used to encrypt a DEK. Each encrypted database is associated with one master key at one time.

    ![IBM Db2 default encryption by using the standard PKCS #11 API](/images/pkcs_db2.svg "IBM Db2 default encryption by using the standard PKCS #11 API"){: caption="Figure 5. IBM Db2 default encryption by using the standard PKCS #11 API" caption-side="bottom"}

With the PKCS #11 library integration, {{site.data.keyword.hscrypto}} supports the industry-standard PKCS #11 API. The {{site.data.keyword.hscrypto}} PKCS #11 library connects your database to {{site.data.keyword.hscrypto}} to perform cryptographic operations. The database system can invoke operations to manage the TDE master encryption keys or the master keys in the {{site.data.keyword.hscrypto}} PKCS #11 library. The {{site.data.keyword.hscrypto}} PKCS #11 library then interacts with your {{site.data.keyword.hscrypto}} instance to provide the highest level of security for storing and managing your TDE master encryption keys or your master keys in the cloud. It, in turn, provides the highest level of security to your data encryption keys and your data.

* For a tutorial on how to use TDE with {{site.data.keyword.hscrypto}}, see [Tutorial: Using Oracle Transparent Database Encryption with Hyper Protect Crypto Services PKCS #11](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11).
* For a tutorial on how to use Db2 default encryption with {{site.data.keyword.hscrypto}}, see [Using IBM Db2 default encryption with {{site.data.keyword.hscrypto}} PKCS #11](/docs/hs-crypto?topic=hs-crypto-tutorial-db2-pkcs11).

### Protecting data in transit with TLS/SSL offloading
{: #ssl-offloading}

Transport Layer Security (TLS) and Secure Sockets Layer (SSL) are cryptographic protocols that are designed to provide communication security over a computer network. The TLS/SSL protocol aims primarily to provide privacy and data integrity between two or more communicating computer applications.

In the context of web servers, the TLS/SSL protocol allows a website to establish the identity. Users of the website can be sure that no one else is masquerading as the website. It is done through a public-private key pair.

{{site.data.keyword.hscrypto}} provides a way to offload the cryptographic operations that are done during the TLS handshake to establish a secure connection to the web server, while it keeps the TLS/SSL private key securely stored in the dedicated HSM. In this way, you have control over your TLS/SSL keys and processing. As a result, security is improved and reputational risk is decreased.

TLS/SSL offloading to the {{site.data.keyword.hscrypto}} HSM enables data in transit protection for web, API, and mobile transactions by using the standard PKCS #11 API. With {{site.data.keyword.hscrypto}}, you can integrate TLS/SSL offloading with other cloud proxies.

For a tutorial on how to offload the SSL workload to a load balancer such as NGINX while managing keys by using {{site.data.keyword.hscrypto}}, see [Using {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} to offload NGINX TLS](https://developer.ibm.com/components/ibmz/tutorials/use-hyper-protect-crypto-services-to-offload-nginx-tls/){: external}.

![Protecting data in transit with TLS/SSL offloading](/images/ssl-offloading.svg "Protecting data in transit with TLS/SSL offloading"){: caption="Figure 6. Protecting data in transit with TLS/SSL offloading" caption-side="bottom"}

## Using {{site.data.keyword.hscrypto}} as Enterprise PKCS #11 HSMs
{: #ep11_hsm}

{{site.data.keyword.hscrypto}} provides the [Enterprise PKCS #11 (EP11) API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref). Cloud application can use this function through [gRPC](https://grpc.io){: external}.

Enterprise PKCS #11 supports stateless cryptography use cases and allows for scaling and redundancy in an enterprise environment. For some use cases around asset protection, the keys can be managed outside the cryptographic service, while all sensitive operations are executed within the HSM boundary. You can use Enterprise PKCS #11 when state handling is an issue, especially for enterprise applications that benefit from the stateless character of Enterprise PKCS #11.

You as a cloud developer can use standard interfaces from your applications for cryptographic operations with data integrity and confidentiality. {{site.data.keyword.hscrypto}} supports secure connectivity from cloud application to cloud HSM, and allows for enterprise control of Cloud HSM for application keys.

As IBM is starting to provide a new set of capabilities to support your workloads to move to the cloud, you can benefit from the cryptographic capabilities of {{site.data.keyword.hscrypto}} for both your new and existing workloads. With the introduction of Enterprise PKCS #11 over gRPC (GREP11), you have access to a full range of cryptographic operations, such as signing, signature validation, message authentication codes, random number generation.

Some code samples for [using GREP11 with Golang](https://github.com/IBM-Cloud/hpcs-grep11-go) and [JavaScript](https://github.com/IBM-Cloud/hpcs-grep11-js){: external} are available for you to try out.

![EP11 HSM](/images/PKCS11.svg "Cryptographic operations with Enterprise PKCS #11"){: caption="Figure 7. Cryptographic operations with Enterprise PKCS #11" caption-side="bottom"}

## What's next
{: #use-case-next}

- You can use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- Use {{site.data.keyword.hscrypto}} to provide highly secured key management capability for your encryption keys. To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](/apidocs/hs-crypto){: external}.
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
