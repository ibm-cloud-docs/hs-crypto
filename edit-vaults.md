---

copyright:
  years: 2022
lastupdated: "2022-02-11"

keywords: Unified Key Orchestrator, vaults, keys, keystores, key management, UKO

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


# Editing vault details
{: #edit-vaults}

You can edit your vaults in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.uko_full_notm}} API. With a vault, you can not only create managed keys or target keystores, but also manage resources that are contained in the vault.
{: shortdesc}


## Editing vault details through the UI
{: #edit-vaults-ui}

To edit vault details through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. Click the vault that you want to edit. The Details side panel is displayed.
4. Click **Edit** to update the **Vault name** and **Description**.
5. Click **Save** to save the property changes.
6. The keys and keystores that are assigned to this vault are displayed in tables. 
7. Optionally, you can add additional keys to the vault by clicking **Create key** under **Keys**, or add a keystore by clicking **Add keystores** under **Target keystores**.



## What's next
{: #edit-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
  
- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

