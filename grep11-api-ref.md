---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-22"

Keywords: EP11, PKCS#11, GREP11, API reference, EP11 over gRPC,

subcollection: hs-crypto

---

{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:download: .download}
{:hide-in-docs: .hide-in-docs}
{:authenticated-content: .authenticated-content}
{:shortdesc: .shortdesc}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:preview: .preview}
{:subsection: outputclass="subsection"}
{:row-headers .row-headers}
{:new_window: target="_blank"}
{:external: target="_blank" .external}

# GREP11 API reference
{: #grep11-api-ref}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 (EP11) APIs over [gRPC](https://grpc.io){: external} calls (also referred to *GREP11*), with which all the Crypto functions are executed in a Hardware Security Module (HSM) on the cloud.
{: shortdesc}

By using the GREP11 API, you can perform the following operations:

- Key generation
- Encrypt and decrypt
- Sign and verify
- Wrap and unwrap keys
- Derive keys
- Build message digest
- Retrieve mechanism information

For each operation, there are a series of suboperations. For example, the `Encrypt` operation is composed of `EncryptInit()`, `Encrypt()`, `EncryptUpdate()`, `EncryptFinal()`, and `EncryptSingle()` suboperations.

- `EncryptInit()` is used to initialize an operation.
- `Encrypt()` is used to encrypt data without the need to perform `EncryptUpdate()` and `EncryptFinal()` suboperations. This suboperation needs to be performed after the `EncryptInit()` call.
- `EncryptUpdate()` and `EncryptFinal()` are used in combination to perform data encryption. These suboperations need to be performed after the `EncryptInit()` call.  
- `EncryptSingle()` is an IBM EP11 extension to the standard PKCS#11 specification, and is used to perform a single call to encrypt data without the need to run the `EncryptInit()`, `Encrypt()`, `EncryptUpdate()`, or `EncryptFinal()` sub-operation.

For information on how the GREP11 functions are related to PKCS #11 and EP11, see [GREP11 introduction](/docs/services/hs-crypto?topic=hs-crypto-enterprise_PKCS11_overview#grep11_intro).

## Accessing the API
{: #access-grep11-functions}

A GREP11 API endpoint, a service ID API key, an IAM endpoint, and an instance ID are needed for initialization before performing any GREP11 API function calls. For details, see [Generating a GREP11 API request](/docs/services/hs-crypto?topic=hs-crypto-set-up-grep11-api#form-grep11-api-request).

## Error handling
{: #grep11-error-handling}

Enterprise PKCS #11 (EP11) over gRPC relies on the gRPC specification for [error handling](https://grpc.io/docs/guides/error/){: external}. When an error occurs, gRPC clients receive a [`message Status` protocol buffer](https://github.com/grpc/grpc/blob/master/src/proto/grpc/status/status.proto){: external}.

```proto3
message Status {
    int32 code = 1;
    string message = 2;
    repeated google.protobuf.Any details = 3;
}
```
{: codeblock}

In the error message,

- `code` includes the status code, which should be an enumerated-type (enum) value of the `google.rpc.Code` field.
- `message` includes a developer-facing error message in English. Any user-facing error message should be localized and sent in the `google.rpc.Status.details` field, or localized by the user.
- `details` lists messages that carry the error details. A common set of message types are available for APIs to use.

Enterprise PKCS #11 (EP11) over gRPC uses the `Detail` field to attach extra error code information.

```proto3
message Grep11Error {
    uint64 Code = 1;
    string Detail = 2;
    bool Retry = 3;
}
```
{: codeblock}

The `Code` field can be cast to the ***CK_RV*** value in PKCS #11. This field contains the error codes defined by the [PKCS #11 specification](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959729){: external} or the vendor extensions defined by EP11. EP11 uses only a subset of return values that PKCS #11 defines. See the **10.1.6 Return values** section in [Enterprise PKCS #11 Library structure](https://www.ibm.com/downloads/cas/WXRDPRAN) for details.

Here is an [example]( https://github.com/vpaprots/ibm-cloud-hyperprotectcrypto/blob/ad02bb8b58bf6845d9953e98aa38afda3099a658/golang/examples/server_test.go#L518){: external} in Golang that deals with errors.

## GREP11 functions
{: #grep11-functions}

Enterprise PKCS #11 (EP11) over gRPC defines gRPC functions based on the EP11 implementation of the PKCS #11 specification. The following function descriptions are created based on the [PKCS #11 specification](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}, with notes specific to EP11. All parameter definitions are in the original form of EP11. For more details about EP11, refer to [Enterprise PKCS #11 (EP11) Library structure](https://www.ibm.com/downloads/cas/WXRDPRAN){: external}.

EP11 function parameters are mapped to the protocol buffer types that can be found in the following functions. You can learn more about protocol buffer types [here](https://developers.google.com/protocol-buffers/docs/proto3#scalar){: external}.

Because the EP11 library is a subset of the PKCS #11 API library, and GREP11 functions are variants from the corresponding EP11 functions, the corresponding functions of EP11 and PKCS #11 are also listed in the GREP11 function tables for your reference. For more details on PKCS #11 and the legal statement, see the [PKCS #11 specification](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}. For details about EP11, see [Enterprise PKCS #11 (EP11) Library structure](https://www.ibm.com/downloads/cas/WXRDPRAN){: external}.
{: note}

Enterprise PKCS #11 (EP11) over gRPC supports programming languages such as Golang, JavaScript, and Java. At the current stage, only code snippets for Golang are included in the API reference. The content will be enriched in later phases.

<br/>

### GenerateRandom
{: #grep11-GenerateRandom}

The `GenerateRandom` function generates random data.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_GenerateRandom`, which is an implementation of PKCS #11 `C_GenerateRandom`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #GenerateRandom_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="GenerateRandom"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 <code>C_GenerateRandom</code>.</p>
    <p><code>GenerateRandom</code> is equivalent to the original PKCS #11 function.
    Internally, hardware-seeded entropy is passed through a FIPS-compliant
    DRNG (ANSI X9.31/ISO 18031, depending on Clic version).</p>
    <p>The host library could generate random numbers without
    dispatching to the backend, if suitable functionality would be
     available on the host.  This is not done in the current implementation.</p>
     <p>This function does not support a size query.</p></td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
CK_RV m_GenerateRandom (
     CK_BYTE_PTR rnd, CK_ULONG rndlen,
     target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_GenerateRandom` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #GenerateRandom_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="GenerateRandom"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>`C_GenerateRandom` generates random or pseudo-random data. `hSession` is the sessions handle; pRandomData points to the location that receives the random data; and `ulRandomLen` is the length in bytes of the random or pseudo-random data to be generated.</td>
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
    <code>
    CKR_ARGUMENTS_BAD,
    CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED,
    CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY,
    CKR_OK, CKR_OPERATION_ACTIVE, CKR_RANDOM_NO_RNG, CKR_SESSION_CLOSED,
    CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    <code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #GenerateRandom_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="GenerateRandom"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #GenerateRandom-snippet}

```Golang
GenerateRandomRequest := &pb.GenerateRandomRequest {
	Len: 1024,
}

GenerateRandomResponse, err := cryptoClient.GenerateRandom(context.Background(), GenerateRandomRequest)
```
{: codeblock}

<br/>

### DigestInit
{: #grep11-DigestInit}

The `DigestInit` function initializes a message-digesting operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DigestInit`, which is an implementation of PKCS #11 `C_DigestInit`.<td>
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
    </code>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DigestInit_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DigestInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td><p>Implementation of PKCS #11 <code>C_DigestInit</code>.</p>
  <p>Create wrapped digest state.</p>
  <p>**Note**: size queries are supported, but the wrapped state is always returned by the backend, unlike most size queries (which return an output size, instead of actual output). <code>Digest</code> states are sufficiently small that they do not introduce noticeable transport overhead, except obviously object wrapping.</p>
  <p>During size queries, the host just discards the returned state, and reports blob size (in <code>len</code>).  When returning blob, *len is checked against returned size.</p>
  <p>The <code>state</code>,<code>len</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter. (Host library must tie blob to session.)</p></td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
CK_RV m_DigestInit (
   unsigned char *state, size_t *statelen,
   const CK_MECHANISM_PTR mech,
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DigestInit` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DigestInit_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DigestInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_DigestInit` initializes a message-digesting operation. `hSession` is the session’s handle; pMechanism points to the digesting mechanism.</p>
    <p>After calling `C_DigestInit`, the application can either call `C_Digest` to digest data in a single part; or call `C_DigestUpdate` zero or more times, followed by `C_DigestFinal`, to digest data in multiple parts.  The message-digesting operation is active until the application uses a call to C_Digest or `C_DigestFinal` to actually obtain the message digest. To process additional data (in single or multiple parts), the application must call `1C_DigestInit1` again.</p>
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
    <td><code>CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.</code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DigestInit_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DigestInit"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DigestInit-snippet}

```Golang
DigestInitRequest := &pb.DigestInitRequest {
	Mech: &pb.Mechanism{Mechanism: ep11.CKM_SHA256},
}

DigestInitResponse, err := cryptoClient.DigestInit(context.Background(), DigestInitRequest)
```
{: codeblock}

<br/>

### Digest
{: #grep11-Digest}

The `Digest` function digests single-part data.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_Digest`, which is an implementation of PKCS #11 `C_Digest`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #Digest_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="Digest"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
  <td>
  <p>Implementation of PKCS #11 <code>C_Digest</code>.</p>
  <p>Note that if a digest object has had exactly 0 (zero) bytes appended to it after creation, in any combination of zero byte transfers, it may still perform a one-pass Digest, even if it should be rejected by a strict implementation. This is a feature.</p>
  <p>Does not update <code>(state, slen)</code>.</p>
  <p>Implementations <i>may</i> perform
  <code>DigestUpdate</code>, <code>DigestFinal<code>, or <code>Digest</code> calls on cleartext digest objects in host code, bypassing HSM backends altogether. This choice may or may not be visible to host code, and it does not impact the security of the operation (as clear objects can not digest sensitive data). </p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Digest` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #Digest_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="Digest"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_Digest` digests data in a single part. `hSession` is the session’s handle, pData points to the data; `ulDataLen` is the length of the data; `pDigest` points to the location that receives the message digest; `pulDigestLen` points to the location that holds the length of the message digest.</p>
    <p>`C_Digest` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The digest operation must have been initialized with `C_DigestInit`.  A call to `C_Digest` always terminates the active digest operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call (i.e., one which returns `CKR_OK`) to determine the length of the buffer needed to hold the message digest.</p>
    <p>`C_Digest` cannot be used to terminate a multi-part operation, and must be called after `C_DigestInit` without intervening `C_DigestUpdate` calls.</p>
    <p>The input data and digest output can be in the same place, i.e., it is OK if pData and pDigest point to the same location.</p>
    <p>`C_Digest` is equivalent to a sequence of `C_DigestUpdate` operations followed by `C_DigestFinal`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #Digest_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="Digest"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #Digest-snippet}

```Golang
DigestRequest := &pb.DigestRequest {
	State: DigestInitResponse.State,
	Data:  digestData,
}

DigestResponse, err := cryptoClient.Digest(context.Background(), DigestRequest)
```
{: codeblock}

<br/>

### DigestUpdate
{: #grep11-DigestUpdate}

The `DigestUpdate` function continues a multiple-part digesting operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DigestUpdate`, which is an implementation of PKCS #11 `C_DigestUpdate`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DigestUpdate_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DigestUpdate"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DigestUpdate` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DigestUpdate_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DigestUpdate"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_DigestUpdate` continues a multiple-part message-digesting operation, processing another data part. `hSession` is the session’s handle, `pPart` points to the data part; `ulPartLen` is the length of the data part.</p>
    <p>The message-digesting operation must have been initialized with `C_DigestInit`. Calls to this function and `C_DigestKey` may be interspersed any number of times in any order. A call to `C_DigestUpdate` which results in an error terminates the current digest operation.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DigestUpdate_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DigestUpdate"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DigestUpdate-snippet}

```Golang
DigestUpdateRequest := &pb.DigestUpdateRequest {
	State: DigestInitResponse.State,
	Data:  digestData[:64],
}

DigestUpdateResponse, err := cryptoClient.DigestUpdate(context.Background(), DigestUpdateRequest)
```
{: codeblock}

<br/>

<!-- ### DigestKey
{: #grep11-DigestKey}

The `DigestKey` function digests a key.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DigestKey`, which is an implementation of PKCS #11 `C_DigestKey`.<td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
message DigestKeyRequest {
	bytes State = 1;
	bytes Key = 2;
}
message DigestKeyResponse {
	bytes State = 1;
}
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DigestKey_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DigestKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_DigestKey</code>.</p>
  <p>Note that, by construction, none of the <code>DigestKey</code> inputs are native PKCS #11 variables. Both are blobs, one containing wrapped state, the other a key object.  No final result is returned, only state is updated during the call.</p>
  <p><code>DigestKey</code> is the only non-polymorphic <code>DigestNNN</code> call. It rejects clear digest objects, since those could reveal key bytes when passed back to the host in the clear.</p>
  <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
  <p>The <code>state</code> blob was output from: <code>DigestInit</code>, <code>DigestUpdate</code>, <code>DigestKey</code>.</p>
</td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
CK_RV m_DigestKey (
    unsigned char *state, size_t statelen,
    const unsigned char *key, size_t keylen,
    target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DigestKey` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DigestKey_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DigestKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_DigestKey` continues a multiple-part message-digesting operation by digesting the value of a secret key. `hSession` is the session’s handle; `hKey` is the handle of the secret key to be digested.</p>
    <p>The message-digesting operation must have been initialized with `C_DigestInit`. Calls to this function and `C_DigestUpdate` may be interspersed any number of times in any order.</p>
    <p>If the value of the supplied key cannot be digested purely for some reason related to its length, `C_DigestKey` should return the error code `CKR_KEY_SIZE_RANGE`.</p>
    </td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
CK_DEFINE_FUNCTION(CK_RV, C_DigestKey)(
    CK_SESSION_HANDLE hSession,
    CK_OBJECT_HANDLE hKey
);
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td><code>CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_HANDLE_INVALID, CKR_KEY_INDIGESTIBLE, CKR_KEY_SIZE_RANGE, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.</code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DigestKey_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DigestKey"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DigestKey-snippet}

```Golang
DigestKeyRequest := &pb.DigestKeyRequest {
	State: DigestInitResponse.State,
	Key:  GenerateKeyResponse.Key,
}

DigestKeyResponse, err := cryptoClient.DigestKey(context.Background(), DigestKeyRequest)
```
{: codeblock}

<br/> -->
### DigestFinal
{: #grep11-DigestFinal}

The `DigestFinal` function finishes a multiple-part digesting operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DigestFinal`, which is an implementation of PKCS #11 `C_DigestFinal`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DigestFinal_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DigestFinal"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DigestFinal` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DigestFinal_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DigestFinal"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_DigestFinal` finishes a multiple-part message-digesting operation, returning the message digest. `hSession` is the session’s handle; `pDigest` points to the location that receives the message digest; `pulDigestLen` points to the location that holds the length of the message digest.</p>
    <p>`C_DigestFinal` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The digest operation must have been initialized with `C_DigestInit`.  A call to `C_DigestFinal` always terminates the active digest operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call (i.e., one which returns `CKR_OK`) to determine the length of the buffer needed to hold the message digest.</p>
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
    <td><code>CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.</code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DigestFinal_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DigestFinal"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DigestFinal-snippet}

```Golang
DigestFinalRequest := &pb.DigestFinalRequest {
	State: DigestUpdateResponse.State,
}

DigestFinalResponse, err := cryptoClient.DigestFinal(context.Background(), DigestFinalRequest)
```
{: codeblock}

<br/>

### DigestSingle
{: #grep11-DigestSingle}

The `DigestSingle` function digests data in one pass, with one call, without constructing an intermediate digest state, and unnecessary roundtrips.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DigestSingle`<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DigestSingle_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DigestSingle"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Nonstandard extension, combination of <code>DigestInit</code> and <code>Digest</code>. Digests data in one pass, with one call, without constructing an intermediate digest state, and unnecessary roundtrips.</p>
  <p>This is the preferred method of digesting cleartext for XCP-aware applications. Functionally, <code>DigestSingle</code> is equivalent to <code>DigestInit</code> followed immediately by <code>Digest</code>.</p>
  <p>If a key needs to be digested, one <i>must</i> use <code>DigestInit</code> and <code>DigestKey</code>, since this function does not handle key blobs.</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DigestSingle` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DigestSingle_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DigestSingle"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DigestSingle-snippet}

```Golang
DigestSingleRequest := &pb.DigestSingleRequest {
	Mech: &pb.Mechanism{Mechanism: ep11.CKM_SHA256},
	Data: digestData,
}

DigestSingleResponse, err := cryptoClient.DigestSingle(context.Background(), DigestSingleRequest)
```
{: codeblock}

<br/>

### EncryptInit
{: #grep11-EncryptInit}

The `EncryptInit` function initializes an encryption operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_EncryptInit`, which is an implementation of PKCS #11 `C_EncryptInit`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #EncryptInit_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="EncryptInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_EncryptInit</code>.</p>
  <p>The <code>(key, klen)</code> blob may be a public-key object, or a secret-key blob. Key type must be consistent with <code>pmech</code>.</p>
  <p>For public-key mechanisms, <code>(key, klen)</code> must contain an SPKI. This SPKI <i>must be MACed</i>, as returned by <code>GenerateKeyPair</code> or alternatively <code>UnwrapKey</code>. The Encrypt state is created without session restrictions.</p>
  <p>For secret-key mechanisms, the Encrypt state inherits object session restrictions from <prm>key,klen<prm>.</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_EncryptInit` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #EncryptInit_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="EncryptInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_EncryptInit` initializes an encryption operation. `hSession` is the session’s handle; `pMechanism` points to the encryption mechanism; `hKey` is the handle of the encryption key.</p>
    <p>The `CKA_ENCRYPT` attribute of the encryption key, which indicates whether the key supports encryption, must be `CK_TRUE`.</p>
    <p>After calling `C_EncryptInit`, the application can either call C_Encrypt to encrypt data in a single part; or call `C_EncryptUpdate` zero or more times, followed by `C_EncryptFinal`, to encrypt data in multiple parts.  The encryption operation is active until the application uses a call to `C_Encrypt` or `C_EncryptFinal` to actually obtain the final piece of ciphertext.  To process additional data (in single or multiple parts), the application must call `C_EncryptInit` again.</p>
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
    <td><code>CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.</code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #EncryptInit_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="EncryptInit"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #EncryptInit-snippet}

```Golang
EncryptInitRequest := &pb.EncryptInitRequest {
	Mech: &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: iv},
	Key:  GenerateKeyResponse.Key,
}

EncryptInitResponse, err := cryptoClient.EncryptInit(context.Background(), EncryptInitRequest)
```
{: codeblock}

<br/>

### DecryptInit
{: #grep11-DecryptInit}

The `DecryptInit` function initializes a decryption operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DecryptInit`, which is an implementation of PKCS #11 `C_DecryptInit`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DecryptInit_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DecryptInit"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DecryptInit` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DecryptInit_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DecryptInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_DecryptInit` initializes a decryption operation. `hSession` is the session’s handle; `pMechanism` points to the decryption mechanism; `hKey` is the handle of the decryption key.</p>
    <p>The `CKA_DECRYPT` attribute of the decryption key, which indicates whether the key supports decryption, must be `CK_TRUE`.</p>
    <p>After calling `C_DecryptInit`, the application can either call C_Decrypt to decrypt data in a single part; or call C_DecryptUpdate zero or more times, followed by `C_DecryptFinal`, to decrypt data in multiple parts.  The decryption operation is active until the application uses a call to `C_Decrypt` or `C_DecryptFinal` to actually obtain the final piece of plaintext. To process additional data (in single or multiple parts), the application must call `C_DecryptInit` again.</p>
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
    <td><code>CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.</code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DecryptInit_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DecryptInit"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DecryptInit-snippet}

```Golang
DecryptInitRequest := &pb.DecryptInitRequest {
	Mech: &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC_PAD, Parameter: iv},
	Key:  GenerateKeyResponse.Key,
}

DecryptInitResponse, err := cryptoClient.DecryptInit(context.Background(), DecryptInitRequest)
```
{: codeblock}

<br/>

### EncryptUpdate
{: #grep11-EncryptUpdate}

The `EncryptUpdate` function continues a multiple-part encryption operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_EncryptUpdate`, which is an implementation of PKCS #11 `C_EncryptUpdate`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #EncryptUpdate_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="EncryptUpdate"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_EncryptUpdate</code>.</p>
  <p>The <code>state</code>,<code>slen</code> blob must be mapped from the PKCS #11 <code>hSession</code> parameter.</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_EncryptUpdate` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #EncryptUpdate_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="EncryptUpdate"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_EncryptUpdate` continues a multiple-part encryption operation, processing another data part. `hSession` is the session’s handle; `pPart` points to the data part; `ulPartLen` is the length of the data part; `pEncryptedPart` points to the location that receives the encrypted data part; `pulEncryptedPartLen` points to the location that holds the length in bytes of the encrypted data part.</p>
    <p>`C_EncryptUpdate` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The encryption operation must have been initialized with `C_EncryptInit`.  This function may be called any number of times in succession. A call to `C_EncryptUpdate` which results in an error other than `CKR_BUFFER_TOO_SMALL` terminates the current encryption operation.</p>
    <p>The `plaintext` and `ciphertext` can be in the same place, i.e., it is OK if `pPart` and `pEncryptedPart` point to the same location.</p>
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
    <td><code>CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.</code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #EncryptUpdate_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="EncryptUpdate"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #EncryptUpdate-snippet}

```Golang
EncryptUpdateRequest := &pb.EncryptUpdateRequest {
	State: EncryptInitResponse.State,
	Plain: plainText[:20],
}

EncryptUpdateResponse, err := cryptoClient.EncryptUpdate(context.Background(), EncryptUpdateRequest)
```
{: codeblock}

<br/>

### DecryptUpdate
{: #grep11-DecryptUpdate}

The `DecryptUpdate` function continues a multiple-part decryption operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DecryptUpdate`, which is an implementation of PKCS #11 `C_DecryptUpdate`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DecryptUpdate_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DecryptUpdate"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DecryptUpdate` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DecryptUpdate_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DecryptUpdate"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_DecryptUpdate` continues a multiple-part decryption operation, processing another encrypted data part. `hSession` is the session’s handle; `pEncryptedPart` points to the encrypted data part; `ulEncryptedPartLen` is the length of the encrypted data part; `pPart` points to the location that receives the recovered data part; `pulPartLen` points to the location that holds the length of the recovered data part.</p>
    <p>`C_DecryptUpdate` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The decryption operation must have been initialized with `C_DecryptInit`.  This function may be called any number of times in succession.  A call to `C_DecryptUpdate` which results in an error other than CKR_BUFFER_TOO_SMALL terminates the current decryption operation.</p>
    <p>The ciphertext and plaintext can be in the same place, i.e., it is OK if `pEncryptedPart` and `pPart` point to the same location.</p></td>
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
    </code>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DecryptUpdate_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DecryptUpdate"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DecryptUpdate-snippet}

```Golang
DecryptUpdateRequest := &pb.DecryptUpdateRequest {
	State:    DecryptInitResponse.State,
	Ciphered: ciphertext[:16],
}

DecryptUpdateResponse, err := cryptoClient.DecryptUpdate(context.Background(), DecryptUpdateRequest)
```
{: codeblock}

<br/>

### Encrypt
{: #grep11-Encrypt}

The `Encrypt` function encrypts single-part data.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_Encrypt`, which is an implementation of PKCS #11 `C_Encrypt`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #Encrypt_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="Encrypt"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
      </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Encrypt` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #Encrypt_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="Encrypt"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_Encrypt` encrypts single-part data. `hSession` is the session’s handle; `pData` points to the data; `ulDataLen` is the length in bytes of the data; `pEncryptedData` points to the location that receives the encrypted data; `pulEncryptedDataLen` points to the location that holds the length in bytes of the encrypted data.</p>
    <p>`C_Encrypt` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The encryption operation must have been initialized with `C_EncryptInit`.  A call to `C_Encrypt` always terminates the active encryption operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call (i.e., one which returns `CKR_OK`) to determine the length of the buffer needed to hold the ciphertext.</p>
    <p>`C_Encrypt` cannot be used to terminate a multi-part operation, and must be called after `C_EncryptInit` without intervening `C_EncryptUpdate` calls.</p>
    <p>For some encryption mechanisms, the input plaintext data has certain length constraints (either because the mechanism can only encrypt relatively short pieces of plaintext, or because the mechanism’s input data must consist of an integral number of blocks).  If these constraints are not satisfied, then `C_Encrypt` will fail with return code `CKR_DATA_LEN_RANGE`.</p>
    <p>The plaintext and ciphertext can be in the same place, i.e., it is OK if `pData` and `pEncryptedData` point to the same location.</p>
    <p>For most mechanisms, `C_Encrypt` is equivalent to a sequence of `C_EncryptUpdate` operations followed by `C_EncryptFinal`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_INVALID, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #Encrypt_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="Encrypt"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #Encrypt-snippet}

```Golang
EncryptRequest := &pb.EncryptRequest {
	State: EncryptInitResponse.State,
	Plain: plainText,
}

EncryptResponse, err := cryptoClient.Encrypt(context.Background(), EncryptRequest)
```
{: codeblock}

<br/>

### Decrypt
{: #grep11-decrypt}

Decrypt decrypts data in a single part.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_Decrypt`, which is an implementation of PKCS #11 `C_Decrypt`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #decrypt_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="decrypt"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>Implementation of PKCS #11 C_Decrypt. It does not update (state, slen).</p>
    <p>The state, slen binary large object (BLOB) must be mapped from the PKCS #11 `hSession` parameter. The state BLOB was output from `DecryptInit`.</p>
    </td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
CK_RV m_Decrypt (const unsigned char *state, size_t slen,
  CK_BYTE_PTR cipher, CK_ULONG clen,
  CK_BYTE_PTR plain, CK_ULONG_PTR plen,
  target_t target) ;
    </pre>
    </code>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Decrypt` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #decrypt_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="decrypt"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
      <p>`C_Decrypt` decrypts encrypted data in a single part.
        <ul>
          <li>`hSession` is the session handle.</li>
          <li>`pEncryptedData` points to the encrypted data.</li>
          <li>`ulEncryptedDataLen` is the length of the encrypted data.</li>
          <li>`pData` points to the location that receives the recovered data.</li>
          <li>`pulDataLen` points to the location that holds the length of the recovered data.</li>
        </ul>
      </p>
    <p>`C_Decrypt` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The decryption operation should be initialized with `C_DecryptInit`. A call to `C_Decrypt` always terminates the active decryption operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call with `CKR_OK` returned to determine the length of the buffer needed to hold the plaintext.</p>
    <p>`C_Decrypt` cannot be used to terminate a multi-part operation, and should be called after `C_DecryptInit` without intervening `C_DecryptUpdate` calls.</p>
    <p>The ciphertext and plaintext can be in the same place, which means it is acceptable if pEncryptedData and pData point to the same location.</p>
    <p>If the input ciphertext data cannot be decrypted because it has an inappropriate length, either `CKR_ENCRYPTED_DATA_INVALID` or `CKR_ENCRYPTED_DATA_LEN_RANGE` can be returned.</p></td>
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
    </code>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_ENCRYPTED_DATA_INVALID, CKR_ENCRYPTED_DATA_LEN_RANGE, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #Decrypt_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="decrypt"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #Decrypt-snippet}

```Golang
DecryptRequest := &pb.DecryptRequest {
	State:    DecryptInitResponse.State,
	Ciphered: ciphertext,
}

DecryptResponse, err := cryptoClient.Decrypt(context.Background(), DecryptRequest)
```
{: codeblock}

<br/>

### EncryptFinal
{: #grep11-EncryptFinal}

The `EncryptFinal` function finishes a multiple-part encryption operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_EncryptFinal`, which is an implementation of PKCS #11 `C_EncryptFinal`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #EncryptFinal_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="EncryptFinal"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_EncryptFinal` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #EncryptFinal_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="EncryptFinal"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_EncryptFinal` finishes a multiple-part encryption operation. `hSession` is the session’s handle; `pLastEncryptedPart` points to the location that receives the last encrypted data part, if any; `pulLastEncryptedPartLen` points to the location that holds the length of the last encrypted data part.</p>
    <p>`C_EncryptFinal` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The encryption operation must have been initialized with `C_EncryptInit`.  A call to `C_EncryptFinal` always terminates the active encryption operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call (i.e., one which returns `CKR_OK`) to determine the length of the buffer needed to hold the ciphertext.</p>
    <p>For some multi-part encryption mechanisms, the input plaintext data has certain length constraints, because the mechanism’s input data must consist of an integral number of blocks.  If these constraints are not satisfied, then `C_EncryptFinal` will fail with return code `CKR_DATA_LEN_RANGE`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #EncryptFinal_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="EncryptFinal"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #EncryptFinal-snippet}

```Golang
EncryptFinalRequest := &pb.EncryptFinalRequest {
	State: EncryptUpdateResponse.State,
}

EncryptFinalResponse, err := cryptoClient.EncryptFinal(context.Background(), EncryptFinalRequest)
```
{: codeblock}

<br/>

### DecryptFinal
{: #grep11-DecryptFinal}

The `DecryptFinal` function finishes a multiple-part decryption operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DecryptFinal`, which is an implementation of PKCS #11 `C_DecryptFinal`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DecryptFinal_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DecryptFinal"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DecryptFinal` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DecryptFinal_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DecryptFinal"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_DecryptFinal` finishes a multiple-part decryption operation. `hSession` is the session’s handle; `pLastPart` points to the location that receives the last recovered data part, if any; `pulLastPartLen` points to the location that holds the length of the last recovered data part.</p>
    <p>`C_DecryptFinal` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The decryption operation must have been initialized with `C_DecryptInit`.  A call to `C_DecryptFinal` always terminates the active decryption operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call (i.e., one which `returns CKR_OK`) to determine the length of the buffer needed to hold the plaintext.</p>
    <p>If the input ciphertext data cannot be decrypted because it has an inappropriate length, then either `CKR_ENCRYPTED_DATA_INVALID` or `CKR_ENCRYPTED_DATA_LEN_RANGE` may be returned.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_ENCRYPTED_DATA_INVALID, CKR_ENCRYPTED_DATA_LEN_RANGE, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DecryptFinal_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DecryptFinal"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DecryptFinal-snippet}

```Golang
DecryptFinalRequest := &pb.DecryptFinalRequest {
	State: DecrypUpdateResponse.State,
}

DecryptFinalResponse, err := cryptoClient.DecryptFinal(context.Background(), DecryptFinalRequest)
```
{: codeblock}

<br/>

### EncryptSingle
{: #grep11-EncryptSingle}

The `EncryptSingle` function processes data in one pass, with one call. Does not return any state to host, only encrypted data.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_EncryptSingle`<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #EncryptSingle_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="EncryptSingle"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Non-standard variant of <code>Encrypt</code>. Processes data in one pass, with one call. Does not return any state to host, only encrypted data.</p>
  <p>This is the preferred method of encrypting data in one pass for XCP-aware applications. Functionally it is equivalent to <code>EncryptInit</code> followed immediately by <code>Encrypt</code>, but it saves roundtrips and wrapping/unwrapping.</p>
  <p>If the backend supports resident keys, the key may be also a resident-key handle.</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_EncryptSingle` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #EncryptSingle_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="EncryptSingle"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #EncryptSingle-snippet}

```Golang
EncryptSingleRequest := &pb.EncryptSingleRequest {
	Mech:  &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC, Parameter: iv},
	Key:   GenerateKeyResponse.Key,
	Plain: plainText,
}

EncryptSingleResponse, err := cryptoClient.EncryptSingle(context.Background(), EncryptSingleRequest)
```
{: codeblock}

<br/>

### DecryptSingle
{: #grep11-DecryptSingle}

The `DecryptSingle` function processes data in one pass, with one call. Does not return any state to host, only decrypted data.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DecryptSingle`<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DecryptSingle_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DecryptSingle"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Non-standard variant of <code>Decrypt</code>. Processes data in one pass, with one call. Does not return any state to host, only decrypted data.</p>
  <p>This is the preferred method of encrypting data in one pass for XCP-aware applications. Functionally it is equivalent to <code>DecryptInit</code> followed immediately by <code>Decrypt</code>, but it saves roundtrips and wrapping/unwrapping.</p>
  <p>If the backend supports resident keys, the key may be also a resident-key handle.</p>
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
   target_t target) ;
      </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Decrypt` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DecryptSingle_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DecryptSingle"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DecryptSingle-snippet}

```Golang
DecryptSingleRequest := &pb.DecryptSingleRequest {
	Mech:     &pb.Mechanism{Mechanism: ep11.CKM_AES_CBC, Parameter: iv},
	Key:      GenerateKeyResponse.Key,
	Ciphered: EncryptSingleResponse.Ciphered,
}

DecryptSingleResponse, err := cryptoClient.DecryptSingle(context.Background(), DecryptSingleRequest)
```
{: codeblock}

<br/>

### SignInit
{: #grep11-SignInit}

The `SignInit` function initializes a signature operation

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_SignInit`, which is an implementation of PKCS #11 `C_SignInit`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #SignInit_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="SignInit"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Decrypt` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #SignInit_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="SignInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_SignInit` initializes a signature operation, where the signature is an appendix to the data. `hSession` is the session's handle; `pMechanism` points to the signature mechanism; `hKey` is the handle of the signature key.</p>
    <p>The `CKA_SIGN` attribute of the signature key, which indicates whether the key supports signatures with appendix, must be `CK_TRUE`.</p>
    <p>After calling `C_SignInit`, the application can either call `C_Sign` to sign in a single part; or call `C_SignUpdate` one or more times, followed by `C_SignFinal`, to sign data in multiple parts. The signature operation is active until the application uses a call to `C_Sign` or `C_SignFinal` to actually obtain the signature. To process additional data (in single or multiple parts), the application must call `C_SignInit` again.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED,CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #SignInit_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="SignInit"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #SignInit-snippet}

```Golang
SignInitRequest := &pb.SignInitRequest {
	Mech:    &pb.Mechanism{Mechanism: ep11.CKM_SHA1_RSA_PKCS},
	PrivKey: GenerateKeyPairResponse.PrivKey,
}

SignInitResponse, err := cryptoClient.SignInit(context.Background(), SignInitRequest)
```
{: codeblock}

<br/>

### VerifyInit
{: #grep11-VerifyInit}

The `VerifyInit` function initializes a verification operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_VerifyInit`, which is an implementation of PKCS #11 `C_VerifyInit`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #VerifyInit_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="VerifyInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_VerifyInit</code>. Given a key blob <code>(key, klen)</code>, initialize a verify session state in <code>(state, slen)</code>. The key blob may be a public key object, or HMAC key bytes. Key blob type must be consistent with <code>pmech</code>.</p>
  <p>For public-key mechanisms, <code>(key, klen)</code> must contain an SPKI. This SPKI may be MACed (such as returned earlier by <code>GenerateKeyPair</code>) or just the SPKI itself (if obtained from an external source, such as a certificate).</p>
  <p>If initializing an HMAC operation, session restrictions of the <code>Verify</code> object are inherited from the HMAC key. Since SPKIs are not tied to sessions, public-key Verify states are session-free.</p>
  <p>The <code>key</code>,<code>klen</code> blob must be mapped from the PKCS #11 <code>hKey</code> parameter.</p>
  <p>**Note**: <code>SignInit</code> and <code>VerifyInit</code> are internally the
  same for HMAC and other symmetric/MAC mechanisms, other than enforcing different restrictions different restrictions (sign and verify, respectively).</p>
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
     target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_VerifyInit` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #VerifyInit_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="VerifyInit"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_VerifyInit` initializes a verification operation, where the signature is an appendix to the data. `hSession` is the session's handle; `pMechanism` points to the structure that specifies the verification mechanism; `hKey` is the handle of the verification key.</p>
    <p>The `CKA_VERIFY` attribute of the verification key, which indicates whether the key supports verification where the signature is an appendix to the data, must be `CK_TRUE`.</p>
    <p>After calling `C_VerifyInit`, the application can either call `C_Verify` to verify a signature on data in a single part; or call `C_VerifyUpdate` one or more times, followed by `C_VerifyFinal`, to verify a signature on data in multiple parts. The verification operation is active until the application calls `C_Verify` or `C_VerifyFinal`. To process additional data (in single or multiple parts), the application must call `C_VerifyInit` again.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_FUNCTION_NOT_PERMITTED, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #VerifyInit_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="VerifyInit"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #VerifyInit-snippet}

```Golang
VerifyInitRequest := &pb.VerifyInitRequest {
	Mech:   &pb.Mechanism{Mechanism: ep11.CKM_SHA1_RSA_PKCS},
	PubKey: GenerateKeyPairResponse.PubKey,
}

VerifyInitResponse, err := cryptoClient.VerifyInit(context.Background(), VerifyInitRequest)
```
{: codeblock}

<br/>

### SignUpdate
{: #grep11-SignUpdate}

The `SignUpdate` function continues a multiple-part signature operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_SignUpdate`, which is an implementation of PKCS #11 `C_SignUpdate`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #SignUpdate_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="SignUpdate"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
      </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_SignUpdate` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #SignUpdate_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="SignUpdate"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_SignUpdate` continues a multiple-part signature operation, processing another data part. `hSession` is the session's handle, pPart points to the data part; `ulPartLen` is the length of the data part.</p>
    <p>The signature operation must have been initialized with `C_SignInit`. This function may be called any number of times in succession. A call to `C_SignUpdate` which results in an error terminates the current signature operation.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN.
    </code></td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #SignUpdate_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="SignUpdate"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #SignUpdate-snippet}

```Golang
SignUpdateRequest := &pb.SignUpdateRequest {
	State: SignInitResponse.State,
	Data:  msgHash[:],
}

SignUpdateResponse, err := cryptoClient.SignUpdate(context.Background(), SignUpdateRequest)
```
{: codeblock}

<br/>

### VerifyUpdate
{: #grep11-VerifyUpdate}

The `VerifyUpdate` function continues a multiple-part verification operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_VerifyUpdate`, which is an implementation of PKCS #11 `C_VerifyUpdate`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #VerifyUpdate_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="VerifyUpdate"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_VerifyUpdate` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #VerifyUpdate_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="VerifyUpdate"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_VerifyUpdate` continues a multiple-part verification operation, processing another data part. `hSession` is the session's handle, `pPart` points to the data part; `ulPartLen` is the length of the data part.</p>
    <p>The verification operation must have been initialized with `C_VerifyInit`. This function may be called any number of times in succession. A call to `C_VerifyUpdate` which results in an error terminates the current verification operation.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #VerifyUpdate_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="VerifyUpdate"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #VerifyUpdate-snippet}

```Golang
VerifyUpdateRequest := &pb.VerifyUpdateRequest {
	State: VerifyInitResponse.State,
	Data:  msgHash[:],
}

VerifyUpdateResponse, err := cryptoClient.VerifyUpdate(context.Background(), VerifyUpdateRequest)
```
{: codeblock}

<br/>

### SignFinal
{: #grep11-SignFinal}

The `SignFinal` function finishes a multiple-part signature operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_SignFinal`, which is an implementation of PKCS #11 `C_SignFinal`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #SignFinal_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="SignFinal"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_SignFinal` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #SignFinal_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="SignFinal"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_SignFinal` finishes a multiple-part signature operation, returning the signature. `hSession` is the session's handle; `pSignature` points to the location that receives the signature; `pulSignatureLen` points to the location that holds the length of the signature.</p>
    <p>`C_SignFinal` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The signing operation must have been initialized with `C_SignInit`. A call to `C_SignFinal` always terminates the active signing operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call (i.e., one which returns `CKR_OK`) to determine the length of the buffer needed to hold the signature.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN, CKR_FUNCTION_REJECTED.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #SignFinal_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="SignFinal"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #SignFinal-snippet}

```Golang
SignFinalRequest := &pb.SignFinalRequest {
	State: SignUpdateResponse.State,
}

SignFinalResponse, err := cryptoClient.SignFinal(context.Background(), SignFinalRequest)
```
{: codeblock}

<br/>

### VerifyFinal
{: #grep11-VerifyFinal}

The `VerifyFinal` function finishes a multiple-part verification operation.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_VerifyFinal`, which is an implementation of PKCS #11 `C_VerifyFinal`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #VerifyFinal_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="VerifyFinal"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_VerifyFinal` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #VerifyFinal_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="VerifyFinal"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_VerifyFinal` finishes a multiple-part verification operation, checking the signature. `hSession` is the session's handle; `pSignature` points to the signature; `ulSignatureLen` is the length of the signature.</p>
    <p>The verification operation must have been initialized with `C_VerifyInit`. A call to `C_VerifyFinal` always terminates the active verification operation.</p>
    <p>A successful call to `C_VerifyFinal` should return either the value `CKR_OK` (indicating that the supplied signature is valid) or `CKR_SIGNATURE_INVALID` (indicating that the supplied signature is invalid). If the signature can be seen to be invalid purely on the basis of its length, then `CKR_SIGNATURE_LEN_RANGE` should be returned. In any of these cases, the active verifying operation is terminated.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SIGNATURE_INVALID, CKR_SIGNATURE_LEN_RANGE.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #VerifyFinal_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="VerifyFinal"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #VerifyFinal-snippet}

```Golang
VerifyFinalRequest := &pb.VerifyFinalRequest {
	State:     VerifyUpdateResponse.State,
	Signature: SignSingleResponse.Signature,
}

VerifyFinalResponse, err := cryptoClient.VerifyFinal(context.Background(), VerifyFinalRequest)
```
{: codeblock}

<br/>

### Sign
{: #grep11-Sign}

The `Sign` function signs single-part data.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_Sign`, which is an implementation of PKCS #11 `C_Sign`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #Sign_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="Sign"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Sign` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #Sign_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="Sign"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_Sign` signs data in a single part, where the signature is an appendix to the data. `hSession` is the session's handle; `pData` points to the data; `ulDataLen` is the length of the data; `pSignature` points to the location that receives the signature; `pulSignatureLen` points to the location that holds the length of the signature.</p>
    <p>`C_Sign` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The signing operation must have been initialized with `C_SignInit`. A call to `C_Sign` always terminates the active signing operation unless it returns `CKR_BUFFER_TOO_SMALL` or is a successful call (i.e., one which returns `CKR_OK`) to determine the length of the buffer needed to hold the signature.</p>
    <p>`C_Sign` cannot be used to terminate a multi-part operation, and must be called after `C_SignInit` without intervening `C_SignUpdate` calls.</p>
    <p>For most mechanisms, `C_Sign` is equivalent to a sequence of `C_SignUpdate` operations followed by `C_SignFinal`.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_INVALID, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN, CKR_FUNCTION_REJECTED.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #Sign_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="Sign"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #Sign-snippet}

```Golang
SignRequest := &pb.SignRequest {
	State: SignInitResponse.State,
	Data:  signData,
}

SignResponse, err := cryptoClient.Sign(context.Background(), SignRequest)
```
{: codeblock}

<br/>

### Verify
{: #grep11-Verify}

The `Verify` function verifies a signature on single-part data.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_Verify`, which is an implementation of PKCS #11 `C_Verify`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #Verify_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="Verify"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_Verify</code>.</p>
  <p>Does not update <code>(state, slen)</code>.</p>
  <p>Note that the relative order of data and signature are reversed relative
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Verify` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #Verify_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="Verify"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td><p>`C_Verify` verifies a signature in a single-part operation, where the signature is an appendix to the data. `hSession` is the session's handle; `pData` points to the data; `ulDataLen` is the length of the data; `pSignature` points to the signature; `ulSignatureLen` is the length of the signature.</p>
    <p>The verification operation must have been initialized with `C_VerifyInit`. A call to `C_Verify` always terminates the active verification operation.</p>
    <p>A successful call to `C_Verify` should return either the value `CKR_OK` (indicating that the supplied signature is valid) or `CKR_SIGNATURE_INVALID` (indicating that the supplied signature is invalid). If the signature can be seen to be invalid purely on the basis of its length, then `CKR_SIGNATURE_LEN_RANGE` should be returned. In any of these cases, the active signing operation is terminated.</p>
    <p>`C_Verify` cannot be used to terminate a multi-part operation, and must be called after `C_VerifyInit` without intervening `C_VerifyUpdate` calls.</p>
    <p>For most mechanisms, `C_Verify` is equivalent to a sequence of `C_VerifyUpdate` operations followed by `C_VerifyFinal`.</p></td>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DATA_INVALID, CKR_DATA_LEN_RANGE, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_OPERATION_NOT_INITIALIZED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SIGNATURE_INVALID, CKR_SIGNATURE_LEN_RANGE.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #Verify_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="Verify"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #Verify-snippet}

```Golang
VerifyRequest := &pb.VerifyRequest {
	State:     VerifyInitResponse.State,
	Data:      signData,
	Signature: SignResponse.Signature,
}

VerifyResponse, err := cryptoClient.Verify(context.Background(), VerifyRequest)
```
{: codeblock}

<br/>

### SignSingle
{: #grep11-SignSingle}

The `SignSingle` function signs or MACs data in one pass, with one call, without constructing intermediate digest state. Does not return any state to host, only result.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_SignSingle`<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #SignSingle_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="SignSingle"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Nonstandard extension, combination of <code>SignInit</code> and <code>Sign</code>. Signs or MACs data in one pass, with one call, without constructing intermediate digest state. Does not return any state to host, only result.</p>
  <p>This is the preferred way of signing, without an additional roundtrip and en/decryption. Functionally, <code>SignSingle</code> is equivalent to <code>SignInit</code> followed immediately by <code>Sign</code>.</p>
  <p>The <code>(key, klen)</code> blob and the <code>pmech</code> mechanism together must be passable to <code>SignInit</code>.</p>
  <p>Multi-data requests for HMAC and CMAC signatures are supported (sub-variants 2 and 3).</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_Decrypt` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #SignSingle_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="SignSingle"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #SignSingle-snippet}

```Golang
SignSingleRequest := &pb.SignSingleRequest {
	PrivKey: GenerateKeyPairResponse.PrivKey,
	Mech:    &pb.Mechanism{Mechanism: ep11.CKM_SHA256_RSA_PKCS},
	Data:    msgHash[:],
}

SignSingleResponse, err := cryptoClient.SignSingle(context.Background(), SignSingleRequest)
```
{: codeblock}

<br/>

### VerifySingle
{: #grep11-VerifySingle}

The `VerifySingle` function signs or MACs data in one pass, with one call, without constructing intermediate digest state.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_VerifySingle`<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #VerifySingle_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="VerifySingle"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Nonstandard extension, combination of <code>VerifyInit</code> and <code>Verify</code>. Signs or MACs data in one pass, with one call, without constructing intermediate digest state. Does not return any state to host, only verification result. There is no size query, since this function returns a Boolean.</p>
  <p>This is the preferred way of verifying a signature, without an additional roundtrip and en/decryption. Functionally, <code>VerifySingle</code> is equivalent to <code>VerifyInit</code> followed immediately by a <code>Verify</code>.</p>
  <p>The <code>(key, klen)</code> blob and the <code>pmech</code> mechanism together must be passable to <code>VerifyInit</code>.</p>
  <p>For public-key mechanisms, <code>(key, klen)</code> must contain an SPKI. This SPKI may be MACed (such as returned as a public key from <code>GenerateKeyPair</code>) or just the SPKI itself (if obtained from an external source, such as a certificate).</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_VerifySingle` return values. For details, see the <i><b>Return values</b></i> chapter of the  <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #VerifySingle_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="VerifySingle"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #VerifySingle-snippet}

```Golang
VerifySingleRequest := &pb.VerifySingleRequest {
	PubKey:    GenerateKeyPairResponse.PubKey,
	Mech:      &pb.Mechanism{Mechanism: ep11.CKM_SHA256_RSA_PKCS},
	Data:      msgHash[:],
	Signature: SignSingleResponse.Signature,
}

VerifySingleResponse, err := cryptoClient.VerifySingle(context.Background(), VerifySingleRequest)
```
{: codeblock}

<br/>

### GenerateKey
{: #grep11-GenerateKey}

The `GenerateKey` function generates a secret key.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_GenerateKey`, which is an implementation of PKCS #11 `C_GenerateKey`.<td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
message GenerateKeyRequest {
	Mechanism Mech = 1;
	map Template = 2;
	string KeyId = 4;
}
message GenerateKeyResponse {
	bytes Key = 4;
	bytes CheckSum = 5;
}
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #GenerateKey_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="GenerateKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_GenerateKey</code>.</p>
  <p>TDES keys are generated with proper parity. This is not observable by the host, but it is needed for proper interoperability: other PKCS #11 implementations <i>should</i> reject DES keys with parity problems.</p>
  <p>If tying an object to a session, <code>(pin, plen)</code> must have been returned by <code>Login</code> to that session. Leaving <code>pin</code> <code>NULL</code> creates a public object, one not bound to a login session.</p>
  <p><code>(key, klen)</code> will return the key blob. <code>(csum, clen)</code> will contain the key's checksum, i.e., the most significant bytes of an all-zero block encrypted by the key. NULL <code>clen</code> is possible, for example for symmetric-key mechanisms without <code>CKA_CHECK_VALUE</code> parameters (such as RC4).</p>
  <p><code>ptempl</code> is used only if the key length (i.e., the <code>CKA_VALUE_LEN</code> attribute) is needed by the mechanism. If the mechanism implicitly specifies key size, <code>ptempl</code> is not checked for size.</p>
  <p>DSA and DH parameter generation ignores <code>(csum, clen)</code>, generating only parameter structures.</p>
  <p>DSA,DH parameters (<code>CKM_DSA_PARAMETER_GEN</code> etc.): pass modulus bitcount in <code>CKA_PRIME_BITS</code> of attributes. Writes P,Q,G structure as cleartext output (i.e., not a blob).</p>
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
   target_t target) ;
      </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_GenerateKey` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #GenerateKey_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="GenerateKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_GenerateKey` generates a secret key or set of domain parameters, creating a new object. `hSession` is the session's handle; `pMechanism` points to the generation mechanism; `pTemplate` points to the template for the new key or set of domain parameters; `ulCount` is the number of attributes in the template; `phKey` points to the location that receives the handle of the new key or set of domain parameters.</p>
    <p>If the generation mechanism is for domain parameter generation, the `CKA_CLASS` attribute will have the value `CKO_DOMAIN_PARAMETERS`; otherwise, it will have the value `CKO_SECRET_KEY`.</p>
    <p>Since the type of key or domain parameters to be generated is implicit in the generation mechanism, the template does not need to supply a key type. If it does supply a key type which is inconsistent with the generation mechanism, `C_GenerateKey` fails and returns the error code `CKR_TEMPLATE_INCONSISTENT`. The `CKA_CLASS` attribute is treated similarly.</p>
    <p>If a call to `C_GenerateKey` cannot support the precise template supplied to it, it will fail and return without creating an object.</p>
    <p>The object created by a successful call to `C_GenerateKey` will have its `CKA_LOCAL` attribute set to `CK_TRUE`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #GenerateKey_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="GenerateKey"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #GenerateKey-snippet}

```Golang
GenerateKeyRequest := &pb.GenerateKeyRequest {
	Mech:     &pb.Mechanism{Mechanism: ep11.CKM_AES_KEY_GEN},
	Template: util.NewAttributeMap(
		util.NewAttribute(ep11.CKA_VALUE_LEN, (uint64)(keyLen/8)),
		util.NewAttribute(ep11.CKA_WRAP, false),
		util.NewAttribute(ep11.CKA_UNWRAP, false),
		util.NewAttribute(ep11.CKA_ENCRYPT, true),
		util.NewAttribute(ep11.CKA_DECRYPT, true),
		util.NewAttribute(ep11.CKA_EXTRACTABLE, false), // set to false!
		util.NewAttribute(ep11.CKA_TOKEN, true),        // ignored by EP11
	),
	KeyId: uuid.NewV4().String(), // optional
}

GenerateKeyResponse, err := cryptoClient.GenerateKey(context.Background(), GenerateKeyRequest)
```
{: codeblock}

<br/>

### GenerateKeyPair
{: #grep11-GenerateKeyPair}

The `GenerateKeyPair` function generates a public-key/private-key pair.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_GenerateKeyPair`, which is an implementation of PKCS #11 `C_GenerateKeyPair`.<td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
message GenerateKeyPairRequest {
	Mechanism Mech = 1;
	map PubKeyTemplate = 2;
	map PrivKeyTemplate = 3;
	string PrivKeyId = 5;
	string PubKeyId = 6;
}
message GenerateKeyPairResponse {
	bytes PrivKey = 5;
	bytes PubKey = 6;
}
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #GenerateKeyPair_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="GenerateKeyPair"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_GenerateKeyPair</code>.</p>
  <p>Keypair parameters are retrieved from <code>pmech</code>, <code>ppublic</code>, and <code>pprivate</code> parameters. For RSA keys, <code>ppublic</code> specifies the modulus size.</p>
  <p>In FIPS mode, only RSA moduluses of 1024+256<code>n</code> bits are supported (integer <code>n</code>). Non-FIPS mode can generate keys of any even number of bits between the limits in the mechanism parameter list.</p>
  <p>Public key is formatted as a standard SPKI (subject publickey info), readable by most libraries. It is integrity-protected by a transport-key specific MAC, which is not part of the SPKI itself. DSA parameter generation returns a non-SPKI structure in the public key field.</p>
  <p>If tying an object to a session, <code>(pin, plen)</code> must have been returned by <code>Login</code> to that session. Leaving <code>pin</code> <code>NULL</code> creates a public object, one which will survive its login session.</p>
  <p>Returns wrapped private key to <code>(key, klen)</code>, public key as a MACed ASN.1/DER structure in <code>(pubkey, pklen)</code>.</p>
  <p>Supported parameter combinations with special notes (beyond those documented by PKCS #11) are the following:</p>
  <p>RSA keys reject public exponents below 17 (0x11). Control points may further restrict the accepted minimum. The Fermat4 exponent, 0x10001, is controlled by a specific control point, matching public-exponent restrictions of FIPS 186-3 (section B.3.1).</p> <p>EC keys (<code>CKM_EC_KEY_PAIR_GEN</code>): curve parameters may be specified as OIDs or symbolic names (our namedCurve variant). Supported symbolic names are "<code>P-nnn</code>" for FP NIST curves (<code>nnn</code> is a supported prime bitcount, 192 to 521), "<code>BP-nnnR</code>" for regular BP curves, and "<code>BP-nnnT</code>" for twisted BP curves of bitcount nnn (160 to 512). (Names must be supplied as ASCII strings, without zero-termination.)</p>
  <p>DSA keys (<code>CKM_DSA_KEY_PAIR_GEN</code>): pass P,Q,G structure as the <code>CKA_IBM_STRUCT_PARAMS</code> attribute of public attributes. Note that individual P,Q,G parameters may not be passed through regular PKCS #11 parameters, they must be combined to a single structure.</p>
  <p>DH keys (<code>CKM_DH_PKCS_KEY_PAIR_GEN</code>): pass P,G structure as the <code>CKA_IBM_STRUCT_PARAMS</code> attribute of public attributes. Note that individual P,G parameters may not be passed through regular PKCS #11 parameters, they must be combined to a single structure. When selecting a private-key (X) bitcount, use the <code>XCP_U32_VALUE_BITS</code> attribute. If not present, or an explicit 0 is supplied, bitcount is selected based on P bitcount.</p>
  <p>Use of session (Login) state replaces standard use of sessions, the mapping is outside library scope.</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_GenerateKeyPair` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #GenerateKeyPair_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="GenerateKeyPair"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_GenerateKeyPair` generates a public/private key pair, creating new key objects. `hSession` is the session's handle; `pMechanism` points to the key generation mechanism; `pPublicKeyTemplate` points to the template for the public key; `ulPublicKeyAttributeCount` is the number of attributes in the public-key template; `pPrivateKeyTemplate` points to the template for the private key; `ulPrivateKeyAttributeCount` is the number of attributes in the private-key template; `phPublicKey` points to the location that receives the handle of the new public key; `phPrivateKey` points to the location that receives the handle of the new private key.</p>
    <p>Since the types of keys to be generated are implicit in the key pair generation mechanism, the templates do not need to supply key types. If one of the templates does supply a key type which is inconsistent with the key generation mechanism, `C_GenerateKeyPair` fails and returns the error code `CKR_TEMPLATE_INCONSISTENT`. The `CKA_CLASS` attribute is treated similarly.</p>
    <p>If a call to `C_GenerateKeyPair` cannot support the precise templates supplied to it, it will fail and return without creating any key objects.</p>
    <p>A call to `C_GenerateKeyPair` will never create just one key and return. A call can fail, and create no keys; or it can succeed, and create a matching public/private key pair.</p>
    <p>The key objects created by a successful call to `C_GenerateKeyPair` will have their `CKA_LOCAL` attributes set to `CK_TRUE`.</p>
    <p>Note carefully the order of the arguments to `C_GenerateKeyPair`. The last two arguments do not have the same order as they did in the original Cryptoki Version 1.0 document. The order of these two arguments has caused some unfortunate confusion.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_DOMAIN_PARAMS_INVALID, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #GenerateKeyPair_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="GenerateKeyPair"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #GenerateKeyPair-snippet}

```Golang
GenerateKeyPairRequest := &pb.GenerateKeyPairRequest {
	Mech:               &pb.Mechanism{Mechanism: ep11.CKM_RSA_PKCS_KEY_PAIR_GEN},
	PubKeyTemplate: util.NewAttributeMap(
		util.NewAttribute(ep11.CKA_ENCRYPT, true),
		util.NewAttribute(ep11.CKA_VERIFY, true), // to verify a signature
		util.NewAttribute(ep11.CKA_MODULUS_BITS, uint64(2048)),
		util.NewAttribute(ep11.CKA_PUBLIC_EXPONENT, publicExponent),
		util.NewAttribute(ep11.CKA_EXTRACTABLE, false),
	),
	PrivateKeyTemplate: util.NewAttributeMap(
		util.NewAttribute(ep11.CKA_PRIVATE, true),
		util.NewAttribute(ep11.CKA_SENSITIVE, true),
		util.NewAttribute(ep11.CKA_DECRYPT, true),
		util.NewAttribute(ep11.CKA_SIGN, true), // to generate a signature
		util.NewAttribute(ep11.CKA_EXTRACTABLE, false),
	),
	PrivKeyId:       uuid.NewV4().String(),
	PubKeyId:        uuid.NewV4().String(),
}

GenerateKeyPairResponse, err := cryptoClient.GenerateKeyPair(context.Background(), GenerateKeyPairRequest)
```
{: codeblock}

<br/>

### WrapKey
{: #grep11-WrapKey}

The `WrapKey` function wraps (encrypts) a key.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_WrapKey`, which is an implementation of PKCS #11 `C_WrapKey`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #WrapKey_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="WrapKey"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_WrapKey` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #WrapKey_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="WrapKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_WrapKey` wraps (i.e., encrypts) a private or secret key. `hSession` is the session's handle; `pMechanism` points to the wrapping mechanism; `hWrappingKey` is the handle of the wrapping key; `hKey` is the handle of the key to be wrapped; `pWrappedKey` points to the location that receives the wrapped key; and `pulWrappedKeyLen` points to the location that receives the length of the wrapped key.</p>
    <p>`C_WrapKey` uses the convention described in Section 5.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959738" target="_blank">PKCS #11 API specification</a> on producing output.</p>
    <p>The `CKA_WRAP` attribute of the wrapping key, which indicates whether the key supports wrapping, must be `CK_TRUE`. The `CKA_EXTRACTABLE` attribute of the key to be wrapped must also be `CK_TRUE`.</p>
    <p>If the key to be wrapped cannot be wrapped for some token-specific reason, despite its having its `CKA_EXTRACTABLE` attribute set to `CK_TRUE`, then `C_WrapKey` fails with error code `CKR_KEY_NOT_WRAPPABLE`. If it cannot be wrapped with the specified wrapping key and mechanism solely because of its length, then `C_WrapKey` fails with error code `CKR_KEY_SIZE_RANGE`.</p>
    <p>
    `C_WrapKey` can be used in the following situations:
    <ul>
    <li>To wrap any secret key with a public key that supports encryption and decryption.</li>
    <li>To wrap any secret key with any other secret key. Consideration must be given to key size and mechanism strength or the token may not allow the operation.</li>
    <li>To wrap a private key with any secret key.</li>
    </ul>
    </p>
    <p>Of course, tokens vary in which types of keys can actually be wrapped with which mechanisms.</p>
    <p>To partition the wrapping keys so they can only wrap a subset of extractable keys the attribute `CKA_WRAP_TEMPLATE` can be used on the wrapping key to specify an attribute set that will be compared against the attributes of the key to be wrapped. If all attributes match according to the `C_FindObject` rules of attribute matching then the wrap will proceed. The value of this attribute is an attribute template and the size is the number of items in the template times the size of `CK_ATTRIBUTE`. If this attribute is not supplied then any template is acceptable. If an attribute is not present, it will not be checked. If any attribute mismatch occurs on an attempt to wrap a key then the function SHALL return `CKR_KEY_HANDLE_INVALID`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_HANDLE_INVALID, CKR_KEY_NOT_WRAPPABLE, CKR_KEY_SIZE_RANGE, CKR_KEY_UNEXTRACTABLE, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_USER_NOT_LOGGED_IN, CKR_WRAPPING_KEY_HANDLE_INVALID, CKR_WRAPPING_KEY_SIZE_RANGE, CKR_WRAPPING_KEY_TYPE_INCONSISTENT.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #WrapKey_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="WrapKey"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #WrapKey-snippet}

```Golang
WrapKeyRequest := &pb.WrapKeyRequest {
	Mech: &pb.Mechanism{Mechanism: ep11.CKM_RSA_PKCS},
	KeK:  GenerateKeyPairResponse.PubKey,
	Key:  GenerateKeyResponse.Key,
}

WrapKeyResponse, err := cryptoClient.WrapKey(context.Background(), WrapKeyRequest)
```
{: codeblock}

<br/>

### UnwrapKey
{: #grep11-UnwrapKey}

The `UnwrapKey` function unwraps (decrypts) a key.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_UnwrapKey`, which is an implementation of PKCS #11 `C_UnwrapKey`.<td>
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
	map Template = 6;
	string UnwrappedId = 7;
}
message UnwrapKeyResponse {
	bytes Unwrapped = 7;
	bytes CheckSum = 8;
}
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #UnwrapKey_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="UnwrapKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_UnwrapKey</code>.</p>
  <p><code>uwmech</code> specifies the encryption mechanism used to decrypt wrapped data. <code>ptempl</code> is a <i>key(pair)</i> parameter list, specifying how to transform the unwrapped data to a new key (must include <code>CKA_KEY_TYPE</code>; for others see <code>GenerateKey</code> and <code>GenerateKeyPair</code>).</p>
  <p>The generated object is returned under <code>(unwrapped, uwlen)</code> as a blob. Symmetric keys return their key checksum (3 bytes) under <code>(csum, cslen)</code>; public-key objects return their public key as an SPKI in <code>(csum, cslen)</code>. Both forms are followed by a 4-byte big-endian value, encoding bitcount of the unwrapped key.</p>
  <p>When transforming an SPKI to a MACed SPKI, one must use CKM_IBM_TRANSPORTKEY as the unwrapping mechanism. This mode supplies the raw SPKI as wrapped data, and ignores the KEK.</p>
  <p>Note that <code>UnwrapKey</code> produces parity-adjusted DES keys (within the blobs), but tolerates input with improper parity.</p>
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
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_UnwrapKey` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #UnwrapKey_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="UnwrapKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_UnwrapKey` unwraps (i.e. decrypts) a wrapped key, creating a new private key or secret key object. `hSession` is the session's handle; `pMechanism` points to the unwrapping mechanism; `hUnwrappingKey` is the handle of the unwrapping key; `pWrappedKey` points to the wrapped key; `ulWrappedKeyLen` is the length of the wrapped key; `pTemplate` points to the template for the new key; `ulAttributeCount` is the number of attributes in the template; `phKey` points to the location that receives the handle of the recovered key.</p>
    <p>The `CKA_UNWRAP` attribute of the unwrapping key, which indicates whether the key supports unwrapping, must be `CK_TRUE`.</p>
    <p>The new key will have the `CKA_ALWAYS_SENSITIVE` attribute set to `CK_FALSE`, and the `CKA_NEVER_EXTRACTABLE` attribute set to `CK_FALSE`. The `CKA_EXTRACTABLE` attribute is by default set to `CK_TRUE`.</p>
    <p>Some mechanisms may modify, or attempt to modify. the contents of the `pMechanism` structure at the same time that the key is unwrapped.</p>
    <p>If a call to `C_UnwrapKey` cannot support the precise template supplied to it, it will fail and return without creating any key object.</p>
    <p>The key object created by a successful call to `C_UnwrapKey` will have its `CKA_LOCAL` attribute set to `CK_FALSE`.</p>
    <p>To partition the unwrapping keys so they can only unwrap a subset of keys the attribute `CKA_UNWRAP_TEMPLATE` can be used on the unwrapping key to specify an attribute set that will be added to attributes of the key to be unwrapped. If the attributes do not conflict with the user supplied attribute template, in â€˜pTemplateâ€™, then the unwrap will proceed. The value of this attribute is an attribute template and the size is the number of items in the template times the size of `CK_ATTRIBUTE`. If this attribute is not present on the unwrapping key then no additional attributes will be added. If any attribute conflict occurs on an attempt to unwrap a key then the function SHALL return `CKR_TEMPLATE_INCONSISTENT`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_DOMAIN_PARAMS_INVALID, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_UNWRAPPING_KEY_HANDLE_INVALID, CKR_UNWRAPPING_KEY_SIZE_RANGE, CKR_UNWRAPPING_KEY_TYPE_INCONSISTENT, CKR_USER_NOT_LOGGED_IN, CKR_WRAPPED_KEY_INVALID, CKR_WRAPPED_KEY_LEN_RANGE.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #UnwrapKey_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="UnwrapKey"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #UnwrapKey-snippet}

```Golang
UnwrapKeyRequest := &pb.UnwrapKeyRequest {
	Mech:     &pb.Mechanism{Mechanism: ep11.CKM_RSA_PKCS},
	KeK:      GenerateKeyPairResponse.PrivKey,
	Wrapped:  WrapKeyResponse.Wrapped,
	Template: util.NewAttributeMap(
		util.NewAttribute(ep11.CKA_CLASS, ep11.CKO_SECRET_KEY),
		util.NewAttribute(ep11.CKA_KEY_TYPE, ep11.CKK_AES),
		util.NewAttribute(ep11.CKA_VALUE_LEN, (uint64)(128/8)),
		util.NewAttribute(ep11.CKA_ENCRYPT, true),
		util.NewAttribute(ep11.CKA_DECRYPT, true),
		util.NewAttribute(ep11.CKA_EXTRACTABLE, true), // must be true to be wrapped
	),
}

UnwrapKeyResponse, err := cryptoClient.UnwrapKey(context.Background(), UnwrapKeyRequest)
```
{: codeblock}

<br/>

### DeriveKey
{: #grep11-DeriveKey}

The `DeriveKey` function derives a key from a base key.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_DeriveKey`, which is an implementation of PKCS #11 `C_DeriveKey`.<td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
message DeriveKeyRequest {
	Mechanism Mech = 1;
	map Template = 2;
	bytes BaseKey = 3;
	bytes Data = 4;
	string NewKeyId = 6;
}
message DeriveKeyResponse {
	bytes NewKey = 6;
	bytes CheckSum = 7;
}
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #DeriveKey_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="DeriveKey"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
      </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_DeriveKey` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #DeriveKey_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="DeriveKey"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_DeriveKey` derives a key from a base key, creating a new key object. `hSession` is the session's handle; `pMechanism` points to a structure that specifies the key derivation mechanism; `hBaseKey` is the handle of the base key; `pTemplate` points to the template for the new key; `ulAttributeCount` is the number of attributes in the template; and `phKey` points to the location that receives the handle of the derived key.</p>
    <p>The values of the `CKA_SENSITIVE`, `CKA_ALWAYS_SENSITIVE`, `CKA_EXTRACTABLE`, and `CKA_NEVER_EXTRACTABLE` attributes for the base key affect the values that these attributes can hold for the newly-derived key. See the description of each particular key-derivation mechanism in Section 5.16.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749" target="_blank">PKCS #11 API specification</a> for any constraints of this type.</p>
    <p>If a call to `C_DeriveKey` cannot support the precise template supplied to it, it will fail and return without creating any key object.</p>
    <p>The key object created by a successful call to `C_DeriveKey` will have its `CKA_LOCAL` attribute set to `CK_FALSE`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_CURVE_NOT_SUPPORTED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_DOMAIN_PARAMS_INVALID, CKR_FUNCTION_CANCELED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_KEY_HANDLE_INVALID, CKR_KEY_SIZE_RANGE, CKR_KEY_TYPE_INCONSISTENT, CKR_MECHANISM_INVALID, CKR_MECHANISM_PARAM_INVALID, CKR_OK, CKR_OPERATION_ACTIVE, CKR_PIN_EXPIRED, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCOMPLETE, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #DeriveKey_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="DeriveKey"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #DeriveKey-snippet}

```Golang
DeriveKeyRequest := &pb.DeriveKeyRequest {
	Mech:     &pb.Mechanism{Mechanism: ep11.CKM_ECDH1_DERIVE, Parameter: combinedCoordinates},
	Template: util.NewAttributeMap(
		util.NewAttribute(ep11.CKA_CLASS, uint64(ep11.CKO_SECRET_KEY)),
		util.NewAttribute(ep11.CKA_KEY_TYPE, uint64(ep11.CKK_AES)),
		util.NewAttribute(ep11.CKA_VALUE_LEN, (uint64)(128/8)),
		util.NewAttribute(ep11.CKA_ENCRYPT, true),
		util.NewAttribute(ep11.CKA_DECRYPT, true),
	),
	BaseKey:  GenerateKeypairResponse.PrivKey, // EC generated key
}

DeriveKeyResponse, err := cryptoClient.DeriveKey(context.Background(), DeriveKeyRequest)
```
{: codeblock}

<br/>

### GetMechanismList
{: #grep11-GetMechanismList}

The `GetMechanismList` function obtains a list of mechanisms supported by a token.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_GetMechanismList`, which is an implementation of PKCS #11 `C_GetMechanismList`.<td>
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
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #GetMechanismList_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="GetMechanismList"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
      </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_GetMechanismList` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #GetMechanismList_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="GetMechanismList"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_GetMechanismList` is used to obtain a list of mechanism types supported by a token. SlotID is the ID of the token's slot; `pulCount` points to the location that receives the number of mechanisms.</p>
    <p>
    There are two ways for an application to call `C_GetMechanismList`:
    <ol>
    <li>If `pMechanismList` is `NULL_PTR`, then all that `C_GetMechanismList` does is return (in `*pulCount`) the number of mechanisms, without actually returning a list of mechanisms. The contents of `*pulCount` on entry to `C_GetMechanismList` has no meaning in this case, and the call returns the value `CKR_OK`.</li>
    <li>If `pMechanismList` is not `NULL_PTR`, then `*pulCount` must contain the size (in terms of `CK_MECHANISM_TYPE` elements) of the buffer pointed to by pMechanismList. If that buffer is large enough to hold the list of mechanisms, then the list is returned in it, and `CKR_OK` is returned. If not, then the call to `C_GetMechanismList` returns the value `CKR_BUFFER_TOO_SMALL`. In either case, the value `*pulCount` is set to hold the number of mechanisms.</li>
    </ol>
    </p>
    <p>Because `C_GetMechanismList` does not allocate any space of its own, an application will often call `C_GetMechanismList` twice. However, this behavior is by no means required.</p>
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
    <code>
    CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OK, CKR_SLOT_ID_INVALID, CKR_TOKEN_NOT_PRESENT, CKR_TOKEN_NOT_RECOGNIZED, CKR_ARGUMENTS_BAD.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #GetMechanismList_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="GetMechanismList"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #GetMechanismList-snippet}

```Golang
GetMechanismListRequest := &pb.GetMechanismListRequest {
}

GetMechanismListResponse, err := cryptoClient.GetMechanismList(context.Background(), GetMechanismListRequest)
```
{: codeblock}

<br/>

### GetMechanismInfo
{: #grep11-GetMechanismInfo}

The `GetMechanismInfo` Function obtains information about a particular mechanism.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_GetMechanismInfo`, which is an implementation of PKCS #11 `C_GetMechanismInfo`.<td>
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
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #GetMechanismInfo_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="GetMechanismInfo"}
{: class="simple-tab-table"}

<table>
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
   target_t target) ;
      </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_GetMechanismInfo` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #GetMechanismInfo_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="GetMechanismInfo"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_GetMechanismInfo` obtains information about a particular mechanism possibly supported by a token. `slotID` is the ID of the token's slot; `type` is the type of mechanism; `pInfo` points to the location that receives the mechanism information.</p>
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
    <code>
    CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_MECHANISM_INVALID, CKR_OK, CKR_SLOT_ID_INVALID, CKR_TOKEN_NOT_PRESENT, CKR_TOKEN_NOT_RECOGNIZED, CKR_ARGUMENTS_BAD.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #GetMechanismInfo_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="GetMechanismInfo"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #GetMechanismInfo-snippet}

```Golang
GetMechanismInfoRequest := &pb.GetMechanismInfoRequest {
	Mech: ep11.CKM_RSA_PKCS,
}

GetMechanismInfoResponse, err := cryptoClient.GetMechanismInfo(context.Background(), GetMechanismInfoRequest)
```
{: codeblock}

<br/>

### GetAttributeValue
{: #grep11-GetAttributeValue}

The `GetAttributeValue` function obtains an attribute value of an object.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_GetAttributeValue`, which is an implementation of PKCS #11 `C_GetAttributeValue`.<td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
message GetAttributeValueRequest {
	bytes Object = 1;
	map Attributes = 2;
}
message GetAttributeValueResponse {
	map Attributes = 2;
}
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #GetAttributeValue_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="GetAttributeValue"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td><p>Implementation of PKCS #11 <code>C_GetAttributeValue</code>.</p>
  <p>Does not represent/need sessions (part of blob), therefore does not
  use the <code>hSession</code> parameter.</p>
  <p>Since currently, we can do shortcuts (such as enumerate actual values
  instead of being more generic), decoding is straightforward.</p>
  </td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
CK_RV m_GetAttributeValue (
   const unsigned char *object, size_t objectlen,
   CK_ATTRIBUTE_PTR attributes, CK_ULONG attributeslen,
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_GetAttributeValue` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #GetAttributeValue_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="GetAttributeValue"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_GetAttributeValue` obtains the value of one or more attributes of an object. `hSession` is the session's handle; `hObject` is the object's handle; `pTemplate` points to a template that specifies which attribute values are to be obtained, and receives the attribute values; `ulCount` is the number of attributes in the template.</p>
    <p>
    For each (`type`, `pValue`, `ulValueLen`) triple in the template, `C_GetAttributeValue` performs the following algorithm:
    <ol>
    <li>If the specified attribute (i.e., the attribute specified by the type field) for the object cannot be revealed because the object is sensitive or unextractable, then the `ulValueLen` field in that triple is modified to hold the value `CK_UNAVAILABLE_INFORMATION`.</li>
    <li>Otherwise, if the specified value for the object is invalid (the object does not possess such an attribute), then the `ulValueLen` field in that triple is modified to hold the value `CK_UNAVAILABLE_INFORMATION`.</li>
    <li>Otherwise, if the `pValue` field has the value `NULL_PTR`, then the `ulValueLen` field is modified to hold the exact length of the specified attribute for the object.</li>
    <li>Otherwise, if the length specified in `ulValueLen` is large enough to hold the value of the specified attribute for the object, then that attribute is copied into the buffer located at `pValue`, and the `ulValueLen` field is modified to hold the exact length of the attribute.</li>
    <li>Otherwise, the `ulValueLen` field is modified to hold the value `CK_UNAVAILABLE_INFORMATION`.</li>
    </ol>
    </p>
    <p>If case 1 applies to any of the requested attributes, then the call should return the value `CKR_ATTRIBUTE_SENSITIVE`. If case 2 applies to any of the requested attributes, then the call should return the value `CKR_ATTRIBUTE_TYPE_INVALID`. If case 5 applies to any of the requested attributes, then the call should return the value `CKR_BUFFER_TOO_SMALL`. As usual, if more than one of these error codes is applicable, `Cryptoki` may return any of them. Only if none of them applies to any of the requested attributes will `CKR_OK` be returned.</p>
    <p>In the special case of an attribute whose value is an array of attributes, for example` CKA_WRAP_TEMPLATE`, where it is passed in with `pValue` not NULL, then if the `pValue` of elements within the array is NULL_PTR then the `ulValueLen` of elements within the array will be set to the required length. If the `pValue` of elements within the array is not NULL_PTR, then the `ulValueLen` element of attributes within the array must reflect the space that the corresponding `pValue` points to, and `pValue` is filled in if there is sufficient room. Therefore it is important to initialize the contents of a buffer before calling `C_GetAttributeValue` to get such an array value. If any `ulValueLen` within the array isn't large enough, it will be set to `CK_UNAVAILABLE_INFORMATION` and the function will return `CKR_BUFFER_TOO_SMALL`, as it does if an attribute in the `pTemplate` argument has `ulValueLen` too small. Note that any attribute whose value is an array of attributes is identifiable by virtue of the attribute type having the `CKF_ARRAY_ATTRIBUTE` bit set.</p>
    <p>Note that the error codes `CKR_ATTRIBUTE_SENSITIVE`, `CKR_ATTRIBUTE_TYPE_INVALID`, and `CKR_BUFFER_TOO_SMALL` do not denote true errors for `C_GetAttributeValue`. If a call to `C_GetAttributeValue` returns any of these three values, then the call must nonetheless have processed every attribute in the template supplied to `C_GetAttributeValue`. Each attribute in the template whose value can be returned by the call to `C_GetAttributeValue` will be returned by the call to `C_GetAttributeValue`.</p>
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
    <code>
    CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_SENSITIVE, CKR_ATTRIBUTE_TYPE_INVALID, CKR_BUFFER_TOO_SMALL, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OBJECT_HANDLE_INVALID, CKR_OK, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #GetAttributeValue_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="GetAttributeValue"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #GetAttributeValue-snippet}

```Golang
GetAttributeValueRequest := &pb.GetAttributeValueRequest {
	Object:     GenerateKeyPairResponse.PrivKey,
	Attributes: util.NewAttributeMap(util.NewAttribute(ep11.CKA_SIGN, uint8(0)),
}

GetAttributeValueResponse, err := cryptoClient.GetAttributeValue(context.Background(), GetAttributeValueRequest)
```
{: codeblock}

<br/>

### SetAttributeValue
{: #grep11-SetAttributeValue}

The `SetAttributeValue` function modifies an attribute value of an object.

<table>
  <tr>
    <th>Description</th>
    <td>Binds to EP11 `m_SetAttributeValue`, which is an implementation of PKCS #11 `C_SetAttributeValue`.<td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
message SetAttributeValueRequest {
	bytes Object = 1;
	map Attributes = 2;
}
message SetAttributeValueResponse {
	bytes Object = 1;
}
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>Wraps EP11 error into <code>message Grep11Error</code>.</td>
  </tr>
</table>
{: caption="Table 1. GREP11" caption-side="top"}
{: #SetAttributeValue_GREP11}
{: tab-title="Enterprise PKCS #11 over gRPC"}
{: tab-group="SetAttributeValue"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
	<td>
  <p>Implementation of PKCS #11 <code>C_SetAttributeValue</code>.</p>
  <p>attribute packing: see _GetAttrValue</p>
  <p>Currently, we only send Boolean attributes, all other attributes are handled by host (and we don't let modify arrays, such as WRAP_TEMPLATE).</p>
  <p>Does not represent/need sessions (part of blob), therefore does not use the PKCS #11 <code>hSession</code> parameter.</p>
  </td>
  </tr>
  <tr>
    <th>Parameters</th>
    <td>
    <pre>
CK_RV m_SetAttributeValue (
   unsigned char *object, size_t objectlen,
   CK_ATTRIBUTE_PTR attributes, CK_ULONG attributeslen,
   target_t target) ;
    </pre>
    </td>
  </tr>
  <tr>
    <th>Return values</th>
    <td>A subset of `C_SetAttributeValue` return values. For details, see the <i><b>Return values</b></i> chapter of the <a href="https://www.ibm.com/downloads/cas/WXRDPRAN" target="_blank">Enterprise PKCS #11 (EP11) Library structure document</a>.</td>
  </tr>
</table>
{: caption="Table 2. EP11" caption-side="top"}
{: #SetAttributeValue_EP11}
{: tab-title="Enterprise PKCS #11"}
{: tab-group="SetAttributeValue"}
{: class="simple-tab-table"}

<table>
  <tr>
    <th>Description</th>
    <td>
    <p>`C_SetAttributeValue` modifies the value of one or more attributes of an object. `hSession` is the session's handle; `hObject` is the object's handle; `pTemplate` points to a template that specifies which attribute values are to be modified and their new values; `ulCount` is the number of attributes in the template.</p>
    <p>Certain objects may not be modified. Calling `C_SetAttributeValue` on such objects will result in the `CKR_ACTION_PROHIBITED` error code. An application can consult the object's `CKA_MODIFIABLE` attribute to determine if an object may be modified or not.</p>
    <p>Only session objects can be modified during a read-only session.</p>
    <p>The template may specify new values for any attributes of the object that can be modified. If the template specifies a value of an attribute which is incompatible with other existing attributes of the object, the call fails with the return code `CKR_TEMPLATE_INCONSISTENT`.</p>
    <p>Not all attributes can be modified; see Section 4.1.2 of the <a href="http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html#_Toc416959749" target="_blank">PKCS #11 API specification</a> for more details.</p>
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
    <code>
    CKR_ACTION_PROHIBITED, CKR_ARGUMENTS_BAD, CKR_ATTRIBUTE_READ_ONLY, CKR_ATTRIBUTE_TYPE_INVALID, CKR_ATTRIBUTE_VALUE_INVALID, CKR_CRYPTOKI_NOT_INITIALIZED, CKR_DEVICE_ERROR, CKR_DEVICE_MEMORY, CKR_DEVICE_REMOVED, CKR_FUNCTION_FAILED, CKR_GENERAL_ERROR, CKR_HOST_MEMORY, CKR_OBJECT_HANDLE_INVALID, CKR_OK, CKR_SESSION_CLOSED, CKR_SESSION_HANDLE_INVALID, CKR_SESSION_READ_ONLY, CKR_TEMPLATE_INCONSISTENT, CKR_TOKEN_WRITE_PROTECTED, CKR_USER_NOT_LOGGED_IN.
    </code>
    </td>
  </tr>
</table>
{: caption="Table 3. PKCS #11" caption-side="top"}
{: #SetAttributeValue_PKCS11}
{: tab-title="PKCS #11"}
{: tab-group="SetAttributeValue"}
{: class="simple-tab-table"}

#### Golang code snippet
{: #SetAttributeValue-snippet}

```Golang
SetAttributeValueRequest := &pb.SetAttributeValueRequest {
	Object:     GenerateKeyPairResponse.PrivKey,
	Attributes: util.NewAttributeMap(util.NewAttribute(ep11.CKA_SIGN, true),
}

SetAttributeValueResponse, err := cryptoClient.SetAttributeValue(context.Background(), SetAttributeValueRequest)
```
{: codeblock}

## Code examples
{: #code-example}

For complete Golang examples on Enterprise PKCS #11 (EP11) over gRPC, see [GREP11 examples](https://github.com/vpaprots/ibm-cloud-hyperprotectcrypto/tree/master/golang){: external}.

GREP11 API supports programming languages with [gRPC libraries](https://www.grpc.io/docs/){:external}. In the [sample](https://github.com/vpaprots/ibm-cloud-hyperprotectcrypto){:external} Github repository, only Golang code examples are provided.
