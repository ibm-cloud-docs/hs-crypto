---

copyright:
  years: 2022
lastupdated: "2022-01-18"

keywords: Unified Key Orchestrator, view keys, key management, kms keys

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


# Viewing a list of keys
{: #view-key-list}

You can view a list of your internal keys and external keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}


## Viewing a list of keys through the UI
{: #view-key-list-ui}

To view a list of your keys through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** on the left navigation pane to view all the available keys.
3. Browse the general characteristics of your keys in the table:

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Name                 | The unique, human-readable name that is assigned to your key. |
    | Vault                | The vault that controls the access to the key.           |
    | State                | Key states include _Pre-active, Active, Deactivated,_ and _Destroyed._ For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external} |
    | Activation date      | The date when the key gets activated. A _Pre-active_ key is to be activated on the activation date. |
    | Deactivation date    | The date when the key gets expired. After the expiration date, the key automatically moves into the _Deactivated_ state. |
    | Last updated         | The date and time that the key was last updated. This field gets updated when the key is created, rotated, or any part of the key metadata is modified.        |
    | Keystore type        | The type of keystore that the key can be assigned to.     |
    | Target keystores     | The keystores that the key is installed in.               |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    {: caption="Table 1. Managed keys table" caption-side="bottom"}



## Viewing a list of keys with the API
{: #view-key-list-api}





## What's next
{: ##view-key-list-next}

- To find out how to create a new key, check out [Creating internal keys](/docs/hs-crypto?topic=hs-crypto-create-internal-keys) or [Creating external keys](/docs/hs-crypto?topic=hs-crypto-create-external-keys).

- To find out more about managing your keys, check out [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list) or [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).


