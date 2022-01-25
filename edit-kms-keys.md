---

copyright:
  years: 2022
lastupdated: "2022-01-25"

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

You can edit your keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}


## Editing key details through the UI
{: #edit-kms-keys-ui}

You can edit both internal and external keys through the UI.

### Editing internal key details through the UI
{: #edit-internal-keys-ui}

To edit the details of an internal KMS key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key that you want to edit, and choose **Show details**.
4. Under **Key properties**, click **Edit** to update the general properties, lifecyle properties, or active period of the key. You can also see the key material properties, including algorithm, length, and key check value.

    You can edit the following key properties.
    
    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key, with 2 - 100 characters in length. |
    | Description          | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | State                | _Pre-active_ keys are not to be installed in target keystores until they are activated. _Active_ keys are to be automatically installed in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states) |
    | Activation date      | (For _Pre-active_ keys) Set the date when the _Pre-active_ key gets activated. You can also manually activate the key later. |
    | Deactivation date    | (Optional) Set the date when the key gets expired. After the expiration date, the key moves into the _Deactivated_ state. |
    {: caption="Table 1. Key properties" caption-side="bottom"}

    You can edit one section at a time. To make changes to another section, save your changes first.
    {: note}

5. Under **Advanced properties**, click **Edit** to update or add new key tags to the key. Key tags are used as identifications of a key.
6. When you finish making changes, click **Save** to save the changes.

You can search for a specific key by using the search bar, or filter keys based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Managed keys** table. For more information, see [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
{: tip}


### Editing external key details through the UI
{: #edit-external-keys-ui}




## Editing key details with the API
{: #edit-kms-keys-api}


## What's next
{: #edit-kms-keys-next}

- To find out instructions on creating a key, check out [Creating internal keys](/docs/hs-crypto?topic=hs-crypto-create-internal-keys) or [Creating and storing external keys](/docs/hs-crypto?topic=hs-crypto-create-external-keys).
  
- To find out instructions on deleting a key, check out [Deleting internal keys](/docs/hs-crypto?topic=hs-crypto-delete-internal-keys) or [Deleting external keys](/docs/hs-crypto?topic=hs-crypto-delete-external-keys).
  
- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
