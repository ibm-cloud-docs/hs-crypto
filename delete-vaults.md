---

copyright:
  years: 2022
lastupdated: "2022-01-20"

keywords: Unified Key Orchestrator, vaults, keys, keystores, key management, UKO

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

Before you delete a vault, make sure that you [delete all managed keys](/docs/hs-crypto?topic=hs-crypto-delete-internal-keys), and [delete or disconnect from all target keystores that are managed](/docs/hs-crypto?topic=hs-crypto-delete-uko-keystores) in the vault.
{: important}

## Deleting vaults through the UI
{: #delete-vaults-ui}

To delete a vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. Click the vault that you want to delete. The side panel is displayed.
4. Make sure that the vault does not contain any keys or keystores, and then click **Delete**.
5. Confirm the delete action by clicking **Delete vault**.

The vault has been deleted and removed from the vault list.

## What's next
{: #delete-vaults-next}


  


