---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-09"

keywords: hsm, cloud hsm, ep11, grep11, pkcs, cryptographic operations, cryptographic functions

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}




# Introducing cloud HSM - {{site.data.keyword.uko_full_notm}} Plan
{: #uko-introduce-cloud-hsm}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} consists of a cloud-based, FIPS 140-2 Level 4 certified hardware security module (HSM) that provides standardized APIs to manage encryption keys and perform cryptographic operations.
{: shortdesc}

## What is cloud HSM?
{: #uko-what-is-cloud-hsm}

A hardware security module (HSM) is a physical device that safeguards and manages digital keys for strong authentication and provides crypto-processing. HSMs protect the cryptographic infrastructure by securely managing, storing, and protecting cryptographic keys inside a tamper-resistant device.

{{site.data.keyword.hscrypto}} consists of a cloud-based dedicated HSM to manage encryption keys and perform cryptographic operations. The FIPS 140-2 Level 4 certified HSM provides the highest level of security for cryptography in the cloud industry. With the Keep Your Own Key (KYOK) feature, you can take ownership of the cloud HSM, which guarantees that no one, including cloud admins, have access to your cryptographic keys. In this way, you can benefit from the highest level of hardware-based encryption without the need to deploy a real HSM on your workstation or local server.

To use the {{site.data.keyword.hscrypto}} cloud HSM to protect your keys and data, first take control of the HSM by loading the [master key](#x2908413){: term}. The master key, as the key-wrapping key, owns the root of trust that encrypts the entire hierarchy of encryption keys. For more information, see [Initializing your service instance](/docs/hs-crypto?topic=hs-crypto-introduce-service).

## Performing cryptographic operations by accessing the cloud HSM
{: #uko-cryptography-cloud-hsm}

{{site.data.keyword.hscrypto}} provides a set of cryptographic functions that are executed in the cloud HSM. You can perform cryptographic operations such as key generation, data encryption, and signature verification. To do so, access the cloud HSM with either the PKCS #11 API or the Enterprise PKCS #11 over gRPC (GREP11) API.



### Accessing the cloud HSM with the PKCS #11 API
{: #uko-access-cloud-hsm-pkcs11}

[Public-Key Cryptography Standards (PKCS) #11](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external} is an industry standard that defines a platform-independent API, called Cryptoki, for devices such as HSMs that hold cryptographic information and perform cryptographic operations. With {{site.data.keyword.hscrypto}}, you can use the standard PKCS #11 API to access the cloud HSM with the PKCS #11 library. The library connects your applications to the cloud HSM to perform cryptographic operations.

With the support of the PKCS #11 API, you don't need to change your existing applications that use the PKCS #11 standard. The PKCS #11 library accepts the PKCS #11 API requests from your applications and remotely accesses the cloud HSM to execute the corresponding cryptographic functions. For more information about the PKCS #11 API, see [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-uko-pkcs11-intro).

### Accessing the cloud HSM with the GREP11 API
{: #uko-access-cloud-hsm-grep11}

In addition to the PKCS #11 API, you can also use the Enterprise PKCS #11 over gRPC (GREP11) API to access the {{site.data.keyword.hscrypto}} cloud HSM. [Enterprise PKCS #11 (EP11)](https://www.ibm.com/security/cryptocards/pciecc3/ep11){: external} is an IBM-supported cryptographic API that is enabled in the {{site.data.keyword.hscrypto}} cloud HSM. EP11 is designed for users that are seeking support for open standards and enhanced security. The [EP11 library](https://www.ibm.com/security/cryptocards/pciecc4/library){: external} offers a wide variety of general-purpose cryptographic functions and provides an interface that is similar to the PKCS #11 API. Existing applications that use PKCS #11 can benefit from enhanced security because the applications can be migrated easily to meet the EP11 requirements.

{{site.data.keyword.hscrypto}} leverages [gRPC](https://grpc.io/){: external} to enable remote application access to the cloud HSM. gRPC is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. With gRPC, applications can remotely access the {{site.data.keyword.hscrypto}} cloud HSM to call EP11 cryptographic functions. For more information about GREP11 API, see [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-uko-grep11-intro).

With the PKCS #11 and GREP11 APIs, you can perform remote cryptographic procedure calls, and, by default, impose message size limits. The maximum receiving message size is 64 MB and the outgoing message size has no limit.
{: note}

### Comparing the PKCS #11 API with the GREP11 API
{: #uko-compare-grep11-pkcs11}

Both the PKCS #11 API and the GREP11 API access the EP11 library that is enabled by the {{site.data.keyword.hscrypto}} cloud HSM to execute cryptographic functions. The following diagram illustrates the two options to interact with the cloud HSM.

![Performing cryptographic operations with the PKCS #11 API or the GREP11 API](/images/pkcs-vs-grep11.svg "Performing cryptographic operations with the PKCS #11 API or the GREP11 API"){: caption="Performing cryptographic operations with PKCS #11 API or GREP11 API" caption-side="bottom"}

Comparing with the GREP11 API, the implementation of the standard PKCS #11 API enables portable applications and provides a wider range of cryptographic operations. The following table shows the main differences between the two options.

| Perspective   |  PKCS #11 API | GREP11 API |
|---------------|--------------|-----------------|
| Interface implementation  | Stateful interface. The result of your API request can vary depending on the implicit state such as session state and user login state. In the stateful case, data is stored on the host. | Stateless interface. The result of your API request always stays the same. In the stateless case, no data is stored on the host. |
| Prior installation   | You need to install the PKCS #11 library on your local workstation first to access the {{site.data.keyword.hscrypto}} cloud HSM.  | No extra installation is needed to access the {{site.data.keyword.hscrypto}} cloud HSM. |
| Application migration   |  If your applications use the standard PKCS #11 API, you do not need to modify your existing applications specifically for EP11 or gRPC.  | In order to use the GREP11 API, you need to make sure that your applications are developed based on the EP11 requirements and gRPC specifications. |
| Authentication and access management  | The PKCS #11 library has a set of standard user types for authentication. You need to define these user types in an independent configuration file and assign different user types the corresponding IBM {{site.data.keyword.iamshort}} (IAM) roles for access management. For more information, see [Best practices for setting up PKCS #11 user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access). | The GREP11 API uses the standard IAM roles to define the corresponding access. For more information, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-uko-manage-access). |
| Additional configuration file   | Required. You need to configure all of the parameters that include user roles in this file to ensure the successful deployment of the PKCS #11 library. For more information, see the [configuration file template](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file).  |  Not required. The parameters that are needed to connect the {{site.data.keyword.hscrypto}} cloud HSM can be set up along with the application code. |
| Keystore   | Provided by {{site.data.keyword.hscrypto}}. The keys that are generated with the PKCS #11 API are protected by the master key and are stored in cloud databases.  |  Not provided by {{site.data.keyword.hscrypto}}. You need to store keys that are generated by the GREP11 API on the local workstation or other devices. |
| Supported cryptographic operations | <p>The PKCS #11 API supports most of the standard PKCS #11 functions:</p><ul><li>General purpose.</li><li>Slot and token management.</li><li>Session management</li><li>Object management.</li><li>Generate keys.</li><li>Wrap and unwrap keys.</li><li>Derive keys.</li><li> Encrypt and decrypt data.</li><li>Sign and verify message.</li><li>Create message digests.</li><li>Retrieve mechanism information.</li><li>Retrieve and set key attributes.</li></ul> | <p>The GREP11 API does not support general purpose functions and session management functions. It supports most of the EP11 cryptographic functions:</p><ul><li>Generate keys.</li><li>Wrap, unwrap, and rewrap keys.</li><li>Derive keys.</li><li> Encrypt and decrypt data.</li><li>Sign and verify message.</li><li>Create message digests.</li><li>Retrieve mechanism information.</li><li>Retrieve and set key attributes.</li></ul> |
{: caption="Comparing the PKCS #11 API with the GREP11 API" caption-side="bottom"}
