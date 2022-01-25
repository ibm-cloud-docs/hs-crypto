---

copyright:
  years: 2022
lastupdated: "2022-01-25"

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

If you want to delete a vault, you need to [delete all managed keys](/docs/hs-crypto?topic=hs-crypto-delete-internal-keys), and [delete or disconnect from all target keystores that are managed](/docs/hs-crypto?topic=hs-crypto-delete-uko-keystores) in the vault first. The Delete function is available for empty vaults only.
{: note}

## Deleting vaults through the UI
{: #delete-vaults-ui}

To delete a vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. Click the vault that you want to delete. The side panel is displayed.
4. Make sure that the vault does not contain any keys or keystores, and then click **Delete**.
5. Confirm the delete action by clicking **Delete vault**.

The vault has been deleted and removed from the vault list. Access groups that are assigned to this vault can no longer access the vault.

## What's next
{: #delete-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-creat-vaults).
  
- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).
  
- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

