---

copyright:
  years: 2022
lastupdated: "2022-01-24"

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


# Granting access to vaults
{: #grant-access-vaults}

You can enable different levels of access to {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} resources in your {{site.data.keyword.cloud_notm}} account by creating and modifying {{site.data.keyword.cloud_notm}} IAM access policies.
{: shortdesc}

Access control in {{site.data.keyword.uko_full_notm}} are managed in vaults. Vaults are secure repositories for your cryptographic keys and keystores. A managed key or internal keystore can be created only in a vault.

As a service administrator or an account owner, determine an [access policy type](/docs/account?topic=account-userroles#policytypes) for users, service IDs, and access groups based on your internal access control requirements. For example, if you want to grant user access to {{site.data.keyword.hscrypto}} at the smallest scope available, you can [assign access to a single key](#grant-access-key-level) in an instance.

A good practice is to grant access permissions as you invite new users to your account or service. For example, consider the following guidelines:

- **Enable user access to the resources in your account by assigning {{site.data.keyword.iamshort}} (IAM) roles.**
    Rather than sharing your admin credentials, create new policies for users who need access to the encryption keys in your account. If you are the admin for your account, you are automatically assigned a *Manager* policy with access to all resources under the account.
- **Grant roles and permissions at the smallest scope needed.**
    For example, if a user needs to access only a high-level view of keys within a specified space, grant the *Reader* role to the user for that space.
- **Regularly audit who can manage access control and delete key resources.**
    Remember that granting a *Manager* role to a user means that the user can modify service policies for other users, in addition to destroying resources.


(To be updated)


## What's next
{: #grant-access-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-creat-vaults).
  
- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
  


