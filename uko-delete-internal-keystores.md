---

copyright:
  years: 2022, 2024
lastupdated: "2024-06-05"

keywords: Unified Key Orchestrator, UKO keystore, delete keystore, internal keystore, KMS keystore

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Deleting internal keystores
{: #delete-internal-keystores}

You can delete internal keystores in {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API. After you delete an internal keystore, all the managed keys are deactivated in this keystore， and associated resources are unlinked.
{: shortdesc}

To delete an internal keystore, [delete all activated keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys) in this keystore first. The key metadata remains in the keystore for 90 days before it gets removed automatically. You can delete the keystore only after the key metadata gets removed. If you want to delete the keystore immediately, [manually remove all key metadata using the KMS API](/apidocs/hs-crypto#purgekey){: external} in 4 hours after you destroy the key. Make sure that you have the **KMS Key Purge** role assigned. For more information about roles, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-uko-manage-access). However, if the keystore is still on the distribution list of any key templates, you can still delete the keystore.
{: note}

## Deleting internal keystores with the UI
{: #delete-internal-keystores-ui}
{: ui}

To delete an internal keystore by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Keystores** from the navigation to view all the available keystores.
3. Click the keystore that you want to delete. The side panel is displayed.
4. Click **Delete** to delete the keystore and all the metadata. 
5. Click **Delete keystore** to confirm the deletion.


The internal keystore has been deleted with all the managed keys deactivated and key templates unlinked. You will no longer be able to access any metadata associated with the keystore. 





## Deleting internal keystores with the API
{: #delete-internal-keystores-api}
{: api}

To delete an internal keystore through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keystores in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Delete an internal keystore by making a `DELETE` call to the following endpoint.

    {{site.data.keyword.hscrypto}} is continuously replacing port-based API endpoints with instance-based API endpoints. For example, for public {{site.data.keyword.uko_full_notm}} endpoint URLs, the format is changed from `uko.<region>.hs-crypto.cloud.ibm.com:<port>` to `<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud`. For a complete list of the endpoint URL schemes and more information about which regions now support instance-based endpoint URLs, see [Instance-based endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints). Note that, for any new service instances created after the dates specified in the table, only instance-based endpoint URLs can be applied. No impact to existing service instances is expected, as the current port-based endpoint scheme stays intact for the time being. However, it is suggested to use the new instance-based scheme wherever possible especially for new projects.
    {: note}
     

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/keystores/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your keystore.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#delete-keystore){: external}.



## What's next
{: #delete-internal-keystores-next}

- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
  
- To find out instructions on editing an internal keystore, check out [Editing internal keystores](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).

