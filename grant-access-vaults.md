---

copyright:
  years: 2022
lastupdated: "2022-01-26"

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

You can enable different levels of access to {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} resources in your {{site.data.keyword.cloud_notm}} account by creating and modifying {{site.data.keyword.cloud_notm}} IAM access policies.
{: shortdesc}

Access control in {{site.data.keyword.uko_full_notm}} are managed in vaults. Vaults are secure repositories for your cryptographic keys and keystores. A managed key or internal keystore can be created only in a vault.

As a service administrator or an account owner, determine an [access policy type](/docs/account?topic=account-userroles#policytypes) for users, service IDs, and access groups based on your internal access control requirements. 

Review [roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access) to learn how {{site.data.keyword.cloud_notm}} IAM roles map to {{site.data.keyword.hscrypto}} actions.
{: tip}

### Step 1. Retrieve the vault ID
{: #access-vault-retrieve-ID}

Retrieve the unique identifier that is associated with the vault that you want to grant someone access to.

To get the ID for a specific vault, you can:

- [Access the {{site.data.keyword.cloud_notm}} console](/docs/hs-crypto?topic=hs-crypto-view-keys#view-key-gui) to browse the vaults in your service instance.
- [Use the {{site.data.keyword.uko_full_notm}} API](/apidocs/uko#get-vaults-v3){: external}  to retrieve a list of your vaults, along with metadata about the vaults.

### Step 2. Grant access to vaults with the console
{: #grant-access-vault-console}

To assign access to a vault with the console:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select a table row, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for that user.
3. From the options menu, click **Assign access**.
4. Click **Assign users additional access**.
5. Click the **IAM services** button.
6. From the list of services, select **{{site.data.keyword.hscrypto}}**.
7. Select **Services based on attributes**.
8. Select the **Instance ID** attribute and select the instance where the vault is located.
9. Select the **vault ID** attribute and enter the ID associated with the vault.
8. Choose a combination of [platform and service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) to assign access for the user.
9. Click **Add**.
10. Continue to add platform and service access roles as needed. When you finish all the access assignment, click **Assign**.

You can also create an access policy through IAM [API](/apidocs/iam-policy-management#create-policy){: external} or [CLI](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_user_policy_create){: external}.
{: note}

## What's next
{: #grant-access-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-creat-vaults).
  
- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
  


