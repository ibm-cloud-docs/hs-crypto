---

copyright:
  years: 2022
lastupdated: "2022-02-11"

keywords: Unified Key Orchestrator, install keys, key management, kms keys

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


# Installing existing keys to keystores
{: #install-key-keystores}

You can use a managed key for encryption and decryption only after it is installed in at least one keystore. You can install existing keys in {{site.data.keyword.uko_full_notm}} to target keystores through the user interface (UI), or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}


## Installing existing keys to keystores through the UI
{: #install-key-keystores-ui}

To install an existing key to target keystores through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key that you want to edit, and choose **Show details**.
4. Click **Set target keystores**.
5. Select one or multiple target keystores that you want to install the key in. Installing a key in multiple keystores enables redundancy.
   
   If you want to install the key to a new keystore, click **Add keystore**. For more instructions, see [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
   
6. Click **Save** to save the changes.



## Installing existing keys to keystores with the API
{: #install-key-keystores-api}




## What's next
{: #install-key-keystores-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-internal-keys).
  
- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  
- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).


