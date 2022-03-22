---

copyright:
  years: 2022
lastupdated: "2022-03-22"

keywords: Unified Key Orchestrator, delete key, key management, kms key, UKO

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
{:term: .term}


# Deleting managed keys
{: #delete-managed-keys}

You can delete your managed keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI).
{: shortdesc}

When you delete a managed key, the key is to be uninstalled from all target keystores and all key materials and the metadata are destroyed permanantly.


## Deleting managed keys through the UI
{: #delete-managed-keys-ui}

To delete a key in _Active_ state, you need to first deactivate the key, and then destroy the key and remove it from the vault. 

To delete a key in _Pre-active_ or _Deactivated_ state, you only need to destroy the key and then remove it from the vault.

For more information about key states and transitions, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states).

Follow these steps to complete the process:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. If the managed key that you want to delete is in _Active_ state, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Deactivated** to deactivate the key first.

   When you change the _Active_ key to _Deactivated_ state, the key is uninstalled from all the target keystores, and not accessible to all associated resources and their data. However, you can still reactivate the key so that it is accessible to the resources again.
    {: note}

4. To destroy a _Pre-active_ or _Deactivated_ key, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Destroyed**.
    
    When you destroy a managed key, the key cannot be restored in {{site.data.keyword.uko_full_notm}}. However, you can still restore your keys in external keystores depending on the settings of the cloud providers. For more information, see [Azure Key Vault soft-delete overview](https://docs.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview){: external}, [Deleting AWS KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/deleting-keys.html){: external}, or [Deleting and purging keys in {{site.data.keyword.keymanagementserviceshort}}](/docs/key-protect?topic=key-protect-delete-purge-keys){: external}.
    {: important}

5. Click **Destroy key** to confirm.
6. To remove the key and the metadata from the vault, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Remove from vault**.
   
   When you remove the managed key from the vault that the key is assigned to, the remaining key metadata is removed permanantly. 
    {: important}

The managed key has been deleted and uninstalled from all target keystores. All key materials and metadata have been destroyed. 



## What's next
{: #delete-managed-keys-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).
  
- To find out how to delete an internal keystore, check out [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).


