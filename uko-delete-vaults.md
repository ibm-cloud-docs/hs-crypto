---

copyright:
  years: 2022, 2023
lastupdated: "2023-06-26"

keywords: Unified Key Orchestrator, vaults, keys, keystores, key management, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Deleting vaults
{: #delete-vaults}

You can delete your vaults in {{site.data.keyword.uko_full_notm}} with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}


If you want to delete a vault, you need to delete all managed keys, and delete or disconnect from all target keystores that are managed in the vault first. The Delete function is available for empty vaults only. For detailed instructions, see [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-keys), [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores), and [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).
{: note}




## Deleting vaults with the {{site.data.keyword.cloud_notm}} console
{: #delete-vaults-ui}
{: ui}

By deleting a vault, access groups that are assigned to this vault can no longer access the vault.
{: important}

To delete a vault by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. Click the vault that you want to delete. The Details side panel is displayed.
4. Make sure that the vault does not contain any keys or keystores, and then click **Delete**.
  
5. Click **Delete vault** to confirm the deletion.

The vault has been deleted and removed from the vault list. Access groups that are assigned to this vault no longer have access to the vault.


## Deleting vaults with the API
{: #delete-vaults-api}
{: api}

To delete a vault through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with vaults in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Delete a vault by making a `DELETE` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/vaults/<vault_id>
    ```
    {: codeblock}

    Replace `<vault_id>` with the ID of your vault.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#delete-vault){: external}.



## What's next
{: #delete-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).
  
- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).
  
- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

