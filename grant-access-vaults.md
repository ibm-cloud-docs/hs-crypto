---

copyright:
  years: 2022
lastupdated: "2022-02-28"

keywords: Unified Key Orchestrator, vaults, keys, keystore, key management, access control

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

You can enable different levels of access to {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} resources in your {{site.data.keyword.cloud_notm}} account by creating and modifying {{site.data.keyword.cloud_notm}} [Identity and Access Management (IAM)](#x7547040){: term} access policies.
{: shortdesc}

Access control in {{site.data.keyword.uko_full_notm}} is managed in vaults. Vaults are secure repositories for your cryptographic keys and keystores. A managed key or internal keystore can be created only in a vault.

As a service administrator or an account owner, you can determine an [access policy type](/docs/account?topic=account-userroles#policytypes) for users, service IDs, and access groups based on your internal access control requirements. 

Review [roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access) to learn how {{site.data.keyword.cloud_notm}} IAM roles map to {{site.data.keyword.hscrypto}} actions.
{: tip}

## Step 1. Retrieve the vault ID
{: #access-vault-retrieve-ID}

Retrieve the unique identifier that is associated with the vault that you want to grant someone access to.

Access the {{site.data.keyword.cloud_notm}} UI to browse the keys that are stored in your service instance by following these steps:

  1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
  2. Click **Vaults** from the navigation to view all the available vaults.
  3. Click the vault that you want to edit. The Details side panel is displayed.
  4. In the **General properties** card, copy the vault ID by clicking the copy icon.



## Step 2. Grant access to vaults from the {{site.data.keyword.cloud_notm}} UI
{: #grant-access-vault-console}

To assign access to a vault for a user from the UI, complete the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select the user from the table, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then select **Assign access**.
3. Select **Assign access to the users**, and then select **IAM services**.
4. From the list of services, select **{{site.data.keyword.hscrypto}}**.
5. Select **Resources based on selected attributes**.
6. Select the **Instance ID** attribute, and select the instance where the vault is located.
7. Select the **Vault ID** attribute and enter the vault ID that is retrieved in Step 1.
8. Choose a combination of [platform and service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) to assign access for the user, and click **Add**.
9. Continue to add platform and service access roles as needed. When you finish all the access assignment, click **Assign**.

You can also create an access policy through IAM [API](/apidocs/iam-policy-management#create-policy){: external} or [CLI](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_user_policy_create){: external}.
{: note}

## What's next
{: #grant-access-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).
  
- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
  


