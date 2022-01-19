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
{:external: target="_blank" .external}
{:term: .term}


# Creating vaults
{: #create-vaults}

You can create vaults in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

A vault is a single unit that controls a user's or an access group's access to keys and keystores through Identity and Access Management (IAM). For more instructions, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).


## Creating vaults through the UI
{: #create-vaults-ui}

To create a vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. To create a vault, click **Create vault**.
4. Enter a name in **Vault name**. The vault name can be of 2 to 100 characters. Optionally, you can add an extended description to your vault in the **Description** section.
5. Click **Create vault** to confirm.

You have successfully created a vault. 

You can also create a vault when you [create a key](/docs/hs-crypto?topic=hs-crypto-create-internal-keys) or [add a keystore](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores).
{: tip}


## What's next
{: #create-vaults-next}


  


