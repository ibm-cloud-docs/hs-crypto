---

copyright:
  years: 2020, 2023
lastupdated: "2023-02-08"

keywords: create test instance, configure api for test, test hpcs, test service onboarding hpcs, wrap key api, upwrap key api

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Setting up the {{site.data.keyword.hscrypto}} API
{: #configure-api-test}

Create a test instance and add code to use our wrap and unwrap API methods.
{: shortdesc}

## Before you begin
{: #configure-api-test-prereqs}

- You must have {{site.data.keyword.iamshort}} (IAM) enabled for your service. For questions and help with adoption, see the
[IAM onboarding guide](/docs/get-coding?topic=get-coding-getting-started-iam-onboarding-overview){: external} or the
[`#iam-adopters` Slack channel](https://ibm-cloudplatform.slack.com/archives/iam-adopters){: external}.
- You must have a basic understanding of IAM key concepts, such as [granting service to service access](/docs/get-coding?topic=get-coding-servicetoservice){: external}.
- You must have a basic understanding of the [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) process. See [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services) to learn how {{site.data.keyword.hscrypto}} integrates with
other cloud data services.

## Step 1. Create a test instance
{: #provision-instance-test}

First, create a test {{site.data.keyword.hscrypto}} instance so that you can set up the API. Normally, your customer is provisioning their own instance of a KMS-enabled service.

1. [Provision an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision)
2. [Retrieve an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID)

## Step 2. Create a root key
{: #create-root-key-test}

Next, create a [root key](/docs/hs-crypto?topic=hs-crypto-understand-concepts#root-key-concept) in your test instance. Root keys cover two main use cases:

- To protect encrypted data at rest with [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption). This process is done by using a root key to wrap and unwrap the data encryption keys (DEKs) that are stored in your service.
- To enable Keep Your Own Key (KYOK) capabilities for your service. Also called _customer-managed encryption_, this model enables support for user-provided root keys that the customer can manage in {{site.data.keyword.hscrypto}}.

You can programmatically create a root key in {{site.data.keyword.hscrypto}} by running the following command.

### Example request
{: #example-create}

```cURL
curl -X POST \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'content-type: application/vnd.ibm.kms.key+json' \
  -H 'correlation-id: <correlation_ID>' \
  -d '{
    "metadata": {
      "collectionType": "application/vnd.ibm.kms.key+json",
      "collectionTotal": 1
    },
    "resources": [
      {
        "type": "application/vnd.ibm.kms.key+json",
        "name": "<key_alias>",
        "description": "<key_description>",
        "extractable": false
      }
    ]
  }'
```
{: codeblock}

Replace the variables in the example request according to the following table.

| Variable | Description |
| --- | --- |
| `region` | **Required.** The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
| `port` | **Required.** The port number of the API endpoint. |
| `IAM_token` | **Required.** Your service to service access token. Include the full contents of the token, including the `Bearer` value, in the cURL request. |
| `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
| `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
| `key_alias` | **Required.** A unique, human-readable name for easy identification of your key. |
| `key_description` | An extended description of your key. |
{: caption="Table 1. Describes the variables needed to create a root key" caption-side="bottom"}

Verify that the key was created by running the following call to browse the keys in your {{site.data.keyword.hscrypto}} instance.

```cURL
curl -X GET \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'correlation-id: <correlation_ID>'
```
{: codeblock}

A successful response returns the ID value for the key, along with other metadata. The ID is a unique identifier that is assigned to the key and is used for subsequent calls to the {{site.data.keyword.hscrypto}} API.

Keep in mind that it is the customer's responsibility to add and centrally manage root keys in their {{site.data.keyword.hscrypto}} instance. As a integrated service, you can retrieve the key ID or key CRN values from your customer's instance by [listing the keys that are available in the specified instance](/apidocs/hs-crypto#getkeys).
{: note}

## Step 3. Wrap a data encryption key
{: #wrap-key-test}

You can use the returned root key ID to wrap a data encryption key (DEK). For each service that adopts {{site.data.keyword.hscrypto}}, the DEK will be different. For example, the DEK might be a LUKS passphrase or an actual AES key. To protect the DEK with the root key, use the wrap API.

Note: As an alternative, we can also generate the DEK for you.

### Example request
{: #example-wrap}

```cURL
curl -X POST \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/wrap \
  -H 'accept: application/vnd.ibm.kms.key_action+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'content-type: application/vnd.ibm.kms.key_action+json' \
  -H 'correlation-id: <correlation_ID>' \
  -H 'prefer: return=minimal' \
  -d '{
    "plaintext": "<data_key>"
  }'
```
{: codeblock}

Replace the variables in the example request according to the following table.

| Variable | Description |
| --- | --- |
| `region` | **Required.** The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
| `port` | **Required.** The port number of the API endpoint. |
| `key_ID` | **Required.** The unique identifier for the root key that you want to use for wrapping. |
| `IAM_token` | **Required.** Your service to service access token. Include the full contents of the token, including the `Bearer` value, in the cURL request. |
| `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
| `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
| `data_key` | The key material of the DEK that you want to manage and protect. The `plaintext` value must be base64 encoded. To generate a new DEK, omit the `plaintext` attribute. The service generates a random plaintext (32 bytes) and wraps that value. In the response, `plaintext` contains the unwrapped DEK and `ciphertext` contains the wrapped value. |
{: caption="Table 2. Describes the variables needed to wrap a specified key" caption-side="bottom"}

The wrapped data encryption key (wDEK), containing the base64 encoded key material, is returned in the response entity-body. The following JSON object shows an example returned value.

### Note
{: #note-wdek}

wDEKs are not stored in the {{site.data.keyword.hscrypto}} service.

```json
{
  "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
  "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
}
```
{: screen}

## Step 4. Unwrap a data encryption key
{: #unwrap-key-test}

To unwrap a data encryption key (DEK), provide the wDEK (the `ciphertext` value) in your unwrap request to {{site.data.keyword.hscrypto}}. To ensure that your unwrap request succeeds, provide the same root key that you used during the initial wrap request.

### Example request
{: #example-unwrap}

```cURL
curl -X POST \
  https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=unwrap \
  -H 'accept: application/vnd.ibm.kms.key_action+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'content-type: application/vnd.ibm.kms.key_action+json' \
  -H 'correlation-id: <correlation_ID>' \
  -H 'prefer: return=minimal' \
  -d '{
    "ciphertext": "<wrapped_data_key>",
  }'
```
{: codeblock}

Replace the variables in the example request according to the following table.

| Variable | Description |
| --- | --- |
| `region` | **Required.** The region abbreviation, such as `us-south` or `au-syd`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
| `port` | **Required.** The port number of the API endpoint. |
| `key_ID` | **Required.** The unique identifier for the root key that you used for wrapping. |
| `IAM_token` | **Required.** Your service to service access token. Include the full contents of the token, including the `Bearer` value, in the cURL request. |
| `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
| `correlation_ID` | The unique identifier that is used to track and correlate transactions. |
| `wrapped_data_key` | **Required.** The `ciphertext` value returned during a wrap operation. |
{: caption="Table 3. Describes the variables needed to unwrap keys" caption-side="bottom"}

The original base64 encoded key material is returned in the response entity-body. The following JSON object shows an example returned value.

```json
{
  "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg=="
}
```
{: screen}

## Next steps
{: #configure-api-test-next-steps}

Your service now supports envelope encryption, which is one of the core capabilities needed. Now, you can map your protected resources to the root key.

- Head over to start [key registration](/docs/hs-crypto?topic=hs-crypto-register-protected-resources)
