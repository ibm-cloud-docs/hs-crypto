---

copyright:
  years: 2020, 2021
lastupdated: "2021-07-01"

keywords: algorithm, cryptographic algorithm, cryptographic operation, cryptographic function, cryptographic api, ep11, pkcs, PKCS11, PKCS 11 API, encrypt and decrypt, sign and verify, digital signing

subcollection: hs-crypto

---

{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:authenticated-content: .authenticated-content}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:preview: .preview}
{:subsection: outputclass="subsection"}
{:row-headers .row-headers}
{:external: target="_blank" .external}
{:term: .term}

# Cryptographic operations: PKCS #11 API
{: #pkcs11-api-ref}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a set of cryptography functions that are executed in a [Hardware Security Module (HSM)](#x6704988){: term} in the cloud. You can perform cryptographic operations by accessing a PKCS #11 library that is written to the PKCS #11 standard. PKCS #11 is a standard that specifies an application programming interface (API), called *Cryptoki*, for
devices that hold cryptographic information and perform cryptographic functions.
{: shortdesc}

For more information about PKCS #11,  see [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro).

## Installing and configuring PKCS #11 library
{: #setup-pkcs11-library}

To perform a PKCS #11 API call, you need to first [install the PKCS #11 library](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external}, and then [set up PKCS #11 user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access).

The library file names use the naming convention: pkcs11-grep11-<**platform**>.so.<**version**>. The platform is either *amd64* or *s390x* and the version is the standard *major.minor.build* syntax. After you download the library, move the library into a folder that is accessible by your applications. For example, if you are running your application on Linux&reg;, you can move the library to `/usr/local/lib`, `/usr/local/lib64`, or `/usr/lib`.

To access the PKCS #11 API, configure the PKCS #11 library by setting the API endpoint, service instance ID, and API key in the `grep11client.yaml` configuration file. And then, initialize the library. For detailed instructions, see [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api).

## Error handling
{: #pkcs11-error-handling}

The PKCS #11 API of {{site.data.keyword.hscrypto}} follows the [standard method of PKCS #11 Cryptographic Token Interface](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959729){: external} for error handling.

## Verifying that keys are protected by crypto units
{: #pkcs11-key-verify}

The PKCS #11 API works with generated key objects that can be stored, updated, and retrieved from a remote keystore
on {{site.data.keyword.cloud_notm}}. As an added level of protection, the key objects that are stored in {{site.data.keyword.cloud_notm}} can also be checked to ensure that no tampering occurs.

Every symmetric key that is generated, derived, or unwrapped contains a digital fingerprint that is stored in a key attribute called CKA_CHECK_VALUE. This attribute is a 3-byte checksum for the key object itself.

After you generate, derive, or unwrap a key object, it is suggested that you store the initial checksum value (contents of the CKA_CHECK_VALUE attribute) along with any unique identifiers of the key object separately. The separately stored checksums can then be used to verify whether keys are tampered with or not.

To verify a key, perform an electronic codebook (ECB) encryption operation of a single block of null (0x00) bytes by using the key to be verified. If the first 3 bytes of the resulting cipher is identical to the value of the CKA_CHECK_VALUE key attribute that is stored locally for the same key, it indicates that the key object is not tampered with. The CKA_CHECK_VALUE key attribute cannot be used to obtain any part of the key value.

An example of how to retrieve checksum values for AES, DES2, and DES3 keys along with the verification of the key checksums can be found [here](https://github.com/IBM-Cloud/hpcs-pkcs11/blob/master/samples/pkcs11-checksum.c){: external}.

## PKCS #11 function list
{: #pkcs11_function_list}

The PKCS #11 standard defines an API called *Cryptoki*. The following table lists the PKCS #11 *Cryptoki* API functions and descriptions.

Not all PKCS #11 functions are implemented by {{site.data.keyword.hscrypto}}. Functions that are implemented are marked with `Yes` in the table.
{: note}

|Category   |PKCS #11 function       |Implemented? (Yes or No)        | Description     |
|---------------|---------------|-------------|-----------------|
|[General Purpose](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959740){: external} |C_Initialize|Yes|Initializes Cryptoki.|
|[General Purpose](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959740){: external} |C_Finalize|Yes|Clean up miscellaneous Cryptoki-associated resources.|
|[General Purpose](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959740){: external} |C_GetInfo|Yes|Obtains general information about Cryptoki.|
|[General Purpose](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959740){: external} |C_GetFunctionList|Yes|Obtains entry points of Cryptoki library functions.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_GetSlotList|Yes|Obtains a list of slots in the system.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_GetSlotInfo|Yes|Obtains information about a particular slot.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_GetTokenInfo|Yes|Obtains information about a particular token.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_WaitForSlotEvent|No|Waits for a slot event (token insertion, removal, and so on) to occur.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_GetMechanismList|Yes|Obtains a list of mechanisms that are supported by a token.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_GetMechanismInfo|Yes|Obtains information about a particular mechanism.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_InitToken|Yes|Initializes a token.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_InitPIN|Yes|Initializes the normal user’s PIN.|
|[Slot and token management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959741){: external} |C_SetPIN|Yes|Modifies the PIN of the current user.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external}|C_OpenSession|Yes|Opens a connection between an application and a particular token or sets up an application callback for token insertion.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external} | C_CloseSession |Yes|Closes a session.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external} |C_CloseAllSessions|Yes|Closes all sessions with a token.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external} |C_GetSessionInfo|Yes|Obtains information about the session.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external} |C_GetOperationState|No|Obtains the cryptographic operations state of a session.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external} |C_SetOperationState|No|Sets the cryptographic operations state of a session.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external} |C_Login|Yes|Logs into a token.|
|[Session management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959742){: external} |C_Logout|Yes|Logs out from a token.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_CreateObject|No|Creates an object.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_CopyObject|No|Creates a copy of an object.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_DestroyObject|Yes|Destroys an object.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_GetObjectSize|Yes|Obtains the size of an object in bytes.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_GetAttributeValue|Yes|Obtains an attribute value of an object.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_SetAttributeValue|Yes|Modifies an attribute value of an object. Only Boolean attributes may be modified.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_FindObjectsInit|Yes|Initializes an object search operation.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_FindObjects|Yes|Continues an object search operation.|
|[Object management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959743){: external} |C_FindObjectsFinal|Yes|Finishes an object search operation.|
|[Encryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959744){: external}|C_EncryptInit |Yes|Initializes an encryption operation.|
|[Encryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959744){: external} |C_Encrypt  |Yes|Encrypts single-part data.|
|[Encryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959744){: external} |C_EncryptUpdate|Yes|Continues a multiple-part encryption operation.|
|[Encryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959744){: external} |C_EncryptFinal |Yes|Finishes a multiple-part encryption operation.|
|[Decryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959745){: external} |C_DecryptInit  |Yes|Initializes a decryption operation.|
|[Decryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959745){: external} |C_Decrypt  |Yes|Decrypts single-part encrypted data.|
|[Decryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959745){: external} |C_DecryptUpdate|Yes|Continues a multiple-part decryption operation.|
|[Decryption](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959745){: external} |C_DecryptFinal|Yes|Finishes a multiple-part decryption operation.|
|[Message digesting](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959746){: external} |C_DigestInit   |Yes|Initializes a message-digesting operation.|
|[Message digesting](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959746){: external} |C_Digest      |Yes|Digests single-part data. The length of the input data cannot be zero and the pointer that points to the input data location cannot be NULL. |
|[Message digesting](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959746){: external} |C_DigestUpdate |Yes|Continues a multiple-part digesting operation. The length of the input data cannot be zero and the pointer that points to the input data location cannot be NULL.|
|[Message digesting](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959746){: external} |C_DigestKey|No|Digests a key.|
|[Message digesting](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959746){: external} |C_DigestFinal  |Yes|Finishes a multiple-part digesting operation.|
|[Signing and MACing](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_SignInit   |Yes|Initializes a signature operation.|
|[Signing and MACing](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_Sign       |Yes|Signs single-part data.|
|[Signing and MACing](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_SignUpdate   |Yes|Continues a multiple-part signature operation.|
|[Signing and MACing](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_SignFinal    |Yes|Finishes a multiple-part signature operation.|
|[Signing and MACing](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_SignRecoverInit|No|Initializes a signature operation, where the data is recovered from the signature.|
|[Signing and MACing](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_SignRecover|No|Signs single-part data, where the data is recovered from the signature.|
|[Verifying signatures and MACs](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_VerifyInit   |Yes|Initializes a verification operation.|
|[Verifying signatures and MACs](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_Verify       |Yes|Verifies a signature on single-part data.|
|[Verifying signatures and MACs](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_VerifyUpdate |Yes|Continues a multiple-part verification operation.|
|[Verifying signatures and MACs](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_VerifyFinal  |Yes|Finishes a multiple-part verification operation.|
|[Verifying signatures and MACs](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_VerifyRecoverInit|No|Initializes a verification operation where the data is recovered from the signature.|
|[Verifying signatures and MACs](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959747){: external} |C_VerifyRecover|No|Verifies a signature on single-part data, where the data is recovered from the signature.|
|[Dual-purpose cryptographic functions](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959748){: external} |C_DigestEncryptUpdate|No|Continues simultaneous multiple-part digesting and encryption operations.|
|[Dual-purpose cryptographic functions](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959748){: external} |C_DecryptDigestUpdate|No|Continues simultaneous multiple-part decryption and digesting operations.|
|[Dual-purpose cryptographic functions](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959748){: external} |C_SignEncryptUpdate|No|Continues simultaneous multiple-part signature and encryption operations.|
|[Dual-purpose cryptographic functions](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959748){: external} |C_DecryptVerifyUpdate|No|Continues simultaneous multiple-part decryption and verification operations.|
|[Key management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749){: external} |C_GenerateKey  |Yes|Generates a secret key.|
|[Key management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749){: external} |C_GenerateKeyPair|Yes|Generates a public or private key pair.|
|[Key management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749){: external} |C_WrapKey      |Yes|Wraps (encrypts) a key.|
|[Key management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749){: external} |C_UnwrapKey    |Yes|Unwraps (decrypts) a key.|
|[Key management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749){: external} |C_DeriveKey    |Yes|Derives a key from a base key.|
|[Random number generation](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959750){: external} |C_SeedRandom   |No|Adds seed material to the random number generator.|
|[Random number generation](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959750){: external} |C_GenerateRandom|Yes|Generates random data. The length of the random data cannot be zero and the pointer that points to the random data location cannot be NULL.|
|[Parallel function management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959751){: external} |C_GetFunctionStatus|No|Legacy function that always returns `CKR_FUNCTION_NOT_PARALLEL`.|
|[Parallel function management](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959751){: external} |C_CancelFunction|No|Legacy function that always returns `CKR_FUNCTION_NOT_PARALLEL`.|
{: caption="Table 1. Describes the implemented PKCS #11 functions by service backend" caption-side="bottom"}

## Supported mechanisms
{: #pkcs-mechanism-list}

A mechanism is referred to as a process to implement a cryptographic operation. It can vary depending on the level of firmware in the IBM 4768 crypto card (also referred to as Crypto Express 6S). The following table shows the mechanisms that are  supported and how they relate to common *Cryptoki* function categories.



| Function group | Supported mechanisms |
|--------------|-----------------------|
|Encrypt and decrypt. | CKM_RSA_PKCS[^services-1], CKM_RSA_PKCS_OAEP[^services-2], CKM_AES_ECB, CKM_AES_CBC, CKM_AES_CBC_PAD, CKM_DES3_ECB, CKM_DES3_CBC, CKM_DES3_CBC_PAD|
|Sign and verify.  | CKM_RSA_PKCS[^services-3], CKM_RSA_PKCS_PSS[^services-4], CKM_RSA_X9_31[^services-5], CKM_SHA1_RSA_PKCS, CKM_SHA256_RSA_PKCS, CKM_SHA224_RSA_PKCS, CKM_SHA384_RSA_PKCS, CKM_SHA512_RSA_PKCS, CKM_SHA1_RSA_PKCS_PSS, CKM_SHA224_RSA_PKCS_PSS, CKM_SHA256_RSA_PKCS_PSS, CKM_SHA384_RSA_PKCS_PSS, CKM_SHA512_RSA_PKCS_PSS, CKM_SHA1_RSA_X9_31, CKM_DSA[^services-6], CKM_DSA_SHA1, CKM_ECDSA[^services-7], CKM_ECDSA_SHA1, CKM_ECDSA_SHA224, CKM_ECDSA_SHA256, CKM_ECDSA_SHA384, CKM_ECDSA_SHA512, CKM_SHA1_HMAC, CKM_SHA256_HMAC, CKM_SHA384_HMAC, CKM_SHA512_HMAC, CKM_SHA512_224_HMAC, CKM_SHA512_256_HMAC, CKM_IBM_ED25519_SHA512|
|Digest. |CKM_SHA_1, CKM_SHA224, CKM_SHA256, CKM_SHA384, CKM_SHA512, CKM_SHA512_224, CKM_SHA512_256|
|Generate key or generate key pair. 	 |CKM_RSA_PKCS_KEY_PAIR_GEN, CKM_RSA_X9_31_KEY_PAIR_GEN, CKM_DSA_KEY_PAIR_GEN, CKM_DSA_PARAMETER_GEN, CKM_EC_KEY_PAIR_GEN (CKM_ECDSA_KEY_PAIR_GEN), CKM_DH_PKCS_KEY_PAIR_GEN, CKM_DH_PKCS_PARAMETER_GEN, CKM_GENERIC_SECRET_KEY_GEN, CKM_AES_KEY_GEN, CKM_DES2_KEY_GEN, CKM_DES3_KEY_GEN|
|Wrap and unwrap. | CKM_RSA_PKCS, CKM_RSA_PKCS_OAEP, CKM_AES_ECB, CKM_AES_CBC, CKM_AES_CBC_PAD, CKM_DES3_ECB, CKM_DES3_CBC, CKM_DES3_CBC_PAD|
|Derive. | CKM_ECDH1_DERIVE, CKM_DH_PKCS_DERIVE, CKM_DES3_ECB_ENCRYPT_DATA, CKM_SHA1_KEY_DERIVATION, CKM_SHA224_KEY_DERIVATION, CKM_SHA256_KEY_DERIVATION, CKM_SHA384_KEY_DERIVATION, CKM_SHA512_KEY_DERIVATION|
{: caption="Table 2. Describes the supported PKCS #11 mechanisms" caption-side="bottom"}

[^services-1]: This mechanism supports only single-part operations that are not able to utilize any of the Update Cryptotoki functions, such as C_EncryptUpdate, C_DecryptUpdate, and C_DigestUpdate.

[^services-2]: This mechanism supports only single-part operations that are not able to utilize any of the Update Cryptotoki functions, such as C_EncryptUpdate, C_DecryptUpdate, and C_DigestUpdate.

[^services-3]: This mechanism supports only single-part operations that are not able to utilize any of the Update Cryptotoki functions, such as C_EncryptUpdate, C_DecryptUpdate, and C_DigestUpdate.

[^services-4]: This mechanism supports only single-part operations that are not able to utilize any of the Update Cryptotoki functions, such as C_EncryptUpdate, C_DecryptUpdate, and C_DigestUpdate.

[^services-5]: This mechanism supports only single-part operations that are not able to utilize any of the Update Cryptotoki functions, such as C_EncryptUpdate, C_DecryptUpdate, and C_DigestUpdate.

[^services-6]: This mechanism supports only single-part operations that are not able to utilize any of the Update Cryptotoki functions, such as C_EncryptUpdate, C_DecryptUpdate, and C_DigestUpdate.

[^services-7]: This mechanism supports only single-part operations that are not able to utilize any of the Update Cryptotoki functions, such as C_EncryptUpdate, C_DecryptUpdate, and C_DigestUpdate.

## Supported attributes and key types
{: #pkcs-attribute-list}

PKCS #11 attributes define object characteristics that set up how an object can be used and accessed. The following table shows the supported attributes and their relationship to the various supported key types.


| Attribute | Description | Supported key types |
|--------------|-----------------------|--------|
| CKA_CLASS   | Object class (type) and is common for all objects. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys  |
| CKA_TOKEN | CK_TRUE if object is a token object; CK_FALSE if object is a session object.  | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys   |
| CKA_PRIVATE | CK_TRUE if object is a private object; CK_FALSE if object is a public object. Default value is token-specific, and may depend on the values of other attributes of the object. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys          |
| CKA_LABEL  | Description of the object. Default is empty.  |EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys         |
| CKA_TRUSTED  | The certificate or key can be trusted for the application that it was created.  |    EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys        |
| CKA_KEY_TYPE   | Type of key.  | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys          |
| CKA_SUBJECT  | DER-encoding of the certificate or key subject name.  | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys         |
| CKA_ID   | Key identifier for public or private key pair or key. Default is empty. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys        |
| CKA_SENSITIVE |  CK_TRUE if key is sensitive.  | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys         |
| CKA_ENCRYPT | CK_TRUE if key supports encryption. |   EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys      |
| CKA_DECRYPT | CK_TRUE if key supports decryption. |EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys          |
| CKA_WRAP | CK_TRUE if key supports wrapping (can be used to wrap other keys).  |     EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys      |
| CKA_UNWRAP |  CK_TRUE if key supports unwrapping (can be used to unwrap other keys). | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys         |
| CKA_SIGN  |  CK_TRUE if key supports signatures where the signature is an appendix to the data. |EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys         |
| CKA_VERIFY  | CK_TRUE if key supports verification where the signature is an appendix to the data. |    EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys |
| CKA_DERIVE |  CK_TRUE if key supports key derivation (other keys can be derived from this key). Default is CK_FALSE. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys |
| CKA_START_DATE  |  Start date for the certificate or key. Default is empty. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys          |
| CKA_END_DATE  |  End date for the certificate or key. Default is empty. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys          |
| CKA_MODULUS |  Modulus n.  |       RSA private keys    |
| CKA_MODULUS_BITS  | Length in bits of modulus n. |        RSA public keys    |
| CKA_PUBLIC_EXPONENT | Public exponent e. |     RSA private keys      |
| CKA_VALUE_LEN  |  Length in bytes of key value.   |         AES keys  |
| CKA_EXTRACTABLE  | CK_TRUE if key is extractable and can be wrapped.  | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys          |
| CKA_LOCAL | CK_TRUE only if the key was generated locally (on the token) with a `C_GenerateKey` or `C_GenerateKeyPair` call or created with a `C_CopyObject` call as a copy of a key that had the CKA_LOCAL attribute set to CK_TRUE. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys          |
| CKA_EC_PARAMS (CKA_ECDSA_PARAMS) | DER-encoding of an ANSI X9.62 Parameters value. | EC private keys, EC public keys        |
| CKA_EC_POINT | DER-encoding of ANSI X9.62 ECPoint value Q. |      EC public keys  |
| CKA_WRAP_WITH_TRUSTED  | CK_TRUE if the key can only be wrapped with a wrapping key that has CKA_TRUSTED set to CK_TRUE. Default is CK_FALSE.  | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys          |
| CKA_CHECK_VALUE | The checksum of the key | AES keys, DES keys |
{: caption="Table 3. Describes the supported attributes" caption-side="bottom"}

## Supported curves
{: #supported-pkcs11-curve-name}

The PKCS #11 library supports limited types of curves for certain mechanisms. The following table lists the supported curve names for different mechanisms. The number in the curve name means the supported prime bitcount.

### Supported curves for generating  Elliptic Curve (EC) keys
{: #supported-pkcs11-ec-curve-name}

Mechanism `CKM_EC_KEY_PAIR_GEN` is supported when you call the `C_GenerateKeyPair` function to generate Elliptic Curve (EC) keys. The curve name parameters must be specified as object identifiers (OIDs) by using `CKA_EC_PARAMS`. You can get the OID by searching the curve name in the [OID repository](http://oid-info.com/basic-search.htm){: external}.

| PKCS #11 mechanism | Supported curve types | Supported curve names |
|---------------------| --------------------- | ----------------------|
|CKM_EC_KEY_PAIR_GEN| [National Institute of Standards and Technology (NIST) curves](https://www.ietf.org/rfc/rfc5480.txt){: external} | <ul><li>P-192, also known as secp192r1 and prime192v1.</li><li>P-224, also known as secp224r1.</li><li>P-256, also known as secp256r1 and prime256v1.</li><li>P-384, also known as secp384r1.</li><li>P-521, also known as secp521r.</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Regular Brain pool (BP) curves](https://tools.ietf.org/html/rfc5639){: external} | <ul><li>BP-160R, also known as brainpoolP160r1.</li><li>BP-192R, also known as brainpoolP192r1.</li><li>BP-224R, also known as brainpoolP224r1.</li><li>BP-256R, also known as brainpoolP256r1.</li><li>BP-320R, also known as brainpoolP320r1.</li><li>BP-384R, also known as brainpoolP384r1.</li><li>BP-512R, also known as brainpoolP512r1.</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Twisted Brain pool (BP) curves](https://tools.ietf.org/html/rfc5639){: external} | <ul><li>BP-160T, also known as brainpoolP160t1.</li><li>BP-192T, also known as brainpoolP192t1.</li><li>BP-224T, also known as brainpoolP224t1.</li><li>BP-256T, also known as brainpoolP256t1.</li><li>BP-320T, also known as brainpoolP320t1.</li><li>BP-384T, also known as brainpoolP384t1.</li><li>BP-512T, also known as brainpoolP512t1.</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Standards for Efficient Cryptography (SEC) curves](https://www.secg.org/sec2-v2.pdf){: external} | <ul><li>secp256k1</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Edwards curves](https://tools.ietf.org/html/rfc8032){: external} | <ul><li>Ed25519</li></ul>|
{: caption="Table 4. Supported curve types for generating EC keys" caption-side="bottom"}



## Standard PKCS #11 API reference
{: #pkcs11-standard-api-ref}

To review the PKCS #11 standard documentation, see:
* [Cryptographic Token Interface Usage Guide Version 2.40](http://docs.oasis-open.org/pkcs11/pkcs11-ug/v2.40/pkcs11-ug-v2.40.html){: external}
* [Cryptographic Token Interface Base Specification Version 2.40 Plus Errata 01](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/pkcs11-base-v2.40.html){: external}
* [Cryptographic Token Interface Current Mechanisms Specification Version 2.40 Plus Errata 01](http://docs.oasis-open.org/pkcs11/pkcs11-curr/v2.40/pkcs11-curr-v2.40.html){: external}
