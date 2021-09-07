---

copyright:
  years: 2021
lastupdated: "2021-09-06"

keywords: error message, error code, error, kms error, key management error message, hpcs error messages, hyper protect crypto services error message

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:note: .note}
{:screen: .screen}

# Error messages for key management
{: #error-messages-kms}

This topic lists error messages that you might encounter when you manage root keys and standard keys with {{site.data.keyword.hscrypto}}. Most error messages have one or more examples, usually `curl`, that shows the request and response.
{: shortdesc}

This is not a complete list of error messages. Some messages that are created by other systems, such as {{site.data.keyword.iamshort}} (IAM), and are then passed to {{site.data.keyword.hscrypto}} are not covered.
{: note}

## Table of contents
{: #error-messages-kms-toc}

The error messages are sorted by alphabetical order, by HTTP status code, and by reason code.

### Sorted by alphabetical order of error messages
{: #error-messages-kms-sorted-by-alphabetical-order}

These error messages that are sorted by the alphabetical order. Some error messages are the same but with different HTTP status code. In those cases, the HTTP status code is included at the end of the error message.

1. Collection total does not match number...
    [details](#error-messages-collection-total-mismatch-err)
2. Data in body does not match data required...
    [details](#error-messages-body-query-param-mismatch-err)
3. Extracting the subject from the bearer...
    [details](#error-messages-bearer-sub-extraction-err)
4. Invalid body data was passed...
    [details](#error-messages-bad-body-err)
5. Key has already been deleted...
    [details](#error-messages-key-deleted-err)
6. Key is not in a valid state (409)
    [details](#error-messages-key-action-invalid-state-err)
7. Key is not in a valid state (422)
    [details](#error-messages-key-invalid-state-err)
8. Key is protecting one or more cloud...
    [details](#error-messages-protected-resource-err)
9. Key metadata became corrupted...
   [details](#error-messages-incomplete-metadata-err)
10. Key restoration has expired
    [details](#error-messages-key-restore-expired)
11. KeyCreateImportAccess instance policy...
    [details](#error-messages-key-create-import-access-err)
12. Missing body in request
    [details](#error-messages-no-body-err)
13. Number of authorizations required to...
    [details](#error-messages-authorizations-not-met)
14. Only a single instance policy can be...
    [details](#error-messages-num-collection-resource-err)
15. Only imported keys can be restored
    [details](#error-messages-key-impt-req-err)
16. Requested action can be completed only with a root key (400)
    [details](#error-messages-key-root-req-err)
17. Requested action can be completed only with a root key (422)
    [details](#error-messages-key-root-req-reg-err)
18. Requested change is not compliant with configuration rules
    [details](#error-config_rule_conflict_err)
19. Signature is invalid
    [details](#error-invalid_sig_exp_err)
20. The action could not be performed on...
    [details](#error-messages-key-expired-err)
21. The encrypted nonce given does not match...
    [details](#error-messages-incorrect-nonce-err)
22. The import token is expired
    [details](#error-messages-import-token-expired-err)
23. The key cannot be deleted because it's...
    [details](#error-messages-prev-key-del-err)
24. The key is not dual auth enabled and...
    [details](#error-messages-not-dual-auth-err)
25. The key was updated recently
    [details](#error-messages-req-too-early-err)
26. The provided ciphertext is invalid or...
    [details](#error-messages-unprocessable-ciphertext-err)
27. The provided encrypted nonce was not...
    [details](#error-messages-incorrect-nonce-iv-err)
28. The resource(s) queried does not belong to the service.
    [details](#error-messages-resource-owner-err)
29. This action can be done only by a service...
    [details](#error-messages-service-only-err)
30. This action is not permitted on this...
    [details](#error-messages-feature-restricted-err)
31. This request requires that the key version...
    [details](#error-messages-key-version-invalid)
32. This root key has been rotated within...
    [details](#error-messages-key-rotation-not-permitted)
33. This root key was created with user-supplied...
    [details](#error-messages-key-payload-req-err)
34. Unauthorized: The user does not have...
    [details](#error-messages-unauthorized-err)

### Sorted by HTTP status code
{: #error-messages-kms-sorted-by-http-status-code}

These are the error messages that are sorted by the HTTP status code.

<table>
    <tr>
    <th>Status code</th>
    <th>Error message</th>
    </tr>
    <tr>
    <td>HTTP 400 - Bad Request</td>
    <td>
      <ul>
        <li>Collection total does not match number of resources - <a href="#error-messages-collection-total-mismatch-err">details</a></li>
        <li>Data in body does not match data required by query parameter - <a href="#error-messages-body-query-param-mismatch-err">details</a></li>
        <li>Extracting the subject from the bearer token failed: Make sure the bearer token passed is the correct one (and correct format) and is allowed to perform requested actions - <a href="#error-messages-bearer-sub-extraction-err">details</a></li>
        <li>Invalid body data was passed: Ensure that the data passed had valid formatting with no invalid characters - <a href="#error-messages-bad-body-err">details</a></li>
        <li>Key restoration has expired - <a href="#error-messages-key-restore-expired">details</a></li>
        <li>Missing body in request - <a href="#error-messages-no-body-err">details</a></li>
        <li>Only a single instance policy can be created per query parameter: Please pass single resource object - <a href="#error-messages-num-collection-resource-err">details</a></li>
        <li>Only imported keys can be restored - <a href="#error-messages-key-impt-req-err">details</a></li>
        <li>Requested action can only be completed with a root key - <a href="#error-messages-key-root-req-err">details</a></li>
        <li>The action could not be performed on the key because the key is expired - <a href="#error-messages-key-expired-err">details</a></li>
        <li>The encrypted nonce given does not match existing record: Please ensure the correct nonce was given in the request - <a href="#error-messages-incorrect-nonce-err">details</a></li>
        <li>The provided encrypted nonce was not encrypted with the key material given OR the provided IV does not match the encrypted nonce - <a href="#error-messages-incorrect-nonce-iv-err">details</a></li>
        <li>This root key was created with user-supplied key material: Key material is required to perform a 'rotate' action -<a href="#error-messages-key-payload-req-err">details</a></li>
      </ul>
    </td>
    </tr>
    <tr>
    <td>HTTP 401 - Unauthorized</td>
    <td>Unauthorized: The user does not have access to the specified resource - <a href="#error-messages-unauthorized-err">details</a></td>
    </tr>
    <tr>
    <td>HTTP 403 - Forbidden</td>
    <td>
      <ul>
        <li>Requested change is not compliant with configuration rules - <a href="#error-config_rule_conflict_err">details</a></li>
        <li>The resource(s) queried does not belong to the service - <a href="#error-messages-resource-owner-err">details</a></li>
        <li>This action can only be done by a service (service to service) - <a href="#error-messages-service-only-err">details</a></li>
        <li>This action is not permitted on this resource: Please contact IBM Hyper Protect Crypto Services or open a service ticket to enable this feature - <a href="#error-messages-feature-restricted-err">details</a></li>
      </ul>
    </td>
    </tr>
    <tr>
    <td>HTTP 409 - Conflict</td>
    <td>
      <ul>
        <li>Key is not in a valid state - <a href="#error-messages-key-action-invalid-state-err">details</a></li>
        <li>Key is protecting one or more cloud resources -<a href="#error-messages-protected-resource-err">details</a></li>
        <li>KeyCreateImportAccess instance policy does not allow this action - <a href="#error-messages-key-create-import-access-err">details</a></li>
        <li>Number of authorizations required to delete is not met - <a href="#error-messages-authorizations-not-met">details</a></li>
        <li>The import token has expired - <a href="#error-messages-import-token-expired-err">details</a></li>
        <li>The key cannot be deleted because it's protecting a cloud resource that has a retention policy: Before you delete this key, contact an account owner to remove the retention policy on each resource that is associated with the key - <a href="#error-messages-prev-key-del-err">details</a></li>
        <li>The key is not dual auth enabled and cannot be set for deletion - <a href="#error-messages-not-dual-auth-err">details</a></li>
        <li>The key was updated recently: Please wait and try again - <a href="#error-messages-req-too-early-err">details</a></li>
        <li>This root key has been rotated within the last hour: Only one 'rotate' action per hour is permitted - <a href="#error-messages-key-rotation-not-permitted">details</a></li>
      </ul>
    </td>
    </tr>
    <tr>
    <td>HTTP 410 - Gone</td>
    <td>Key has already been deleted: Please delete references to this key - <a href="#error-messages-key-deleted-err">details</a></td>
    </tr>
    <tr>
    <td>HTTP 422 - Unprocessable Entity</td>
    <td>
      <ul>
        <li>Key is not in a valid state - <a href="#error-messages-key-invalid-state-err">details</a></li>
        <li>Requested action can only be completed with a root key - <a href="#error-messages-key-root-req-reg-err">details</a></li>
        <li>Signature is invalid - <a href="#error-invalid-sig-exp-err-message">details</a></li>
        <li>The provided ciphertext is invalid or corrupted -<a href="#error-messages-unprocessable-ciphertext-err">details</a></li>
        <li>This request requires that the key version is later than current registration key version - <a href="#error-messages-key-version-invalid">details</a></li>
      </ul>
    </td>
    </tr>
    <tr>
    <td>HTTP 500 - Internal Server Error</td>
    <td>Key metadata became corrupted: Please delete this key - <a href="#error-messages-incomplete-metadata-err">details</a></td>
    </tr>
</table>

### Sorted by reason code
{: #error-messages-kms-sorted-by-reason-code}

These are the error messages sorted by the reason code.

- AUTHORIZATIONS_NOT_MET -
    [details](#error-messages-authorizations-not-met)
- BAD_BODY_ERR -
    [details](#error-messages-bad-body-err)
- BEARER_SUB_EXTRACTION_ERR -
    [details](#error-messages-bearer-sub-extraction-err)
- BODY_QUERY_PARAM_MISMATCH_ERR -
    [details](#error-messages-body-query-param-mismatch-err)
- COLLECTION_TOTAL_MISMATCH_ERR -
    [details](#error-messages-collection-total-mismatch-err)
- CONFIG_RULE_CONFLICT_ERR
    [details](#error-config_rule_conflict_err)
- FEATURE_RESTRICTED_ERR -
    [details](#error-messages-feature-restricted-err)
- IMPORT_TOKEN_EXPIRED_ERR -
    [details](#error-messages-import-token-expired-err)
- INCOMPLETE_METADATA_ERR -
    [details](#error-messages-incomplete-metadata-err)
- INCORRECT_NONCE_ERR -
    [details](#error-messages-incorrect-nonce-err)
- INCORRECT_NONCE_IV_ERR -
    [details](#error-messages-incorrect-nonce-iv-err)
- INVALID_SIG_EXP_ERR
    [details](#error-invalid_sig_exp_err)
- KEY_ACTION_INVALID_STATE_ERR -
    [details](#error-messages-key-action-invalid-state-err)
- KEY_CREATE_IMPORT_ACCESS_ERR -
    [details](#error-messages-key-create-import-access-err)
- KEY_DELETED_ERR -
    [details](#error-messages-key-deleted-err)
- KEY_EXPIRED_ERR -
    [details](#error-messages-key-expired-err)
- KEY_IMPT_REQ_ERR -
    [details](#error-messages-key-impt-req-err)
- KEY_INVALID_STATE_ERR -
    [details](#error-messages-key-invalid-state-err)
- KEY_PAYLOAD_REQ_ERR -
    [details](#error-messages-key-payload-req-err-message)
- KEY_RESTORE_EXPIRED -
    [details](#error-messages-key-restore-expired)
- KEY_ROOT_REQ_ERR -
    [details](#error-messages-key-root-req-err)
- KEY_ROOT_REQ_REG_ERR -
    [details](#error-messages-key-root-req-reg-err)
- KEY_ROTATION_NOT_PERMITTED -
    [details](#error-messages-key-rotation-not-permitted)
- KEY_VERSION_INVALID -
    [details](#error-messages-key-version-invalid)
- NO_BODY_ERR -
    [details](#error-messages-no-body-err)
- NOT_DUAL_AUTH_ERR -
    [details](#error-messages-not-dual-auth-err)
- NUM_COLLECTION_RESOURCE_ERR -
    [details](#error-messages-num-collection-resource-err)
- PREV_KEY_DEL_ERR -
    [details](#error-messages-prev-key-del-err)
- PROTECTED_RESOURCE_ERR -
    [details](#error-messages-protected-resource-err)
- REQ_TOO_EARLY_ERR -
    [details](#error-messages-req-too-early-err)
- RESOURCE_OWNER_ERR -
    [details](#error-messages-resource-owner-err)
- SERVICE_ONLY_ERR -
    [details](#error-messages-service-only-err)
- UNAUTHORIZED_ERR -
    [details](#error-messages-unauthorized-err)
- UNPROCESSABLE_CIPHERTEXT_ERR -
    [details](#error-messages-unprocessable-ciphertext-err)

## 1 - Collection total does not match number...
{: #error-messages-collection-total-mismatch-err}

### Message
{: #error-messages-collection-total-mismatch-err-message}

Collection total does not match number of resources

Reason code: COLLECTION_TOTAL_MISMATCH_ERR

### HTTP status code
{: #error-messages-collection-total-mismatch-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-collection-total-mismatch-err-context}

This error occurs when an
[instance policy](/apidocs/key-protect#set-instance-policies){: external}
is created.

The value of the `metadata.collectionTotal` field does not match the number of
resources in the `resources` array.

The `create instance policy` request fails because the
`metadata.collectionTotal` is 2, while 1 (one) resource was provided in the
`resources` array.

```sh
# this request fails because the collectionTotal is 2 and there is 1 (one) resource
$ curl -X PUT \
    "https://us-south.kms.cloud.ibm.com/api/v2/instance/policies?policy=dualAuthDelete" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.policy+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.policy+json",
                "collectionTotal": 2
            },
            "resources": [
                {
                    "policy_type": "dualAuthDelete",
                    "policy_data": {
                        "enabled": false
                    }
                }
            ]
        }'
```
{: codeblock}

#### JSON response
{: #error-messages-collection-total-mismatch-err-context-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources":[
        {
            "errorMsg": "Bad Request: Instance policy could not be created. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "COLLECTION_TOTAL_MISMATCH_ERR",
                    "message": "Collection total does not match number of resources",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 2 - Data in body does not match data required...
{: #error-messages-body-query-param-mismatch-err}

### Message
{: #error-messages-body-query-param-mismatch-err-message}

Data in body does not match data required by query parameter

Reason code: BODY_QUERY_PARAM_MISMATCH_ERR

### HTTP status code
{: #error-messages-body-query-param-mismatch-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-body-query-param-mismatch-err-context}

This error occurs when an
[instance policy](/apidocs/key-protect#set-instance-policies){: external}
is created.

The query parameter, which specifies the policy (dualAuthDelete, allowedNetwork,
or allowedIP), does not match the first `policy_type` in the `resources`
array.

The `create instance policy` request fails because the `policy` query parameter
(dualAuthDelete) does not match the `resources.policy_type` (badName).

```sh
# this request fails because the query parameter does not match the resource
$ curl -X PUT \
    "https://us-south.kms.cloud.ibm.com/api/v2/instance/policies?policy=dualAuthDelete" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.policy+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.policy+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "policy_type": "badName",
                    "policy_data": {
                        "enabled": false
                    }
                }
            ]
        }'
```
{: codeblock}

#### JSON response
{: #error-messages-body-query-param-mismatch-err-context-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Instance policy could not be created. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "BODY_QUERY_PARAM_MISMATCH_ERR",
                    "message": "Data in body does not match data required by query parameter",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 3 - Extracting the subject from the bearer...
{: #error-messages-bearer-sub-extraction-err}

### Message
{: #error-messages-bearer-sub-extraction-err-message}

Extracting the subject from the bearer token failed: Make sure the bearer token
passed is the correct one (and correct format) and is allowed to perform
requested actions

Reason code: BEARER_SUB_EXTRACTION_ERR

### HTTP status code
{: #error-messages-bearer-sub-extraction-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-bearer-sub-extraction-err-context}

The identify and access management (IAM) access token, or format, was invalid.
If this is a **curl** request, then the **authorization** header needs to be set
using this format:

```sh
-H "authorization: Bearer $ACCESS_TOKEN"
```
{: screen}

Depending on which platform (Linux&reg;, Mac, Windows&reg;) or shell (bash, sh, zsh) you
are using, you need to be aware of using single versus double quotation marks. Some
systems will **not** interpret variables inside single quotation mark. For example,
('Bearer $ACCESS_TOKEN') cannot replace `$ACCESS_TOKEN` with the value.
{: note}

Make sure you specify a valid IAM token. You might need to login (again) if your
token has expired. Here are a few lines of command line interface (CLI) code to
login and set the access token.

```sh
# login with single sign on (sso)
$ ibmcloud login --sso

# set the region (-r) and resource group (-g)
$ ibmcloud target -r us-south -g Default

# set the ACCESS_TOKEN environment variable (with Bearer)
$ export ACCESS_TOKEN=`ibmcloud iam oauth-tokens | grep IAM | cut -d \: -f 2 | sed 's/^ *//'`

# show the access token
$ echo $ACCESS_TOKEN

Bearer eyJraWQiOiIyMDIwMDcyNDE4MzEiLCJh...<redacted>...o4qlcKjl9sVqLa8Q

# set the ACCESS_TOKEN environment variable (without Bearer)
$ export ACCESS_TOKEN=`ibmcloud iam oauth-tokens | grep IAM | cut -d ' ' -f 5 | sed 's/^ *//'`

eyJraWQiOiIyMDIwMDcyNDE4MzEiLCJh...<redacted>...o4qlcKjl9sVqLa8Q
```
{: codeblock}

## 4 - Invalid body data was passed...
{: #error-messages-bad-body-err}

### Message
{: #error-messages-bad-body-err-message}

Invalid body data was passed: Please ensure the data passed had valid
formatting with no invalid characters

Reason code: BAD_BODY_ERR

### HTTP status code
{: #error-messages-bad-body-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-bad-body-err-context}

Some examples of this error are:

- Create an instance policy
    - Only one of each policy can be created
    - No `resources` section was provided
    - Extraneous fields in the `resources` section (see example 1)

- Create a key
    - One resource is required (see example 2)
    - Metadata is empty (see example 3)
    - Key has zero value or it's empty

#### Example 1
{: #error-messages-bad-body-err-context-example-1}

The `create instance policy` request fails because the resource contains an
extra field (`extra_field`).

```sh
# this request fails because there is an extra field in the body
$ curl -X PUT \
    "https://us-south.kms.cloud.ibm.com/api/v2/instance/policies?policy=dualAuthDelete" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.policy+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.policy+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "policy_type": "dualAuthDelete",
                    "policy_data": {
                        "enabled": false
                    },
                    "extra_field": "junk data"
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-bad-body-err-context-example-1-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Instance policy could not be created. Please see `reasons` for more details.",
            "reasons":[
                {
                    "code": "BAD_BODY_ERR",
                    "message": "Invalid body data was passed. Please ensure the data passed had valid formatting with no invalid characters: json: unknown field \"extra_field\"",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

#### Example 2
{: #error-messages-bad-body-err-context-example-2}

The `create key` request fails because there is more than 1 (one) resource.

```sh
# this request fails because there is more than 1 (one) resource
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "Root-key-1",
                    "description": "example-key",
                    "extractable": false
                },
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "Root-key-2",
                    "description": "example-key",
                    "extractable": false
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-bad-body-err-context-example-2-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Key could not be created. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "BAD_BODY_ERR",
                    "message": "Invalid body data was passed. Please ensure the data passed had valid formatting with no invalid characters: Only creation of one key per request is supported",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

#### Example 3
{: #error-messages-bad-body-err-context-example-3}

This create key request fails because the `metadata` is empty.

```sh
# this request fails because the metadata is empty
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json" \
    -d '{
            "metadata": {},
            "resources": [
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "Root-key-1",
                    "description": "example-key",
                    "extractable": false
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-bad-body-err-context-example-3-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Key could not be created. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "BAD_BODY_ERR",
                    "message": "Invalid body data was passed. Please ensure the data passed had valid formatting with no invalid characters: CollectionMetadata is empty",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 5 - Key has already been deleted...
{: #error-messages-key-deleted-err}

### Message
{: #error-messages-key-deleted-err-message}

Key has already been deleted: Please delete references to this key

Reason code: KEY_DELETED_ERR

### HTTP status code
{: #error-messages-key-deleted-err-http}

410 - Gone

The HTTP `410 Gone` client error response code indicates that access to the
target resource is no longer available at the origin server and that this
condition is likely to be permanent.

If you don't know whether this condition is temporary or permanent, a 404 status
code needs to be used instead.

A `410` response is cacheable by default.

### Context
{: #error-messages-key-deleted-err-context}

The `delete key` request fails because the key was previously deleted. You
cannot delete a key more than once.

#### Example
{: #error-messages-key-deleted-err-context-example}

```sh
# delete an existing key
$ ibmcloud kp key delete $KEY_ID -i $KP_INSTANCE_ID

Deleting key: '0c17...<redacted>...5c34', from instance: 'a192...<redacted>...7411'...
OK
Deleted Key
0c17...<redeacted>...5c34

# this request fails because the key was previously deleted
$ curl -X DELETE \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json"
```
{: codeblock}

##### JSON response
{: #error-messages-key-deleted-err-context-example-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Gone: Key could not be deleted. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "KEY_DELETED_ERR",
                    "message": "Key has already been deleted. Please delete references to this key.",
                    "status": 410,
                    "moreInfo":"https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 6 - Key is not in a valid state
{: #error-messages-key-action-invalid-state-err}

### Message
{: #error-messages-key-action-invalid-state-err-message}

Key is not in a valid state

Reason code: KEY_ACTION_INVALID_STATE_ERR

### HTTP status code
{: #error-messages-key-action-invalid-state-err-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file, which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-key-action-invalid-state-err-context}

This error occurs when an "action" is performed on a key and the
[key state](/docs/key-protect?topic=key-protect-key-states)
is not valid.

Some actions to consider:

- The key state must be active (state value is 1) to wrap, unwrap, rotate, set
    key for deletion (dual auth), unset key for deletion (dual auth), or disable
    the key

- This error occurs when you try to enable an expired key (state value is 3) or
    restore a key that has been destroyed (state value is 5)

#### Example 1
{: #error-messages-key-action-invalid-state-err-context-example-1}

The `key disable` request fails because you cannot disable a key that was
previously disabled.

```sh
# disable a key the first time
$ ibmcloud kp key disable $KEY_ID -i $KP_INSTANCE_ID

Disabling key: '6933...<redacted>...5dbf', in instance: 'a192...<redacted>...7411'...
OK

# this CLI request fails because the key is deleted a second time
$ ibmcloud key disable $KEY_ID -i $KP_INSTANCE_ID

Disabling key: '69332...<redacted>...5dbf', in instance: 'a192...<redacted>...7411'...
FAILED
kp.Error:
    correlation_id='aca1...<redacted>...66e9',
    msg='Conflict:
        Key is not in active state:
        Key could not be disabled.
        Please see `reasons` for more details.',
    reasons='[KEY_ACTION_INVALID_STATE_ERR:
        Key is not in a valid state -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'

# this API request fails because the key is deleted a third time
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/disable" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json"
```
{: codeblock}

##### JSON response
{: #error-messages-key-action-invalid-state-err-context-example-1-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: Key is not in active state: Key could not be disabled. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "KEY_ACTION_INVALID_STATE_ERR",
                    "message": "Key is not in a valid state",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

#### Example 2
{: #error-messages-key-action-invalid-state-err-context-example-2}

The `key disable` request fails because the key has expired and you are
attempting to change the key state from disabled (state value is 3) to enabled
(state value is 1).

The following steps return a `key has been disabled` error.

1. Create a key with an expiration date

2. Allow the expiration date to pass

3. Enable the key

```sh
# on a Mac, add 1 (one) minute to the current time
$ EXPIRE=$(date -u -v+1M "+%Y-%m-%dT%H:%M:%SZ")

$ echo $EXPIRE

# step 1 - create a key with an expiration date
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "Root-key-1",
                    "description": "example-key",
                    "expirationDate": "'$EXPIRE'",
                    "extractable": false
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-key-action-invalid-state-err-context-example-2-json-1}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "type": "application/vnd.ibm.kms.key+json",
            "id": "88d649f8-41b8-4426-b52b-45c88953d5b8",
            "name": "Root-key-1",
            "description": "example-key",
            "state": 1,
            "expirationDate": "2020-08-12T23:38:09Z",
            "extractable": false,
            "crn": "crn:v1:bluemix:public:kms:us-south:a/ea998d3389c3473aa0987652b46fb146:a192d603-0b8d-452f-aac3-f9e1f95e7411:key:88d649f8-41b8-4426-b52b-45c88953d5b8",
            "imported": false,
            "deleted": false
        }
    ]
}
```
{: screen}

```sh
# capture the key id
$ KEY_ID=88d649f8-41b8-4426-b52b-45c88953d5b8

# step 2 - allow the expiration date to pass by sleeping for 1 (one) minute
$ sleep 60

# step 3 - fails because you cannot enable a key after the expiration date
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/enable" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json"
```
{: codeblock}

##### JSON response
{: #error-messages-key-action-invalid-state-err-context-example-2-json-2}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: Key is not in suspended state: Key could not be enabled. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code":" KEY_ACTION_INVALID_STATE_ERR",
                    "message": "Key is not in a valid state",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 7 - Key is not in a valid state
{: #error-messages-key-invalid-state-err}

### Message
{: #error-messages-key-invalid-state-err-message}

Key is not in a valid state

Reason code: KEY_INVALID_STATE_ERR

### HTTP status code
{: #error-messages-key-invalid-state-err-http}

422 - Unprocessable Entity

The HTTP `422 Unprocessable Entity` response status code indicates that the
server understands the content type of the request entity, and the syntax of the
request entity is correct, but it was unable to process the contained
instructions.

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-invalid-state-err-context}

This error applies to keys used for "Registrations."

The key state must be active (state value is 1) when registering the key with a
cloud resource.

Registrations are associations between root keys and other cloud resources, such
as Cloud Object Storage (COS) buckets or Cloud Databases deployments.

For more information about Registrations, see
[viewing associations between root keys and encrypted IBM Cloud resources](/docs/key-protect?topic=key-protect-view-protected-resources).

## 8 - Key is protecting one or more cloud...
{: #error-messages-protected-resource-err}

### Message
{: #error-messages-protected-resource-err-message}

Key is protecting one or more cloud resources

Reason code: PROTECTED_RESOURCE_ERR

### HTTP status code
{: #error-messages-protected-resource-err-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file, which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-protected-resource-err-context}

This error applies to keys used for "Registrations."

A key that is registered for a cloud resource cannot be deleted unless the
`force` option is specified.

You must use the `force` option to delete a root key that is registered with
another cloud resource.

Registrations are associations between root keys and other cloud resources, such
as Cloud Object Storage (COS) buckets or Cloud Databases deployments.

For more information about Registrations, see
[viewing associations between root keys and encrypted IBM Cloud resources](/docs/key-protect?topic=key-protect-view-protected-resources).

[See this explanation](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference#kp-key-delete)
of deleting keys that are registered with another cloud resource (look at the
`force` option).

```sh
# this CLI request fails because the registration was not deleted
$ ibmcloud kp key delete $KEY_ID -i $KP_INSTANCE_ID

Deleting key: 52a9d772-8982-4620-bfb4-b070dd812a0c, from instance: b0d84b32-09d0-4314-8049-da78e3b9ab6f...
FAILED
kp.Error:
    correlation_id='c27b7948-4a1f-4cbd-8770-cb3616888e27',
    msg='Conflict:
        Key could not be deleted.
        Please see "reasons" for more details.',
    reasons='[PROTECTED_RESOURCE_ERR:
        Key is protecting one or more cloud resources -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/docs/key-protect?topic=key-protect-troubleshooting#unable-to-delete-keys]'

# this CLI request succeeds when using the --force option
# the registration between Key Protect and the cloud resource exists
$ ibmcloud kp key delete $KEY_ID -i $KP_INSTANCE_ID --force --output json

{
    "id": "52a9d772-8982-4620-bfb4-b070dd812a0c"
}
```
{: codeblock}

## 9 - Key metadata became corrupted...
{: #error-messages-incomplete-metadata-err}

### Message
{: #error-messages-incomplete-metadata-err-message}

Key metadata became corrupted: Please delete this key

Reason code: INCOMPLETE_METADATA_ERR

### HTTP status code
{: #error-messages-incomplete-metadata-err-http}

500 - Internal Server Error

The HTTP `500 Internal Server` server error response code indicates that the
server encountered an unexpected condition that prevented it from fulfilling the
request.

This error response is a generic "catch-all" response. Usually, this indicates
that the server cannot find a better 5xx error code to response. Sometimes, server
administrators log error responses like the 500 status code with more details
about the request to prevent the error from happening again in the future.

### Context
{: #error-messages-incomplete-metadata-err-context}

This error is returned when there is an internal error.

If you get this error, please contact
[IBM support](/unifiedsupport/supportcenter){: external}

## 10 - Key restoration has expired
{: #error-messages-key-restore-expired}

### Message
{: #error-messages-key-restore-expired-message}

Key restoration has expired

Reason code: KEY_RESTORE_EXPIRED

### HTTP status code
{: #error-messages-key-restore-expired-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-restore-expired-context}

This error occurs when you try to restore a key that was deleted more than 30
days ago.

## 11 - KeyCreateImportAccess instance policy...
{: #error-messages-key-create-import-access-err}

### Message
{: #error-messages-key-create-import-access-err-message}

KeyCreateImportAccess instance policy does not allow this action

Reason code: KEY_CREATE_IMPORT_ACCESS_ERR

### HTTP status code
{: #error-messages-key-create-import-access-err-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-key-create-import-access-err-context}

The `KeyCreateImportAccess` instance policy was enabled and a request to create
or import a key was not allowed.

For example, the instance policy does not allow creating a standard key and a
request to create a standard key was rejected.

#### Example
{: #error-messages-key-create-import-access-err-example}

The following steps return this error.

1. Enable the instance policy and prevent creating standard keys

2. Attempt to create a standard key, which fails

3. Remove (disable) the instance policy, which allows creating standard keys

4. Create a standard key, which succeeds

```sh
# step 1 - enable an instance policy, which prevents creating standard keys
$ curl -X PUT \
    "https://us-south.kms.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess" \
    -H "accept: application/vnd.ibm.kms.policy+json" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.policy+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.policy+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "policy_type": "keyCreateImportAccess",
                    "policy_data": {
                        "enabled": true,
                        "attributes": {
                            "create_root_key": true,
                            "create_standard_key": false,
                            "import_root_key": true,
                            "import_standard_key": true,
                            "enforce_token": true
                        }
                    }
                }
            ]
        }'

# step 2a - fails when using the ibmcloud CLI
# because the instance policy prevents creating standard keys
$ ibmcloud kp key create my-standard-key --standard-key

FAILED
kp.Error:
    correlation_id='43c45c85-7a1f-478c-b235-49decec8c88f',
    msg='Conflict:
        Key could not be created:
        Please see `reasons` for more details (KEY_CREATE_IMPORT_ACCESS_ERR)',
    reasons='[KEY_CREATE_IMPORT_ACCESS_ERR:
        KeyCreateImportAccess instance policy does not allow this action -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'

# step 2b - fails when using the the ibmcloud API
# because the instance policy prevents creating standard keys
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "my-standard-key",
                    "description": "my-standard-key",
                    "extractable": true
                }
            ]
        }'
```
{: codeblock}

#### JSON response from ibmcloud API
{: #error-messages-key-create-import-access-err-example-json-1}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: Key could not be created: Please see `reasons` for more details (KEY_CREATE_IMPORT_ACCESS_ERR)",
            "reasons": [
                {
                    "code": "KEY_CREATE_IMPORT_ACCESS_ERR",
                    "message": "KeyCreateImportAccess instance policy does not allow this action",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

Steps 3-4 disables the `keyCreateImportAccess` policy and successfully creates a
standard key.

```sh
# step 3 - disable the policy, that is, enable creating standard keys
$ curl -X PUT \
    "https://us-south.kms.cloud.ibm.com/api/v2/instance/policies?policy=keyCreateImportAccess" \
    -H "accept: application/vnd.ibm.kms.policy+json" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.policy+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.policy+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "policy_type": "keyCreateImportAccess",
                    "policy_data": {
                        "enabled": false
                    }
                }
            ]
        }'

# step 4a - create a standard key using the ibmcloud CLI
$ ibmcloud kp key create my-standard-key --standard-key -o json

{
    "id": "3511e0bc-e32d-40b8-b6c2-96cd651858a4",
    "name": "my-standard-key",
    "type": "application/vnd.ibm.kms.key+json",
    "extractable": true,
    "state": 1,
    "crn": "crn:v1:bluemic:public:kms:us-south:a/819bdf4436ef4c198fdf4f0b81d53116:87fa68d0-fa10-47d0-a201-603949808530:key:3511e0bc-e32d-40b8-b6c2-96cd651858a4",
    "deleted": false
}

# step 4b - create a standard key using the ibmcloud API
curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "my-standard-key",
                    "description": "my-standard-key",
                    "extractable": true
                }
            ]
        }'
```
{: codeblock}

#### JSON response from ibmcloud API
{: #error-messages-key-create-import-access-err-example-json-2}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "type": "application/vnd.ibm.kms.key+json",
            "id": "60d72058-ec53-4d77-b7ef-ba56443e76d5",
            "name": "my-standard-key",
            "description": "my-standard-key",
            "state": 1,
            "extractable": true,
            "crn":"crn:v1:bluemix:public:kms:us-south:a/819bdf4436ef4c198fdf4f0b81d53116:87fa68d0-fa10-47d0-a201-603949808530:key:60d72058-ec53-4d77-b7ef-ba56443e76d5",
            "imported": false,
            "deleted": false
        }
    ]
}
```
{: screen}

## 12 - Missing body in request
{: #error-messages-no-body-err}

### Message
{: #error-messages-no-body-err-message}

Missing body in request

Reason code: NO_BODY_ERR

### HTTP status code
{: #error-messages-no-body-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-no-body-err-context}

This error occurs when you "rewrap" or "unwrap" a key and there is no body.

#### Example
{: #error-messages-no-body-err-context-example}

The following steps return a `missing body in request` error.

1. Create a root key

2. Create a data encryption key (DEK), this is the `plaintext`

3. Wrap the DEK with the root key, this creates a `ciphertext`

4. Request **fails** to unwrap the new ciphertext to reveal the original DEK
   (plaintext) because of a missing body

5. Request **succeeds** to unwrap the new ciphertext to reveal the original DEK
   (plaintext) because the body is specified

```sh
# step 1 - create a root key
$ KEY_ID=$(ibmcloud kp key create example-key -i $KP_INSTANCE_ID --output json | jq -r '.["id"]')

$ echo $KEY_ID

66ffaf5b-86c8-4a50-8a2a-920ae71f86dc

# step 2 - create a random, base64-encoded, 32-byte data encryption key (DEK)
$ PLAINTEXT=$(openssl rand -base64 32)

$ echo $PLAINTEXT

2eLAD3LyD3H2bq8dIDAy0A/lN9DSE/Ne3bwu40CdErs=

# step 3 - wrap the DEK (plaintext key) with the root key, creating the ciphertext
$ CIPHERTEXT=$(ibmcloud kp key wrap $KEY_ID -i $KP_INSTANCE_ID -p $PLAINTEXT --output json | jq -r '.["Ciphertext"]')

$ echo $CIPHERTEXT

eyJjaXBoZXJ0ZXh0IjoiR0VnTFZGSmpK...<redacted>...YWU3MWY4NmRjIn0=

# step 4 - fails to unwrap the ciphertext, which reveals the original DEK
# (plaintext), because there is no body (the -d option)
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/unwrap" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json"
```
{: codeblock}

#### JSON response
{: #error-messages-no-body-err-context-example-json-1}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Action could not be performed on key. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "NO_BODY_ERR",
                    "message": "Missing body in request",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

```sh
# step 5 - succeeds to unwrap the ciphertext because the request is complete
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/unwrap" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json" \
    -d '{
           "ciphertext": "'$CIPHERTEXT'"
        }'
```
{: codeblock}

#### JSON response
{: #error-messages-no-body-err-context-example-json-2}

```json
{
    "plaintext": "2eLAD3LyD3H2bq8dIDAy0A/lN9DSE/Ne3bwu40CdErs=",
    "keyVersion": {
        "id": "66ffaf5b-86c8-4a50-8a2a-920ae71f86dc"
    }
}
```
{: screen}

## 13 - Number of authorizations required to...
{: #error-messages-authorizations-not-met}

### Message
{: #error-messages-authorizations-not-met-message}

Number of authorizations required to delete is not met

Reason code: AUTHORIZATIONS_NOT_MET

### HTTP status code
{: #error-messages-authorizations-not-met-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-authorizations-not-met-context}

A key with a `dual authorization policy` cannot be deleted without an
authorization from two users.

#### Example
{: #error-messages-authorizations-not-met-context-example}

These steps illustrate how to create the error message.

1. Create a root key

2. Enable the dual authorization policy

3. List the policies (verify dual authorization is enabled)

4. Delete the key, which **fails** because not enough authorizations are met to
   delete the key

```sh
# step 1 - create a root key
$ KEY_ID=$(ibmcloud kp key create example-key -i $KP_INSTANCE_ID --output json | jq -r '.["id"]')

$ echo $KEY_ID

8f97b016-bc31-4e3d-9cd6-a0a1c7caffdb

# step 2 - enable the dual authorization policy
$ ibmcloud kp key policy-update dual-auth-delete $KEY_ID -i $KP_INSTANCE_ID --enable

Setting a rotation interval for key ID: 8f97b016-bc31-4e3d-9cd6-a0a1c7caffdb...
OK

Key ID          8f97b016-bc31-4e3d-9cd6-a0a1c7caffdb
Created By      IBMid-...<redacted>...
Creation Date   2020-08-13T22:33:50Z
Last Updated    2020-08-13T22:33:50Z
Updated By      IBMid-...<redacted>...
Enabled         true

# step 3 - list the policies (verify dual authorization is enabled)
$ ibmcloud kp key policies $KEY_ID -i $KP_INSTANCE_ID --output json

[
    {
        "createdBy": "IBMid-...<redacted>...",
        "creationDate": "2020-08-13T22:33:50Z",
        "crn": "crn:v1:bluemix:public:kms:us-south:a/ea998d3389c3473aa0987652b46fb146:a192d603-0b8d-452f-aac3-f9e1f95e7411:policy:0b93cd65-8359-4891-9289-8701f4c6ad9c",
        "lastUpdateDate": "2020-08-13T22:33:50Z",
        "updatedBy": "IBMid-...<redacted>...",
        "dualAuthDelete": {
            "enabled": true
        }
    }
]

# step 4 - fails because not enough authorizations are met to delete the key
$ curl -X DELETE \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json"
```
{: codeblock}

##### JSON response
{: #error-messages-authorizations-not-met-context-example-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: 1 prior authorization(s) are required for deletion: Key could not be deleted. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "AUTHORIZATIONS_NOT_MET",
                    "message": "Number of authorizations required to delete is not met",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 14 - Only a single instance policy can be...
{: #error-messages-num-collection-resource-err}

### Message
{: #error-messages-num-collection-resource-err-message}

Only a single instance policy can be created per query parameter: Please
pass single resource object

Reason code: NUM_COLLECTION_RESOURCE_ERR

### HTTP status code
{: #error-messages-num-collection-resource-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-num-collection-resource-err-context}

The `create instance policy` request fails because the same policy was
specified more than once.

You can specify multiple policies in the request if each policy is
unique. For example, you could create instance policies for `dualAuthDelete` and
`allowedIP` in the same request.

#### Example
{: #error-messages-num-collection-resource-err-context-example}

This request fails because more than one instance policy was provided.

```sh
# this request fails because the dualAuthDelete policy was specified more than once
$ curl -X PUT \
    "https://us-south.kms.cloud.ibm.com/api/v2/instance/policies?policy=dualAuthDelete" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.policy+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.policy+json",
                "collectionTotal": 2
            },
            "resources": [
                {
                    "policy_type": "dualAuthDelete",
                    "policy_data": {
                        "enabled": false
                    }
                },
                {
                    "policy_type": "dualAuthDelete",
                    "policy_data": {
                        "enabled": false
                    }
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-num-collection-resource-err-context-example-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Instance policy could not be created. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "NUM_COLLECTION_RESOURCE_ERR",
                    "message": "Only a single instance policy can be created per query parameter. Please pass single resource object",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 15 - Only imported keys can be restored
{: #error-messages-key-impt-req-err}

### Message
{: #error-messages-key-impt-req-err-message}

Only imported keys can be restored

Reason code: KEY_IMPT_REQ_ERR

### HTTP status code
{: #error-messages-key-impt-req-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-impt-req-err-context}

{{site.data.keyword.hscrypto}} can restore a previously deleted
root key, which restores access to the associated data in the cloud.

As an admin, you might need to restore a root key that was imported into
{{site.data.keyword.hscrypto}} to access data the key
previously protected.

When you restore a key, you move the key from the _Destroyed_ (state value is 5)
to the _Active_ (state value is 1) key state, and you restore access to any data
that was previously encrypted with the key.

You can restore a deleted key within 30 days of the deletion. This capability is
available only for root keys that were created with a `key material`, also known
as the "payload."

You can only restore root keys that were created with a `key material`, using
the `kp key create` command with the `-k, --key-material` option. You _cannot_
restore a root key if the `--key-material` option was **not** specified.

If you want to restore a deleted root key then you **must** save the
`key material` that was used to create the root key. You _cannot_ restore a
deleted key without provided the original `key material`.

#### Example
{: #error-messages-key-impt-req-err-context-example}

Follow these steps to create the `only imported keys can be restored` error.

1. Create a root key without a key material (payload)

2. Delete the key

3. Sleep 30 seconds

4. Create a key material

5. Restore the key and provide a key material (payload)

```sh
# step 1 - create a root key without a key material (payload)
$ KEY_ID=$(ibmcloud kp key create example-key -i $KP_INSTANCE_ID --output json | jq -r '.["id"]')

$ echo $KEY_ID

e631925f-affb-457e-886d-57cb2a5f565b

# step 2 - delete the key
$ ibmcloud kp key delete $KEY_ID -i $KP_INSTANCE_ID

Deleting key: 'e631925f-affb-457e-886d-57cb2a5f565b', from instance: 'a192d603-0b8d-452f-aac3-f9e1f95e7411'...
OK
Deleted Key
e631925f-affb-457e-886d-57cb2a5f565b

# step 3 - sleep 30 seconds
$ sleep 30

# step 4 - create a key material
$ KEY_MATERIAL=$(openssl rand -base64 32)

$ echo $KEY_MATERIAL

lZM/guRnn/VklwRBoNOP/AUdCtpDNSo3+xXXhwrnO7c=

# step 5 - this CLI request fails because you can only restore keys
# that were imported (created with a key material or an import token)
$ ibmcloud kp key restore $KEY_ID -i $KP_INSTANCE_ID --key-material $KEY_MATERIAL

Restoring key: 'e631925f-affb-457e-886d-57cb2a5f565b', in instance: 'a192d603-0b8d-452f-aac3-f9e1f95e7411'...
FAILED
kp.Error:
    correlation_id='6d000f60-47f2-4a49-ba72-f02a8efa2945',
    msg='Bad Request:
        Key could not be restored.
        Please see `reasons` for more details.',
    reasons='[KEY_IMPT_REQ_ERR:
        Only imported keys can be restored. -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'

# step 5 - this API request fails because you can only restore keys
# that were imported (created with a key material or an import token)
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/restore" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "payload": "'$KEY_MATERIAL'"
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-key-impt-req-err-context-example-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Key could not be restored. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "KEY_IMPT_REQ_ERR",
                    "message": "Only imported keys can be restored.",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 16 - Requested action can only be completed...
{: #error-messages-key-root-req-err}

### Message
{: #error-messages-key-root-req-err-message}

Requested action can only be completed with a root key

Reason code: KEY_ROOT_REQ_ERR

### HTTP status code
{: #error-messages-key-root-req-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-root-req-err-context}

Many key "actions" can only be performed on "root" keys. This is a list of
commands that can only be performed on root keys.

- `disable key`
- `enable key`
- `restore key`
- `rotate key`
- `unwrap key`
- `wrap key`

#### Example
{: #error-messages-key-root-req-err-context-example}

This example creates a "standard" key then attempts to disable it. This fails
because only "root" keys can be disabled.

```sh
# create a standard key
$ KEY_ID=$(ibmcloud kp key create example-key -i $KP_INSTANCE_ID --output json --standard-key | jq -r '.["id"]')

$ echo $KEY_ID

b2dae7bb-2da5-493e-99d2-a6379e35e58c

# this request fails because a standard key cannot be disabled
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/disable" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json"
```
{: codeblock}

##### JSON response
{: #error-messages-key-root-req-err-context-example-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Key could not be disabled. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "KEY_ROOT_REQ_ERR",
                    "message": "Requested action can only be completed with a root key.",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 17 - Requested action can only be completed...
{: #error-messages-key-root-req-reg-err}

### Message
{: #error-messages-key-root-req-reg-err-message}

Requested action can only be completed with a root key

Reason code: KEY_ROOT_REQ_REG_ERR

### HTTP status code
{: #error-messages-key-root-req-reg-err-http}

422 - Unprocessable Entity

The HTTP `422 Unprocessable Entity` response status code indicates that the
server understands the content type of the request entity, and the syntax of the
request entity is correct, but it was unable to process the contained
instructions.

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-root-req-reg-err-context}

This error applies to keys used for "Registrations." A "root" key is required to
create a registration. This error is returned when a
[create registration API request](/apidocs/key-protect#createregistration){: external}
is made.

Registrations are associations between root keys and other cloud resources, such
as Cloud Object Storage (COS) buckets or Cloud Databases deployments.

For more information about Registrations, see
[viewing associations between root keys and encrypted IBM Cloud resources](/docs/key-protect?topic=key-protect-view-protected-resources).

## 18 - Requested change is not compliant...
{: #error-config_rule_conflict_err}

### Message
{: #error-config-rule-conflict-err-message}

Requested change is not compliant with configuration rules

Reason code: CONFIG_RULE_CONFLICT_ERR

### HTTP status code
{: #error-config-rule-conflict-err-http}

403 - Forbidden

The HTTP `403 Forbidden` client error status response code indicates that the
server understood the request but refuses to authorize it.

This status is similar to `401`, but in this case, reauthenticating will make
no difference. The access is permanently forbidden and tied to the application
logic, such as insufficient rights to a resource.

### Context
{: #error-config-rule-conflict-err-context}

This error message occurs when an instance policy prevents access to a resource.
For example, if the request originated from a public IP address and the instance
policy prohibits access from a public IP address, then you will receive this
error message.

## 19 - Signature is invalid
{: #error-invalid_sig_exp_err}

### Message
{: #error-invalid-sig-exp-err-message}

Signature is invalid

Reason code: INVALID_SIG_EXP_ERR

### HTTP status code
{: #error-invalid-sig-exp-err-http}

422 - Unprocessable Entity

The HTTP `422 Unprocessable Entity` response status code indicates that the
server understands the content type of the request entity, and the syntax of the
request entity is correct, but it was unable to process the contained
instructions.

The client cannot repeat this request without modification.
### Context
{: #error-invalid-sig-exp-err-context}

An error occurred when a key was rewrapped.

If you get this error, please contact
[IBM support](/unifiedsupport/supportcenter){: external}

## 20 - The action could not be performed on...
{: #error-messages-key-expired-err}

### Message
{: #error-messages-key-expired-err-message}

The action could not be performed on the key because the key is expired

Reason code: KEY_EXPIRED_ERR

### HTTP status code
{: #error-messages-key-expired-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-expired-err-context}

This error occurs when restoring a deleted key after the key has expired.

#### Example
{: #error-messages-key-expired-err-context-example}

A `key restore` request fails because the key is deleted and the key has expired.

The following steps will create this error.

1. Create a key material (payload) and an expiration date

2. Create a root key using the key material and the expiration date

3. Capture the key ID

4. Allow the expiration date to pass

5. Delete the key

6. Restore the key, which **fails** because you cannot restore a deleted key
   after the expiration date

```sh
# step 1 - create a key material (payload) and an expiration date
#          create an expiration date, on a Mac, add 1 (one) minute to the current time
$ KEY_MATERIAL=$(openssl rand -base64 32)
$ EXPIRE=$(date -u -v+1M "+%Y-%m-%dT%H:%M:%SZ")

# step 2 - Create a root key using the key material and the expiration date
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "Root-key-1",
                    "payload": "'$KEY_MATERIAL'",
                    "description": "example-key",
                    "expirationDate": "'$EXPIRE'",
                    "extractable": false
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-key-expired-err-context-example-json-1}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "type": "application/vnd.ibm.kms.key+json",
            "id": "aa713df1-857c-4c46-be80-3051756280c9",
            "name": "Root-key-1",
            "description": "example-key",
            "state": 1,
            "expirationDate": "2020-08-14T19:33:47Z",
            "extractable": false,
            "crn": "crn:v1:bluemix:public:kms:us-south:a/ea998d3389c3473aa0987652b46fb146:a192d603-0b8d-452f-aac3-f9e1f95e7411:key:aa713df1-857c-4c46-be80-3051756280c9",
            "imported": true,
            "deleted": false
        }
    ]
}
```
{: screen}

```sh
# step 3 - capture the key id
$ KEY_ID=aa713df1-857c-4c46-be80-3051756280c9

# step 4 - allow the expiration date to pass by sleeping for 1 (one) minute
$ sleep 60

# step 5 - delete the key
$ ibmcloud kp key delete $KEY_ID

Deleting key: 'aa713df1-857c-4c46-be80-3051756280c9', from instance: 'a192d603-0b8d-452f-aac3-f9e1f95e7411'...
OK
Deleted Key
aa713df1-857c-4c46-be80-3051756280c9

# step 6 - fails because you cannot restore a deleted key after the expiration date
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/restore" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "payload": "'$KEY_MATERIAL'"
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-key-expired-err-context-example-json-2}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: The key expired on 2020-08-14 19:33:47 +0000 UTC: Key could not be restored. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "KEY_EXPIRED_ERR",
                    "message": "The action could not be performed on the key because the key is expired.",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 21 - The encrypted nonce given does not match...
{: #error-messages-incorrect-nonce-err}

### Message
{: #error-messages-incorrect-nonce-err-message}

The encrypted nonce given does not match existing record: Please ensure the
correct nonce was given in the request

Reason code: INCORRECT_NONCE_ERR

### HTTP status code
{: #error-messages-incorrect-nonce-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-incorrect-nonce-err-context}

This error message is applicable to the `restore` and `rotate` key interfaces.

This example is based on the `restore` key command and it uses the
[CLI](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference)
because the output is easier to follow than the
[API](/apidocs/key-protect){: external}.

**Step 1** - set up the problem by creating a root key using an import token and
then delete the key

```sh
# create an import token that expires in 15 minutes (900 seconds) and allows 10 retrievals
$ ibmcloud kp import-token create -e 900 -m 10

Created                         Expires                         Max Retrievals   Remaining Retrievals
2020-08-18 19:05:51 +0000 UTC   2020-08-18 19:20:51 +0000 UTC   10               10

# create a random, base64-encoded, 32-byte key material
$ KEY_MATERIAL=$(openssl rand -base64 32)

$ echo $KEY_MATERIAL

DL4Avc1yL7DhclfV9Uksvzy8VkYIKWZA9InYQv/iiro=

# extract the nonce that was created by the "kp import-token create" command
$ NONCE=$(ibmcloud kp import-token show | jq -r '.["nonce"]')

$ echo $NONCE

6SB0nQ8ROUCPUiyF

# extract the public key that was created by the "kp import-token create" command
$ PUBLIC_KEY=$(ibmcloud kp import-token show | jq -r '.["payload"]')

$ echo $PUBLIC_KEY

LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0t ...<redacted>... QyBLRVktLS0tLQo=

# encrypt the key material using the public key
$ ibmcloud kp import-token key-encrypt -k $KEY_MATERIAL -p $PUBLIC_KEY

Encrypted Key
rATe0oyYy+793MDlxQi2kJxf5BqLbmVY ...<redacted>... gNVJ5oxm7KX94iE=

# capture the encrypted key material
$ ENCRYPTED_KEY=rATe0oyYy+793MDlxQi2kJxf5BqLbmVY ...<redacted>... gNVJ5oxm7KX94iE=

# encrypt the nonce
$ ibmcloud kp import-token nonce-encrypt -k $KEY_MATERIAL -n $NONCE

Encrypted Nonce                            IV
+KjUDFD38r8zlXKJkn+dOR4/xNYN5ozpvKCiIQ==   CSPZwm2qJ5mL00oP

# capture the encrypted nonce and the initialization vector (IV)
$ ENCRYPTED_NONCE=+KjUDFD38r8zlXKJkn+dOR4/xNYN5ozpvKCiIQ==
$ IV=CSPZwm2qJ5mL00oP

# create a root key using an import token, provide an encrypted key, nonce, and initialization vector (IV)
$ KEY_ID=$(ibmcloud kp key create my-imported-root-key -k $ENCRYPTED_KEY -n $ENCRYPTED_NONCE -v $IV --output json | jq -r '.["id"]')

$ echo $KEY_ID

fa0a7d81-a947-4bac-883d-952f6288f0a9

# delete the root key
$ ibmcloud kp key delete $KEY_ID

Deleting key: 'fa0a7d81-a947-4bac-883d-952f6288f0a9', from instance: 'a192d603-0b8d-452f-aac3-f9e1f95e7411'...
OK
Deleted Key
fa0a7d81-a947-4bac-883d-952f6288f0a9
```
{: codeblock}

**Step 2** - trigger the error by creating an import token, which is required to
restore the key, and restore the key, then restore the key

```sh
# NOTE: the "kp key restore" requires an import token to complete the process,
# if you follow this example, the import token created above can still exist and
# the example works; otherwise, if the import token has expired then you need to
# create a new import token prior to restoring the key

# create an import token that expires in 15 minutes (900 seconds) and allows 10 retrievals
$ ibmcloud kp import-token create -e 900 -m 10

Created                         Expires                         Max Retrievals   Remaining Retrievals
2020-08-18 19:12:35 +0000 UTC   2020-08-18 19:27:35 +0000 UTC   10               10

# extract the nonce that was created by the "kp import-token create" command
$ NONCE=$(ibmcloud kp import-token show | jq -r '.["nonce"]')

$ echo $NONCE

N3x8F0ihAZ51nj6M

# extract the public key that was created by the "kp import-token create" command
$ PUBLIC_KEY=$(ibmcloud kp import-token show | jq -r '.["payload"]')

$ echo $PUBLIC_KEY

LS0tLS1CRUdJTiBQVUJMSUMgS0VZLS0t ...<redacted>... QyBLRVktLS0tLQo=

# encrypt the key material using the public key
$ ibmcloud kp import-token key-encrypt -k $KEY_MATERIAL -p $PUBLIC_KEY

Encrypted Key
qkhpyERrqgU+q6M0ulCyFLP4/uAyTRNJ ...<redacted>... RvVRAyhPP9civbU=

# capture the encrypted key material
$ ENCRYPTED_KEY=qkhpyERrqgU+q6M0ulCyFLP4/uAyTRNJ ...<redacted>... RvVRAyhPP9civbU=

# encrypt the nonce
$ ibmcloud kp import-token nonce-encrypt -k $KEY_MATERIAL -n $NONCE

Encrypted Nonce                            IV
nrrCczvYXvc6T7J2G+EOLjHZO1cpPyu/nhsIlA==   N6oLJnUqaKF3v5Sd

# Normally, you would capture the last encrypted nonce and the initialization
# vector (IV) (from the import token). Then use those new values with the
# "key restore" command.

# To force an error we are using the old (original) encrypted nonce and IV to
# restore the key, which fails because the ENCRYPTED_NONCE does not match the
# value in the import token

# we skipped these steps to force an error
# $ ENCRYPTED_NONCE=nrrCczvYXvc6T7J2G+EOLjHZO1cpPyu/nhsIlA==
# $ IV=N6oLJnUqaKF3v5Sd

# use the CLI to restore the deleted key
# this fails because the ENCRYPTED_NONCE does not match the value in the import token
$ ibmcloud kp key restore $KEY_ID -k $ENCRYPTED_KEY -n $ENCRYPTED_NONCE -v $IV --output json

FAILED
kp.Error:
    correlation_id='a9412941-7986-421d-a67f-b22892e7634d',
    msg='Bad Request:
        Key could not be restored.
        Please see `reasons` for more details.',
    reasons='[INCORRECT_NONCE_ERR:
        The encrypted nonce given does not match existing record,
        please ensure the correct nonce was given in the request -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'
```
{: codeblock}

## 22 - The import token has expired
{: #error-messages-import-token-expired-err}

### Message
{: #error-messages-import-token-expired-err-message}

The import token has expired

Reason code: IMPORT_TOKEN_EXPIRED_ERR

### HTTP status code
{: #error-messages-import-token-expired-err-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you can get a `409` response when uploading a file which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-import-token-expired-err-context}

#### Example 1
{: #error-messages-import-token-expired-err-context-example-1}

Using the API, create an import token, allow it to expire, then attempt to
retrieve it.

```sh
# create an import token
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/import_token" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/json" \
    -d '{
            "expiration": 300,
            "maxAllowedRetrievals": 2
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-import-token-expired-err-context-example-1-json-1}

```json
{
    "maxAllowedRetrievals": 2,
    "creationDate": "2020-08-18T19:54:57Z",
    "expirationDate": "2020-08-18T19:59:57Z",
    "remainingRetrievals":2
}
```
{: screen}

```sh
# retrieve the import token after it expires
$ curl -X GET \
    "https://us-south.kms.cloud.ibm.com/api/v2/import_token" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.import_token+json"
```
{: codeblock}

##### JSON response
{: #error-messages-import-token-expired-err-context-example-1-json-2}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: Import Token could not be retrieved. Please see `reasons` for more details.",
            "reasons":[
                {
                    "code": "IMPORT_TOKEN_EXPIRED_ERR",
                    "message": "The import token has expired.",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

#### Example 2
{: #error-messages-import-token-expired-err-context-example-2}

Using the CLI, create an import token, allow it to expire, then attempt to
retrieve it.

```sh
# create an import token that expires in 5 minutes (300 seconds) and allows 2 retrievals
$ ibmcloud kp import-token create -e 300 -m 2

Created                         Expires                         Max Retrievals   Remaining Retrievals
2020-08-18 19:39:06 +0000 UTC   2020-08-18 19:44:06 +0000 UTC   2                2

# sleep 300 seconds, which allows the import token to expire
$ sleep 300

# show the import token
$ ibmcloud kp import-token show

FAILED
kp.Error:
    correlation_id='fb677c6e-9bfa-422e-a14b-0e221bbad32b',
    msg='Conflict:
        Import Token could not be retrieved.
        Please see `reasons` for more details.',
    reasons='[IMPORT_TOKEN_EXPIRED_ERR:
        The import token has expired. -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'
```
{: codeblock}

## 23 - The key cannot be deleted because it's...
{: #error-messages-prev-key-del-err}

### Message
{: #error-messages-prev-key-del-err-message}

The key cannot be deleted because it's protecting a cloud resource that has
a retention policy: Before you delete this key, contact an account owner to
remove the retention policy on each resource that is associated with the key

Reason code: PREV_KEY_DEL_ERR

### HTTP status code
{: #error-messages-prev-key-del-err-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-prev-key-del-err-context}

This error occurs when a key, used for "Registrations", is deleted.

In most cases, a key with registrations can be deleted using the `--force`
option.

If the registered resource has `preventKeyDeletion` set to `true`, then a force
delete will fail and this error message will be shown.

In other words, all registrations must have `preventKeyDeletion` set to `false`.

Registrations are associations between root keys and other cloud resources, such
as Cloud Object Storage (COS) buckets or Cloud Databases deployments.

For more information about Registrations, see
[viewing associations between root keys and encrypted IBM Cloud resources](/docs/key-protect?topic=key-protect-view-protected-resources).

## 24 - The key is not dual auth enabled and...
{: #error-messages-not-dual-auth-err}

### Message
{: #error-messages-not-dual-auth-err-message}

The key is not dual auth enabled and cannot be set for deletion

Reason code: NOT_DUAL_AUTH_ERR

### HTTP status code
{: #error-messages-not-dual-auth-err-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-not-dual-auth-err-context}

This error occurs when you try to authorize a deletion or remove an
authorization and the key **does not** have a `dual authorization` policy.

These examples show the error using the API and the CLI.

#### Example 1
{: #error-messages-not-dual-auth-err-context-example-1}

This example attempts to authorize a deletion and remove an authorization using
the API.

```sh
# create a root key
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.key+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "type": "application/vnd.ibm.kms.key+json",
                    "name": "root-example-key",
                    "description": "root-example-key",
                    "extractable": false
                }
            ]
        }'
```
{: codeblock}

##### JSON response
{: #error-messages-not-dual-auth-err-context-example-1-json-1}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "type": "application/vnd.ibm.kms.key+json",
            "id": "eb086d96-3b2c-48b5-bf31-c8f0305eea77",
            "name": "root-example-key",
            "description": "root-example-key",
            "state": 1,
            "extractable": false,
            "crn":"crn:v1:bluemix:public:kms:us-south:a/ea998d3389c3473aa0987652b46fb146:a192d603-0b8d-452f-aac3-f9e1f95e7411:key:eb086d96-3b2c-48b5-bf31-c8f0305eea77",
            "imported": false,
            "deleted": false
        }
    ]
}
```
{: screen}

Authorize deletion for a key with a dual authorization policy.

```sh
# set the KEY_ID
$ KEY_ID=eb086d96-3b2c-48b5-bf31-c8f0305eea77

# this request fails because the key DOES NOT have a dual authorization policy
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/setKeyForDeletion" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json"
```
{: codeblock}

##### JSON response
{: #error-messages-not-dual-auth-err-context-example-1-json-2}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: Action could not be performed on key. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "NOT_DUAL_AUTH_ERR",
                    "message":"The key is not dual auth enabled and cannot be set for deletion",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

Remove an authorization for a key with a dual authorization policy.

```sh
# this request fails because the key DOES NOT have a dual authorization policy
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/unsetKeyForDeletion" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json"
```
{: codeblock}

##### JSON response
{: #error-messages-not-dual-auth-err-context-example-1-json-3}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: Action could not be performed on key. Please see `reasons` for more details.",
            "reasons": [
                {
                    "code": "NOT_DUAL_AUTH_ERR",
                    "message": "The key is not dual auth enabled and cannot be set for deletion",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

#### Example 2
{: #error-messages-not-dual-auth-err-context-example-2}

This example attempts to authorize a deletion and remove an authorization using
the CLI.

Note: the `$KEY_ID` was set in the previous example.

```sh
# this request fails because the key DOES NOT have a dual authorization policy
$ ibmcloud kp key schedule-delete $KEY_ID

Scheduling key for deletion...
FAILED
kp.Error:
    correlation_id='3d941968-c599-43b3-b681-306422079412',
    msg='Conflict:
        Action could not be performed on key.
        Please see `reasons` for more details.',
    reasons='[NOT_DUAL_AUTH_ERR:
        The key is not dual auth enabled and cannot be set for deletion -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'

# this request fails because the key DOES NOT have a dual authorization policy
$ ibmcloud kp key cancel-delete $KEY_ID

Cancelling key for deletion...
FAILED
kp.Error:
    correlation_id='5b04a667-573c-44d1-82d5-39730af56a75',
    msg='Conflict:
        Action could not be performed on key.
        Please see `reasons` for more details.',
    reasons='[NOT_DUAL_AUTH_ERR:
        The key is not dual auth enabled and cannot be set for deletion -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'
```
{: codeblock}

## 25 - The key was updated recently
{: #error-messages-req-too-early-err}

### Message
{: #error-messages-req-too-early-err-message}

The key was updated recently: Please wait and try again

Reason code: REQ_TOO_EARLY_ERR

### HTTP status code
{: #error-messages-req-too-early-err-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-req-too-early-err-context}

This error occurs when you `enable` or `restore` a key within 30 seconds of the
last action.

You must wait at least 30 seconds between the last "action" and enabling or
restoring a key.

This example fails because the key was enabled too soon after disabling a key.

```sh
# create a root key
$ KEY_ID=$(ibmcloud kp key create example-key -i $KP_INSTANCE_ID --output json | jq -r '.["id"]')

$ echo $KEY_ID

54f53384-b563-4466-860a-c42ce42f7ac9

# disable the key
$ ibmcloud kp key disable $KEY_ID -i $KP_INSTANCE_ID

Disabling key: '54f53384-b563-4466-860a-c42ce42f7ac9', in instance: 'a192d603-0b8d-452f-aac3-f9e1f95e7411'...
OK

# this request fails because the key was enabled too soon
$ ibmcloud kp key enable $KEY_ID -i $KP_INSTANCE_ID

Enabling key: '54f53384-b563-4466-860a-c42ce42f7ac9', in instance: 'a192d603-0b8d-452f-aac3-f9e1f95e7411'...
FAILED
kp.Error:
    correlation_id='59c343a7-c20f-43ea-9e50-da45cecbc8a6',
    msg='Conflict:
        Key could not be enabled.
        Please see `reasons` for more details.',
    reasons='[REQ_TOO_EARLY_ERR:
        The key was updated recently.
        Please wait and try again. -
        FOR_MORE_INFO_REFER: https://cloud.ibm.com/apidocs/key-protect]'

# this request succeeds because the key was disabled at least 30 seconds ago
$ ibmcloud kp key enable $KEY_ID -i $KP_INSTANCE_ID

Enabling key: '54f53384-b563-4466-860a-c42ce42f7ac9', in instance: 'a192d603-0b8d-452f-aac3-f9e1f95e7411'...
OK
```
{: codeblock}

## 26 - The provided ciphertext is invalid or...
{: #error-messages-unprocessable-ciphertext-err}

### Message
{: #error-messages-unprocessable-ciphertext-err-message}

The provided ciphertext is invalid or corrupted

Reason code: UNPROCESSABLE_CIPHERTEXT_ERR

### HTTP status code
{: #error-messages-unprocessable-ciphertext-err-http}

422 - Unprocessable Entity

The HTTP `422 Unprocessable Entity` response status code indicates that the
server understands the content type of the request entity, and the syntax of the
request entity is correct, but it was unable to process the contained
instructions.

The client cannot repeat this request without modification.

### Context
{: #error-messages-unprocessable-ciphertext-err-context}

This typically means the hardware security module (HSM) could not process the
data because the input was invalid.

This error is returned when there is an internal error.

If you get this error, please contact
[IBM support](/unifiedsupport/supportcenter){: external}

## 27 - The provided encrypted nonce was not...
{: #error-messages-incorrect-nonce-iv-err}

### Message
{: #error-messages-incorrect-nonce-iv-err-message}

The provided encrypted nonce was not encrypted with the key material given
OR the provided IV does not match the encrypted nonce

Reason code: INCORRECT_NONCE_IV_ERR

### HTTP status code
{: #error-messages-incorrect-nonce-iv-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-incorrect-nonce-iv-err-context}

This typically means the hardware security module (HSM) could not process the
data because the input was invalid.

This error is returned when there is an internal error.

If you get this error, please contact
[IBM support](/unifiedsupport/supportcenter){: external}

## 28 - The resource(s) queried does not belong to the service
{: #error-messages-resource-owner-err}

### Message
{: #error-messages-resource-owner-err-message}

The resource(s) queried does not belong to the service

Reason code: RESOURCE_OWNER_ERR

### HTTP status code
{: #error-messages-resource-owner-err-http}

403 - Forbidden

The HTTP `403 Forbidden` client error status response code indicates that the
server understood the request but refuses to authorize it.

This status is similar to `401`, but in this case, re-authenticating will make
no difference. The access is permanently forbidden and tied to the application
logic, such as insufficient rights to a resource.

### Context
{: #error-messages-resource-owner-err-context}

This error message occurs in a service-to-service request. The service attempts
to delete a key, which is not allowed. That is, another service cannot delete a
{{site.data.keyword.hscrypto}} key.

One example of using service-to-service access is a user configuring a Cloud
Object Storage (COS) bucket to encrypt their data using a
{{site.data.keyword.hscrypto}} key.

Using the COS example, COS cannot delete the key used to encrypt data.

## 29 - This action can only be done by a service...
{: #error-messages-service-only-err}

### Message
{: #error-messages-service-only-err-message}

This action can only be done by a service (service to service)

Reason code: SERVICE_ONLY_ERR

### HTTP status code
{: #error-messages-service-only-err-http}

403 - Forbidden

The HTTP `403 Forbidden` client error status response code indicates that the
server understood the request but refuses to authorize it.

This status is similar to `401`, but in this case, re-authenticating will make
no difference. The access is permanently forbidden and tied to the application
logic, such as insufficient rights to a resource.

### Context
{: #error-messages-service-only-err-context}

Some actions, such as creating a "registration", can only be performed by
another service, in what is known as a service-to-service request.

For example, if you configuring a Cloud Object Storage (COS) bucket to encrypt
data using a {{site.data.keyword.hscrypto}} key, then the COS
service need to create the registration.

A service-to-service request is required to create, delete, replace, or update a
registration.

See this resource for more information about registrations.

- [API documentation](/apidocs/key-protect#createregistration){: external}

## 30 - This action is not permitted on this...
{: #error-messages-feature-restricted-err}

### Message
{: #error-messages-feature-restricted-err-message}

This action is not permitted on this resource: Please contact IBM Key
Protect or open a service ticket to enable this feature

Reason code: FEATURE_RESTRICTED_ERR

### HTTP status code
{: #error-messages-feature-restricted-err-http}

403 - Forbidden

The HTTP `403 Forbidden` client error status response code indicates that the
server understood the request but refuses to authorize it.

This status is similar to `401`, but in this case, re-authenticating will make
no difference. The access is permanently forbidden and tied to the application
logic, such as insufficient rights to a resource.

### Context
{: #error-messages-feature-restricted-err-context}

You are attempting to create, update, or use an instance policy with a feature
that is not supported.

For example, instance policy was created for an `allowedIp` address range, which
only supports IPv4 addresses. You then made a request to the instance with an
IPv6 address, which returns this error.

## 31 - This request requires that the key version...
{: #error-messages-key-version-invalid}

### Message
{: #error-messages-key-version-invalid-message}

This request requires that the key version is later than current
registration key version

Reason code: KEY_VERSION_INVALID

### HTTP status code
{: #error-messages-key-version-invalid-http}

422 - Unprocessable Entity

The HTTP `422 Unprocessable Entity` response status code indicates that the
server understands the content type of the request entity, and the syntax of the
request entity is correct, but it was unable to process the contained
instructions.

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-version-invalid-context}

This error applies to keys used for "Registrations."

When a service, such as Cloud Object Storage (COS), tries to replace or restore
a key it checks the timestamp of the key.

If the key timestamp is less than the timestamp of the key used by the
registration then this error occurs.

The key used buy the service must have a timestamp equal to or greater than the
registration's key.

Registrations are associations between root keys and other cloud resources, such
as Cloud Object Storage (COS) buckets or Cloud Databases deployments.

For more information about Registrations, see
[viewing associations between root keys and encrypted IBM Cloud resources](/docs/key-protect?topic=key-protect-view-protected-resources).

## 32 - This root key has been rotated within...
{: #error-messages-key-rotation-not-permitted}

### Message
{: #error-messages-key-rotation-not-permitted-message}

This root key has been rotated within the last hour: Only one 'rotate'
action per hour is permitted

Reason code: KEY_ROTATION_NOT_PERMITTED

### HTTP status code
{: #error-messages-key-rotation-not-permitted-http}

409 - Conflict

The HTTP `409 Conflict` response status code indicates a request conflict with
current state of the server.

Conflicts are most likely to occur in response to a `PUT` request. For example,
you might get a `409` response when uploading a file which is older than the one
already on the server resulting in a version control conflict.

### Context
{: #error-messages-key-rotation-not-permitted-context}

A root key can be rotated, at most, once an hour. Attempting to rotate a root
key any sooner than one hour returns this error message.

```sh
# step 1 - create a root key and provide a key material
$ KEY_MATERIAL=$(openssl rand -base64 32)

$ echo $KEY_MATERIAL

dlYulSKD5cEG/XoAV8vv4QiQe/s3SlBzPY+PKgq92/0=

$ KEY_ID=$(ibmcloud kp key create rotate-example-key -i $KP_INSTANCE_ID --key-material $KEY_MATERIAL --output json | jq -r '.["id"]')

$ echo $KEY_ID

1604b4f3-6ba0-459c-8f65-400ed981a5eb

# step 2 - this request succeeds because there is no time
#          restriction when rotating the key the first time
$ KEY_MATERIAL_NEW_1=$(openssl rand -base64 32)

$ echo $KEY_MATERIAL_NEW_1

rK9CCRHxr8RpVvKQSEvud1zHAPnXl3PvhaPwx2aRxGE=

$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/rotate" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json" \
    -d '{
            "payload": "'$KEY_MATERIAL_NEW_1'"
        }'

# step 3 - this request fails because the key was
#          last rotated less than one hour ago
$ KEY_MATERIAL_NEW_2=$(openssl rand -base64 32)

$ echo $KEY_MATERIAL_NEW_2

pQX+ghaaH/r/s54ICWuwq3jQDPWlHQMDhAV0mwpBf2w=

$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/rotate" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json" \
    -d '{
            "payload": "'$KEY_MATERIAL_NEW_2'"
        }'
```
{: codeblock}

#### JSON response
{: #error-messages-key-rotation-not-permitted-context-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Conflict: Action could not be performed on key: Please see `reasons` for more details (KEY_ROTATION_NOT_PERMITTED)",
            "reasons": [
                {
                    "code": "KEY_ROTATION_NOT_PERMITTED",
                    "message": "This root key has been rotated within the last hour: Only one 'rotate' action per hour is permitted",
                    "status": 409,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect"
                }
            ]
        }
    ]
}
```
{: screen}

## 33 - This root key was created with user-supplied...
{: #error-messages-key-payload-req-err}

### Message
{: #error-messages-key-payload-req-err-message}

This root key was created with user-supplied key material: Key material is
required to perform a 'rotate' action

Reason code: KEY_PAYLOAD_REQ_ERR

### HTTP status code
{: #error-messages-key-payload-req-err-http}

400 - Bad Request

The HTTP `400 Bad Request` response status code indicates that the server cannot
or will not process the request due to something that is perceived to be a
client error (for example, malformed request syntax, invalid request message framing,
or deceptive request routing).

The client cannot repeat this request without modification.

### Context
{: #error-messages-key-payload-req-err-context}

If a root key was created with a key material (payload), then a key material
must be specified to rotate the key.

```sh
# step 1 - create a root key and provide a key material
$ KEY_MATERIAL=$(openssl rand -base64 32)

$ echo $KEY_MATERIAL

HpHM2YG9PMLBo4fZmV2WODZTTWlwaKmy496MoCE7w7U=

$ KEY_ID=$(ibmcloud kp key create rotate-example-key -i $KP_INSTANCE_ID --key-material $KEY_MATERIAL --output json | jq -r '.["id"]')

$ echo $KEY_ID

e52ee578-af71-4cd7-ba19-f1a8020d6a10

# step 2 - rotate the key without a new key material
$ curl -X POST \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys/$KEY_ID/actions/rotate" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.key_action+json"
```
{: codeblock}

#### JSON response
{: #error-messages-key-payload-req-err-context-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Bad Request: Action could not be performed on key: Please see `reasons` for more details (KEY_PAYLOAD_REQ_ERR)",
            "reasons": [
                {
                    "code": "KEY_PAYLOAD_REQ_ERR",
                    "message": "This root key was created with user-supplied key material: Key material is required to perform a 'rotate' action",
                    "status": 400,
                    "moreInfo": "https://cloud.ibm.com/apidocs/key-protect",
                    "target": {
                        "type": "field",
                        "name": "payload"
                    }
                }
            ]
        }
    ]
}
```
{: screen}

## 34 - Unauthorized: The user does not have...
{: #error-messages-unauthorized-err}

### Message
{: #error-messages-unauthorized-err-message}

Unauthorized: The user does not have access to the specified resource

Reason code: UNAUTHORIZED_ERR

### HTTP status code
{: #error-messages-unauthorized-err-http}

401 - Unauthorized

The HTTP `401 Unauthorized` client error status response code indicates that the
request has not been applied because it lacks valid authentication credentials
for the target resource.

This status is sent with a `WWW-Authenticate` header that contains information
on how to authorize correctly.

This status is similar to `403`, but in this case, authentication is possible.

### Context
{: #error-messages-unauthorized-err-context}

This error message is returned when the user does not have access to a resource.

This example applies an instance policy that limits access to a range of IP
addresses. When a request from outside the allowed range is received, it returns
an error.

```sh
# limit  access to a range of IP addresses
$ curl -X PUT \
    "https://us-south.kms.cloud.ibm.com/api/v2/instance/policies?policy=allowedIP" \
    -H "authorization: Bearer $ACCESS_TOKEN" \
    -H "bluemix-instance: $KP_INSTANCE_ID" \
    -H "content-type: application/vnd.ibm.kms.policy+json" \
    -d '{
            "metadata": {
                "collectionType": "application/vnd.ibm.kms.policy+json",
                "collectionTotal": 1
            },
            "resources": [
                {
                    "policy_type": "allowedIP",
                    "policy_data": {
                        "enabled": true,
                        "attributes": {
                            "allowed_ip": [
                                "65.128.226.252/24"
                            ]
                        }
                    }
                }
            ]
        }'
```

Retrieving keys will fail because the request is outside the allowed range of IP
addresses.

```sh
# this fails because the request is outside the allowed range of IP addresses
$ curl -X GET \
    "https://us-south.kms.cloud.ibm.com/api/v2/keys" \
    -H "authorization: Bearer $ACCESS_TOKEN"
    -H "bluemix-instance: $KP_INSTANCE_ID"
```
{: codeblock}

#### JSON response
{: #error-messages-unauthorized-err-context-json}

```json
{
    "metadata": {
        "collectionType": "application/vnd.ibm.kms.error+json",
        "collectionTotal": 1
    },
    "resources": [
        {
            "errorMsg": "Unauthorized: The user does not have access to the specified resource"
        }
    ]
}
```
