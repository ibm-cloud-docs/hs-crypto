---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-05"

keywords: hsm, cloud hsm, tke cli, trusted key entry plug-in, ep11, grep11, cryptographic operations, cryptographic functions

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}



# Introducing EP11 over gRPC - {{site.data.keyword.uko_full_notm}} Plan
{: #uko-grep11-intro}

Enterprise PKCS #11 (EP11) is designed for customers that are seeking support for open standards and enhanced security. The EP11 library provides a stateless interface, which is similar to the industry-standard [Public-Key Cryptography Standards (PKCS) #11 API](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}. PKCS #11 API defines a platform-independent API to cryptographic tokens, such as hardware security modules (HSM) and smart cards. Existing applications that use PKCS #11 can benefit from enhanced security with secure key cryptography as well as a stateless interface, which makes the cryptographic operations much more efficient.

More information about the EP11 Library can be found in the [Enterprise PKCS #11 (EP11) Library structure document](https://www.ibm.com/security/cryptocards/pciecc4/library){: external}. For more information about EP11 capabilities and extensions, see [EP11 introduction](https://www.ibm.com/security/cryptocards/pciecc3/ep11){: external}.

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a set of EP11 over gRPC (GREP11) API calls, with which all the cryptographic functions are executed in the cloud HSM of {{site.data.keyword.hscrypto}}. The GREP11 API is a stateless interface for cryptographic operations on cloud.

{{site.data.keyword.hscrypto}} leverages frameworks such as gRPC to enable remote application access. gRPC is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} by calling the EP11 API remotely through gRPC. For more information about gRPC, see [the gRPC documentation](https://grpc.io/docs/guides/index.html){: external}.

With the GREP11 API, you can perform the following operations:

- Key generation.
- Encrypt and decrypt.
- Sign and verify.
- Wrap and unwrap keys.
- Derive keys.
- Build message digest.
- Retrieve mechanism information.

For some operations, there are a series of sub-operations. For example, the multi-part data encryption operation is composed of the `EncryptInit()`, `EncryptUpdate()`, and `EncryptFinal()` sub-operations.

- `EncryptInit()` is used to initialize an operation.
- `Encrypt()` is used to encrypt single-part data without the need to perform `EncryptUpdate()` and `EncryptFinal()` sub-operations. This operation needs to be performed after the `EncryptInit()` call.
- `EncryptUpdate()` and `EncryptFinal()` are used in combination to perform multi-part data encryption. These sub-operations need to be performed after the `EncryptInit()` call.
- `EncryptSingle()` is an IBM EP11 extension to the standard PKCS #11 specification, and is used to perform a single call to encrypt single-part data without the need to run the `EncryptInit()` and `Encrypt()` sub-operations.

The following diagram shows the three calling sequence flows of GREP11 functions to perform encryption. The flows can also apply to other operations such as decrypt, digest, sign, and verify. For more information about the GREP11 API, see [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

![GREP11 functions calling flow for encryption](/images/grep11-encryption-flow.svg "GREP11 functions calling flow for encryption"){: caption="Figure 1. Three calling flows of GREP11 functions for encryption" caption-side="bottom"}



## Post-quantum cryptography support
{: #grep11-support-post-quantum}

With the GREP11 API, you can also perform [post-quantum cryptographic](https://en.wikipedia.org/wiki/Post-quantum_cryptography){: external} operations. Traditional cryptography relies on complicated mathematical problems that are difficult for classical computers to solve. However, with the computing capabilities, quantum computers can solve these problems. Post-quantum cryptography is considered to be resistant to cryptanalytic attacks from quantum computers. It usually uses asymmetric algorithms and has multiple approaches.

The GREP11 API provides the [Dilithium algorithm](https://pq-crystals.org/dilithium/){: external} for post-quantum cryptography. It is a lattice-based digital signature scheme and can be used for signature generation and verification. Currently, only the [high-security version of round 2 Dilithium](http://oid-info.com/get/1.3.6.1.4.1.2.267.1.6.5){: external} is supported and it is not available for `SignUpdate` and `VerifyUpdate` operations.

The Dilithium algorithm is supported only by the {{site.data.keyword.IBM_notm}} 4769 crypto card, also referred to as Crypto Express 7S (CEX7S). If you create your instances in Virtual Private Cloud (VPC) based regions, where the CEX7S crypto cards are used, you can use the Dilithium algorithm for post-quantum cryptography with the GREP11 API. For a list of VPC-based regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).
{: note}

For more information about Dilithium algorithm support in GREP11, see [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref). You can also find Dilithium algorithm code examples in the following repositories:
- [The sample GREP11 GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external}
- [The sample GREP11 GitHub repository for JavaScript](https://github.com/IBM-Cloud/hpcs-grep11-js){: external}
