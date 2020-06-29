---

copyright:
  years: 2018, 2019
lastupdated: "2020-05-27"

keywords: hsm, cloud hsm, tke cli, trusted key entry plug-in, ep11, grep11, cryptographic operations, cryptographic functions, imprint mode, smart card, master key, load master key

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Introducing cloud HSM and EP11 over gRPC
{: #HSM-overview}

Hardware security module (HSM) is a physical device that safeguards and manages digital keys for strong authentication and provides crypto-processing. HSMs protect the cryptographic infrastructure by securely managing, storing, and protecting cryptographic keys inside a tamper-resistant device.

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is a cloud-based, FIPS 140-2 Level 4 certified HSM. With the support of Bring Your Own Key (BYOK), {{site.data.keyword.hscrypto}} acts as a dedicated key management service to provide a complete envelope of protection around the cryptographic keys. The customer-controlled {{site.data.keyword.hscrypto}} HSM backbones the key management service through the Keep Your Own Key (KYOK) support and [master key](#x2908413){: term} protection with the highest level of security for cryptography. It guarantees that no one, including cloud admins, has access to your keys. In order to use {{site.data.keyword.hscrypto}} to protect your keys and data, you need to first load the master key parts to the HSM. For more information, see [Introduction to service instance initialization](/docs/hs-crypto?topic=hs-crypto-introduce-service). For a detailed procedure, see [Initializing service instances](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

With the introduction of Enterprise PKCS#11 (EP11) over [gRPC](https://grpc.io){: external}, you can also leverage the cloud HSM of {{site.data.keyword.hscrypto}} to access a full range of cryptographic operations to your sensitive data. The cryptographic operations include signing, signature validation, message authentication codes, random number generation.

## Introduction to EP11 over gRPC
{: #grep11_intro}

EP11 is designed for customers that are seeking support for open standards and enhanced security. The EP11 library provides a stateless interface, which is similar to the industry-standard [Public-Key Cryptography Standards (PKCS) #11 API](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}. PKCS #11 API defines a platform-independent API to cryptographic tokens, such as hardware security modules (HSM) and smart cards. Existing applications that use PKCS #11 can benefit from enhanced security with secure key cryptography as well as stateless interface, which makes the cryptographic operations much more efficient.

More information about the EP11 Library can be found in the [Enterprise PKCS #11 (EP11) Library structure document](http://public.dhe.ibm.com/security/cryptocards/pciecc4/EP11/docs/ep11-structure.pdf){: external}. For more information about EP11 capabilities and extensions, see [EP11 introduction](https://www.ibm.com/security/cryptocards/pciecc3/software#1062266){: external}.

{{site.data.keyword.hscrypto}} provides a set of EP11 APIs over gRPC calls, with which all the cryptographic functions are executed in the HSM of {{site.data.keyword.hscrypto}}. EP11 over gRPC is a stateless interface for cryptographic operations on cloud.

{{site.data.keyword.hscrypto}} leverages frameworks such as gRPC to enable remote application access. gRPC is a modern open source high-performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} by calling the EP11 API remotely through gRPC. For more information about gRPC, see [the gRPC documentation](https://grpc.io/docs/guides/index.html){: external}.

With the GREP11 APIs, you can perform the following operations:

- Key generation.
- Encrypt and decrypt.
- Sign and verify.
- Wrap and unwrap keys.
- Derive keys.
- Build message digest.
- Retrieve mechanism information.

For each operation, there are a series of suboperations. For example, the `Encrypt` operation is composed of `EncryptInit()`, `Encrypt()`, `EncryptUpdate()`, `EncryptFinal()`, and `EncryptSingle()` suboperations.

- `EncryptInit()` is used to initialize an operation.
- `Encrypt()` is used to encrypt data without the need to perform `EncryptUpdate()` and `EncryptFinal()` suboperations. This suboperation needs to be performed after the `EncryptInit()` call.
- `EncryptUpdate()` and `EncryptFinal()` are used in combination to perform data encryption. These suboperations need to be performed after the `EncryptInit()` call.
- `EncryptSingle()` is an IBM EP11 extension to the standard PKCS#11 specification, and is used to perform a single call to encrypt data without the need to run the `EncryptInit()`, `Encrypt()`, `EncryptUpdate()`, or `EncryptFinal()` sub-operation.

The following table shows the implemented functions in EP11 over gRPC, and how the functions are related to PKCS #11 and EP11. For more information on the GREP11 API, see [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

PKCS #11 functions that are marked with an asterisk (*) in the table are implemented by EP11 over gRPC. Others are not implemented.
{: note}

|PKCS #11        |Enterprise PKCS #11        |Enterprise PKCS #11 over gRPC   | Description     |
|---------------|-------------|---------|-----------------|
|C_Initialize|N/A|N/A|Initializes Cryptoki.|
|C_Finalize|N/A|N/A|Clean up miscellaneous Cryptoki-associated resources.|
|C_GetInfo|N/A|N/A|Obtains general information about Cryptoki.|
|C_GetFunctionList|N/A|N/A|Obtains entry points of Cryptoki library functions.|
|C_GetSlotList|N/A|N/A|Obtains a list of slots in the system.|
|C_GetSlotInfo|N/A|N/A|Obtains information about a particular slot.|
|C_GetTokenInfo|N/A|N/A|Obtains information about a particular token.|
|C_WaitForSlotEvent|N/A|N/A|Waits for a slot event (token insertion, removal, etc.) to occur.|
|C_GetMechanismList*|m_GetMechanismList|GetMechanismList|Obtains a list of mechanisms supported by a token.|
|C_GetMechanismInfo*|m_GetMechanismInfo|GetMechanismInfo|Obtains information about a particular mechanism.|
|C_InitToken|N/A|N/A|Initializes a token.|
|C_InitPIN|N/A|N/A|Initializes the normal user’s PIN.|
|C_SetPIN|N/A|N/A|Modifies the PIN of the current user.|
|C_OpenSession|N/A|N/A|Opens a connection between an application and a particular token or sets up an application callback for token insertion.|
|C_CloseSession|N/A|N/A|Closes a session.|
|C_CloseAllSessions|N/A|N/A|Closes all sessions with a token.|
|C_GetSessionInfo|N/A|N/A|Obtains information about the session.|
|C_GetOperationState|N/A|N/A|Obtains the cryptographic operations state of a session.|
|C_SetOperationState|N/A|N/A|Sets the cryptographic operations state of a session.|
|C_Login|N/A|N/A|Logs into a token.|
|C_Logout|N/A|N/A|Logs out from a token.|
|C_CreateObject|N/A|N/A|Creates an object.|
|C_CopyObject|N/A|N/A|Creates a copy of an object.|
|C_DestroyObject|N/A|N/A|Destroys an object.|
|C_GetObjectSize|N/A|N/A|Obtains the size of an object in bytes.|
|C_GetAttributeValue*|m_GetAttributeValue|GetAttributeValue|Obtains an attribute value of an object.|
|C_SetAttributeValue*|m_SetAttributeValue|SetAttributeValue|Modifies an attribute value of an object. Only Boolean attributes may be modified.|
|C_FindObjectsInit|N/A|N/A|Initializes an object search operation.|
|C_FindObjects|N/A|N/A|Continues an object search operation.|
|C_FindObjectsFinal|N/A|N/A|Finishes an object search operation.|
|C_EncryptInit*  |m_EncryptInit|EncryptInit|Initializes an encryption operation.|
|C_Encrypt*  |m_Encrypt|Encrypt|Encrypts single-part data.|
|C_EncryptUpdate*|m_EncryptUpdate|EncryptUpdate|Continues a multiple-part encryption operation.|
|C_EncryptFinal* |m_EncryptFinal|EncryptFinal|Finishes a multiple-part encryption operation.|
|N/A            |m_EncryptSingle|EncryptSingle|{{site.data.keyword.IBM_notm}} extension, non-standard variant of Encrypt. Processes data in one pass, with one call. Does not return any state to host other than encrypted data.|
|C_DecryptInit*  |m_DecryptInit|DecryptInit|Initializes a decryption operation.|
|C_Decrypt*  |m_Decrypt|Decrypt|Decrypts single-part encrypted data.|
|C_DecryptUpdate*|m_DecryptUpdate|DecryptUpdate|Continues a multiple-part decryption operation.|
|C_DecryptFinal*|m_DecryptFinal|DecryptFinal|Finishes a multiple-part decryption operation.|
|N/A         |m_DecryptSingle |DecryptSingle|{{site.data.keyword.IBM_notm}} extension, non-standard variant of Decrypt. Processes data in one pass, with one call. Does not return any state to host other than decrypted data.|
|C_DigestInit*   |m_DigestInit|DigestInit|Initializes a message-digesting operation.|
|C_Digest*      |m_Digest|Digest|Digests single-part data.|
|C_DigestUpdate* |m_DigestUpdate|DigestUpdate|Continues a multiple-part digesting operation.|
|C_DigestKey|N/A|N/A|Digests a key.|
|C_DigestFinal*  |m_DigestFinal|DigestFinal|Finishes a multiple-part digesting operation.|
|N/A         |m_DigestSingle|DigestSingle|{{site.data.keyword.IBM_notm}} extension, nonstandard extension, combination of DigestInit and Digest. Digests data in one pass, with one call, without constructing an intermediate digest state, and unnecessary roundtrips|
|C_SignInit*    |m_SignInit|SignInit|Initializes a signature operation.|
|C_Sign*       |m_Sign|Sign|Signs single-part data.|
|C_SignUpdate*   |m_SignUpdate|SignUpdate|Continues a multiple-part signature operation.|
|C_SignFinal*    |m_SignFinal|SignFinal|Finishes a multiple-part signature operation.|
|C_SignRecoverInit|N/A|N/A|Initializes a signature operation, where the data is recovered from the signature.|
|C_SignRecover|N/A|N/A|Signs single-part data, where the data is recovered from the signature.|
|N/A         |m_SignSingle|SignSingle|{{site.data.keyword.IBM_notm}} extension, nonstandard extension, combination of SignInit and Sign. Signs or MACs data in one pass, with one call, without constructing intermediate digest state. Does not return any state to host other than the result.|
|C_VerifyInit*   |m_VerifyInit|VerifyInit|Initializes a verification operation.|
|C_Verify*       |m_Verify|Verify|Verifies a signature on single-part data.|
|C_VerifyUpdate* |m_VerifyUpdate|VerifyUpdate|Continues a multiple-part verification operation.|
|C_VerifyFinal*  |m_VerifyFinal|VerifyFinal|Finishes a multiple-part verification operation.|
|C_VerifyRecoverInit|N/A|N/A|Initializes a verification operation where the data is recovered from the signature.|
|C_VerifyRecover|N/A|N/A|Verifies a signature on single-part data, where the data is recovered from the signature.|
|N/A         |m_VerifySingle |VerifySingle|{{site.data.keyword.IBM_notm}} extension, nonstandard extension, combination of VerifyInit and Verify. Signs or MACs data in one pass, with one call, without constructing intermediate digest state. Does not return any state to host other than verification result.|
|C_DigestEncryptUpdate|N/A|N/A|Continues simultaneous multiple-part digesting and encryption operations.|
|C_DecryptDigestUpdate|N/A|N/A|Continues simultaneous multiple-part decryption and digesting operations.|
|C_SignEncryptUpdate|N/A|N/A|Continues simultaneous multiple-part signature and encryption operations.|
|C_DecryptVerifyUpdate|N/A|N/A|Continues simultaneous multiple-part decryption and verification operations.|
|C_GenerateKey*  |m_GenerateKey|GenerateKey|Generates a secret key.|
|C_GenerateKeyPair*|m_GenerateKeyPair|GenerateKeyPair|Generates a public-key/private-key pair.|
|C_WrapKey*      |m_WrapKey|WrapKey|Wraps (encrypts) a key.|
|C_UnwrapKey*    |m_UnwrapKey|UnwrapKey|Unwraps (decrypts) a key.|
|C_DeriveKey*    |m_DeriveKey|DeriveKey|Derives a key from a base key.|
|C_SeedRandom   |N/A|N/A|Adds seed material to the random number generator.|
|C_GenerateRandom*|m_GenerateRandom|GenerateRandom|Generates random data.|
|C_GetFunctionStatus|N/A|N/A|Legacy function which always returns `CKR_FUNCTION_NOT_PARALLEL`.|
|C_CancelFunction|N/A|N/A|Legacy function which always returns `CKR_FUNCTION_NOT_PARALLEL`.|
{: caption="Table 1. Describes the implemented functions in EP11 over gRPC" caption-side="top"}
