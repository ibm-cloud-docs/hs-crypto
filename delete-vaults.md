---

copyright:
  years: 2022
lastupdated: "2022-01-19"

keywords: Unified Key Orchestrator, vaults, keys, keystore, key management

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


# Deleting vaults
{: #delete-vaults}

You can delete your vaults in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}


## Deleting vaults through the UI
{: #delete-vaults-ui}

Before you delete a vault, make sure that you delete all the managed keys, and delete or disconnect from all the target keystores in the vault.
{: note}

To delete a vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. Click the vault that you want to delete to open the side panel.
4. Make sure that the vault does not contain any keys or keystores, and then click **Delete**.
5. Click **Delete vault** to delete the vault.



## What's next
{: #delete-vaults-next}


  


