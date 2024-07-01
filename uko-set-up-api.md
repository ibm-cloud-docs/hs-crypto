---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-01"

keywords: set up api, uko api, Unified Key Orchestrator api, 

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Setting up {{site.data.keyword.uko_full_notm}} API calls - {{site.data.keyword.uko_full_notm}} Plan
{: #set-up-uko-api}


You can use [{{site.data.keyword.uko_full_notm}} API](/apidocs/uko){: external} to create, retrieve, and destroy key templates, keys and keystores in the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} for {{site.data.keyword.uko_full_notm}}.
{: shortdesc}


Setting up {{site.data.keyword.uko_full_notm}} API calls only applies to the {{site.data.keyword.uko_full_notm}} Plan.
{: note}

When you use the {{site.data.keyword.uko_full_notm}} API to create IBM Cloud KMS keys that are installed in internal KMS keystores, these keys are root keys and can be used for [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption). You can also use the [key management service API](/apidocs/hs-crypto){: external} to create internal IBM Cloud KMS keys and perform actions towards keys. 

## Retrieving your IBM Cloud credentials
{: #retrieve-uko-credentials}

To work with the API, you need to generate your service and authentication credentials. Complete the following steps to gather your credentials:

1. [Generate an {{site.data.keyword.cloud_notm}} IAM access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).

2. [Retrieve the instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID) that uniquely identifies your {{site.data.keyword.hscrypto}} instance.

## Forming your {{site.data.keyword.uko_full_notm}} API request
{: #form-uko-api-request}

When you make an API call to the service, structure your API request according to how you initially provisioned your instance of {{site.data.keyword.hscrypto}}.

To build your request, pair a [regional service endpoint](/docs/hs-crypto?topic=hs-crypto-regions) with the appropriate authentication credentials. For example, if you created a service instance for the `us-south` region, use the following endpoint and API headers to browse keys in your service:

If you create your instances after April 12 2024 in certain regions, you might need to use the new API endpoints with the new format as `<instance_ID>.ep11.<REGION>.hs-crypto.appdomain.cloud`. The availability date varies by region. For more information about the supported regions, the availability dates, and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).
{: note}
 



```cURL 
curl --location --request GET 'https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/managed_keys' \
    --header 'Authorization: Bearer <access_token>' \ 
    --header 'Content-Type: application/json' \
    --header 'Accept: application/json' \ 
    --header 'UKO-Vault: <vault_id>'
```
{: codeblock}

* Replace `<region>` and `<instance_ID>` with the region and port number of your API endpoint. You can get the `<region>` and `<instance_ID>` in your provisioned service instance UI dashboard through **Overview** &gt; **{{site.data.keyword.uko_full_notm}} endpoint URL**. Or, you can dynamically [retrieve the API endpoint URL](/apidocs/uko#endpoint-urls){: external}. 

    Note that the port range of a {{site.data.keyword.hscrypto}} instance is between `8000` - `19999`.

* Replace `<access_token>` with your retrieved service and authentication credentials.
* Replace `<vault_id>` with the ID of the vault that your keys are assigned to.

Want to track your API requests in case something goes wrong? When you include the `-v` flag as part of cURL request, you get a `correlation-id` value in the response headers. You can use this value to correlate and track the request for debugging purposes.
{: tip}


## What's next
{: #set-up-uko-api-next-steps}

You're all set to start managing your encryption keys and data. To find out more about programmatically managing your keys, check out the [Unified Key Orchestrator API reference doc](/apidocs/uko){: external}.
