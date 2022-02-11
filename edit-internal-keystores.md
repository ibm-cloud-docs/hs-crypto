---

copyright:
  years: 2022
lastupdated: "2022-02-11"

keywords: Unified Key Orchestrator, UKO keystore, edit keystore, key management, internal keystore, KMS keystore

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


# Editing internal keystores
{: #edit-internal-keystores}

You can edit your internal keystores in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

## Editing internal keystores through the UI
{: #edit-internal-keystores-ui}

To edit the details of an internal KMS keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the internal keystore that you want to edit. The Details side panel is displayed.
4. Click **Edit** to update the **Keystore name** and **Description**. 
   
   You can filter and search the keys that are assigned to this keystore, but you cannot edit key details or change key states from the side panel. To edit the details of the keys, see [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
   {: tip}

5. Click **Save** to save the changes.




## Editing internal keystores with the API
{: #edit-internal-keystores-api}






## What's next
{: #edit-internal-keystores-next}

- To find out instructions on adding an internal keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores).

- To find out how to delete an internal keystore, check out [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores).

- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).