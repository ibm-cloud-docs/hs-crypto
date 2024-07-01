---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-01"

keywords: Unified Key Orchestrator, vaults, keys, keystores, key management, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Deleting vaults
{: #delete-vaults}

You can delete your vaults in {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

 
If you want to delete a vault, you need to delete all managed keys, delete or archive all key templates, and delete or disconnect from all keystores that are managed in the vault first. The Delete function is available for empty vaults only. Make sure to have an empty vault by referring to the following instructions:  
- To delete managed keys, see [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys&interface=ui).
- To delete or archive all key templates, see [Deleting key templates](/docs/hs-crypto?topic=hs-crypto-delete-template&interface=ui) and [Archiving and unarchiving key templates](/docs/hs-crypto?topic=hs-crypto-archive-template&interface=ui). 
- To delete or disconnect from all keystores, see [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores) and [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores). 
{: note}


## Deleting vaults with the UI
{: #delete-vaults-ui}
{: ui}

 
By deleting a vault, access groups that are assigned to this vault can no longer access the vault.
{: important}

To delete a vault by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. Click the vault that you want to delete. The Details side panel is displayed.
4. Make sure that the vault does not contain any key templates, keys, or keystores, and then click **Delete**.
    
     
    If any archived key templates are assigned to this vault, the archived key templates are also deleted with the vault. 
    {: note}
    
5. Click **Delete vault** to confirm the deletion.

The vault has been deleted and removed from the vault list. Access groups that are assigned to this vault no longer have access to the vault.


## Deleting vaults with the API
{: #delete-vaults-api}
{: api}

To delete a vault through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with vaults in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Delete a vault by making a `DELETE` call to the following endpoint.

    

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/vaults/<vault_id>
    
    ```
    {: codeblock}

    Replace `<vault_id>` with the ID of your vault.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#delete-vault){: external}.



## What's next
{: #delete-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).
  
- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).
  
- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

