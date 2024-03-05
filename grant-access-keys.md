---

copyright:
  years: 2018, 2024
lastupdated: "2024-02-27"

keywords: grant access, iam, iam access, assign access, access policy, key access

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Granting access to keys
{: #grant-access-keys}

You can enable different levels of access to {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} resources in your {{site.data.keyword.cloud_notm}} account by creating and modifying {{site.data.keyword.cloud_notm}} IAM access policies.
{: shortdesc}

As a service administrator or an account owner, determine an [access policy type](/docs/account?topic=account-userroles#policytypes) for users, service IDs, and access groups based on your internal access control requirements. For example, if you want to grant user access to {{site.data.keyword.hscrypto}} at the smallest scope available, you can [assign access to a single key](#grant-access-key-level) in an instance.

A good practice is to grant access permissions as you invite new users to your account or service. For example, consider the following guidelines:

- **Enable user access to the resources in your account by assigning {{site.data.keyword.iamshort}} (IAM) roles.**
    Rather than sharing your admin credentials, create new policies for users who need access to the encryption keys in your account. If you are the admin for your account, you are automatically assigned a *Manager* policy with access to all resources under the account.
- **Grant roles and permissions at the smallest scope needed.**
    For example, if a user needs to access only a high-level view of keys within a specified space, grant the *Reader* role to the user for that space.
- **Regularly audit who can manage access control and delete key resources.**
    Remember that granting a *Manager* role to a user means that the user can modify service policies for other users, in addition to destroying resources.

## Granting access to all keys in an instance
{: #grant-access-instance-level}

You can grant access to keys within a {{site.data.keyword.hscrypto}} service instance by using the UI.

Review [roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access) to learn how {{site.data.keyword.cloud_notm}} IAM roles map to {{site.data.keyword.hscrypto}} actions.
{: tip}

To assign access:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select the user, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for that user.
3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select **Specific resources**. 
7. Select the **Service Instance ID** attribute type, enter the [instance ID that is retrieved](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID) and click **Next**.
8. Under **Roles and actions**, choose a combination of [platform and service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) to assign access for the user and click **Next**.
9. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
10. After confirmation, click **Add** &gt; **Assign**.

## Granting access to a single key in an instance
{: #grant-access-key-level}

You can also assign access to a single key in a {{site.data.keyword.hscrypto}} service instance.

### Step 1. Retrieve the key ID
{: #access-key-retrieve-ID}

Retrieve the unique identifier that is associated with the key that you want to grant someone access to.

To get the ID for a specific key, you can:

- [Access the UI](/docs/hs-crypto?topic=hs-crypto-view-keys#view-key-gui) to browse the keys that are stored in your service instance.
- [Use the {{site.data.keyword.hscrypto}} key management service API](/docs/hs-crypto?topic=hs-crypto-view-keys#retrieve-keys-api) to retrieve a list of your keys, along with metadata about the keys.

### Step 2. Create an access policy
{: #access-key-create-policy}

Use the retrieved key ID to create an access policy:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select the user, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for that user.
3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select **Specific resources**. 
7. Select the **Service Instance ID** attribute type and enter the [instance ID that is retrieved](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
8. Click **Add a condition**, enter the following identifying information about the key, and click **Next**:
    1. Select **Resource Type**, and enter `key`.
    2. Select **Resource ID**, and enter the ID that is assigned to your key by the {{site.data.keyword.hscrypto}} service.
9. Under **Roles and actions**, choose a combination of [platform and service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) to assign access for the user and click **Next**.
10. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
11. After confirmation, click **Add** &gt; **Assign**.

## Granting access to key rings in an instance
{: #grant-access-key-ring-level}

A key ring is a collection of keys that are located within your service instance, in which you can restrict access through IAM access policy. For more information on key rings, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings).

You can grant access to key rings within a {{site.data.keyword.hscrypto}} instance by using the
UI, IAM API, or IAM CLI.

Review [roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access) to learn how {{site.data.keyword.cloud_notm}} IAM roles map to {{site.data.keyword.hscrypto}} actions.
{: tip}

### Granting access to key rings with the UI
{: #grant-access-key-ring-console}

To assign access to a key ring with the UI:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select a table row, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for that user.
3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select **Specific resources**. 
7. Select the **Service Instance ID** attribute type and enter the [instance ID that is retrieved](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
8. Click **Add a condition**, select the **Key Ring ID** attribute to enter the ID associated with the key ring, and click **Next**.
9. Under **Roles and actions**, choose a combination of [platform and service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) to assign access for the user and click **Next**.
10. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
11. After confirmation, click **Add** &gt; **Assign**.


You can also create an access policy through IAM [API](/apidocs/iam-policy-management#create-policy){: external} or [CLI](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_user_policy_create){: external}.
{: note}
