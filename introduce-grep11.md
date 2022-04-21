---

copyright:
  years: 2018, 2022
lastupdated: "2022-04-21"

keywords: hsm, cloud hsm, tke cli, trusted key entry plug-in, ep11, grep11, cryptographic operations, cryptographic functions

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Introducing EP11 over gRPC
{: #grep11-intro}

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

The following diagram shows the three calling sequence flows of GREP11 functions to perform encryption. The flows can also apply to other operations such as decrypt, digest, sign and verify. For more information about the GREP11 API, see [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

![GREP11 functions calling flow for encryption](/images/grep11-encryption-flow.svg "GREP11 functions calling flow for encryption"){: caption="Figure 1. Three calling flows of GREP11 functions for encryption" caption-side="bottom"}
