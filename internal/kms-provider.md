---

copyright:
  years: 2018, 2021
lastupdated: "2021-04-26"

keywords: hyper protect crypto services integration, kms provider, set up kms provider

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}

{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}

# Working with {{site.data.keyword.cloud_notm}} KMS provider services
{: #kms-providers}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is a public, single-tenant key management service (KMS) that provides KMS functionality for {{site.data.keyword.cloud_notm}}. As support for dedicated and private KMS environments becomes available, Bring Your Own Key (BYOK) adopting teams can integrate their services directly to {{site.data.keyword.cloud_notm}} KMS providers to offer tailored KMS experiences for cloud customers.
{: shortdesc}

## List of {{site.data.keyword.cloud_notm}} KMS providers
{: #kms-providers-list}

Teams can integrate to the following list of KMS providers:

| KMS provider | Environment type |
| -- | -- |
| [{{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-getting-started-tutorial) | Public, multi-tenant KMS with cloud-based HSM |
| {{site.data.keyword.hscrypto}}| Dedicated KMS with cloud-based HSM |
| {{site.data.keyword.keymanagementserviceshort}} for [{{site.data.keyword.cloud_notm}} Private](https://www.ibm.com/support/knowledgecenter/SSBS6K/product_welcome_cloud_private.html) | Private KMS with on-premises HSM |



To integrate with a KMS provider, adopting teams must modify how their service discovers KMS instances for a given user so that the corresponding KMS endpoints are found dynamically, without needing to hardcode to the {{site.data.keyword.hscrypto}} public API.

In turn, KMS providers need to register their services appropriately and provide additional information to the resource controller to make themselves and their instances easily discoverable by the adopting teams.

## Setting up your service as a KMS provider
{: #set-up-kms-provider}

To designate a service as a KMS provider, teams can modify the resource catalog entry for their offering so that the resource controller identifies the service by its `sub_type` field.

With this change, teams that want to integrate with a KMS provider can search for all KMS instances that belong to a given user by specifying the `sub_type` value in the [Global Search and Tagging (GhoST)](/docs/get-coding?topic=get-coding-ghost_overview) service.

### Updating the catalog entry
{: #update-catalog}

You can use the [{{site.data.keyword.cloud_notm}} resource catalog API](https://{DomainName}/apidocs/globalcatalog) to update the catalog entry for your offering, and then designate your service as a KMS provider.

To set up your service as a KMS provider:

1. In the [resource catalog](https://globalcatalog.cloud.ibm.com), search the name of your offering to inspect its catalog entry.
2. From the _Overview_ tab, note the ID value that uniquely identifies your offering in the resource catalog service.
3. Use the catalog ID to retrieve the JSON representation of the catalog entry for your offering.

    ```cURL
    curl -s 'https://globalcatalog.cloud.ibm.com/api/v1/<catalog_entry_ID>?complete=true' > catalog_entry.json
    ```
    {: codeblock}

    Replace `<catalog_entry_ID>` with the value that you retrieved in the previous step. Then, open the `catalog_entry.json` file to inspect the details about your offering.

4. In `catalog_entry.json` file, search for the `metadata.service.type` field, and then specify `kms` as its value.
5. Update the catalog entry for your offering by calling the resource catalog API.

    ```cURL
    curl -X PUT
      https://globalcatalog.cloud.ibm.com/api/v1/<catalog_entry_ID>
      -H 'Content-Type: application/json'
      -H 'Authorization: Bearer <token>'
      -d @catalog_entry.json
    ```
    {: codeblock}

    Replace `<catalog_entry_ID>` with the value that you retrieved in step 2.

### Updating your broker
{: #update-broker}

Update your broker so that it returns the following details to the [resource controller](/docs/get-coding?topic=get-coding-resource-controller) when it invokes your service instance creation API.

```
{
    "dashboard_url": "<your dashboard url>",
    "extensions": {
        "endpoints": {
            "public": "<public endpoint for the instance>",
            "private": "<optional - private network endpoint for the instance>"
        }
    }
}
```
{: codeblock}

This information is passed by the resource controller to [Global Search and Tagging (GhoST)](/docs/get-coding?topic=get-coding-ghost_overview) for indexing as part of the instance entry metadata.

## Integrating with KMS provider services
{: #integrate-kms-provider}

If your offering wants to integrate with an existing KMS provider service, your team can search for all KMS instances that are associated with a given user by specifying `sub_type` instead of service name. This is done by querying Global Search and Tagging (GhoST).

```cURL
curl -X POST
    'https://api.global-search-tagging.cloud.ibm.com/v2/resources/search?limit=50&account_id=<account_ID>'
    -H 'Authorization: Bearer <token>'
    -H 'Content-Type: application/json'
    -d '{
        "query": "(type:resource-instance AND doc.sub_type:kms)"
    }'
```
{: codeblock}

Calling the GhoST API does not require special access. For example, you can create your {{site.data.keyword.hscrypto}} instances by using a user token, and then use the same token to run your query in GhoST.
{: tip}

The following JSON output shows an example service instance. From the response, adopting teams can see which endpoint hosts a particular KMS service instance.

```json
{
    ...,
    "doc": {
        ...,
        "id": "crn:v1:public:hscrypto:us-south:a/80e35ac1582a2b1a7b633e6107f9295a:67be47c6-cac0-415d-b298-0e6d45d6cb51::",
        "sub_type": "kms",
        "extensions": {
            ...,
            "endpoints": {
                "public": "<public endpoint for the instance>",
                "private": "<optional - private network endpoint for the instance>"
            }
        },
        ...
    },
    ...
}
```
{: codeblock}
