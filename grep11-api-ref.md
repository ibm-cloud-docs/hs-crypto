---

copyright:
  years: 2018, 2023
lastupdated: "2023-08-24"

keywords: algorithm, cryptographic algorithm, cryptographic operation, cryptographic function, cryptographic api, ep11, pkcs, grep11, ep11 over grpc, enterprise pkcs, encrypt and decrypt, sign and verify, digital signing

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

# Cryptographic operations: GREP11 API
{: #grep11-api-ref}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a set of cryptography functions that are executed in a [Hardware Security Module (HSM)](#x6704988){: term} in the cloud. You can perform cryptographic operations by remotely accessing these functions with the Enterprise PKCS #11 (EP11) over gRPC API calls (also referred to as GREP11).
{: shortdesc}

For more information about how the GREP11 functions are related to PKCS #11 and EP11, see [GREP11 introduction](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm#access-cloud-hsm-pkcs11). 

The GREP11 API can process up to 500 requests/second for a single crypto unit.
{: note}

## Accessing the API
{: #access-grep11-functions}

A GREP11 API endpoint, a service ID API key, an IAM endpoint are needed for initialization before you perform any GREP11 API function calls. For more information, see [Generating a GREP11 API request](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api#form-grep11-api-request).

## Error handling
{: #grep11-error-handling}

GREP11 relies on the gRPC specification for [error handling](https://grpc.io/docs/guides/error/){: external}. When an error occurs, gRPC clients receive a [`message Status` protocol buffer](https://github.com/grpc/grpc/blob/master/src/proto/grpc/status/status.proto){: external}.

```proto3
message Status {
    int32 code = 1;
    string message = 2;
    repeated google.protobuf.Any details = 3;
}
```
{: codeblock}

In the error message,

- `code` includes the status code, which needs to be an enumerated-type (enum) value of the `google.rpc.Code` field.
- `message` includes a developer-facing error message in English. Any user-facing error message needs to be localized and sent in the `google.rpc.Status.details` field, or localized by the user.
- `details` lists messages that carry the error details. A common set of message types is available for the API to use.

GREP11 uses the `Detail` field to attach extra error code information.

```proto3
message Grep11Error {
    uint64 Code = 1;
    string Detail = 2;
    bool Retry = 3;
}
```
{: codeblock}

The `Code` field can be cast to the ***CK_RV*** value in PKCS #11. This field contains the error codes that are defined by the [PKCS #11 specification](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959729){: external} or the vendor extensions that are defined by EP11. EP11 uses only a subset of return values that PKCS #11 defines. For more information, see the **10.1.6 Return values** section in [Enterprise PKCS #11 Library structure](https://www.ibm.com/security/cryptocards/pciecc4/library).

An [example](https://github.com/IBM-Cloud/hpcs-grep11-go/blob/master/examples/server_test.go#L863){: external} in Golang that deals with errors is available.

## GREP11 function list
{: #grep11_function_list}

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
|C_WaitForSlotEvent|N/A|N/A|Waits for a slot event (token insertion, removal, and so on) to occur.|
|C_GetMechanismList*|m_GetMechanismList|GetMechanismList|Obtains a list of mechanisms that are supported by a token.|
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
|C_Login|N/A|N/A|Logs in to a token.|
|C_Logout|N/A|N/A|Logs out from a token.|
|C_CreateObject|N/A|N/A|Creates an object.|
|C_CopyObject|N/A|N/A|Creates a copy of an object.|
|C_DestroyObject|N/A|N/A|Destroys an object.|
|C_GetObjectSize|N/A|N/A|Obtains the size of an object in bytes.|
|C_GetAttributeValue*|m_GetAttributeValue|GetAttributeValue|Obtains an attribute value of an object.|
|C_SetAttributeValue*|m_SetAttributeValue|SetAttributeValue|Modifies an attribute value of an object. Only Boolean attributes can be modified.|
|C_FindObjectsInit|N/A|N/A|Initializes an object search operation.|
|C_FindObjects|N/A|N/A|Continues an object search operation.|
|C_FindObjectsFinal|N/A|N/A|Finishes an object search operation.|
|C_EncryptInit*  |m_EncryptInit|EncryptInit|Initializes an encryption operation.|
|C_Encrypt*  |m_Encrypt|Encrypt|Encrypts single-part data.|
|C_EncryptUpdate*|m_EncryptUpdate|EncryptUpdate|Continues a multiple-part encryption operation.|
|C_EncryptFinal* |m_EncryptFinal|EncryptFinal|Finishes a multiple-part encryption operation.|
|N/A            |m_EncryptSingle|EncryptSingle|{{site.data.keyword.IBM_notm}} extension, non-standard variant of `Encrypt`. Processes data in one pass, with one call. Does not return any state to host other than encrypted data.|
|N/A   |m_ReencryptSingle| ReencryptSingle  | {{site.data.keyword.IBM_notm}} extension, non-standard variant of `Encrypt`. Decrypts data with the original key and encrypts the raw data with a different key in a single call within the cloud HSM. Does not return any state to host other than the reencrypted data. |
|C_DecryptInit*  |m_DecryptInit|DecryptInit|Initializes a decryption operation.|
|C_Decrypt*  |m_Decrypt|Decrypt|Decrypts single-part encrypted data.|
|C_DecryptUpdate*|m_DecryptUpdate|DecryptUpdate|Continues a multiple-part decryption operation.|
|C_DecryptFinal*|m_DecryptFinal|DecryptFinal|Finishes a multiple-part decryption operation.|
|N/A         |m_DecryptSingle |DecryptSingle|{{site.data.keyword.IBM_notm}} extension, non-standard variant of `Decrypt`. Processes data in one pass, with one call. Does not return any state to host other than decrypted data.|
|C_DigestInit*   |m_DigestInit|DigestInit|Initializes a message-digesting operation.|
|C_Digest*      |m_Digest|Digest|Digests single-part data. The length of the input data cannot be zero and the pointer that points to the input data location cannot be NULL. |
|C_DigestUpdate* |m_DigestUpdate|DigestUpdate|Continues a multiple-part digesting operation. The length of the input data cannot be zero and the pointer that points to the input data location cannot be NULL. |
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
|C_GenerateKeyPair*|m_GenerateKeyPair|GenerateKeyPair|Generates a public-key and private-key pair.|
|C_WrapKey*      |m_WrapKey|WrapKey|Wraps (encrypts) a key.|
|C_UnwrapKey*    |m_UnwrapKey|UnwrapKey|Unwraps (decrypts) a key.|
|N/A   | N/A  | RewrapKeyBlob  | Transfers ownership of a BLOB that is controlled by the current master key to the new master key when the new master key is committed. This function is a special administration command that is supported only by GREP11. |
|C_DeriveKey*    |m_DeriveKey|DeriveKey|Derives a key from a base key.|
|C_SeedRandom   |N/A|N/A|Adds seed material to the random number generator.|
|C_GenerateRandom*|m_GenerateRandom|GenerateRandom|Generates random data. The length of the random data cannot be zero and the pointer that points to the random data location cannot be NULL. The maximum length of the random data that can be requested is 1 million bytes.|
|C_GetFunctionStatus|N/A|N/A|Legacy function that always returns `CKR_FUNCTION_NOT_PARALLEL`.|
|C_CancelFunction|N/A|N/A|Legacy function that always returns `CKR_FUNCTION_NOT_PARALLEL`.|
{: caption="Table 1. Describes the implemented functions in EP11 over gRPC" caption-side="bottom"}

## Supported mechanisms
{: #grep11-mechanism-list}

A mechanism is referred to as a process to implement a cryptographic operation. It can vary depending on the level of firmware in the crypto card. The following table shows the mechanisms that are currently supported and how they relate to common GREP11 function categories.

| Function group | Supported mechanisms |
|--------------|-----------------------|
|Encrypt and decrypt | CKM_RSA_PKCS<sup>1</sup>, CKM_RSA_PKCS_OAEP<sup>1</sup>, CKM_AES_ECB, CKM_AES_CBC, CKM_AES_CBC_PAD, CKM_DES3_ECB, CKM_DES3_CBC, CKM_DES3_CBC_PAD|
|Sign and verify  | CKM_RSA_PKCS<sup>1</sup>, CKM_RSA_PKCS_PSS<sup>1</sup>, CKM_RSA_X9_31<sup>1</sup>, CKM_SHA1_RSA_PKCS, CKM_SHA256_RSA_PKCS, CKM_SHA224_RSA_PKCS, CKM_SHA384_RSA_PKCS, CKM_SHA512_RSA_PKCS, CKM_SHA1_RSA_PKCS_PSS, CKM_SHA224_RSA_PKCS_PSS, CKM_SHA256_RSA_PKCS_PSS, CKM_SHA384_RSA_PKCS_PSS, CKM_SHA512_RSA_PKCS_PSS, CKM_SHA1_RSA_X9_31, CKM_DSA<sup>1</sup>, CKM_DSA_SHA1, CKM_ECDSA<sup>1</sup>, CKM_ECDSA_SHA1, CKM_ECDSA_SHA224, CKM_ECDSA_SHA256, CKM_ECDSA_SHA384, CKM_ECDSA_SHA512, CKM_SHA1_HMAC, CKM_SHA256_HMAC, CKM_SHA384_HMAC, CKM_SHA512_HMAC, CKM_SHA512_224_HMAC, CKM_SHA512_256_HMAC, CKM_IBM_ED25519_SHA512<sup>4</sup>, CKM_IBM_ECDSA_OTHER<sup>2</sup>, CKM_IBM_DILITHIUM<sup>3</sup> |
|Digest |CKM_SHA_1, CKM_SHA224, CKM_SHA256, CKM_SHA384, CKM_SHA512, CKM_SHA512_224, CKM_SHA512_256|
|Generate key or generate key pair 	 |CKM_RSA_PKCS_KEY_PAIR_GEN, CKM_RSA_X9_31_KEY_PAIR_GEN, CKM_DSA_KEY_PAIR_GEN, CKM_DSA_PARAMETER_GEN, CKM_EC_KEY_PAIR_GEN (CKM_ECDSA_KEY_PAIR_GEN), CKM_DH_PKCS_KEY_PAIR_GEN, CKM_DH_PKCS_PARAMETER_GEN, CKM_GENERIC_SECRET_KEY_GEN, CKM_AES_KEY_GEN, CKM_DES2_KEY_GEN, CKM_DES3_KEY_GEN, CKM_IBM_DILITHIUM |
|Wrap and unwrap | CKM_RSA_PKCS, CKM_RSA_PKCS_OAEP, CKM_AES_ECB, CKM_AES_CBC, CKM_AES_CBC_PAD, CKM_DES3_ECB, CKM_DES3_CBC, CKM_DES3_CBC_PAD|
|Derive | CKM_ECDH1_DERIVE, CKM_DH_PKCS_DERIVE, CKM_DES3_ECB_ENCRYPT_DATA, CKM_SHA1_KEY_DERIVATION, CKM_SHA224_KEY_DERIVATION, CKM_SHA256_KEY_DERIVATION, CKM_SHA384_KEY_DERIVATION, CKM_SHA512_KEY_DERIVATION|
{: caption="Table 2. Describes the supported GREP11 mechanisms" caption-side="bottom"}


1: This mechanism supports only single-part operations that are not able to utilize any of the Update GREP11 functions, such as `EncryptUpdate`, `DecryptUpdate`, and `DigestUpdate`.

2: This mechanism is only available for GREP11 `SignSingle` and `VerifySingle` operations.

3: This mechanism is not supported by the IBM 4768 crypto card and is not available for `SignUpdate` and `VerifyUpdate` operations.

4: This mechanism supports single-part (`SignInit`, `Sign`, `VerifyInit`, `Verify`), `SignSingle`, and `VerifySingle` operations.


## Supported attributes and key types
{: #grep11-attribute-list}

GREP11 attributes define object characteristics that set up how an object can be used and accessed. The following table shows the supported attributes and their relationship to the various supported key types.

| Attribute    | Description           | Supported key types |
|--------------|-----------------------|---------------------|
| CKA_CHECK_VALUE | The checksum of the key | AES keys, DES keys |
| CKA_COPYABLE | If set to CKA_TRUE, the object can be copied by using the PKCS#11 C_CopyObject function | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys  |
| CKA_DECRYPT  | CK_TRUE if key supports decryption. | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys          |
| CKA_DERIVE   | CK_TRUE if key supports key derivation (other keys can be derived from this key). Default is CK_FALSE. | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys          |
| CKA_EC_PARAMS (CKA_ECDSA_PARAMS) | DER-encoding of an ANSI X9.62 Parameters value. | EC private keys, EC public keys        |
| CKA_ENCRYPT  | CK_TRUE if key supports encryption. | EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys      |
| CKA_EXTRACTABLE  | CK_TRUE if key is extractable and can be wrapped. | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys          |
| CKA_IBM_PQC_PARAMS  | Supporting parameters for post-quantum cryptography mechanisms. In the case of the Dilithium mechanism `CKM_IBM_DILITHIUM`, it provides a marshaled object identifier (OID) that represents the strength of Dilithium algorithm to use. Currently, only the strength of [Dilithium 4 round 2](http://oid-info.com/get/1.3.6.1.4.1.2.267.1.6.5){: external} is supported. |  Dilithium keys  |
| CKA_KEY_TYPE | Type of key.      | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys  |
| CKA_LOCAL  | CK_TRUE only if the key was generated locally (on the token) with a `C_GenerateKey` or `C_GenerateKeyPair` call or created with a `C_CopyObject` call as a copy of a key, which had its CKA_LOCAL attribute set to CK_TRUE.   | EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys          |
| CKA_MODIFIABLE | Set to CK_TRUE if the object can be modified.| EC private keys, EC public keys, RSA private keys, RSA public keys, DH private keys, DH public keys, DSA private keys, DSA public keys, AES keys, DES keys, Generic keys |
| CKA_MODULUS_BITS  | Length in bits of modulus n. |       RSA public keys    |
| CKA_PUBLIC_EXPONENT  | Public exponent e.             |     RSA private keys      |
| CKA_PUBLIC_KEY_INFO | DER-encoding of the SubjectPublicKeyInfo for the public key. The value is derived from the underlying public key data and is empty by default. | RSA public keys, EC public keys |
| CKA_SIGN     | CK_TRUE if key supports signatures where the signature is an appendix to the data. | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys         |
| CKA_TRUSTED  | The certificate or key can be trusted for the application that it was created. | EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys |
| CKA_UNWRAP   | CK_TRUE if key supports unwrapping (can be used to unwrap other keys). | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys         |
| CKA_VALUE_LEN  |    Length in bytes of key value.     |         AES keys  |
| CKA_VERIFY   | CK_TRUE if key supports verification where the signature is an appendix to the data. | EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys |
| CKA_WRAP     | CK_TRUE if key supports wrapping (can be used to wrap other keys). |   EC public keys, RSA public keys, DH public keys, DSA public keys, AES keys, DES keys, Generic keys      |
| CKA_WRAP_WITH_TRUSTED  | CK_TRUE if the key can be wrapped only with a wrapping key that has CKA_TRUSTED set to CK_TRUE. Default is CK_FALSE. | EC private keys, RSA private keys, DH private keys, DSA private keys, AES keys, DES keys, Generic keys          |
{: caption="Table 3. Describes the supported attributes" caption-side="bottom"}

## Supported curves
{: #supported-grep11-curve-name}

The EP11 library supports limited types of curves for certain mechanisms. The following table lists the supported curve names for different mechanisms. The number in the curve name means the supported prime bitcount.

### Supported curves for generating Elliptic Curve (EC) keys
{: #supported-grep11-ec-curve-name}

Mechanism `CKM_EC_KEY_PAIR_GEN` is supported when you call the `GenerateKeyPair` function to generate Elliptic Curve (EC) keys. The curve name parameters must be specified as object identifiers (OIDs) by using `CKA_EC_PARAMS`. You can get the OID by searching the curve name in the [OID repository](http://oid-info.com/basic-search.htm){: external}.

| GREP11 mechanism | Supported curve types | Supported curve names |
| ---------------------| --------------------- | ----------------------|
|CKM_EC_KEY_PAIR_GEN| [National Institute of Standards and Technology (NIST) curves](https://www.ietf.org/rfc/rfc5480.txt){: external} | <ul><li>P-192, also known as secp192r1 and prime192v1.</li><li>P-224, also known as secp224r1.</li><li>P-256, also known as secp256r1 and prime256v1.</li><li>P-384, also known as secp384r1.</li><li>P-521, also known as secp521r.</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Regular Brain pool (BP) curves](https://tools.ietf.org/html/rfc5639){: external} | <ul><li>BP-160R, also known as brainpoolP160r1.</li><li>BP-192R, also known as brainpoolP192r1.</li><li>BP-224R, also known as brainpoolP224r1.</li><li>BP-256R, also known as brainpoolP256r1.</li><li>BP-320R, also known as brainpoolP320r1.</li><li>BP-384R, also known as brainpoolP384r1.</li><li>BP-512R, also known as brainpoolP512r1.</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Twisted Brain pool (BP) curves](https://tools.ietf.org/html/rfc5639){: external} | <ul><li>BP-160T, also known as brainpoolP160t1.</li><li>BP-192T, also known as brainpoolP192t1.</li><li>BP-224T, also known as brainpoolP224t1.</li><li>BP-256T, also known as brainpoolP256t1.</li><li>BP-320T, also known as brainpoolP320t1.</li><li>BP-384T, also known as brainpoolP384t1.</li><li>BP-512T, also known as brainpoolP512t1.</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Standards for Efficient Cryptography (SEC) curves](https://www.secg.org/sec2-v2.pdf){: external} | <ul><li>secp256k1</li></ul> |
|CKM_EC_KEY_PAIR_GEN| [Edwards curves](https://tools.ietf.org/html/rfc8032){: external} | <ul><li>Ed25519</li></ul>|
{: caption="Table 4. Supported curve types for generating EC keys" caption-side="bottom"}



## Performing cryptographic operations with GREP11 functions
{: #grep11-functions}

You can perform cryptographic operations by calling GREP11 functions that are defined based on the EP11 implementation of the PKCS #11 specification. The following function descriptions are created based on the [PKCS #11 specification](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}, with notes specific to EP11. All parameter definitions are in the original form of EP11. For more information about EP11, see [Enterprise PKCS #11 (EP11) Library structure](https://www.ibm.com/security/cryptocards/pciecc4/library){: external}.

EP11 function parameters are mapped to the protocol buffer types that can be found in the following functions. You can learn more about protocol buffer types in [Google Developers](https://developers.google.com/protocol-buffers/docs/proto3#scalar){: external}.

Because the EP11 library is a subset of the PKCS #11 API library, and GREP11 functions are variants from the corresponding EP11 functions, the corresponding functions of EP11 and PKCS #11 are also listed in the GREP11 function tables for your reference.
{: note}

GREP11 supports any programming language with a gRPC library. At the current stage, only code snippets or examples for Golang and JavaScript are included in the API reference. The content is enriched in later phases. The code snippets are based on the following external GitHub repositories that provide complete examples for using the GREP11 API. Some of the code snippets reference helper functions within the examples repositories.

- [The Golang examples repository](https://github.com/IBM-Cloud/hpcs-grep11-go){: external}
- [The JavaScript examples repository](https://github.com/IBM-Cloud/hpcs-grep11-js){: external}

## Retrieving supported crypto algorithms 
{: #grep11-operation-retrieve-mechanisms}

You can use the following functions to retrieve cryptographic algorithms or mechanisms that are supported by GREP11. With this information, you can understand the specific mechanisms that can be set when you call a function. For the full list of supported mechanisms, you can also see the [mechanisms categorized by function groups](/docs/hs-crypto?topic=hs-crypto-faq-security-compliance#faq-EP11-mechanisms).

### GetMechanismList
{: #grep11-GetMechanismList}

The `GetMechanismList` function obtains a list of mechanism types that are supported by a token.

<table id="GetMechanismList_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="GetMechanismList" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_GetMechanismList</code>, which is an implementation of PKCS #11 <code>C_GetMechanismList</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message GetMechanismListRequest {
    }
    message GetMechanismListResponse {
      repeated uint64 Mechs = 2;
    }
    </pre>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="GetMechanismList_EP11" tab-title="Enterprise PKCS #11" tab-group="GetMechanismList" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Implementation of PKCS #11 <code>C_GetMechanismList</code>.
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_GetMechanismList (
      CK_SLOT_ID slot,
      CK_MECHANISM_TYPE_PTR mechs, CK_ULONG_PTR mechslen,
      target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_GetMechanismList</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="GetMechanismList_PKCS11" tab-title="PKCS #11" tab-group="GetMechanismList" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_GetMechanismList</code> is used to obtain a list of mechanism types supported by a token. <code>SlotID</code> is the ID of the token's slot; <code>pulCount</code> points to the location that receives the number of mechanisms.</p>
    <p>
    Two ways are available for an application to call <code>C_GetMechanismList</code>:
    <ol>
    <li>If <code>pMechanismList</code> is <code>NULL_PTR</code>, then all that <code>C_GetMechanismList</code> does is return (in <code>*pulCount</code>) the number of mechanisms, without returning a list of mechanisms. The contents of <code>*pulCount</code> on entry to <code>C_GetMechanismList</code> has no meaning in this case, and the call returns the value <code>CKR_OK</code>.</li>
    <li>If <code>pMechanismList</code> is not <code>NULL_PTR</code>, then <code>*pulCount</code> must contain the size (in terms of <code>CK_MECHANISM_TYPE</code> elements) of the buffer pointed to by <code>pMechanismList</code>. If that buffer is large enough to hold the list of mechanisms, then the list is returned in it, and <code>CKR_OK</code> is returned. If not, then the call to <code>C_GetMechanismList</code> returns the value <code>CKR_BUFFER_TOO_SMALL</code>. In either case, the value <code>*pulCount</code> is set to hold the number of mechanisms.</li>
    </ol>
    </p>
    <p>Because <code>C_GetMechanismList</code> does not allocate any space of its own, an application often calls <code>C_GetMechanismList</code> twice. However, this behavior is by no means required.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_GetMechanismList)(
      CK_SLOT_ID slotID,
      CK_MECHANISM_TYPE_PTR pMechanismList,
      CK_ULONG_PTR pulCount
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_SLOT_ID_INVALID, CKR_TOKEN_NOT_PRESENT, CKR_TOKEN_NOT_RECOGNIZED, CKR_ARGUMENTS_BAD.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    GetMechanismListRequest := &pb.GetMechanismListRequest {
    }

    GetMechanismListResponse, err := cryptoClient.GetMechanismList(context.Background(), GetMechanismListRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.GetMechanismList({}, (err, data) => {
      if (err) throw err;

      console.log('MECHANISMS:', data.Mechs);
    });
    ```
    {: codeblock}


### GetMechanismInfo
{: #grep11-GetMechanismInfo}

The `GetMechanismInfo` Function obtains information about a particular mechanism.

<table id="GetMechanismInfo_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="GetMechanismInfo" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_GetMechanismInfo</code>, which is an implementation of PKCS #11 <code>C_GetMechanismInfo</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message GetMechanismInfoRequest {
      uint64 Mech = 2;
    }
    message GetMechanismInfoResponse {
      MechanismInfo MechInfo = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="GetMechanismInfo_EP11" tab-title="Enterprise PKCS #11" tab-group="GetMechanismInfo" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Implementation of PKCS #11 <code>C_GetMechanismInfo</code>.
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_GetMechanismInfo (
      CK_SLOT_ID slot,
      CK_MECHANISM_TYPE mech,
      CK_MECHANISM_INFO_PTR mechInfo,
      target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_GetMechanismInfo</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="GetMechanismInfo_PKCS11" tab-title="PKCS #11" tab-group="GetMechanismInfo" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_GetMechanismInfo</code> obtains information about a particular mechanism that might be supported by a token. <code>slotID</code> is the ID of the token's slot; <code>type</code> is the type of mechanism; <code>pInfo</code> points to the location that receives the mechanism information.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_GetMechanismInfo)(
      CK_SLOT_ID slotID,
      CK_MECHANISM_TYPE type,
      CK_MECHANISM_INFO_PTR pInfo
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_OK, CKR_SLOT_ID_INVALID, CKR_TOKEN_NOT_PRESENT, CKR_TOKEN_NOT_RECOGNIZED, CKR_ARGUMENTS_BAD.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    GetMechanismInfoRequest := &pb.GetMechanismInfoRequest {
        Mech: ep11.CKM_RSA_PKCS,
    }

    GetMechanismInfoResponse, err := cryptoClient.GetMechanismInfo(context.Background(), GetMechanismInfoRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.GetMechanismInfo({
      Mech: ep11.CKM_AES_KEY_GEN
      }, (err, data) => {
        if (err) throw err;

        console.log('MECHANISM INFO:', data.MechInfo);
    });
    ```
    {: codeblock}


## Generating and deriving keys
{: #grep11-operation-generate-keys}

GREP11 provides the following functions to generate symmetric and asymmetric cryptographic keys. Based on the mechanism and key length you specify, you can generate various types of keys for various usages. You can also derive a key from a base key to stretch keys into longer keys or to obtain keys of a required format.

### GenerateKey
{: #grep11-GenerateKey}

The `GenerateKey` function generates a secret key for symmetric encryption.

<table id="GenerateKey_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="GenerateKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_GenerateKey</code>, which is an implementation of PKCS #11 <code>C_GenerateKey</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message GenerateKeyRequest {
      Mechanism Mech = 1;
      map&lt;uint64,AttributeValue&gt; Template = 6;
    }
    message GenerateKeyResponse {
      bytes KeyBytes = 4;
      bytes CheckSum = 5;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="GenerateKey_EP11" tab-title="Enterprise PKCS #11" tab-group="GenerateKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_GenerateKey</code>.</p>
    <p>TDES keys are generated with proper parity, which is not observable by the host. But it is needed for proper interoperability: other PKCS #11 implementations needs to reject DES keys with parity problems.</p>
    <p>If an object is tied to a session, <code>(pin, plen)</code> must be return by <code>Login</code> to that session. Leaving <code>pin</code> <code>NULL</code> creates a public object, one not bound to a login session.</p>
    <p><code>(key, klen)</code> returns the key blob. <code>(csum, clen)</code> contains the key's checksum, that is, the most significant bytes of an all-zero block encrypted by the key. NULL <code>clen</code> is possible, for example for symmetric-key mechanisms without <code>CKA_CHECK_VALUE</code> parameters (such as RC4).</p>
    <p><code>ptempl</code> is used only if the key length (that is, the <code>CKA_VALUE_LEN</code> attribute) is needed by the mechanism. If the mechanism implicitly specifies key size, <code>ptempl</code> is not checked for size.</p>
    <p>DSA and DH parameter generation ignores <code>(csum, clen)</code>, generating only parameter structures.</p>
    <p>DSA, DH parameters (<code>CKM_DSA_PARAMETER_GEN</code>): pass modulus bitcount in <code>CKA_PRIME_BITS</code> of attributes. Writes P,Q,G structure as cleartext output (that is, not a blob).</p>
    <p>The <code>pin</code> blob was output from: <code>Login</code>.</p>
    <p>PKCS #11 <code>phKey</code> is not mapped to any EP11 parameter. (Host library must bind wrapped key to handle.)</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_GenerateKey (
      CK_MECHANISM_PTR mech,
      CK_ATTRIBUTE_PTR template, CK_ULONG templatelen,
      const unsigned char *pin, size_t pinlen,
      unsigned char *key, size_t *keylen,
      unsigned char *checkSum, size_t *checkSumlen,
      target_t target
      );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_GenerateKey</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="GenerateKey_PKCS11" tab-title="PKCS #11" tab-group="GenerateKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_GenerateKey</code> generates a secret key or set of domain parameters, creating a new object. <code>hSession</code> is the session's handle; <code>pMechanism</code> points to the generation mechanism; <code>pTemplate</code> points to the template for the new key or set of domain parameters; <code>ulCount</code> is the number of attributes in the template; <code>phKey</code> points to the location that receives the handle of the new key or set of domain parameters.</p>
    <p>If the generation mechanism is for domain parameter generation, the <code>CKA_CLASS</code> attribute has the value <code>CKO_DOMAIN_PARAMETERS</code>; otherwise, it has the value <code>CKO_SECRET_KEY</code>.</p>
    <p>Since the type of key or domain parameters to be generated is implicit in the generation mechanism, the template does not need to supply a key type. If it does supply a key type that is inconsistent with the generation mechanism, <code>C_GenerateKey</code> fails and returns the error code <code>CKR_TEMPLATE_INCONSISTENT</code>. The <code>CKA_CLASS</code> attribute is treated in the same way.</p>
    <p>If a call to <code>C_GenerateKey</code> cannot support the precise template that is supplied to it, it fails and returns without creating an object.</p>
    <p>The object created by a successful call to <code>C_GenerateKey</code> has the <code>CKA_LOCAL</code> attribute set to <code>CK_TRUE</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_GenerateKey)(
      CK_SESSION_HANDLE hSession
      CK_MECHANISM_PTR pMechanism,
      CK_ATTRIBUTE_PTR pTemplate,
      CK_ULONG ulCount,
      CK_OBJECT_HANDLE_PTR phKey
      );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Setup the AES key's attributes
    keyTemplate := ep11.EP11Attributes{
        ep11.CKA_VALUE_LEN:   keyLen / 8,
        ep11.CKA_WRAP:        false,
        ep11.CKA_UNWRAP:      false,
        ep11.CKA_ENCRYPT:     true,
        ep11.CKA_DECRYPT:     true,
        ep11.CKA_EXTRACTABLE: false,
    }

    GenerateKeyRequest := &pb.GenerateKeyRequest{
        Mech:     &pb.Mechanism{Mechanism: ep11.CKM_AES_KEY_GEN},
        Template: util.AttributeMap(keyTemplate),
    }

    GenerateKeyResponse, err := cryptoClient.GenerateKey(context.Background(), GenerateKeyRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    let keyLen = 128;

    let keyTemplate = new util.AttributeMap(
      new util.Attribute(ep11.CKA_VALUE_LEN, keyLen / 8),
      new util.Attribute(ep11.CKA_WRAP, false),
      new util.Attribute(ep11.CKA_UNWRAP, false),
      new util.Attribute(ep11.CKA_ENCRYPT, true),
      new util.Attribute(ep11.CKA_DECRYPT, true),
      new util.Attribute(ep11.CKA_EXTRACTABLE, false),
      new util.Attribute(ep11.CKA_TOKEN, true)
      );
    client.GenerateKey({
      Mech: { Mechanism: ep11.CKM_AES_KEY_GEN },
      Template: keyTemplate,
      KeyId: uuidv4()
    }, (err, data={}) => {
      cb(err, data.KeyBytes, data.CheckSum);
    });

    ```
    {: codeblock}


### GenerateKeyPair
{: #grep11-GenerateKeyPair}

The `GenerateKeyPair` function generates a public key and private key pair.

<table id="GenerateKeyPair_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="GenerateKeyPair" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_GenerateKeyPair</code>, which is an implementation of PKCS #11 <code>C_GenerateKeyPair</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message GenerateKeyPairRequest {
      Mechanism Mech = 1;
      map&lt;uint64,AttributeValue&gt; PrivKeyTemplate = 7;
      map&lt;uint64,AttributeValue&gt; PubKeyTemplate = 8;
      }
    message GenerateKeyPairResponse {
      bytes PrivKeyBytes = 5;
      bytes PubKeyBytes = 6;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="GenerateKeyPair_EP11" tab-title="Enterprise PKCS #11" tab-group="GenerateKeyPair" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_GenerateKeyPair</code>.</p>
    <p>Keypair parameters are retrieved from <code>pmech</code>, <code>ppublic</code>, and <code>pprivate</code> parameters. For RSA keys, <code>ppublic</code> specifies the modulus size.</p>
    <p>In FIPS mode, only RSA moduluses of 1024+256 <code>n</code> bits are supported (integer <code>n</code>). Non-FIPS mode can generate keys of any even number of bits between the limits in the mechanism parameter list.</p>
    <p>Public key is formatted as a standard SPKI (subject public key information), readable by most libraries. It is integrity-protected by a transport-key specific MAC, which is not part of the SPKI itself. DSA parameter generation returns a non-SPKI structure in the public key field.</p>
    <p>If you tie an object to a session, <code>(pin, plen)</code> must be returned by <code>Login</code> to that session. Leaving <code>pin</code> <code>NULL</code> creates a public object, one that survives the login session.</p>
    <p>Returns wrapped private key to <code>(key, klen)</code>, public key as a MACed ASN.1/DER structure in <code>(pubkey, pklen)</code>.</p>
    <p>The following supported parameter combinations with special notes are beyond what are documented by PKCS #11:</p>
    <p>RSA keys reject public exponents below 17 (0x11). Control points can further restrict the accepted minimum. The Fermat4 exponent, 0x10001, is controlled by a specific control point, matching public-exponent restrictions of FIPS 186-3 (section B.3.1).</p> <p>EC keys (<code>CKM_EC_KEY_PAIR_GEN</code>): curve parameters can be specified as OIDs or symbolic names (our namedCurve variant). Supported symbolic names are "<code>P-nnn</code>" for NIST curves (<code>nnn</code> is a supported prime bitcount, 192 - 521), "<code>BP-nnnR</code>" for regular BP curve. (Names must be supplied as ASCII strings, without zero-termination.)</p>
    <p>DSA keys (<code>CKM_DSA_KEY_PAIR_GEN</code>): pass P,Q,G structure as the <code>CKA_IBM_STRUCT_PARAMS</code> attribute of public attributes. Individual P,Q,G parameters might not be passed through regular PKCS #11 parameters, they must be combined to a single structure.</p>
    <p>DH keys (<code>CKM_DH_PKCS_KEY_PAIR_GEN</code>): pass P,G structure as the <code>CKA_IBM_STRUCT_PARAMS</code> attribute of public attributes. Individual P,G parameters might not be passed through regular PKCS #11 parameters, they must be combined to a single structure. When you select a private-key (X) bitcount, use the <code>XCP_U32_VALUE_BITS</code> attribute. If not present, or an explicit 0 is supplied, bitcount is selected based on P bitcount.</p>
    <p>Use of session (Login) state replaces standard use of sessions. The mapping is outside library scope.</p>
    <p>The <code>pin</code> blob was output from: <code>Login</code>.</p>
    <p>PKCS #11 <code>hSession</code> is not mapped to any EP11 parameter. (The call is not directly associated with any session.)</p>
    <p>PKCS #11 <code>phPublicKey</code> is not mapped to any EP11 parameter. (Host library must associate pubkey (SPKI) with handle.)</p>
    <p>PKCS #11 <code>phPrivateKey</code> is not mapped to any EP11 parameter. (Host library must associate private key with handle.)</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_GenerateKeyPair (
      CK_MECHANISM_PTR mech,
      CK_ATTRIBUTE_PTR pubKeyTemplate, CK_ULONG pubKeyTemplatelen,
      CK_ATTRIBUTE_PTR privKeyTemplate, CK_ULONG privKeyTemplatelen,
      const unsigned char *pin, size_t pinlen,
      unsigned char *privKey, size_t *privKeylen,
      unsigned char *pubKey, size_t *pubKeylen,
      target_t target
      );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_GenerateKeyPair</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="GenerateKeyPair_PKCS11" tab-title="PKCS #11" tab-group="GenerateKeyPair" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_GenerateKeyPair</code> generates a public and private key pair, creating new key objects. <code>hSession</code> is the session's handle; <code>pMechanism</code> points to the key generation mechanism; <code>pPublicKeyTemplate</code> points to the template for the public key; <code>ulPublicKeyAttributeCount</code> is the number of attributes in the public-key template; <code>pPrivateKeyTemplate</code> points to the template for the private key; <code>ulPrivateKeyAttributeCount</code> is the number of attributes in the private-key template; <code>phPublicKey</code> points to the location that receives the handle of the new public key; <code>phPrivateKey</code> points to the location that receives the handle of the new private key.</p>
    <p>Since the types of keys to be generated are implicit in the key pair generation mechanism, the templates do not need to supply key types. If one of the templates does supply a key type that is inconsistent with the key generation mechanism, <code>C_GenerateKeyPair</code> fails and returns the error code <code>CKR_TEMPLATE_INCONSISTENT</code>. The <code>CKA_CLASS</code> attribute is treated similarly.</p>
    <p>If a call to <code>C_GenerateKeyPair</code> cannot support the precise templates that are supplied to it, it fails and returns without creating any key objects.</p>
    <p>A call to <code>C_GenerateKeyPair</code> never creates just one key and returns. A call can fail, and create no keys; or it can succeed, and create a matching public and private key pair.</p>
    <p>The key objects created by a successful call to <code>C_GenerateKeyPair</code> have the <code>CKA_LOCAL</code> attributes set to <code>CK_TRUE</code>.</p>
    <p>Note carefully the order of the arguments to <code>C_GenerateKeyPair</code>. The last two arguments do not have the same order as they did in the original Cryptoki Version 1.0 document. The order of these two arguments caused some unfortunate confusion.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_GenerateKeyPair)(
      CK_SESSION_HANDLE hSession,
      CK_MECHANISM_PTR pMechanism,
      CK_ATTRIBUTE_PTR pPublicKeyTemplate,
      CK_ULONG ulPublicKeyAttributeCount,
      CK_ATTRIBUTE_PTR pPrivateKeyTemplate,
      CK_ULONG ulPrivateKeyAttributeCount,
      CK_OBJECT_HANDLE_PTR phPublicKey,
      CK_OBJECT_HANDLE_PTR phPrivateKey
      );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_DOMAIN_PARAMS_INVALID, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Generate RSA key pair
    publicExponent := []byte{0x11}
    publicKeyTemplate := ep11.EP11Attributes{
        ep11.CKA_ENCRYPT:         true,
        ep11.CKA_VERIFY:          true,
        ep11.CKA_MODULUS_BITS:    2048,
        ep11.CKA_PUBLIC_EXPONENT: publicExponent,
        ep11.CKA_EXTRACTABLE:     false,
    }
    privateKeyTemplate := ep11.EP11Attributes{
        ep11.CKA_PRIVATE:     true,
        ep11.CKA_SENSITIVE:   true,
        ep11.CKA_DECRYPT:     true,
        ep11.CKA_SIGN:        true,
        ep11.CKA_EXTRACTABLE: false,
    }
    GenerateKeypairRequest := &pb.GenerateKeyPairRequest{
        Mech:            &pb.Mechanism{Mechanism: ep11.CKM_RSA_PKCS_KEY_PAIR_GEN},
        PubKeyTemplate:  util.AttributeMap(publicKeyTemplate),
        PrivKeyTemplate: util.AttributeMap(privateKeyTemplate),
    }
    GenerateKeyPairResponse, err := cryptoClient.GenerateKeyPair(context.Background(), GenerateKeypairRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    const publicKeyTemplate = new util.AttributeMap(
      new util.Attribute(ep11.CKA_ENCRYPT, true),
      new util.Attribute(ep11.CKA_VERIFY, true),
      new util.Attribute(ep11.CKA_MODULUS_BITS, 2048),
      new util.Attribute(ep11.CKA_PUBLIC_EXPONENT, publicExponent),
      new util.Attribute(ep11.CKA_EXTRACTABLE, false)
    );

    const privateKeyTemplate = new util.AttributeMap(
      new util.Attribute(ep11.CKA_PRIVATE, true),
      new util.Attribute(ep11.CKA_SENSITIVE, true),
      new util.Attribute(ep11.CKA_DECRYPT, true),
      new util.Attribute(ep11.CKA_SIGN, true),
      new util.Attribute(ep11.CKA_EXTRACTABLE, false),
    );

    client.GenerateKeyPair({
      Mech: {
        Mechanism: ep11.CKM_RSA_PKCS_KEY_PAIR_GEN
      },
      PubKeyTemplate: publicKeyTemplate,
      PrivKeyTemplate: privateKeyTemplate,
      PubKeyId: uuidv4(),
      PrivKeyId: uuidv4()
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

### DeriveKey
{: #grep11-DeriveKey}

The `DeriveKey` function derives a key from a base key.

<table id="DeriveKey_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DeriveKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DeriveKey</code>, which is an implementation of PKCS #11 <code>C_DeriveKey</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DeriveKeyRequest {
        Mechanism Mech = 1;
        bytes BaseKey = 3;
        bytes Data = 4;
        map&lt;uint64,AttributeValue&gt; Template = 8;
    }
    message DeriveKeyResponse {
        bytes NewKeyBytes = 6;
        bytes CheckSum = 7;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DeriveKey_EP11" tab-title="Enterprise PKCS #11" tab-group="DeriveKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_DeriveKey</code>.</p>
    <p>The <code>basekey</code>,<code>bklen</code> blob must be mapped from the PKCS #11 <code>hBaseKey</code> parameter.</p>
    <p>PKCS #11 <code>hSession</code> is not mapped to any EP11 parameter. (The call is not directly associated with any session.)</p>
    <p>PKCS #11 <code>phKey</code> is not mapped to any EP11 parameter. (Host library must bind returned key to handle.)</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DeriveKey (
        CK_MECHANISM_PTR mech,
        CK_ATTRIBUTE_PTR template, CK_ULONG templatelen,
        const unsigned char *baseKey, size_t baseKeylen,
        const unsigned char *data, size_t datalen,
        const unsigned char *pin, size_t pinlen,
        unsigned char *newKey, size_t *newKeylen,
        unsigned char *checkSum, size_t *checkSumlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DeriveKey</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="DeriveKey_PKCS11" tab-title="PKCS #11" tab-group="DeriveKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_DeriveKey</code> derives a key from a base key, creating a new key object. <code>hSession</code> is the session's handle; <code>pMechanism</code> points to a structure that specifies the key derivation chanism; <code>hBaseKey</code> is the handle of the base key; <code>pTemplate</code> points to the template for the new key; <code>ulAttributeCount</code> is the number of attributes in the template; and <code>phKey</code> points to the location that receives the handle of the derived key.</p>
    <p>The values of the <code>CKA_SENSITIVE</code>, <code>CKA_ALWAYS_SENSITIVE</code>, <code>CKA_EXTRACTABLE</code>, and <code>KA_NEVER_EXTRACTABLE</code> attributes for the base key affect the values that these attributes can hold for the newly derived key. See the description of each particular key-derivation mechanism in Section 5.16.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749" target="_blank">PKCS #11 API specification</a> for any constraints of this type.</p>
    <p>If a call to <code>C_DeriveKey</code> cannot support the precise template that is supplied to it, it fails and returns without creating any key object.</p>
    <p>The key object created by a successful call to <code>C_DeriveKey</code> has the <code>CKA_LOCAL</code> attribute set to <code>CK_FALSE</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_DeriveKey)(
        CK_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism,
        CK_OBJECT_HANDLE hBaseKey,
        CK_ATTRIBUTE_PTR pTemplate,
        CK_ULONG ulAttributeCount,
        CK_OBJECT_HANDLE_PTR phKey
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_DOMAIN_PARAMS_INVALID, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Derive AES key for Alice
    deriveKeyTemplate := ep11.EP11Attributes{
        ep11.CKA_CLASS:     ep11.CKO_SECRET_KEY,
        ep11.CKA_KEY_TYPE:  ep11.CKK_AES,
        ep11.CKA_VALUE_LEN: 128 / 8,
        ep11.CKA_ENCRYPT:   true,
        ep11.CKA_DECRYPT:   true,
    }
    // Extract Bob's EC coordinates
    combinedCoordinates, err := util.GetPubkeyBytesFromSPKI(bobECKeypairResponse.PubKeyBytes)
    if err != nil {
        return nil, fmt.Errorf("Bob's EC public key cannot obtain coordinates: %s", err)
    }

    aliceDeriveKeyRequest := &pb.DeriveKeyRequest{
        Mech:     &pb.Mechanism{Mechanism: ep11.CKM_ECDH1_DERIVE, Parameter: util.SetMechParm(combinedCoordinates)},
        Template: util.AttributeMap(deriveKeyTemplate),
        BaseKey:  aliceECKeypairResponse.PrivKeyBytes,
    }

    // Derive AES key for Alice
    aliceDeriveKeyResponse, err := cryptoClient.DeriveKey(context.Background(),  aliceDeriveKeyRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    //results are created through GenerateKeyPair
    const [alice, bob] = results;

    const deriveKeyTemplate = new util.AttributeMap(
    new util.Attribute(ep11.CKA_CLASS, ep11.CKO_SECRET_KEY),
    new util.Attribute(ep11.CKA_KEY_TYPE, ep11.CKK_AES),
    new util.Attribute(ep11.CKA_VALUE_LEN, 128/8),
    new util.Attribute(ep11.CKA_ENCRYPT, true),
    new util.Attribute(ep11.CKA_DECRYPT, true),
    );

    const derived = [];

    async.eachSeries([
    { PubKey: bob.PubKeyBytes, PrivKey: alice.PrivKeyBytes },
    { PubKey: alice.PubKeyBytes, PrivKey: bob.PrivKeyBytes }
    ], (data, cb) => {
    const combinedCoordinates = util.getPubKeyBytesFromSPKI(data.PubKey);

    client.DeriveKey({
      Mech: {
        Mechanism: ep11.CKM_ECDH1_DERIVE,
        ParameterB: combinedCoordinates
      },
      Template: deriveKeyTemplate,
      BaseKey: data.PrivKey
    }, (err, data={}) => {
      if (!err) {
        derived.push(data);
      }

      cb(err);
    });
    }
    ```
    {: codeblock}

## Protecting keys
{: #grep11-operation-manage-keys}

You can protect a key by wrapping it and then decrypt the key by invoking the unwrapping feature.

### WrapKey
{: #grep11-WrapKey}

The `WrapKey` function wraps (encrypts) a key.

<table id="WrapKey_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="WrapKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_WrapKey</code>, which is an implementation of PKCS #11 <code>C_WrapKey</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message WrapKeyRequest {
        bytes Key = 1;
        bytes KeK = 2;
        bytes MacKey = 3;
        Mechanism Mech = 4;
    }
    message WrapKeyResponse {
        bytes Wrapped = 5;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="WrapKey_EP11" tab-title="Enterprise PKCS #11" tab-group="WrapKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Implementation of PKCS #11 <code>C_WrapKey</code>.
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_WrapKey (
        const unsigned char *key, size_t keylen,
        const unsigned char *keK, size_t keKlen,
        const unsigned char *macKey, size_t macKeylen,
        const CK_MECHANISM_PTR mech,
        CK_BYTE_PTR wrapped, CK_ULONG_PTR wrappedlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_WrapKey</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="WrapKey_PKCS11" tab-title="PKCS #11" tab-group="WrapKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_WrapKey</code> wraps (that is, encrypts) a private or secret key. <code>hSession</code> is the session's handle; <code>pMechanism</code> points to the wrapping mechanism; <code>hWrappingKey</code> is the handle of the wrapping key; <code>hKey</code> is the handle of the key to be wrapped; <code>pWrappedKey</code> points to the location that receives the wrapped key; and <code>pulWrappedKeyLen</code> points to the location that receives the length of the wrapped key.</p>
    <p><code>C_WrapKey</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The <code>CKA_WRAP</code> attribute of the wrapping key, which indicates whether the key supports wrapping, must be <code>CK_TRUE</code>. The <code>CKA_EXTRACTABLE</code> attribute of the key to be wrapped must also be <code>CK_TRUE</code>.</p>
    <p>If the key to be wrapped cannot be wrapped for some token-specific reason, despite its having its <code>CKA_EXTRACTABLE</code> attribute set to <code>CK_TRUE</code>, then <code>C_WrapKey</code> fails with error code <code>CKR_KEY_NOT_WRAPPABLE</code>. If it cannot be wrapped with the specified wrapping key and mechanism solely because of its length, then <code>C_WrapKey</code> fails with error code <code>CKR_KEY_SIZE_RANGE</code>.</p>
    <p>
    <code>C_WrapKey</code> can be used in the following situations:
    <ul>
    <li>To wrap any secret key with a public key that supports encryption and decryption.</li>
    <li>To wrap any secret key with any other secret key. Consideration must be given to key size and mechanism strength or the token might not allow the operation.</li>
    <li>To wrap a private key with any secret key.</li>
    </ul>
    </p>
    <p>Tokens vary in which types of keys can be wrapped with which mechanisms.</p>
    <p>To partition the wrapping keys so that they can wrap only a subset of extractable keys, the attribute <code>CKA_WRAP_TEMPLATE</code> can be used on the wrapping key to specify an attribute set that can be compared against the attributes of the key to be wrapped. If all attributes match according to the <code>C_FindObject</code> rules of attribute matching, the wrap operation proceeds. The value of this attribute is an attribute template and the size is the number of items in the template times the size of <code>CK_ATTRIBUTE</code>. If this attribute is not supplied, any template is acceptable. If an attribute is not present, it is not checked. If any attribute mismatch occurs on an attempt to wrap a key, the function returns <code>CKR_KEY_HANDLE_INVALID</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_WrapKey)(
        CK_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism,
        CK_OBJECT_HANDLE hWrappingKey,
        CK_OBJECT_HANDLE hKey,
        CK_BYTE_PTR pWrappedKey,
        CK_ULONG_PTR pulWrappedKeyLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_HANDLE_INVALID, CKR_KEY_NOT_WRAPPABLE, CKR_KEY_SIZE_RANGE, CKR_KEY_UNEXTRACTABLE, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN, CKR_WRAPPING_KEY_HANDLE_INVALID, CKR_WRAPPING_KEY_SIZE_RANGE, CKR_WRAPPING_KEY_TYPE_INCONSISTENT.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    WrapKeyRequest := &pb.WrapKeyRequest {
        Mech: &pb.Mechanism{Mechanism: ep11.CKM_RSA_PKCS},
        KeK:  GenerateKeyPairResponse.PubKeyBytes,
        Key:  GenerateKeyResponse.KeyBytes,
    }

    WrapKeyResponse, err := cryptoClient.WrapKey(context.Background(), WrapKeyRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.WrapKey({
      Mech: {
        Mechanism: ep11.CKM_RSA_PKCS
      },
      KeK: rsa.PubKeyBytes,
      Key: aes.KeyBytes
    }, (err, data={}) => {
      cb(err, data.Wrapped);
    });
    ```
    {: codeblock}


### UnwrapKey
{: #grep11-UnwrapKey}

The `UnwrapKey` function unwraps (decrypts) a key.

<table id="UnwrapKey_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="UnwrapKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_UnwrapKey</code>, which is an implementation of PKCS #11 <code>C_UnwrapKey</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message UnwrapKeyRequest {
        bytes Wrapped = 1;
        bytes KeK = 2;
        bytes MacKey = 3;
        Mechanism Mech = 5;
        map&lt;uint64,AttributeValue&gt; Template = 9;
    }
    message UnwrapKeyResponse {
        bytes UnwrappedBytes = 7;
        bytes CheckSum = 8;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="UnwrapKey_EP11" tab-title="Enterprise PKCS #11" tab-group="UnwrapKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
	<td>
    <p>Implementation of PKCS #11 <code>C_UnwrapKey</code>.</p>
    <p><code>uwmech</code> specifies the encryption mechanism that is used to decrypt wrapped data. <code>ptempl</code> is a <em>key(pair)</em> parameter list, specifying how to transform the unwrapped data to a new key (must include <code>CKA_KEY_TYPE</code>).</p>
    <p>The generated object is returned under <code>(unwrapped, uwlen)</code> as a blob. Symmetric keys return their key checksum (3 bytes) under <code>(csum, cslen)</code>; public-key objects return their public key as an SPKI in <code>(csum, cslen)</code>. Both forms are followed by a 4-byte big-endian value, encoding bitcount of the unwrapped key.</p>
    <p>When an SPKI is being transformed to a MACed SPKI, one must use CKM_IBM_TRANSPORTKEY as the unwrapping mechanism. This mode supplies the raw SPKI as wrapped data, and ignores the KEK.</p>
    <p><code>UnwrapKey</code> produces parity-adjusted DES keys (within the blobs), but tolerates input with improper parity.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_UnwrapKey (
        const CK_BYTE_PTR wrapped, CK_ULONG wrappedlen,
        const unsigned char *keK, size_t keKlen,
        const unsigned char *macKey, size_t macKeylen,
        const unsigned char *pin, size_t pinlen,
        const CK_MECHANISM_PTR mech,
        const CK_ATTRIBUTE_PTR template, CK_ULONG templatelen,
        unsigned char *unwrapped, size_t *unwrappedlen,
        CK_BYTE_PTR checkSum, CK_ULONG *checkSumlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_UnwrapKey</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="UnwrapKey_PKCS11" tab-title="PKCS #11" tab-group="UnwrapKey" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_UnwrapKey</code> unwraps (that is, decrypts) a wrapped key, creating a new private key or secret key object. <code>hSession</code> is the session's handle; <code>pMechanism</code> points to the unwrapping mechanism; <code>hUnwrappingKey</code> is the handle of the unwrapping key; <code>pWrappedKey</code> points to the wrapped key; <code>ulWrappedKeyLen</code> is the length of the wrapped key; <code>pTemplate</code> points to the template for the new key; <code>ulAttributeCount</code> is the number of attributes in the template; <code>phKey</code> points to the location that receives the handle of the recovered key.</p>
    <p>The <code>CKA_UNWRAP</code> attribute of the unwrapping key, which indicates whether the key supports unwrapping, must be <code>CK_TRUE</code>.</p>
    <p>The new key has the <code>CKA_ALWAYS_SENSITIVE</code> attribute set to <code>CK_FALSE</code>, and the <code>CKA_NEVER_EXTRACTABLE</code> attribute set to <code>CK_FALSE</code>. The <code>CKA_EXTRACTABLE</code> attribute is by default set to <code>CK_TRUE</code>.</p>
    <p>Some mechanisms can modify, or attempt to modify. The contents of the <code>pMechanism</code> structure at the same time that the key is unwrapped.</p>
    <p>If a call to <code>C_UnwrapKey</code> cannot support the precise template that is supplied to it, it fails and returns without creating any key object.</p>
    <p>The key object created by a successful call to <code>C_UnwrapKey</code> has its <code>CKA_LOCAL</code> attribute set to <code>CK_FALSE</code>.</p>
    <p>To partition the unwrapping keys so they can unwrap only a subset of keys the attribute <code>CKA_UNWRAP_TEMPLATE</code> can be used on the unwrapping key to specify an attribute set that is added to attributes of the key to be unwrapped. If the attributes do not conflict with the user supplied attribute template, in <code>pTemplate</code>, the unwrap operation proceeds. The value of this attribute is an attribute template and the size is the number of items in the template times the size of <code>CK_ATTRIBUTE</code>. If this attribute is not present on the unwrapping key, then no extra attributes are added. If any attribute conflict occurs on an attempt to unwrap a key, then the function SHALL return <code>CKR_TEMPLATE_INCONSISTENT</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_UnwrapKey)(
        CK_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism,
        CK_OBJECT_HANDLE hUnwrappingKey,
        CK_BYTE_PTR pWrappedKey,
        CK_ULONG ulWrappedKeyLen,
        CK_ATTRIBUTE_PTR pTemplate,
        CK_ULONG ulAttributeCount,
        CK_OBJECT_HANDLE_PTR phKey
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_DOMAIN_PARAMS_INVALID, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_UNWRAPPING_KEY_HANDLE_INVALID, CKR_UNWRAPPING_KEY_SIZE_RANGE, CKR_UNWRAPPING_KEY_TYPE_INCONSISTENT, CKR_USER_NOT_LOGGED_IN, CKR_WRAPPED_KEY_INVALID, CKR_WRAPPED_KEY_LEN_RANGE.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    aesUnwrapKeyTemplate := ep11.EP11Attributes{
        ep11.CKA_CLASS:       ep11.CKO_SECRET_KEY,
        ep11.CKA_KEY_TYPE:    ep11.CKK_AES,
        ep11.CKA_VALUE_LEN:   128 / 8,
        ep11.CKA_ENCRYPT:     true,
        ep11.CKA_DECRYPT:     true,
        ep11.CKA_EXTRACTABLE: true, // must be true to be wrapped
    }
    UnwrapKeyRequest := &pb.UnwrapKeyRequest{
        Mech:     &pb.Mechanism{Mechanism: ep11.CKM_RSA_PKCS},
        KeK:      GenerateKeyPairResponse.PrivKeyBytes,
        Wrapped:  WrapKeyResponse.Wrapped,
        Template: util.AttributeMap(aesUnwrapKeyTemplate),
    }

    // Unwrap the AES key
    UnwrapKeyResponse, err := cryptoClient.UnwrapKey(context.Background(), UnwrapKeyRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    const aesUnwrapKeyTemplate = new util.AttributeMap(
    new util.Attribute(ep11.CKA_CLASS, ep11.CKO_SECRET_KEY),
    new util.Attribute(ep11.CKA_KEY_TYPE, ep11.CKK_AES),
    new util.Attribute(ep11.CKA_VALUE_LEN, 128/8),
    new util.Attribute(ep11.CKA_ENCRYPT, true),
    new util.Attribute(ep11.CKA_DECRYPT, true),
    new util.Attribute(ep11.CKA_EXTRACTABLE, true)
    );

    client.UnwrapKey({
        Mech: {
            Mechanism: ep11.CKM_RSA_PKCS
        },
        KeK: rsa.PrivKeyBytes,
        Wrapped: wrapped,
        Template: aesUnwrapKeyTemplate
    }, (err, data={}) => {
        cb(err, wrapped, data.UnwrappedBytes, data.CheckSum);
    });
    ```
    {: codeblock}

### RewrapKeyBlob
{: #grep11-rewrapKeyBlob}

The `RewrapKeyBlob` function reencrypts generated key binary large objects (BLOBs) with the new committed master key that is contained within the HSM. Keys that are reencrypted can be used only after the HSM is finalized with the new committed master key.

This function is a special administration command that is supported only by GREP11. There is no corresponding EP11 function or PKCS #11 function for `RewrapKeyBlob`.
{: note}

<table id="RewrapKeyBlob_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="RewrapKeyBlob" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Transfers ownership of a BLOB that is controlled by the current master key to the new master key when the new master key is committed.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message RewrapKeyBlobRequest {
    	bytes WrappedKey = 1;
    }
    message RewrapKeyBlobResponse {
    	bytes RewrappedKey = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    RewrapKeyBlobRequest := &pb.RewrapKeyBlobRequest {
        WrappedKey: GenerateKeyResponse.KeyBytes,
    }

    // Rewrap an existing key blob using the HSM's new wrapping key
    RewrapKeyBlobResponse, err := cryptoClient.RewrapKeyBlob(context.Background(),  RewrapKeyBlobRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.RewrapKeyBlob({
      WrappedKey: wrappedKey
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

## Retrieving and modifying attributes for keys 
{: #grep11-operation-attribute-value}

When you generate keys or perform key operations, you define an attribute template as one of the parameters. You can retrieve the attributes for a specific key object and modify some attributes after the key is created.

### GetAttributeValue
{: #grep11-GetAttributeValue}

The `GetAttributeValue` function obtains an attribute value of an object.

<table id="GetAttributeValue_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="GetAttributeValue" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_GetAttributeValue</code>, which is an implementation of PKCS #11 <code>C_GetAttributeValue</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message GetAttributeValueRequest {
        bytes Object = 1;
        map&lt;uint64,AttributeValue&gt; Attributes = 3;
    }
    message GetAttributeValueResponse {
        map&lt;uint64,AttributeValue&gt; Attributes = 4;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="GetAttributeValue_EP11" tab-title="Enterprise PKCS #11" tab-group="GetAttributeValue" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 <code>C_GetAttributeValue</code>.</p>
    <p>Does not represent or need sessions (part of blob), therefore does not use the <code>hSession</code> parameter.</p>
    <p>EP11 uses more straightforward ways to decode, such as enumerating actual values instead of being more generic.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_GetAttributeValue (
        const unsigned char *object, size_t objectlen,
        CK_ATTRIBUTE_PTR attributes, CK_ULONG attributeslen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_GetAttributeValue</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="GetAttributeValue_PKCS11" tab-title="PKCS #11" tab-group="GetAttributeValue" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_GetAttributeValue</code> obtains the value of one or more attributes of an object. <code>hSession</code> is the session's handle; <code>hObject</code> is the object's handle; <code>pTemplate</code> points to a template that specifies which attribute values are to be obtained, and receives the attribute values; <code>ulCount</code> is the number of attributes in the template.</p>
    <p>
    For each (<code>type</code>, <code>pValue</code>, <code>ulValueLen</code>) triple in the template, <code>C_GetAttributeValue</code> performs the following algorithm:
    <ol>
    <li>If the specified attribute (that is, the attribute that is specified by the type field) for the object cannot be revealed because the object is sensitive or unextractable, then the <code>ulValueLen</code> field in that triple is modified to hold the value <code>CK_UNAVAILABLE_INFORMATION</code>.</li>
    <li>Otherwise, if the specified value for the object is invalid (the object does not possess such an attribute), then the <code>ulValueLen</code> field in that triple is modified to hold the value <code>CK_UNAVAILABLE_INFORMATION</code>.</li>
    <li>Otherwise, if the <code>pValue</code> field has the value <code>NULL_PTR</code>, then the <code>ulValueLen</code> field is modified to hold the exact length of the specified attribute for the object.</li>
    <li>Otherwise, if the length specified in <code>ulValueLen</code> is large enough to hold the value of the specified attribute for the object, then that attribute is copied into the buffer that is at <code>pValue</code>, and the <code>ulValueLen</code> field is modified to hold the exact length of the attribute.</li>
    <li>Otherwise, the <code>ulValueLen</code> field is modified to hold the value <code>CK_UNAVAILABLE_INFORMATION</code>.</li>
    </ol>
    </p>
    <p>If case 1 applies to any of the requested attributes, then the call needs to return the value <code>CKR_ATTRIBUTE_SENSITIVE</code>. If case 2 applies to any of the requested attributes, then the call needs to return the value <code>CKR_ATTRIBUTE_TYPE_INVALID</code>. If case 5 applies to any of the requested attributes, then the call needs to return the value <code>CKR_BUFFER_TOO_SMALL</code>. As usual, if more than one of these error codes is applicable, <code>Cryptoki</code> can return any of them. Only if none of them applies to any of the requested attributes, <code>CKR_OK</code> is returned.</p>
    <p>In the special case of an attribute whose value is an array of attributes, for example <code>CKA_WRAP_TEMPLATE</code>, where it is passed in with <code>pValue</code> not NULL, then if the <code>pValue</code> of elements within the array is NULL_PTR then the <code>ulValueLen</code> of elements within the array is set to the required length. If the <code>pValue</code> of elements within the array is not NULL_PTR, then the <code>ulValueLen</code> element of attributes within the array must reflect the space that the corresponding <code>pValue</code> points to, and <code>pValue</code> is filled in if there is sufficient room. Therefore, it is important to initialize the contents of a buffer before <code>C_GetAttributeValue</code> is called to get such an array value. If any <code>ulValueLen</code> within the array isn't large enough, it is set to <code>CK_UNAVAILABLE_INFORMATION</code> and the function returns <code>CKR_BUFFER_TOO_SMALL</code>, as it does if an attribute in the <code>pTemplate</code> argument has <code>ulValueLen</code> too small. Any attribute whose value is an array of attributes is identifiable by the <code>CKF_ARRAY_ATTRIBUTE</code> set of the attribute type.</p>
    <p>The error codes <code>CKR_ATTRIBUTE_SENSITIVE</code>, <code>CKR_ATTRIBUTE_TYPE_INVALID</code>, and <code>CKR_BUFFER_TOO_SMALL</code> do not denote true errors for <code>C_GetAttributeValue</code>. If a call to <code>C_GetAttributeValue</code> returns any of these three values, then the call must nonetheless have processed every attribute in the template that is supplied to <code>C_GetAttributeValue</code>. Each attribute in the template whose value can be returned by the call to <code>C_GetAttributeValue</code> is returned by the call to <code>C_GetAttributeValue</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_GetAttributeValue)(
        CK_SESSION_HANDLE hSession,
        CK_OBJECT_HANDLE hObject,
        CK_ATTRIBUTE_PTR pTemplate,
        CK_ULONG ulCount
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_SENSITIVE, CKR_ATTRIBUTE_TYPE_INVALID, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OBJECT_HANDLE_INVALID, CKR_OK, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Only retrieve supported EP11 attributes
    attributeList := ep11.EP11Attributes{
        ep11.CKA_DECRYPT: false, // attribute where you would like to retrieve its current value
    }

    GetAttributeValueRequest := &pb.GetAttributeValueRequest{
        Object:     GenerateKeyPairResponse.PrivKeyBytes,
        Attributes: util.AttributeMap(attributeList),
    }

    GetAttributeValueResponse, err := cryptoClient.GetAttributeValue(context.Background(), GetAttributeValueRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    const attributeTemplate = new util.AttributeMap(
    new util.Attribute(ep11.CKA_SIGN, 0)
    );

    client.GetAttributeValue({
      Object: keys.PrivKey,
      Attributes: attributeTemplate
    }, (err, response) => {
      callback(err, response);
      console.log('ATTRIBUTE:', response.Attributes);
    });
    ```
    {: codeblock}

### SetAttributeValue
{: #grep11-SetAttributeValue}

The `SetAttributeValue` function modifies an attribute value of an object.

<table id="SetAttributeValue_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="SetAttributeValue" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_SetAttributeValue</code>, which is an implementation of PKCS #11 <code>C_SetAttributeValue</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message SetAttributeValueRequest {
        bytes Object = 1;
        map&lt;uint64,AttributeValue&gt; Attributes = 3;
    }
    message SetAttributeValueResponse {
        bytes Object = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="SetAttributeValue_EP11" tab-title="Enterprise PKCS #11" tab-group="SetAttributeValue" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_SetAttributeValue</code>.</p>
    <p>Attribute packing: see _GetAttrValue</p>
    <p>Currently, Ep11 only sends Boolean attributes, all other attributes are handled by host (and EP11 does not modify arrays, such as WRAP_TEMPLATE).</p>
    <p>Does not represent or need sessions (part of blob), therefore does not use the PKCS #11 <code>hSession</code> parameter.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_SetAttributeValue (
        unsigned char *object, size_t objectlen,
        CK_ATTRIBUTE_PTR attributes, CK_ULONG attributeslen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_SetAttributeValue</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="SetAttributeValue_PKCS11" tab-title="PKCS #11" tab-group="SetAttributeValue" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_SetAttributeValue</code> modifies the value of one or more attributes of an object. <code>hSession</code> is the session's handle; <code>hObject</code> is the object's handle; <code>pTemplate</code> points to a template that specifies which attribute values are to be modified and their new values; <code>ulCount</code> is the number of attributes in the template.</p>
    <p>Certain objects might not be modified. Calling <code>C_SetAttributeValue</code> on such objects results in the <code>CKR_ACTION_PROHIBITED</code> error code. An application can consult the object's <code>CKA_MODIFIABLE</code> attribute to determine whether an object can be modified.</p>
    <p>Only session objects can be modified during a read-only session.</p>
    <p>The template can specify new values for any attributes of the object that can be modified. If the template specifies a value of an attribute that is incompatible with other existing attributes of the object, the call fails with the return code <code>CKR_TEMPLATE_INCONSISTENT</code>.</p>
    <p>Not all attributes can be modified; see Section 4.1.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749" target="_blank">PKCS #11 API specification</a> for more information.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_SetAttributeValue)(
        CK_SESSION_HANDLE hSession,
        CK_OBJECT_HANDLE hObject,
        CK_ATTRIBUTE_PTR pTemplate,
        CK_ULONG ulCount
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ACTION_PROHIBITED, CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OBJECT_HANDLE_INVALID, CKR_OK, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Only set supported R/W EP11 attributes
    attributeList := ep11.EP11AttributeP{
        CKA_DECRYPT: true,
    }

    SetAttributeValueRequest := &pb.SetAttributeValueRequest{
        Object:     GenerateKeyPair.PrivKeyBytes,
        Attributes: util.AttributeMap(attributeList),
    }
    SetAttributeValueResponse, err := cryptoClient.SetAttributeValue(context.Background(), SetAttributeValueRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    const attributeTemplate = new util.AttributeMap(
    new util.Attribute(ep11.CKA_SIGN, true)
    );

    client.SetAttributeValue({
      Object: keys.PrivKey,
      Attributes: attributeTemplate
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


## Generating random data
{: #grep11-operation-generate-random-data}

You can generate high-quality random data, such as initialization values (IVs), PIN, and password, for use in cryptographic operations.

### GenerateRandom
{: #grep11-GenerateRandom}

The `GenerateRandom` function generates random data. When you use this function, make sure not to set the length of the random data to be zero and the pointer that points to the random data location to be NULL.

<table id="GenerateRandom_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="GenerateRandom" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_GenerateRandom</code>, which is an implementation of PKCS #11 <code>C_GenerateRandom</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message GenerateRandomRequest {
        uint64 Len = 1;
    }
    message GenerateRandomResponse {
        bytes Rnd = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="GenerateRandom_EP11" tab-title="Enterprise PKCS #11" tab-group="GenerateRandom" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 <code>C_GenerateRandom</code>.</p>
    <p><code>GenerateRandom</code> is equivalent to the original PKCS #11 function. Internally, hardware-seeded entropy is passed through a FIPS-compliant DRNG (ANSI X9.31/ISO 18031, depending on Clic version).</p>
    <p>The host library could generate random numbers without dispatching to the backend, if suitable functionality would be available on the host. This is not done in the current implementation.</p>
    <p>This function does not support a size query.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_GenerateRandom (
        CK_BYTE_PTR rnd, CK_ULONG rndlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_GenerateRandom</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="GenerateRandom_PKCS11" tab-title="PKCS #11" tab-group="GenerateRandom" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><code>C_GenerateRandom</code> generates random or pseudo-random data. <code>hSession</code> is the sessions handle; <code>pRandomData</code> points to the location that receives the random data; and <code>ulRandomLen</code> is the length in bytes of the random or pseudo-random data to be generated.</td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_GenerateRandom)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pRandomData,
        CK_ULONG ulRandomLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD,
    CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED,
    CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY,
    CKR_OK, CKR_OPERATION_ACTIVE, CKR_RANDOM_NO_RNG, CKR_SESSION_CLOSED,
    CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    GenerateRandomRequest := &pb.GenerateRandomRequest {
      Len: 1024,
    }

    GenerateRandomResponse, err := cryptoClient.GenerateRandom(context.Background(), GenerateRandomRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.GenerateRandom({
      Len: ep11.AES_BLOCK_SIZE
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

## Encrypting and decrypting data
{: #grep11-operation-encrypt-decrypt-data}

By specifying the cryptographic mechanism, you can perform symmetric or asymmetric encryption and decryption functions. You might need to call a series of subfunctions to encrypt or decrypt data. For example, the multi-part data encryption operation is composed of the `EncryptInit`, `EncryptUpdate`, and `EncryptFinal` suboperations.

### EncryptInit
{: #grep11-EncryptInit}

The `EncryptInit` function initializes an encryption operation. You need to call this function first to perform an encryption.

<table id="EncryptInit_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="EncryptInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_EncryptInit</code>, which is an implementation of PKCS #11 <code>C_EncryptInit</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message EncryptInitRequest {
        Mechanism Mech = 2;
        bytes Key = 3;
    }
    message EncryptInitResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="EncryptInit_EP11" tab-title="Enterprise PKCS #11" tab-group="EncryptInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_EncryptInit</code>.</p>
    <p>The <code>(key, klen)</code> blob can be a public-key object, or a secret-key blob. Key type must be consistent with <code>pmech</code>.</p>
    <p>For public-key mechanisms, <code>(key, klen)</code> must contain an SPKI. This SPKI is integrity-protected with a MAC key, as returned by <code>GenerateKeyPair</code> or alternatively <code>UnwrapKey</code>. The Encrypt state is created without session restrictions.</p>
    <p>For secret-key mechanisms, the Encrypt state inherits object session restrictions from <code>(key, klen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
    <p><code>(key, klen)</code> must be a key blob.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_EncryptInit (
        unsigned char *state, size_t *statelen,
        CK_MECHANISM_PTR mech,
        const unsigned char *key, size_t keylen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_EncryptInit</code> return values. For more information, see the <strong>Return values</strong> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="EncryptInit_PKCS11" tab-title="PKCS #11" tab-group="EncryptInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_EncryptInit</code> initializes an encryption operation. <code>hSession</code> is the session’s handle; <code>pMechanism</code> points to the encryption mechanism; <code>hKey</code> is the handle of the encryption key.</p>
    <p>The <code>CKA_ENCRYPT</code> attribute of the encryption key, which indicates whether the key supports encryption, must be <code>CK_TRUE</code>.</p>
    <p>After the application calls <code>C_EncryptInit</code>, the application can either call C_Encrypt to encrypt data in a single part; or call <code>C_EncryptUpdate</code> zero or more times, followed by <code>C_EncryptFinal</code>, to encrypt data in multiple parts.  The encryption operation is active until the application uses a call to <code>C_Encrypt</code> or <code>C_EncryptFinal</code> to obtain the final piece of ciphertext. To process extra data (in single or multiple parts), the application must call <code>C_EncryptInit</code> again.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_EncryptInit)(
        CK_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism,
        CK_OBJECT_HANDLE hKey
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Generate 16 bytes of random data for the initialization vector
    GenerateRandomRequest := &pb.GenerateRandomRequest{
        Len: (uint64)(ep11.AES_BLOCK_SIZE),
    }
    GenerateRandomResponse, err := cryptoClient.GenerateRandom(context.Background(), GenerateRandomRequest)
    if err != nil {
        return nil, fmt.Errorf("GenerateRandom error: %s", err)
    }
    iv := GenerateRandomResponse.Rnd[:ep11.AES_BLOCK_SIZE]
    fmt.Println("Generated IV")

    EncryptInitRequest := &pb.EncryptInitRequest{
        Mech: &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: util.SetMechParm(iv)},
        Key:  GenerateKeyResponse.KeyBytes,
    }

    EncryptInitResponse, err := cryptoClient.EncryptInit(context.Background(), EncryptInitRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.EncryptInit({
    	Mech: {
        Mechanism: ep11.CKM_AES_CBC_PAD,
        ParameterB: iv
      },
      Key: key
    }, (err, data={}) => {
      cb(err, data.State);
    });
    ```
    {: codeblock}

### Encrypt
{: #grep11-Encrypt}

The `Encrypt` function encrypts single-part data. You don't need to perform the `EncryptUpdate` and `EncryptFinal` suboperations for a single-part encryption. Before you call this function, make sure to run `EncryptInit` first.

<table id="Encrypt_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="Encrypt" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_Encrypt</code>, which is an implementation of PKCS #11 <code>C_Encrypt</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message EncryptRequest {
        bytes State = 1;
        bytes Plain = 2;
    }
    message EncryptResponse {
        bytes Ciphered = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="Encrypt_EP11" tab-title="Enterprise PKCS #11" tab-group="Encrypt" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_Encrypt</code>.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
    <p>The <code>state</code> blob was output from: <code>EncryptInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_Encrypt (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR plain, CK_ULONG plainlen,
        CK_BYTE_PTR ciphered, CK_ULONG_PTR cipheredlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Encrypt</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="Encrypt_PKCS11" tab-title="PKCS #11" tab-group="Encrypt" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_Encrypt</code> encrypts single-part data. <code>hSession</code> is the session’s handle; <code>pData</code> points to the data; <code>ulDataLen</code> is the length in bytes of the data; <code>pEncryptedData</code> points to the location that receives the encrypted data; <code>pulEncryptedDataLen</code> points to the location that holds the length in bytes of the encrypted data.</p>
    <p><code>C_Encrypt</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The encryption operation must be initialized with <code>C_EncryptInit</code>. A call to <code>C_Encrypt</code> always terminates the active encryption operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call (that is, one that returns <code>CKR_OK</code>) to determine the length of the buffer that is needed to hold the ciphertext.</p>
    <p><code>C_Encrypt</code> cannot be used to terminate a multi-part operation, and must be called after <code>C_EncryptInit</code> without intervening <code>C_EncryptUpdate</code> calls.</p>
    <p>For some encryption mechanisms, the input plain text data has certain length constraints (either because the mechanism can encrypt only relatively short pieces of plain text, or because the mechanism’s input data must consist of an integral number of blocks). If these constraints are not satisfied, then <code>C_Encrypt</code> fails with return code <code>CKR_DATA_LEN_RANGE</code>.</p>
    <p>The plain text and ciphertext can be in the same place, that is, it is OK if <code>pData</code> and <code>pEncryptedData</code> point to the same location.</p>
    <p>For most mechanisms, <code>C_Encrypt</code> is equivalent to a sequence of <code>C_EncryptUpdate</code> operations followed by <code>C_EncryptFinal</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_Encrypt)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pData,
        CK_ULONG ulDataLen,
        CK_BYTE_PTR pEncryptedData,
        CK_ULONG_PTR pulEncryptedDataLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_INVALID, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    plainText := "Encrypt this message"

    EncryptRequest := &pb.EncryptRequest {
        State: EncryptInitResponse.State,
        Plain: plainText,
    }

    EncryptResponse, err := cryptoClient.Encrypt(context.Background(), EncryptRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.Encrypt({
      State: state,
      Plain: Buffer.from(message)
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


### EncryptUpdate
{: #grep11-EncryptUpdate}

The `EncryptUpdate` function continues a multiple-part encryption operation. Before you call this function, make sure to run `EncryptInit` first.

<table id="EncryptUpdate_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="EncryptUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_EncryptUpdate</code>, which is an implementation of PKCS #11 <code>C_EncryptUpdate</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message EncryptUpdateRequest {
        bytes State = 1;
        bytes Plain = 2;
    }
    message EncryptUpdateResponse {
        bytes State = 1;
        bytes Ciphered = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="EncryptUpdate_EP11" tab-title="Enterprise PKCS #11" tab-group="EncryptUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_EncryptUpdate</code>.</p>
    <p>The <code>state</code>, <code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
    <p>The <code>state</code> blob was output from: <code>EncryptInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_EncryptUpdate (
        unsigned char *state, size_t statelen,
        CK_BYTE_PTR plain, CK_ULONG plainlen,
        CK_BYTE_PTR ciphered, CK_ULONG_PTR cipheredlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_EncryptUpdate</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="EncryptUpdate_PKCS11" tab-title="PKCS #11" tab-group="EncryptUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_EncryptUpdate</code> continues a multiple-part encryption operation, processing another data part. <code>hSession</code> is the session’s handle; <code>pPart</code> points to the data part; <code>ulPartLen</code> is the length of the data part; <code>pEncryptedPart</code> points to the location that receives the encrypted data part; <code>pulEncryptedPartLen</code> points to the location that holds the length in bytes of the encrypted data part.</p>
    <p><code>C_EncryptUpdate</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The encryption operation must be initialized with <code>C_EncryptInit</code>.  This function can be called any number of times in succession. A call to <code>C_EncryptUpdate</code> which results in an error other than <code>CKR_BUFFER_TOO_SMALL</code> terminates the current encryption operation.</p>
    <p>The <code>plaintext</code> and <code>ciphertext</code> can be in the same place, that is, it is OK if <code>pPart</code> and <code>pEncryptedPart</code> point to the same location.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_EncryptUpdate)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pPart,
        CK_ULONG ulPartLen,
        CK_BYTE_PTR pEncryptedPart,
        CK_ULONG_PTR pulEncryptedPartLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    plainText := `
    This is a very long message that needs to be encrypted by performing
    multiple EncrypytUpdate functions`

    // Use EncryptUpdate if you would like to breakup
    // the encrypt operation into multiple suboperations
    EncryptUpdateRequest1 := &pb.EncryptUpdateRequest {
        State: EncryptInitResponse.State,
        Plain: plainText[:20],
    }

    EncryptUpdateResponse, err := cryptoClient.EncryptUpdate(context.Background(), EncryptUpdateRequest1)

    ciphertext := EncryptUpdateResponse.Ciphered[:]

    EncryptUpdateRequest2 := &pb.EncryptUpdateRequest {
        State: EncryptUpdateResponse.State,
        Plain: plainText[20:],
    }

    EncryptUpdateResponse, err := cryptoClient.EncryptUpdate(context.Background(), EncryptUpdateRequest2)

    ciphertext = append(ciphertext, EncryptUpdateResponse.Ciphered...)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.EncryptUpdate({
      State: state,
      Plain: Buffer.from(message.substr(20))
    }, (err, data={}) => {
      cb(err, data.State, Buffer.concat([ciphertext, data.Ciphered]));
    });
    ```
    {: codeblock}

### EncryptFinal
{: #grep11-EncryptFinal}

The `EncryptFinal` function finishes a multiple-part encryption operation.

<table id="EncryptFinal_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="EncryptFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_EncryptFinal</code>, which is an implementation of PKCS #11 <code>C_EncryptFinal</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message EncryptFinalRequest {
        bytes State = 1;
    }
    message EncryptFinalResponse {
        bytes Ciphered = 2;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="EncryptFinal_EP11" tab-title="Enterprise PKCS #11" tab-group="EncryptFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_EncryptFinal</code>.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
    <p>The <code>state</code> blob was output from: <code>EncryptInit</code>, <code>EncryptUpdate</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_EncryptFinal (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR ciphered, CK_ULONG_PTR cipheredlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_EncryptFinal</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="EncryptFinal_PKCS11" tab-title="PKCS #11" tab-group="EncryptFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_EncryptFinal</code> finishes a multiple-part encryption operation. <code>hSession</code> is the session’s handle; <code>pLastEncryptedPart</code> points to the location that receives the last encrypted data part, if any; <code>pulLastEncryptedPartLen</code> points to the location that holds the length of the last encrypted data part.</p>
    <p><code>C_EncryptFinal</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The encryption operation must be initialized with <code>C_EncryptInit</code>. A call to <code>C_EncryptFinal</code> always terminates the active encryption operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call (that is, one that returns <code>CKR_OK</code>) to determine the length of the buffer that is needed to hold the ciphertext.</p>
    <p>For some multi-part encryption mechanisms, the input plain text data has certain length constraints because the mechanism’s input data must consist of an integral number of blocks. If these constraints are not satisfied, then <code>C_EncryptFinal</code> fails with return code <code>CKR_DATA_LEN_RANGE</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_EncryptFinal)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pLastEncryptedPart,
        CK_ULONG_PTR pulLastEncryptedPartLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    EncryptFinalRequest := &pb.EncryptFinalRequest {
        State: EncryptUpdateResponse.State,
    }

    EncryptFinalResponse, err := cryptoClient.EncryptFinal(context.Background(), EncryptFinalRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.EncryptFinal({
      State: state
    }, (err, data={}) => {
      cb(err, Buffer.concat([ciphertext, data.Ciphered]));
    });
    ```
    {: codeblock}

### EncryptSingle
{: #grep11-EncryptSingle}

The `EncryptSingle` function processes data in one pass with one call. It does not return any state to host and returns only the encrypted data. This function is an IBM EP11 extension to the standard PKCS #11 specification and is a combination of the `EncryptInit` and `Encrypt` functions. It enables you to complete an encryption operation with a single call instead of a series of calls.

<table id="EncryptSingle_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="EncryptSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_EncryptSingle</code><td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message EncryptSingleRequest {
        bytes Key = 1;
        Mechanism Mech = 2;
        bytes Plain = 3;
    }
    message EncryptSingleResponse {
        bytes Ciphered = 4;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="EncryptSingle_EP11" tab-title="Enterprise PKCS #11" tab-group="EncryptSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Non-standard variant of <code>Encrypt</code>. Processes data in one pass, with one call. Does not return any state to host, only encrypted data.</p>
    <p>This is the preferred method of encrypting data in one pass for XCP-aware applications. Functionally it is equivalent to <code>EncryptInit</code> followed immediately by <code>Encrypt</code>, but it saves roundtrips, wrapping, and unwrapping.</p>
    <p>If the backend supports resident keys, the key can be also a resident-key handle.</p>
    <p>See also: <code>Encrypt</code>, <code>EncryptInit</code>, <code>DecryptSingle</code>.</p>
    <p>The <code>key</code> blob was output from: <code>GenerateKey</code>, <code>UnwrapKey</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_EncryptSingle (
        const unsigned char *key, size_t keylen,
        CK_MECHANISM_PTR mech,
        CK_BYTE_PTR plain, CK_ULONG plainlen,
        CK_BYTE_PTR ciphered, CK_ULONG_PTR cipheredlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Encrypt</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Generate 16 bytes of random data for the initialization vector
    GenerateRandomRequest := &pb.GenerateRandomRequest{
        Len: (uint64)(ep11.AES_BLOCK_SIZE),
    }
    GenerateRandomResponse, err := cryptoClient.GenerateRandom(context.Background(),  GenerateRandomRequest)
    if err != nil {
        return nil, fmt.Errorf("GenerateRandom error: %s", err)
    }

    iv := GenerateRandomResponse.Rnd[:ep11.AES_BLOCK_SIZE]
    fmt.Println("Generated IV")

    plainText := "Encrypt this message"
    EncryptSingleRequest := &pb.EncryptSingleRequest{
        Mech: &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: util.SetMechParm(iv)},
        Key:  GenerateKeyResponse.KeyBytes,
        Plain: plainText,
    }

    EncryptSingleResponse, err := cryptoClient.EncryptSingle(context.Background(), EncryptSingleRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.EncryptSingle({
      Mech: {
        Mechanism: ep11.CKM_AES_CBC_PAD,
        ParameterB: iv
      },
      Key: aliceDerived.NewKey,
      Plain: Buffer.from(message)
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

### ReencryptSingle
{: #grep11-ReencryptSingle}

With the `ReencryptSingle` function, you can decrypt data with the original key and then encrypt the raw data with a different key in a single call within the cloud HSM. The key types that are used for this operation can be the same or different. This function is an IBM EP11 extension to the standard PKCS #11 specification. This single call is a viable option where a large amount of data needs to be reencrypted with different keys, and bypasses the need to perform a combination of `DecryptSingle` and `EncryptSingle` functions for each data item that needs to be reencrypted. It does not return any state to host and returns only the reencrypted data.

<table id="ReencryptSingle_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="ReencryptSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_ReencryptSingle</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message ReencryptSingleRequest {
        bytes DecKey = 1;
        bytes EncKey = 2;
        Mechanism DecMech = 3;
        Mechanism EncMech = 4;
        bytes Ciphered = 5;
    }
    message ReencryptSingleResponse {
        bytes Reciphered = 6;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="ReencryptSingle_EP11" tab-title="Enterprise PKCS #11" tab-group="ReencryptSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Non-standard variant of <code>Encrypt</code>. Processes data in one pass, with one call. Does not return any state to host, only the reencrypted data.</p>
    <p>Decrypts data with the original key and then encrypts the raw data with a different key within the cloud HSM.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_ReencryptSingle (
        const unsigned char *dkey, size_t dkeylen,
        const unsigned char *ekey, size_t ekeylen,
        CK_MECHANISM_PTR decmech,
        CK_MECHANISM_PTR encmech,
        CK_BYTE_PTR in, CK_ULONG inlen,
        CK_BYTE_PTR ciphered, CK_ULONG_PTR cipheredlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Encrypt</code> and <code>C_Decrypt</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    var msg = []byte("Data to encrypt")
    EncryptKey1Request := &pb.EncryptSingleRequest{
        Key:   GenerateKey1Response.KeyBytes,
        Mech:  &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: util.SetMechParm(iv)},
        Plain: msg,
    }
    EncryptKey1Response, err := cryptoClient.EncryptSingle(context.Background(), EncryptKey1Request)
    if err != nil {
        return nil, fmt.Errorf("Encrypt error: %s", err)
    }

    ReencryptSingleRequest := &pb.ReencryptSingleRequest{
        DecKey:   GenerateKey1Response.KeyBytes, // original key
        EncKey:   GenerateKey2Response.KeyBytes, // new key
        DecMech:  &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: util.SetMechParm(iv)},
        EncMech:  &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: util.SetMechParm(iv)},
        Ciphered: RencryptKey1Response.Ciphered,
    }

    ReencryptSingleResponse, err := cryptoClient.ReencryptSingle(context.Background(), ReencryptSingleRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.ReencryptSingle({
    Decmech: {
      Mechanism: mech1,
      ParameterB: iv
    },
    Encmech: {
      Mechanism: mech2,
      ParameterB: iv
    },
    In: encipherState.Ciphered,
    DKey: keyBlob1,
    Ekey: keyBlob2,
    }, (err, response) => {
    callback(err, response);
    });
    ```
    {: codeblock}

### DecryptInit
{: #grep11-DecryptInit}

The `DecryptInit` function initializes a decryption operation. You need to call this function first to perform a decryption.

<table id="DecryptInit_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DecryptInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DecryptInit</code>, which is an implementation of PKCS #11 <code>C_DecryptInit</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DecryptInitRequest {
        Mechanism Mech = 2;
        bytes Key = 3;
    }
    message DecryptInitResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DecryptInit_EP11" tab-title="Enterprise PKCS #11" tab-group="DecryptInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Implementation of PKCS #11 <code>C_DecryptInit</code>.
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DecryptInit (
        unsigned char *state, size_t *statelen,
        CK_MECHANISM_PTR mech,
        const unsigned char *key, size_t keylen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DecryptInit</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="DecryptInit_PKCS11" tab-title="PKCS #11" tab-group="DecryptInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_DecryptInit</code> initializes a decryption operation. <code>hSession</code> is the session’s handle; <code>pMechanism</code> points to the decryption mechanism; <code>hKey</code> is the handle of the decryption key.</p>
    <p>The <code>CKA_DECRYPT</code> attribute of the decryption key, which indicates whether the key supports decryption, must be <code>CK_TRUE</code>.</p>
    <p>After the application calls <code>C_DecryptInit</code>, the application can either call <code>C_Decrypt</code> to decrypt data in a single part; or call <code>C_DecryptUpdate</code> zero or more times, followed by <code>C_DecryptFinal</code>, to decrypt data in multiple parts. The decryption operation is active until the application uses a call to <code>C_Decrypt</code> or <code>C_DecryptFinal</code> to obtain the final piece of plaintext. To process extra data (in single or multiple parts), the application must call <code>C_DecryptInit</code> again.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_DecryptInit)(
        K_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism,
        CK_OBJECT_HANDLE hKey
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Generate 16 bytes of random data for the initialization vector
    GenerateRandomRequest := &pb.GenerateRandomRequest{
        Len: (uint64)(ep11.AES_BLOCK_SIZE),
    }
    GenerateRandomResponse, err := cryptoClient.GenerateRandom(context.Background(), GenerateRandomRequest)
    if err != nil {
        return nil, fmt.Errorf("GenerateRandom error: %s", err)
    }
    iv := GenerateRandomResponse.Rnd[:ep11.AES_BLOCK_SIZE]
    fmt.Println("Generated IV")

    DecryptInitRequest := &pb.DecryptInitRequest{
        Mech: &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: util.SetMechParm(iv)},
        Key:  GenerateKeyResponse.KeyBytes,
    }

    DecryptInitResponse, err := cryptoClient.DecryptInit(context.Background(), DecryptInitRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DecryptInit({
      Mech: {
        Mechanism: ep11.CKM_AES_CBC_PAD,
        ParameterB: iv
      },
      Key: key
    }, (err, data={}) => {
      cb(err, data.State);
    });
    ```
    {: codeblock}


### Decrypt
{: #grep11-decrypt}

The `Decrypt` function decrypts data in a single part. You don't need to perform the `DecryptUpdate` and `DecryptFinal` suboperations for a single-part decryption. Before you call this function, make sure to run `DecryptInit` first.

<table id="Decrypt_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="Decrypt" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_Decrypt</code>, which is an implementation of PKCS #11 <code>C_Decrypt</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DecryptRequest {
        bytes State = 1;
        bytes Ciphered = 2;
    }
    message DecryptResponse {
       bytes Plain = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="Decrypt_EP11" tab-title="Enterprise PKCS #11" tab-group="Decrypt" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 <code>C_Decrypt</code>. It does not update <code>(state, slen)</code>.</p>
    <p>The state, slen binary large object (BLOB) must be mapped from the PKCS #11 <code>hSession</code> parameter. The state BLOB was output from <code>DecryptInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_Decrypt (const unsigned char *state, size_t slen,
        CK_BYTE_PTR cipher, CK_ULONG clen,
        CK_BYTE_PTR plain, CK_ULONG_PTR plen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Decrypt</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="Decrypt_PKCS11" tab-title="PKCS #11" tab-group="Decrypt" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
      <p><code>C_Decrypt</code> decrypts encrypted data in a single part.
        <ul>
          <li><code>hSession</code> is the session handle.</li>
          <li><code>pEncryptedData</code> points to the encrypted data.</li>
          <li><code>ulEncryptedDataLen</code> is the length of the encrypted data.</li>
          <li><code>pData</code> points to the location that receives the recovered data.</li>
          <li><code>pulDataLen</code> points to the location that holds the length of the recovered data.</li>
        </ul>
      </p>
    <p><code>C_Decrypt</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The decryption operation needs to be initialized with <code>C_DecryptInit</code>. A call to <code>C_Decrypt</code> always terminates the active decryption operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call with <code>CKR_OK</code> returned to determine the length of the buffer that is needed to hold the plain text.</p>
    <p><code>C_Decrypt</code> cannot be used to terminate a multi-part operation, and needs to be called after <code>C_DecryptInit</code> without intervening <code>C_DecryptUpdate</code> calls.</p>
    <p>The ciphertext and plain text can be in the same place, which means it is acceptable if pEncryptedData and pData point to the same location.</p>
    <p>If the input ciphertext data cannot be decrypted because it has an inappropriate length, either <code>CKR_ENCRYPTED_DATA_INVALID</code> or <code>CKR_ENCRYPTED_DATA_LEN_RANGE</code> can be returned.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_Decrypt)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pEncryptedData,
        CK_ULONG ulEncryptedDataLen,
        CK_BYTE_PTR pData,
        CK_ULONG_PTR pulDataLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_ENCRYPTED_DATA_INVALID, CKR_ENCRYPTED_DATA_LEN_RANGE, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    DecryptRequest := &pb.DecryptRequest{
        State:    DecryptInitResponse.State,
        Ciphered: ciphertext, // encrypted data from a previous encrypt operation
    }

    DecryptResponse, err := cryptoClient.Decrypt(context.Background(), DecryptRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.Decrypt({
      State: state,
      Ciphered: ciphertext
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

### DecryptUpdate
{: #grep11-DecryptUpdate}

The `DecryptUpdate` function continues a multiple-part decryption operation. Before you call this function, make sure to run `DecryptInit` first.

<table id="DecryptUpdate_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DecryptUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DecryptUpdate</code>, which is an implementation of PKCS #11 <code>C_DecryptUpdate</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DecryptUpdateRequest {
        bytes State = 1;
        bytes Ciphered = 2;
    }
    message DecryptUpdateResponse {
        bytes State = 1;
        bytes Plain = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DecryptUpdate_EP11" tab-title="Enterprise PKCS #11" tab-group="DecryptUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_DecryptUpdate</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
    <p>The <code>state</code> blob was output from: <code>DecryptInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DecryptUpdate (
        unsigned char *state, size_t statelen,
        CK_BYTE_PTR ciphered, CK_ULONG cipheredlen,
        CK_BYTE_PTR plain, CK_ULONG_PTR plainlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DecryptUpdate</code> return values. For more information, see the <em><strong>Return values</strong></em>chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="DecryptUpdate_PKCS11" tab-title="PKCS #11" tab-group="DecryptUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_DecryptUpdate</code> continues a multiple-part decryption operation, processing another encrypted data part. <code>hSession</code> is the session’s handle; <code>pEncryptedPart</code> points to the encrypted data part; <code>ulEncryptedPartLen</code> is the length of the encrypted data part; <code>pPart</code> points to the location that receives the recovered data part; <code>pulPartLen</code> points to the location that holds the length of the recovered data part.</p>
    <p><code>C_DecryptUpdate</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The decryption operation must be initialized with <code>C_DecryptInit</code>.  This function can be called any number of times in succession.  A call to <code>C_DecryptUpdate</code> which results in an error other than CKR_BUFFER_TOO_SMALL terminates the current decryption operation.</p>
    <p>The ciphertext and plain text can be in the same place, that is, it is OK if <code>pEncryptedPart</code> and <code>pPart</code> point to the same location.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_DecryptUpdate)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pEncryptedPart,
        CK_ULONG ulEncryptedPartLen,
        CK_BYTE_PTR pPart,
        CK_ULONG_PTR pulPartLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

     ```Golang
     // Use DecryptUpdate if you would like to breakup
     // the decrypt operation into multiple suboperations
     DecryptUpdateRequest1 := &pb.DecryptUpdateRequest{
         State:    DecryptInitResponse.State,
         Ciphered: ciphertext[:16], // encrypted data from a previous encrypt operation
     }

     DecryptUpdateResponse, err := cryptoClient.DecryptUpdate(context.Background(), DecryptUpdateRequest1)

     plaintext := DecryptUpdateResponse.Plain[:]

     DecryptUpdateRequest2 := &pb.DecryptUpdateRequest{
         State:    DecryptUpdateResponse.State,
         Ciphered: ciphertext[16:], // encrypted data from a previous encrypt operation
     }

     DecryptUpdateResponse, err := cryptoClient.DecryptUpdate(context.Background(), DecryptUpdateRequest2)

     plaintext = append(plaintext, DecryptUpdateResponse.Plain...)
     ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DecryptUpdate({
    State: state,
    Ciphered: ciphertext.slice(0, 16)
    }, (err, data={}) => {
    cb(err, data.State, data.Plain);
    });
    ```
    {: codeblock}


### DecryptFinal
{: #grep11-DecryptFinal}

The `DecryptFinal` function finishes a multiple-part decryption operation.

<table id="DecryptFinal_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DecryptFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DecryptFinal</code>, which is an implementation of PKCS #11 <code>C_DecryptFinal</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DecryptFinalRequest {
        bytes State = 1;
    }
    message DecryptFinalResponse {
        bytes Plain = 2;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DecryptFinal_EP11" tab-title="Enterprise PKCS #11" tab-group="DecryptFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 <code>C_DecryptFinal</code>.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
    <p>The <code>state</code> blob was output from: <code>DecryptInit</code>, <code>DecryptUpdate</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DecryptFinal (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR plain, CK_ULONG_PTR plainlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DecryptFinal</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="DecryptFinal_PKCS11" tab-title="PKCS #11" tab-group="DecryptFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_DecryptFinal</code> finishes a multiple-part decryption operation. <code>hSession</code> is the session’s handle; <code>pLastPart</code> points to the location that receives the last recovered data part, if any; <code>pulLastPartLen</code> points to the location that holds the length of the last recovered data part.</p>
    <p><code>C_DecryptFinal</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The decryption operation must be initialized with <code>C_DecryptInit</code>.  A call to <code>C_DecryptFinal</code> always terminates the active decryption operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call (that is, one that <code>returns CKR_OK</code>) to determine the length of the buffer that is needed to hold the plain text.</p>
    <p>If the input ciphertext data cannot be decrypted because it has an inappropriate length, then either <code>CKR_ENCRYPTED_DATA_INVALID</code> or <code>CKR_ENCRYPTED_DATA_LEN_RANGE</code> can be returned.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_DecryptFinal)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pLastPart,
        CK_ULONG_PTR pulLastPartLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_ENCRYPTED_DATA_INVALID, CKR_ENCRYPTED_DATA_LEN_RANGE, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    DecryptFinalRequest := &pb.DecryptFinalRequest {
      State: DecrypUpdateResponse.State,
    }

    DecryptFinalResponse, err := cryptoClient.DecryptFinal(context.Background(), DecryptFinalRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DecryptFinal({
      State: state
    }, (err, data={}) => {
      cb(err, Buffer.concat([plaintext, data.Plain]));
    });
    ```
    {: codeblock}


### DecryptSingle
{: #grep11-DecryptSingle}

The `DecryptSingle` function processes data in one pass with one call. It does not return any state to host and returns only the decrypted data. This function is an IBM EP11 extension to the standard PKCS #11 specification and is a combination of the `DecryptInit` and `Decrypt` functions. It enables you to complete a decryption operation with a single call instead of a series of calls.

<table id="DecryptSingle_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DecryptSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DecryptSingle</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DecryptSingleRequest {
        bytes Key = 1;
        Mechanism Mech = 2;
        bytes Ciphered = 3;
    }
    message DecryptSingleResponse {
        bytes Plain = 4;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DecryptSingle_EP11" tab-title="Enterprise PKCS #11" tab-group="DecryptSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Non-standard variant of <code>Decrypt</code>. Processes data in one pass, with one call. Does not return any state to host, only decrypted data.</p>
    <p>This is the preferred method of encrypting data in one pass for XCP-aware applications. Functionally it is equivalent to <code>DecryptInit</code> followed immediately by <code>Decrypt</code>, but it saves roundtrips, wrapping, and unwrapping.</p>
    <p>If the backend supports resident keys, the key can be also a resident-key handle.</p>
    <p>See also: <code>Decrypt</code>, <code>DecryptInit</code>, <code>EncryptSingle</code>.</p>
    <p>The <code>key</code> blob was output from: <code>GenerateKey</code>, <code>UnwrapKey</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DecryptSingle (
        const unsigned char *key, size_t keylen,
        CK_MECHANISM_PTR mech,
        CK_BYTE_PTR ciphered, CK_ULONG cipheredlen,
        CK_BYTE_PTR plain, CK_ULONG_PTR plainlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Decrypt</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Generate 16 bytes of random data for the initialization vector
    GenerateRandomRequest := &pb.GenerateRandomRequest{
        Len: (uint64)(ep11.AES_BLOCK_SIZE),
    }
    GenerateRandomResponse, err := cryptoClient.GenerateRandom(context.Background(),  GenerateRandomRequest)
    if err != nil {
        return nil, fmt.Errorf("GenerateRandom error: %s", err)
    }
    iv := GenerateRandomResponse.Rnd[:ep11.AES_BLOCK_SIZE]
    fmt.Println("Generated IV")

    DecryptSingleRequest := &pb.DecryptSingleRequest {
        Key:      GenerateKeyResponse.KeyBytes,
        Mech:     &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: util.SetMechParm(iv)},
        Ciphered: EncryptSingleResponse.Ciphered, // encrypted data from a previous encrypt operation
    }

    DecryptSingleResponse, err := cryptoClient.DecryptSingle(context.Background(), DecryptSingleRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DecryptSingle({
      Mech: {
        Mechanism: ep11.CKM_AES_CBC_PAD,
        ParameterB: iv
      },
      Key: bobDerived.NewKey,
      Ciphered: ciphertext
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


## Signing and verifying data
{: #grep11-operation-sign-verify-data}

GREP11 provides a set of functions to sign data and verify signatures or message authentication codes (MACs). You might need to call a series of subfunctions to perform a signing operation. For example, the multi-part data signature operation consists of the `SignInit`, `SignUpdate`, and `SignFinal` suboperations.

### SignInit
{: #grep11-SignInit}

The `SignInit` function initializes a signature operation. You need to call this function first to perform a signature operation.

<table id="SignInit_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="SignInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_SignInit</code> , which is an implementation of PKCS #11 <code>C_SignInit</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message SignInitRequest {
        Mechanism Mech = 2;
        bytes PrivKey = 3;
    }
    message SignInitResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="SignInit_EP11" tab-title="Enterprise PKCS #11" tab-group="SignInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Implementation of PKCS #11 <code>C_SignInit</code>.
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_SignInit (
        unsigned char *state, size_t *statelen,
        CK_MECHANISM_PTR mech,
        const unsigned char *privKey, size_t privKeylen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code> C_Decrypt</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="SignInit_PKCS11" tab-title="PKCS #11" tab-group="SignInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_SignInit</code> initializes a signature operation, where the signature is an appendix to the data. <code>hSession</code> is the session's handle; <code>pMechanism</code> points to the signature mechanism; <code>hKey</code> is the handle of the signature key.</p>
    <p>The <code>CKA_SIGN</code> attribute of the signature key, which indicates whether the key supports signatures with appendix, must be <code>CK_TRUE</code>.</p>
    <p>After the application calls <code>C_SignInit</code>, the application can either call <code>C_Sign</code> to sign in a single part; or call <code>C_SignUpdate</code> one or more times, followed by <code>C_SignFinal</code>, to sign data in multiple parts. The signature operation is active until the application uses a call to <code>C_Sign</code> or <code>C_SignFinal</code> to obtain the signature. To process extra data (in single or multiple parts), the application must call <code>C_SignInit</code> again.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_SignInit)(
        CK_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism,
        CK_OBJECT_HANDLE hKey
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    SignInitRequest := &pb.SignInitRequest {
        Mech:    &pb.Mechanism{Mechanism: ep11.CKM_SHA1_RSA_PKCS},
        PrivKey: GenerateKeyPairResponse.PrivKeyBytes,
    }

    SignInitResponse, err := cryptoClient.SignInit(context.Background(), SignInitRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.SignInit({
      Mech: {
        Mechanism: ep11.CKM_SHA1_RSA_PKCS
      },
      PrivKey: keys.PrivKeyBytes
    }, (err, data={}) => {
      cb(err, data.State);
    });
    ```
    {: codeblock}


### Sign
{: #grep11-Sign}

The `Sign` function signs single-part data. You don't need to perform the `SignUpdate` and `SignFinal` suboperations for a single-part signature. Before you call this function, make sure to run `SignInit` first.

<table id="Sign_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="Sign" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_Sign</code>, which is an implementation of PKCS #11 <code>C_Sign</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message SignRequest {
        bytes State = 1;
        bytes Data = 2;
    }
    message SignResponse {
        bytes Signature = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="Sign_EP11" tab-title="Enterprise PKCS #11" tab-group="Sign" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_Sign</code>.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must map session to stored state.)</p>
    <p>The <code>state</code> blob was output from: <code>SignInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_Sign (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR data, CK_ULONG datalen,
        CK_BYTE_PTR signature, CK_ULONG_PTR signaturelen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Sign</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="Sign_PKCS11" tab-title="PKCS #11" tab-group="Sign" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_Sign</code> signs data in a single part, where the signature is an appendix to the data. <code>hSession</code> is the session's handle; <code>pData</code> points to the data; <code>ulDataLen</code> is the length of the data; <code>pSignature</code> points to the location that receives the signature; <code>pulSignatureLen</code> points to the location that holds the length of the signature.</p>
    <p><code>C_Sign</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The signing operation must be initialized with <code>C_SignInit</code>. A call to <code>C_Sign</code> always terminates the active signing operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call (that is, one that returns <code>CKR_OK</code>) to determine the length of the buffer that is needed to hold the signature.</p>
    <p><code>C_Sign</code> cannot be used to terminate a multi-part operation, and must be called after <code>C_SignInit</code> without intervening <code>C_SignUpdate</code> calls.</p>
    <p>For most mechanisms, <code>C_Sign</code> is equivalent to a sequence of <code>C_SignUpdate</code> operations followed by <code>C_SignFinal</code>.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_Sign)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pData,
        CK_ULONG ulDataLen,
        CK_BYTE_PTR pSignature,
        CK_ULONG_PTR pulSignatureLen
    );
    </pre></td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_INVALID, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN, CKR_FUNCTION_REJECTED.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    msgHash := sha256.Sum256([]byte("This data needs to be signed"))
    SignRequest := &pb.SignRequest{
        State: SignInitResponse.State,
        Data:  msgHash[:],
    }

    // Sign the data
    SignResponse, err := cryptoClient.Sign(context.Background(), SignRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.Sign({
      State: state,
      Data: dataToSign
    }, (err, data={}) => {
      cb(err, data.Signature);
    });
    ```
    {: codeblock}


### SignUpdate
{: #grep11-SignUpdate}

The `SignUpdate` function continues a multiple-part signature operation. Before you call this function, make sure to run `SignInit` first.

<table id="SignUpdate_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="SignUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_SignUpdate</code>, which is an implementation of PKCS #11 <code>C_SignUpdate</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message SignUpdateRequest {
        bytes State = 1;
        bytes Data = 2;
    }
    message SignUpdateResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="SignUpdate_EP11" tab-title="Enterprise PKCS #11" tab-group="SignUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p></p>Implementation of PKCS #11 <code>C_SignUpdate</code>.
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must map session to stored state.)</p>
    <p>The <code>state</code> blob was output from: <code>SignInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_SignUpdate (
        unsigned char *state, size_t statelen,
        CK_BYTE_PTR data, CK_ULONG datalen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_SignUpdate</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="SignUpdate_PKCS11" tab-title="PKCS #11" tab-group="SignUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_SignUpdate</code> continues a multiple-part signature operation, processing another data part. <code>hSession</code> is the session's handle, <code>pPart</code> points to the data part; <code>ulPartLen</code> is the length of the data part.</p>
    <p>The signature operation must be initialized with <code>C_SignInit</code>. This function can be called any number of times in succession. A call to <code>C_SignUpdate</code> which results in an error terminates the current signature operation.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_SignUpdate)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pPart,
        CK_ULONG ulPartLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Use SignUpdate if you would like to breakup
    // the sign operation into multiple suboperations
    SignUpdateRequest1 := &pb.SignUpdateRequest {
        State: SignInitResponse.State,
        Data:  msgHash[:16],
    }

    SignUpdateResponse, err := cryptoClient.SignUpdate(context.Background(), SignUpdateRequest1)

    SignUpdateRequest2 := &pb.SignUpdateRequest {
        State: SignUpdateResponse.State,
        Data:  msgHash[16:],
    }

    SignUpdateResponse, err := cryptoClient.SignUpdate(context.Background(), SignUpdateRequest2)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.SignUpdate({
      State: state,
      Data: digest
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


### SignFinal
{: #grep11-SignFinal}

The `SignFinal` function finishes a multiple-part signature operation.

<table id="SignFinal_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="SignFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_SignFinal</code>, which is an implementation of PKCS #11 <code>C_SignFinal</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message SignFinalRequest {
        bytes State = 1;
    }
    message SignFinalResponse {
        bytes Signature = 2;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="SignFinal_EP11" tab-title="Enterprise PKCS #11" tab-group="SignFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_SignFinal</code>.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must map session to stored state.)</p>
    <p>The <code>state</code> blob was output from: <code>SignInit</code>, <code>SignUpdate</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_SignFinal (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR signature, CK_ULONG_PTR signaturelen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_SignFinal</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="SignFinal_PKCS11" tab-title="PKCS #11" tab-group="SignFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_SignFinal</code> finishes a multiple-part signature operation, returning the signature. <code>hSession</code> is the session's handle; <code>pSignature</code> points to the location that receives the signature; <code>pulSignatureLen</code> points to the location that holds the length of the signature.</p>
    <p><code>C_SignFinal</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The signing operation must be initialized with <code>C_SignInit</code>. A call to <code>C_SignFinal</code> always terminates the active signing operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call (that is, one that returns <code>CKR_OK</code>) to determine the length of the buffer that is needed to hold the signature.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_SignFinal)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pSignature,
        CK_ULONG_PTR pulSignatureLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN, CKR_FUNCTION_REJECTED.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    SignFinalRequest := &pb.SignFinalRequest {
        State: SignUpdateResponse.State,
    }

    SignFinalResponse, err := cryptoClient.SignFinal(context.Background(), SignFinalRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.SignFinal({
      State: state
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


### SignSingle
{: #grep11-SignSingle}

The `SignSingle` function signs or MACs data in one pass with one call and without constructing intermediate digest state. It doesn't return any state to host and returns only result. This function is an IBM EP11 extension to the standard PKCS #11 specification and is a combination of the `SignInit` and `Sign` functions. It enables you to complete a signing operation with a single call instead of a series of calls.

<table id="SignSingle_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="SignSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_SignSingle</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message SignSingleRequest {
        bytes PrivKey = 1;
        Mechanism Mech = 2;
        bytes Data = 3;
    }
    message SignSingleResponse {
        bytes Signature = 4;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="SignSingle_EP11" tab-title="Enterprise PKCS #11" tab-group="SignSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Nonstandard extension, combination of <code>SignInit</code> and <code>Sign</code>. Signs or MACs data in one pass, with one call, without constructing intermediate digest state. Does not return any state to host, only result.</p>
    <p>This is the preferred way of signing, without an extra roundtrip, encryption, and decryption. Functionally, <code>SignSingle</code> is equivalent to <code>SignInit</code> followed immediately by <code>Sign</code>.</p>
    <p>The <code>(key, klen)</code> blob and the <code>pmech</code> mechanism together must be passable to <code>SignInit</code>.</p>
    <p>Multi-data requests for HMAC and CMAC signatures are supported (subvariants 2 and 3).</p>
    <p>See also: <code>SignInit</code>, <code>Sign</code>, <code>VerifySingle</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_SignSingle (
        const unsigned char *privKey, size_t privKeylen,
        CK_MECHANISM_PTR mech,
        CK_BYTE_PTR data, CK_ULONG datalen,
        CK_BYTE_PTR signature, CK_ULONG_PTR signaturelen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Decrypt</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    msgHash := sha256.Sum256([]byte("This data needs to be signed"))
    SignSingleRequest := &pb.SignSingleRequest {
        PrivKey: GenerateKeyPairResponse.PrivKeyBytes,
        Mech:    &pb.Mechanism{Mechanism: ep11.CKM_SHA256_RSA_PKCS},
        Data:    msgHash[:],
    }

    SignSingleResponse, err := cryptoClient.SignSingle(context.Background(), SignSingleRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.SignSingle({
      Mech: {
        Mechanism: ep11.CKM_ECDSA
      },
      PrivKey: key,
      Data: digest
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


### VerifyInit
{: #grep11-VerifyInit}

The `VerifyInit` function initializes a verification operation. You need to call this function first to verify a signature.

<table id="VerifyInit_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="VerifyInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_VerifyInit</code>, which is an implementation of PKCS #11 <code>C_VerifyInit</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message VerifyInitRequest {
        Mechanism Mech = 2;
        bytes PubKey = 3;
    }
    message VerifyInitResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="VerifyInit_EP11" tab-title="Enterprise PKCS #11" tab-group="VerifyInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_VerifyInit</code>. Given a key blob <code>(key, klen)</code>, initialize a verify session state in <code>(state, slen)</code>. The key blob can be a public key object, or HMAC key bytes. Key blob type must be consistent with <code>pmech</code>.</p>
    <p>For public-key mechanisms, <code>(key, klen)</code> must contain an SPKI. This SPKI CKA_UNWRAP can be MACed (such as returned earlier by <code>GenerateKeyPair</code>) or just the SPKI itself (if obtained from an external source, such as a certificate).</p>
    <p>If an HMAC operation is initialized, session restrictions of the <code>Verify</code> object are inherited from the HMAC key. Since SPKIs are not tied to sessions, public-key Verify states are session-free.</p>
    <p>The <code>key</code>,<code>klen</code> blob must be mapped from the PKCS #11 <code>hKey</code> parameter.</p>
    <p><strong>Note</strong>: <code>SignInit</code> and <code>VerifyInit</code> are internally the
    same for HMAC and other symmetric/MAC mechanisms.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_VerifyInit (
        unsigned char *state, size_t *statelen,
        CK_MECHANISM_PTR mech,
        const unsigned char *pubKey, size_t pubKeylen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_VerifyInit</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="VerifyInit_PKCS11" tab-title="PKCS #11" tab-group="VerifyInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_VerifyInit</code> initializes a verification operation, where the signature is an appendix to the data. <code>hSession</code> is the session's handle; <code>pMechanism</code> points to the structure that specifies the verification mechanism; <code>hKey</code> is the handle of the verification key.</p>
    <p>The <code>CKA_VERIFY</code> attribute of the verification key, which indicates whether the key supports verification where the signature is an appendix to the data, must be <code>CK_TRUE</code>.</p>
    <p>After the application calls <code>C_VerifyInit</code>, the application can either call <code>C_Verify</code> to verify a signature on data in a single part; or call <code>C_VerifyUpdate</code> one or more times, followed by <code>C_VerifyFinal</code>, to verify a signature on data in multiple parts. The verification operation is active until the application calls <code>C_Verify</code> or <code>C_VerifyFinal</code>. To process extra data (in single or multiple parts), the application must call <code>C_VerifyInit</code> again.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_VerifyInit)(
        CK_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism,
        CK_OBJECT_HANDLE hKey
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    VerifyInitRequest := &pb.VerifyInitRequest {
      Mech:   &pb.Mechanism{Mechanism: ep11.CKM_SHA1_RSA_PKCS},
      PubKey: GenerateKeyPairResponse.PubKeyBytes,
    }

    VerifyInitResponse, err := cryptoClient.VerifyInit(context.Background(), VerifyInitRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.VerifyInit({
      Mech: {
        Mechanism: ep11.CKM_SHA1_RSA_PKCS
      },
      PubKey: keys.PubKeyBytes
    }, (err, data={}) => {
      cb(err, signature, data.State);
    });
    ```
    {: codeblock}


### Verify
{: #grep11-Verify}

The `Verify` function verifies a signature on single-part data. You don't need to perform the `VerifyUpdate` and `VerifyFinal` suboperations for a single-part verification. Before you call this function, make sure to run `VerifyInit` first.

<table id="Verify_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="Verify" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_Verify</code>, which is an implementation of PKCS #11 <code>C_Verify</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message VerifyRequest {
        bytes State = 1;
        bytes Data = 2;
        bytes Signature = 3;
    }
    message VerifyResponse {
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="Verify_EP11" tab-title="Enterprise PKCS #11" tab-group="Verify" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_Verify</code>.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The relative order of data and signature are reversed relative
    to <code>VerifySingle</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must map session to stored state.)</p>
    <p>The <code>state</code> blob was output from: <code>VerifyInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_Verify (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR data, CK_ULONG datalen,
        CK_BYTE_PTR signature, CK_ULONG signaturelen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Verify</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="Verify_PKCS11" tab-title="PKCS #11" tab-group="Verify" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_Verify</code> verifies a signature in a single-part operation, where the signature is an appendix to the data. <code>hSession</code> is the session's handle; <code>pData</code> points to the data; <code>ulDataLen</code> is the length of the data; <code>pSignature</code> points to the signature; <code>ulSignatureLen</code> is the length of the signature.</p>
    <p>The verification operation must be initialized with <code>C_VerifyInit</code>. A call to <code>C_Verify</code> always terminates the active verification operation.</p>
    <p>A successful call to <code>C_Verify</code> needs to return either the value <code>CKR_OK</code> (indicating that the supplied signature is valid) or <code>CKR_SIGNATURE_INVALID</code> (indicating that the supplied signature is invalid). If the signature is invalid purely based on its length, then <code>CKR_SIGNATURE_LEN_RANGE</code> needs to be returned. In any of these cases, the active signing operation is terminated.</p>
    <p><code>C_Verify</code> cannot be used to terminate a multi-part operation, and must be called after <code>C_VerifyInit</code> without intervening <code>C_VerifyUpdate</code> calls.</p>
    <p>For most mechanisms, <code>C_Verify</code> is equivalent to a sequence of <code>C_VerifyUpdate</code> operations followed by <code>C_VerifyFinal</code>.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_Verify)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pData,
        CK_ULONG ulDataLen,
        CK_BYTE_PTR pSignature,
        CK_ULONG ulSignatureLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_INVALID, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SIGNATURE_INVALID, CKR_SIGNATURE_LEN_RANGE.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    VerifyRequest := &pb.VerifyRequest {
        State:     VerifyInitResponse.State,
        Data:      msgHash[:],
        Signature: SignResponse.Signature,
    }

    VerifyResponse, err := cryptoClient.Verify(context.Background(), VerifyRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.Verify({
      State: state,
      Data: dataToSign,
      Signature: signature
    }, (err, data={}) => {
      cb(err, signature);
    });
    ```
    {: codeblock}


### VerifyUpdate
{: #grep11-VerifyUpdate}

The `VerifyUpdate` function continues a multiple-part verification operation. Before you call this function, make sure to run `VerifyInit` first.

<table id="VerifyUpdate_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="VerifyUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_VerifyUpdate</code>, which is an implementation of PKCS #11 <code>C_VerifyUpdate</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message VerifyUpdateRequest {
        bytes State = 1;
        bytes Data = 2;
    }
    message VerifyUpdateResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="VerifyUpdate_EP11" tab-title="Enterprise PKCS #11" tab-group="VerifyUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_VerifyUpdate</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must map session to stored state.)</p>
    <p>The <code>state</code> blob was output from: <code>VerifyInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_VerifyUpdate (
        unsigned char *state, size_t statelen,
        CK_BYTE_PTR data, CK_ULONG datalen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_VerifyUpdate</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="VerifyUpdate_PKCS11" tab-title="PKCS #11" tab-group="VerifyUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_VerifyUpdate</code> continues a multiple-part verification operation, processing another data part. <code>hSession</code> is the session's handle, <code>pPart</code> points to the data part; <code>ulPartLen</code> is the length of the data part.</p>
    <p>The verification operation must be initialized with <code>C_VerifyInit</code>. This function can be called any number of times in succession. A call to <code>C_VerifyUpdate</code> that results in an error terminates the current verification operation.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_VerifyUpdate)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pPart,
        CK_ULONG ulPartLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Use VerifyUpdate if you would like to breakup
    // the verify operation into multiple suboperations
    VerifyUpdateRequest1 := &pb.VerifyUpdateRequest {
      State: VerifyInitResponse.State,
      Data:  msgHash[:16],
    }

    VerifyUpdateResponse, err := cryptoClient.VerifyUpdate(context.Background(), VerifyUpdateRequest1)

    VerifyUpdateRequest2 := &pb.VerifyUpdateRequest {
      State: VerifyUpdateResponse.State,
      Data:  msgHash[16:],
    }

    VerifyUpdateResponse, err := cryptoClient.VerifyUpdate(context.Background(), VerifyUpdateRequest2)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.VerifyUpdate({
      State: state,
      Data: digest
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


### VerifyFinal
{: #grep11-VerifyFinal}

The `VerifyFinal` function finishes a multiple-part verification operation.

<table id="VerifyFinal_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="VerifyFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_VerifyFinal</code>, which is an implementation of PKCS #11 <code>C_VerifyFinal</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message VerifyFinalRequest {
        bytes State = 1;
        bytes Signature = 2;
    }
    message VerifyFinalResponse {
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="VerifyFinal_EP11" tab-title="Enterprise PKCS #11" tab-group="VerifyFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_VerifyFinal</code>.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must map session to stored state.)</p>
    <p>The <code>state</code> blob was output from: <code>VerifyInit</code>, <code>VerifyUpdate</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_VerifyFinal (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR signature, CK_ULONG signaturelen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_VerifyFinal</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="VerifyFinal_PKCS11" tab-title="PKCS #11" tab-group="VerifyFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_VerifyFinal</code> finishes a multiple-part verification operation, checking the signature. <code>hSession</code> is the session's handle; <code>pSignature</code> points to the signature; <code>ulSignatureLen</code> is the length of the signature.</p>
    <p>The verification operation must be initialized with <code>C_VerifyInit</code>. A call to <code>C_VerifyFinal</code> always terminates the active verification operation.</p>
    <p>A successful call to <code>C_VerifyFinal</code> needs to return either the value <code>CKR_OK</code> (indicating that the supplied signature is valid) or <code>CKR_SIGNATURE_INVALID</code> (indicating that the supplied signature is invalid). If the signature is invalid based on its length, then <code>CKR_SIGNATURE_LEN_RANGE</code> needs to be returned. In any of these cases, the active verifying operation is terminated.</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_VerifyFinal)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pSignature,
        CK_ULONG ulSignatureLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SIGNATURE_INVALID, CKR_SIGNATURE_LEN_RANGE.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    VerifyFinalRequest := &pb.VerifyFinalRequest {
        State:     VerifyUpdateResponse.State,
        Signature: SignResponse.Signature,
    }

    VerifyFinalResponse, err := cryptoClient.VerifyFinal(context.Background(), VerifyFinalRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.VerifyFinal({
      State: state,
      Signature: signature
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


### VerifySingle
{: #grep11-VerifySingle}

The `VerifySingle` function signs or MACs data in one pass with one call and without constructing intermediate digest state. It does not return any state to host and returns only the verification result. This function is an IBM EP11 extension to the standard PKCS #11 specification and is a combination of the `VerifyInit` and `Verify` functions. It enables you to complete a verification operation with a single call instead of a series of calls.

<table id="VerifySingle_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="VerifySingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_VerifySingle</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message VerifySingleRequest {
        bytes PubKey = 1;
        Mechanism Mech = 2;
        bytes Data = 3;
        bytes Signature = 4;
    }
    message VerifySingleResponse {
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="VerifySingle_EP11" tab-title="Enterprise PKCS #11" tab-group="VerifySingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Nonstandard extension, combination of <code>VerifyInit</code> and <code>Verify</code>. Signs or MACs data in one pass, with one call, without constructing intermediate digest state. Does not return any state to host, only verification result. No size query is available because this function returns a Boolean.</p>
    <p>This is the preferred way of verifying a signature, without an extra roundtrip, encryption, decryption. Functionally, <code>VerifySingle</code> is equivalent to <code>VerifyInit</code> followed immediately by a <code>Verify</code>.</p>
    <p>The <code>(key, klen)</code> blob and the <code>pmech</code> mechanism together must be passable to <code>VerifyInit</code>.</p>
    <p>For public-key mechanisms, <code>(key, klen)</code> must contain an SPKI. This SPKI can be MACed (such as returned as a public key from <code>GenerateKeyPair</code>) or just the SPKI itself (if obtained from an external source, such as a certificate).</p>
    <p>See also: <code>VerifyInit</code>, <code>Verify</code>, <code>SignSingle</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_VerifySingle (
        const unsigned char *pubKey, size_t pubKeylen,
        CK_MECHANISM_PTR mech,
        CK_BYTE_PTR data, CK_ULONG datalen,
        CK_BYTE_PTR signature, CK_ULONG signaturelen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_VerifySingle</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    VerifySingleRequest := &pb.VerifySingleRequest {
        PubKey:    GenerateKeyPairResponse.PubKeyByytes,
        Mech:      &pb.Mechanism{Mechanism: ep11.CKM_SHA256_RSA_PKCS},
        Data:      msgHash[:],
        Signature: SignSingleResponse.Signature,
    }

    VerifySingleResponse, err := cryptoClient.VerifySingle(context.Background(), VerifySingleRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.VerifySingle({
      Mech: {
        Mechanism: ep11.CKM_SHA256_RSA_PKCS
      },
      PubKey: keys.PubKey,
      Data: digest,
      Signature: signature
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

## Protecting data integrity through message digests
{: #grep11-operation-digest-data}

GREP11 provides a set of functions to create message digests that are designed to protect the integrity of a piece of data. You might need to call a series of subfunctions to perform a digesting operation. For example, the multi-part digesting operation consists of the `DigestInit`, `DigestUpdate`, and `DigestFinal` suboperations.

### DigestInit
{: #grep11-DigestInit}

The `DigestInit` function initializes a message-digesting operation. You need to run this function first to perform a digesting operation.

<table id="DigestInit_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DigestInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DigestInit</code>, which is an implementation of PKCS #11 <code>C_DigestInit</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DigestInitRequest {
        Mechanism Mech = 2;
    }
    message DigestInitResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DigestInit_EP11" tab-title="Enterprise PKCS #11" tab-group="DigestInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 <code>C_DigestInit</code>.</p>
    <p>Create wrapped digest state.</p>
    <p><strong>Note</strong>: size queries are supported, but the wrapped state is always returned by the backend, unlike most size queries (which return an output size, instead of actual output). <code>Digest</code> states are sufficiently small that they do not introduce noticeable transport overhead.</p>
    <p>During size queries, the host just discards the returned state, and reports blob size (in <code>len</code>). When blob is being returned, <code>len</code> is checked against returned size.</p>
    <p>The <code>state</code>,<code>len</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must tie blob to session.)</p></td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DigestInit (
        unsigned char *state, size_t *len,
        const CK_MECHANISM_PTR mech,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DigestInit</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="DigestInit_PKCS11" tab-title="PKCS #11" tab-group="DigestInit" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_DigestInit</code> initializes a message-digesting operation. <code>hSession</code> is the session’s handle; <code>pMechanism</code> points to the digesting mechanism.</p>
    <p>After the application calls <code>C_DigestInit</code>, the application can either call <code>C_Digest</code> to digest data in a single part; or call <code>C_DigestUpdate</code> zero or more times, followed by <code>C_DigestFinal</code>, to digest data in multiple parts.  The message-digesting operation is active until the application uses a call to <code>C_Digest</code> or <code>C_DigestFinal</code> to obtain the message digest. To process extra data (in single or multiple parts), the application must call <code>1C_DigestInit1</code> again.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_DigestInit)(
        CK_SESSION_HANDLE hSession,
        CK_MECHANISM_PTR pMechanism
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    DigestInitRequest := &pb.DigestInitRequest {
        Mech: &pb.Mechanism{Mechanism: ep11.CKM_SHA256},
    }

    DigestInitResponse, err := cryptoClient.DigestInit(context.Background(), DigestInitRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DigestInit({
      Mech: {
        Mechanism: ep11.CKM_SHA256
      }
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}


### Digest
{: #grep11-Digest}

The `Digest` function digests single-part data. You don't need to call the `DigestUpdate` and `DigestFinal` functions for digesting single-part data. Before you call this function, make sure to run `DigestInit` first. When you set parameters, note not to specify the length of the input data to be zero and the pointer that points to the input data location to be NULL.

<table id="Digest_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="Digest" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_Digest</code>, which is an implementation of PKCS #11 <code>C_Digest</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DigestRequest {
        bytes State = 1;
        bytes Data = 2;
    }
    message DigestResponse {
        bytes Digest = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="Digest_EP11" tab-title="Enterprise PKCS #11" tab-group="Digest" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_Digest</code>.</p>
    <p>If a digest object has exactly 0 (zero) bytes that are appended to it after creation, in any combination of zero-byte transfers, it can still perform a one-pass Digest, even if it needs to be rejected by a strict implementation.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>Implementations might perform
    <code>DigestUpdate</code>, <code>DigestFinal</code>, or <code>Digest</code> calls on cleartext digest objects in host code, bypassing HSM backends altogether. This choice might or might not be visible to host code, and it does not impact the security of the operation (as clear objects might not digest sensitive data). </p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. The <code>state</code> blob was output from: <code>DigestInit</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_Digest (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR data, CK_ULONG datalen,
        CK_BYTE_PTR digest, CK_ULONG_PTR digestlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_Digest</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="Digest_PKCS11" tab-title="PKCS #11" tab-group="Digest" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_Digest</code> digests data in a single part. <code>hSession</code> is the session’s handle, pData points to the data; <code>ulDataLen</code> is the length of the data; <code>pDigest</code> points to the location that receives the message digest; <code>pulDigestLen</code> points to the location that holds the length of the message digest.</p>
    <p><code>C_Digest</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The digest operation must be initialized with <code>C_DigestInit</code>.  A call to <code>C_Digest</code> always terminates the active digest operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call (that is, one that returns <code>CKR_OK</code>) to determine the length of the buffer that is needed to hold the message digest.</p>
    <p><code>C_Digest</code> cannot be used to terminate a multi-part operation, and must be called after <code>C_DigestInit</code> without intervening <code>C_DigestUpdate</code> calls.</p>
    <p>The input data and digest output can be in the same place, that is, it is OK if pData and pDigest point to the same location.</p>
    <p><code>C_Digest</code> is equivalent to a sequence of <code>C_DigestUpdate</code> operations followed by <code>C_DigestFinal</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_Digest)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pData,
        CK_ULONG ulDataLen,
        CK_BYTE_PTR pDigest,
        CK_ULONG_PTR pulDigestLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    digestData := []byte("Create a digest for this string")
    DigestRequest := &pb.DigestRequest {
        State: DigestInitResponse.State,
        Data:  digestData,
    }

    DigestResponse, err := cryptoClient.Digest(context.Background(), DigestRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.Digest({
        State: state,
        Data: Buffer.from(digestData)
      }, (err, data={}) => {
        cb(err, data.Digest);
      });
    }
    ```
    {: codeblock}


### DigestUpdate
{: #grep11-DigestUpdate}

The `DigestUpdate` function continues a multiple-part digesting operation. Before you call this function, make sure to run `DigestInit` first. When you set parameters, note not to specify the length of the input data to be zero and the pointer that points to the input data location to be NULL.

<table id="DigestUpdate_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DigestUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DigestUpdate</code>, which is an implementation of PKCS #11 <code>C_DigestUpdate</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DigestUpdateRequest {
        bytes State = 1;
        bytes Data = 2;
    }
    message DigestUpdateResponse {
        bytes State = 1;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DigestUpdate_EP11" tab-title="Enterprise PKCS #11" tab-group="DigestUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Implementation of PKCS #11 <code>C_DigestUpdate</code>.</p>
    <p><code>DigestUpdate</code> is polymorphic,
    accepting both wrapped or clear digest objects, updating state in the same format.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must map session to stored state.)</p>
    <p>The <code>state</code> blob was output from: <code>DigestInit</code>, <code>DigestUpdate</code>, <code>DigestKey</code>.</p>
    <p>See also: <code>DigestInit</code></p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DigestUpdate (
        unsigned char *state, size_t statelen,
        CK_BYTE_PTR data, CK_ULONG datalen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DigestUpdate</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="DigestUpdate_PKCS11" tab-title="PKCS #11" tab-group="DigestUpdate" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p><code>C_DigestUpdate</code> continues a multiple-part message-digesting operation, processing another data part. <code>hSession</code> is the session’s handle, <code>pPart</code> points to the data part; <code>ulPartLen</code> is the length of the data part.</p>
    <p>The message-digesting operation must be initialized with <code>C_DigestInit</code>. Calls to this function and <code>C_DigestKey</code> can be interspersed any number of times in any order. A call to <code>C_DigestUpdate</code> which results in an error terminates the current digest operation.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_DigestUpdate)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pPart,
        CK_ULONG ulPartLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    // Use DigestUpdate if you would like to breakup
    // the digest operation into multiple suboperations
    DigestUpdateRequest1 := &pb.DigestUpdateRequest {
        State: DigestInitResponse.State,
        Data:  digestData[:16],
    }

    DigestUpdateResponse, err := cryptoClient.DigestUpdate(context.Background(), DigestUpdateRequest1)

    DigestUpdateRequest2 := &pb.DigestUpdateRequest {
        State: DigestUpdateResponse.State,
        Data:  digestData[16:],
    }

    DigestUpdateResponse, err := cryptoClient.DigestUpdate(context.Background(), DigestUpdateRequest2)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DigestUpdate({
      State: state,
      Data: Buffer.from(digestData.substr(0, 64))
    }, (err, data={}) => {
      cb(err, data.State);
    });
    ```
    {: codeblock}


### DigestFinal
{: #grep11-DigestFinal}

The `DigestFinal` function finishes a multiple-part digesting operation.

<table id="DigestFinal_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DigestFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DigestFinal</code>, which is an implementation of PKCS #11 <code>C_DigestFinal</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DigestFinalRequest {
        bytes State = 1;
    }
    message DigestFinalResponse {
        bytes Digest = 2;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DigestFinal_EP11" tab-title="Enterprise PKCS #11" tab-group="DigestFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 <code>C_DigestFinal</code>.</p>
    <p><code>DigestFinal</code> is polymorphic, accepting both wrapped or clear digest objects.</p>
    <p>Does not update <code>(state, slen)</code>.</p>
    <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
    <p>The <code>state</code> blob was output from: <code>DigestInit</code>, <code>DigestUpdate</code>, <code>DigestKey</code>.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DigestFinal (
        const unsigned char *state, size_t statelen,
        CK_BYTE_PTR digest, CK_ULONG_PTR digestlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DigestFinal</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

<table id="DigestFinal_PKCS11" tab-title="PKCS #11" tab-group="DigestFinal" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td><p><code>C_DigestFinal</code> finishes a multiple-part message-digesting operation, returning the message digest. <code>hSession</code> is the session’s handle; <code>pDigest</code> points to the location that receives the message digest; <code>pulDigestLen</code> points to the location that holds the length of the message digest.</p>
    <p><code>C_DigestFinal</code> uses the convention that is described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The digest operation must be initialized with <code>C_DigestInit</code>. A call to <code>C_DigestFinal</code> always terminates the active digest operation unless it returns <code>CKR_BUFFER_TOO_SMALL</code> or is a successful call (that is, one that returns <code>CKR_OK</code>) to determine the length of the buffer that is needed to hold the message digest.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_DEFINE_FUNCTION(CK_RV, C_DigestFinal)(
        CK_SESSION_HANDLE hSession,
        CK_BYTE_PTR pDigest,
        CK_ULONG_PTR pulDigestLen
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    DigestFinalRequest := &pb.DigestFinalRequest {
        State: DigestUpdateResponse.State,
    }

    DigestFinalResponse, err := cryptoClient.DigestFinal(context.Background(), DigestFinalRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DigestFinal({
      State: state
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

### DigestSingle
{: #grep11-DigestSingle}

The `DigestSingle` function digests data in one pass with one call and without constructing an intermediate digest state and unnecessary roundtrips. This function is an IBM EP11 extension to the standard PKCS #11 specification and is a combination of the `DigestInit` and `Digest` functions. It enables you to complete a digesting operation with a single call instead of a series of calls.

<table id="DigestSingle_GREP11" tab-title="Enterprise PKCS #11 over gRPC" tab-group="DigestSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>Binds to EP11 <code>m_DigestSingle</code>.<td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    message DigestSingleRequest {
        Mechanism Mech = 1;
        bytes Data = 2;
    }
    message DigestSingleResponse {
        bytes Digest = 3;
    }
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into message <code>Grep11Error</code>.</td>
    </tr>
</table>

<table id="DigestSingle_EP11" tab-title="Enterprise PKCS #11" tab-group="DigestSingle" class="simple-tab-table">
    <tr>
    <th>Description</th>
    <td>
    <p>Nonstandard extension, combination of <code>DigestInit</code> and <code>Digest</code>. Digests data in one pass, with one call, without constructing an intermediate digest state, and unnecessary roundtrips.</p>
    <p>This is the preferred method of digesting cleartext for XCP-aware applications. Functionally, <code>DigestSingle</code> is equivalent to <code>DigestInit</code> followed immediately by <code>Digest</code>.</p>
    <p>If a key needs to be digested, one <em>must</em> use <code>DigestInit</code> and <code>DigestKey</code>, since this function does not handle key blobs.</p>
    <p>Does not return any state to host, only digest result. There are no non-PKCS #11 parameters, since everything is used directly from the PKCS #11 call.</p>
    </td>
    </tr>
    <tr>
    <th>Parameters</th>
    <td>
    <pre>
    CK_RV m_DigestSingle (
        CK_MECHANISM_PTR mech,
        CK_BYTE_PTR data, CK_ULONG datalen,
        CK_BYTE_PTR digest, CK_ULONG_PTR digestlen,
        target_t target
    );
    </pre>
    </td>
    </tr>
    <tr>
    <th>Return values</th>
    <td>A subset of <code>C_DigestSingle</code> return values. For more information, see the <em><strong>Return values</strong></em> chapter of the  <a href="https://www.ibm.com/security/cryptocards/pciecc4/library" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
    </tr>
</table>

**Code snippets**

- Golang code snippet

    ```Golang
    digestData := []byte("Create a digest for this string")
    DigestSingleRequest := &pb.DigestSingleRequest {
        Mech: &pb.Mechanism{Mechanism: ep11.CKM_SHA256},
        Data: digestData,
    }

    DigestSingleResponse, err := cryptoClient.DigestSingle(context.Background(), DigestSingleRequest)
    ```
    {: codeblock}

- JavaScript code snippet

    ```JavaScript
    client.DigestSingle({
      Mech: {
        Mechanism: ep11.CKM_SHA256
      },
      Data: Buffer.from(digestData)
    }, (err, response) => {
      callback(err, response);
    });
    ```
    {: codeblock}

## Code examples
{: #code-example}

GREP11 API supports programming languages with [gRPC libraries](https://www.grpc.io/docs/){: external}. Two sample GitHub repositories are provided for you to test the GREP11 API:

- [The sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external}
- [The sample GitHub repository for JavaScript](https://github.com/IBM-Cloud/hpcs-grep11-js){: external}
