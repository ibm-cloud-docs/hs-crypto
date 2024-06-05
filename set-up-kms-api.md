---

copyright:
  years: 2018, 2024
lastupdated: "2024-06-04"

keywords: set up api, kms api, key protect api, key management service API, using api

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Managing your keys with the key management service API
{: #set-up-kms-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides a [key management service API](/apidocs/hs-crypto){: external} to store, retrieve, and generate encryption keys.
{: shortdesc}

## Retrieving your IBM Cloud credentials
{: #retrieve-kms-credentials}

To work with the API, you need to generate your service and authentication credentials. To gather your credentials:

1. [Generate an {{site.data.keyword.cloud_notm}} IAM access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
2. [Retrieve the instance ID that uniquely identifies your {{site.data.keyword.hscrypto}} service instance](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

## Forming your key management service API request
{: #form-kms-api-request}

When you make an API call to the service, structure your API request according to how you initially provisioned your instance of {{site.data.keyword.hscrypto}}.

To build your request, pair a [regional service endpoint](/docs/hs-crypto?topic=hs-crypto-regions) with the appropriate authentication credentials. For example, if you created a service instance for the `us-south` region, use the following endpoint and API headers to browse keys in your service:

 

{{site.data.keyword.hscrypto}} is continuously replacing port-based API endpoints with instance-based API endpoints. For example, for public key management endpoint URLs, the format is changed from `api.<region>.hs-crypto.cloud.ibm.com:<port>` to `<instance_ID>.api.<region>.hs-crypto.appdomain.cloud`. For a complete list of the endpoint URL schemes and more information about which regions now support instance-based endpoint URLs, see [Instance-based endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints). Note that, for any new service instances created after the dates specified in the table, only instance-based endpoint URLs can be applied. No impact to existing service instances is expected, as the current port-based endpoint scheme stays intact for the time being. However, it is suggested to use the new instance-based scheme wherever possible especially for new projects.
{: note}
 


```cURL
curl -X GET \
    https://<INSTANCE_ID>.api.us-south.hs-crypto.appdomain.cloud/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>'
```
{: codeblock}

* Replace `<port>` with the port number of your API endpoint. You can get the `<port>` in your provisioned service instance dashboard through **Overview** &gt; **Key management endpoint URL**. Or, you can dynamically [retrieve the API endpoint URL](/apidocs/hs-crypto#getinstance){: external}. 
    
    Note that the port range of a {{site.data.keyword.hscrypto}} instance is between `8000` - `19999`.
    
    The returned value includes:
    
    ```
    {
      "instance_id": "<instance_ID>",
      "kms": {
        "public": "<instance_ID>.api.<region>.hs-crypto.appdomain.cloud",
        "private":"<instance_ID>.api.private.<region>.hs-crypto.appdomain.cloud"
      },
        "ep11": {
        "public": "<instance_ID>.ep11.<region>.hs-crypto.appdomain.cloud",
        "private":"<instance_ID>.ep11.private.<region>.hs-crypto.appdomain.cloud"
      }
    }
    ```
    {: screen}

    For the key management service, use the `<region>` and `<instance_ID>` in the `kms` section.

* Replace `<access_token>` and `<instance_ID>` with your retrieved service and authentication credentials.

Want to track your API requests in case something goes wrong? When you include the `-v` flag as part of cURL request, you get a `correlation-id` value in the response headers. You can use this value to correlate and track the request for debugging purposes.
{: tip}


## What's next
{: #set-up-kms-api-next-steps}

You're all set to start managing your encryption keys and data. To find out more about programmatically managing your keys, [check out the key management service API reference doc](/apidocs/hs-crypto){: external}.
