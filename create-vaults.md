---

copyright:
  years: 2022
lastupdated: "2022-03-22"

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


# Creating vaults
{: #create-vaults}

You can use {{site.data.keyword.hscrypto}} to create a group of keys and keystores for a target group of users that require the same {{site.data.keyword.iamshort}} (IAM) access permissions in a vault. You can create vaults in {{site.data.keyword.uko_full_notm}} through the user interface (UI).
{: shortdesc}


As a _Vault Administrator_, you can bundle the keys and keystores in your {{site.data.keyword.hscrypto}} instance into groups called _vault_. A vault is a collection of keys, internal keystores, and external keystores that require the same IAM access permissions. For example, if you have a group of team members who need a particular type of access to a specific group of keys and keystores, you can create a vault and assign the appropriate IAM access policy to the target user group. The users that are assigned access to the vault can create and manage the resources that exist within the vault.

Vaults are also useful in cases where it is important for one business unit to have access to a set of keys and keystores that another business unit cannot have. An account administrator can create vaults for each business unit and [assign the appropriate level of access](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults) to the appropriate users. In the case where the account administrator wants to delegate platform management of a specific vault to someone else, they can assign a user a [Vault Administrator role](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-service-access-roles). The sub-administrator is then able to manage the vault and grant access to the appropriate users.

Before you create a vault for your {{site.data.keyword.hscrypto}} instance, keep in mind the following considerations:

- Vaults can hold KMS keys and keystores, but not EP11 keys and keystores.

    Vaults can contain both KMS keys and keystores. There is no limit on how many keys can exist within a vault. Vaults don't apply to Enterprise PKCS #11 (EP11) keys and keystores.

- A key or a keystore only can belong to one vault at a time.

    A managed key or a target keystore can belong to only one vault. You need to assign a vault to a managed key or a target keystore upon creation.


For more information about granting access, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).


## Creating vaults through the UI
{: #create-vaults-ui}

To create a vault through the UI, complete the following steps through the **Vaults** page. Optionally, you can create a vault when you [create a managed key](/docs/hs-crypto?topic=hs-crypto-create-managed-keys) or [add a keystore](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores).

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. To create a vault, click **Create vault**.
4. Enter a name in **Vault name**. The vault name can be of 1 to 100 characters. Optionally, you can add an extended description to your vault in the **Description** section.
5. Click **Create vault** to confirm.

You have successfully created a vault. 



## What's next
{: #create-vaults-next}

- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
  
- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

