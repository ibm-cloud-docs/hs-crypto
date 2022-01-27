---

copyright:
  years: 2022
lastupdated: "2022-01-27"

keywords: Unified Key Orchestrator, delete key, key management, kms key, UKO

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}


# Deleting internal keys
{: #delete-internal-keys}

You can delete your internal KMS keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API. 
{: shortdesc}

When you delete an internal key, the key is to be uninstalled from all target keystores and all key materials and its metadata are destroyed permenantly.

Currently, if dual authorization is enabled for key, the key cannot be deleted.
{: note}



## Deleting internal keys through the UI
{: #delete-internal-keys-ui}

To delete a key in _active_ state, you need to first deactivate the key, and then destroy the key and remove it from the vault. 

To delete a key in _pre-active_ or _deactivated_ state, you only need to destroy the key and then remove it from the vault.

For more information about key states and transitions, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states).

Follow these steps to complete the process:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. If the key that you want to delete is in _active_ state, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Deactivated** to deactivate the key first.

   When you change the _active_ key to _deactivated_ state, the key is uninstalled from all the target keystores, and all associated {{site.data.keyword.cloud_notm}} resources are not accessible.
    {: important}

4. To destroy a _pre-active_ or _deactivated_ key, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Destroyed**.
    
    When you destroy the key, the key material is destroyed permenantly. 
    {: important}

5. Click **Destroy key** to confirm.
6. To remove the key and the metadata from the vault, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Remove from vault**.
   
   When you remove the key from the vault that the key is assigned to, the remaining key metadata is removed permenantly. 
    {: important}

The internal key has been deleted and uninstalled from all target keystores. All key materials and metadata have been destroyed. 


## Deleting internal keys with the API
{: #delete-internal-keys-api}




## What's next
{: #delete-internal-keys-next}

- To find out instructions on creating a key, check out [Creating internal keys](/docs/hs-crypto?topic=hs-crypto-create-internal-keys) or [Creating and storing external keys](/docs/hs-crypto?topic=hs-crypto-create-external-keys).
  
- To find out how to delete an internal keystore, check out [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
