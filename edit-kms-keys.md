---

copyright:
  years: 2022
lastupdated: "2022-03-22"

keywords: Unified Key Orchestrator, edit keys, key management, kms keys, UKO

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


# Editing key details
{: #edit-kms-keys}

You can edit your keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI).
{: shortdesc}


## Editing key details through the UI
{: #edit-kms-keys-ui}

To edit the details of a managed key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key that you want to edit, and choose **Show details**.
4. In each property card under **Key properties**, click **Edit** to update the key properties. 

    You can update the general properties, lifecycle properties, or active period of the key. Or, you can also view the key material properties, including algorithm, length, and key check value. The following are a few properties that you can edit.
    
    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. Note that when you change the name of a managed key, the key is to be renamed in all target keystores that it is installed in. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | State                | Key states include _Pre-active_, _Active_, _Deactivated_, and _Destroyed_. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states) |
    | Activation date      | Plan a date to activate the key. No automatic state change is triggered. |
    | Expiration date      | Plan a date to deactivate the key. No automatic state change is triggered. |
    {: caption="Table 1. Key properties" caption-side="bottom"}

    You can edit one property card at a time. To make changes to another property card, save your changes first.
    {: note}

5. In the **Target keystores** card, you can also add or remove the target keystores that the key is installed in by clicking **Set target keystores**. You can only use a key for encryption for decryption after it is installed in at least one target keystore.
6. Under **Advanced properties**, click **Edit** to update or add new key tags to the key. Key tags are used as identifications of a key.
7. When you finish making changes, click **Save** to save the changes.

You can search for a specific key by using the search bar, or filter keys based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Managed keys** table. For more information, see [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
{: tip}



## What's next
{: #edit-kms-keys-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).
  
- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).
  
- To find out how to install an existing key to a keystore, check out [Setting target keystores for existing keys](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).

