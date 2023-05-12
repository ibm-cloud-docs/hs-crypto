---

copyright:
  years: 2022, 2023
lastupdated: "2023-05-12"

keywords: Unified Key Orchestrator, UKO keystore, delete keystore, internal keystore, KMS keystore

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Deleting internal keystores
{: #delete-internal-keystores}

You can delete internal keystores in {{site.data.keyword.uko_full_notm}} with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API. After you delete an internal keystore, all the managed keys are deactivated in this keystore and associated resources are detached.
{: shortdesc}

To delete an internal keystore, [delete all activated keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys) in this keystore first. The key metadata remains in the keystore for 90 days before it gets removed automatically. You can delete the keystore only after the key metadata gets removed. If you want to delete the keystore immediately, [manually remove all key metadata using the KMS API](/apidocs/hs-crypto#purgekey){: external} in 4 hours after you destroy the key. Make sure that you have the **KMS Key Purge** role assigned. For more information about roles, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-uko-manage-access). 
{: note}

## Deleting internal keystores with the {{site.data.keyword.cloud_notm}} console
{: #delete-internal-keystores-ui}
{: ui}

To delete an internal keystore by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the keystore that you want to delete. The side panel is displayed.
4. Click **Delete** to delete the keystore and all the metadata. 
5. Click **Delete keystore** to confirm the deletion.


The internal keystore has been deleted with all the managed keys deactivated in this keystore and associated resources detached.


<key-template>
The internal keystore has been deleted with all the managed keys deactivated and key templates detached. You will no longer be able to access any metadata associated with the keystore. 
</ket-template>

## Deleting internal keystores with the API
{: #delete-internal-keystores-api}
{: api}

To delete an internal keystore through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Delete an internal keystore by making a `DELETE` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/keystores/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your keystore.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#delete-keystore){: external}.



## What's next
{: #delete-internal-keystores-next}

- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
  
- To find out instructions on editing an internal keystore, check out [Editing internal keystores](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).

