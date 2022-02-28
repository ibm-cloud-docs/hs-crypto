---

copyright:
  years: 2022
lastupdated: "2022-02-28"

keywords: Unified Key Orchestrator, search keys, key management, kms keys

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


# Filtering and searching keys
{: #search-key-list}

You can filter and search for your managed keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI).
{: shortdesc}


## Filtering keys through the UI
{: #filter-key-list-ui}

To filter keys through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the table.
4. Specify the filter criteria as you need, and click **Apply**.
   
   You can set the following filter criteria.

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Vault                | The vault that controls access to the key.            |
    | Activation           | Set a date range of when you activate the key.  |
    | Expiration           | Set a date range of when you deactivate the key.  |
    | Creation             | Set a date range of when the key was created.             |
    | Keystores            | The keystores that the key is installed in.               |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Minimum key length   | The minimum number of bits that represents the encryption strength of the key.   |
    | Maximum key length   | The maximum number of bits that represents the encryption strength of the key.   |
    | State                | Key states include _Pre-active_, _Active_, _Deactivated_, and _Destroyed_. For more information, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). |
    {: caption="Table 1. Filter managed keys" caption-side="bottom"}


##  Searching for keys through the UI
{: #search-key-list-ui}

To search for a key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. To search for key name or description, type a word in the search bar.



## What's next
{: #search-key-list-next}

- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list).
  
- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).

- To find out how to install an existing key to a keystore, check out [Setting target keystores for existing keys](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).

