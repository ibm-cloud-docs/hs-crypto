---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

keywords: set up API, use key management API, use KMS API, access Hyper Protect Crypto Services API, access KMS API

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}

# Setting up the APIs
{: #set-up-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a key management API to store, retrieve, and generate encryption keys.
{: shortdesc}

## Retrieving your IBM Cloud credentials
{: #retrieve_credentials}

To work with the APIs, you need to generate your service and authentication credentials. To gather your credentials:

1. [Generate an {{site.data.keyword.cloud_notm}} IAM access token](/docs/services/hs-crypto?topic=hs-crypto-retrieve-access-token).
2. [Retrieve the instance ID that uniquely identifies your {{site.data.keyword.hscrypto}} service instance](/docs/services/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

## Forming your key management API request
{: #form-kms-api-request}

When you make an API call to the service, structure your API request according to how you initially provisioned your instance of {{site.data.keyword.hscrypto}}.

To build your request, pair a [regional service endpoint](/docs/services/hs-crypto?topic=hs-crypto-regions) with the appropriate authentication credentials. For example, if you created a service instance for the `us-south` region, use the following endpoint and API headers to browse keys in your service:

```cURL
curl -X GET \
    https://api.us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>'
```
{: codeblock}

* Replace `<port>` with the port number of your API endpoint. You can get the `<port>` from the **Manage** tab of your provisioned service instance dashboard or by dynamically [retrieving the API endpoint URL](https://{DomainName}/apidocs/hs-crypto#retrieve-the-api-endpoint-url){: external}. The returned value includes:

  ```
  {
    "instance_id": "<instance_ID>",
    "APIConnectInfo": api.<region>.hs-crypto.cloud.ibm.com:<port>",
  ```
  {: screen}
For the key management service, use the <port> in `https://api.<region>.hs-crypto.cloud.ibm.com:<port>` in the `kms` section.

* Replace `<access_token>` and `<instance_ID>` with your retrieved service and authentication credentials.

Want to track your API requests in case something goes wrong? When you include the `-v` flag as part of cURL request, you get a `correlation-id` value in the response headers. You can use this value to correlate and track the request for debugging purposes.
{: tip}

## What's next
{: #set-up-api-next-steps}

You're all set to start managing your encryption keys and data. To find out more about programmatically managing your keys, [check out the key management API reference doc](https://{DomainName}/apidocs/key-protect){: external}.
