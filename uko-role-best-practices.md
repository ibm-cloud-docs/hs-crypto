---

copyright:
  years: 2022, 2024
lastupdated: "2024-03-07"

keywords: UKO access, UKO account authentication, UKO custom roles, Unified Key Orchestrator

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Setting up custom roles for {{site.data.keyword.uko_full_notm}} 
{: #uko-role-best-practices}

To manage users and access to {{site.data.keyword.uko_full_notm}} keys, keystores, and vaults, {{site.data.keyword.hscrypto}} provides [default service-level IAM access roles](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-service-access-roles) to assign and control access. If you want to set up more granular custom roles to manage user access to meet the requirements of your enterprise, here are some best practices that you can follow.
{: shortdesc}

## Step 1: Create custom IAM roles
{: #step1-create-custom-roles-uko}

To create a custom role, complete the following steps:

1. In the UI, go to **Manage** &gt; **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role. This name must be unique within the account. You can see this role name in the UI when you assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when you assign access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `MyVaultAdministrator`.
5. Optionally, you can enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description is also displayed in the UI when you assign access to the service.
6. From the list of services, select **{{site.data.keyword.hscrypto}}**.
7. Select **Add** to add actions for the role. 

    The following table lists the suggested custom roles and corresponding actions for your reference:

    | Role | Description | Actions |
    | --- | --- | --- |
    | My vault administrator | Manages vaults. | * `hs-crypto.managed-keys.read` \n * `hs-crypto.managed-keys.list` \n * `hs-crypto.target-keystores.read` \n * `hs-crypto.target-keystores.list` \n * `hs-crypto.key-templates.read` \n * `hs-crypto.key-templates.list` \n * `hs-crypto.vaults.read` \n * `hs-crypto.vaults.list` \n * `hs-crypto.vaults.write` \n * `hs-crypto.vaults.delete` \n * `hs-crypto.uko.initiate-paid-upgrade` \n * `hs-crypto.uko.add-paid-keystore` |
    | My keystore administrator | Manages keystores. | * `hs-crypto.managed-keys.read` \n * `hs-crypto.managed-keys.list` \n * `hs-crypto.target-keystores.read` \n * `hs-crypto.target-keystores.list` \n * `hs-crypto.target-keystores.write` \n * `hs-crypto.target-keystores.delete` \n * `hs-crypto.key-templates.read` \n * `hs-crypto.key-templates.list` \n * `hs-crypto.vaults.read` \n * `hs-crypto.vaults.list` \n * `hs-crypto.uko.initiate-paid-upgrade` \n * `hs-crypto.uko.add-paid-keystore` |
    | My key administrator | Manages special permissions for administrative tasks, such as destructive actions. | * `hs-crypto.managed-keys.deactivated-destroy` \n * `hs-crypto.managed-keys.destroyed-remove` \n * `hs-crypto.managed-keys.read` \n * `hs-crypto.managed-keys.list` \n * `hs-crypto.managed-keys.delete` \n * `hs-crypto.target-keystores.read` \n * `hs-crypto.target-keystores.list` \n * `hs-crypto.key-templates.read` \n * `hs-crypto.key-templates.list` \n * `hs-crypto.key-templates.write` \n * `hs-crypto.key-templates.delete` \n * `hs-crypto.vaults.read` \n * `hs-crypto.vaults.list` |
    | My key custodian - creator | Manages and creates keys. For a complete key lifecycle, both Creator and Deployer roles are needed. To implement separation of duties, assign Creator and Deployer role to different people. | * `hs-crypto.managed-keys.preactivation-destroy` \n * `hs-crypto.managed-keys.active-install` \n * `hs-crypto.managed-keys.active-uninstall` \n * `hs-crypto.managed-keys.deactivated-install` \n * `hs-crypto.managed-keys.deactivated-uninstall` \n * `hs-crypto.managed-keys.read` \n * `hs-crypto.managed-keys.list` \n * `hs-crypto.managed-keys.write` \n * `hs-crypto.managed-keys.generate` \n * `hs-crypto.managed-keys.distribute` \n * `hs-crypto.managed-keys.write-dates` \n * `hs-crypto.managed-keys.write-tags` \n * `hs-crypto.target-keystores.read` \n * `hs-crypto.target-keystores.list` \n * `hs-crypto.key-templates.read` \n * `hs-crypto.key-templates.list` \n * `hs-crypto.key-templates.write` \n * `hs-crypto.vaults.read` \n * `hs-crypto.vaults.list` |
    | My key custodian - deployer | Manages and deploys keys. For a complete key lifecycle, both Creator and Deployer roles are needed. To implement separation of duties, assign Creator and Deployer role to different people. | * `hs-crypto.managed-keys.preactivation-activate` \n * `hs-crypto.managed-keys.preactivation-destroy` \n * `hs-crypto.managed-keys.active-deactivate` \n * `hs-crypto.managed-keys.active-install` \n * `hs-crypto.managed-keys.active-uninstall` \n * `hs-crypto.managed-keys.deactivated-install` \n * `hs-crypto.managed-keys.deactivated-reactivate` \n * `hs-crypto.managed-keys.deactivated-uninstall` \n * `hs-crypto.managed-keys.read` \n * `hs-crypto.managed-keys.list` \n * `hs-crypto.managed-keys.write` \n * `hs-crypto.managed-keys.distribute` \n * `hs-crypto.managed-keys.write-dates` \n * `hs-crypto.managed-keys.write-tags` \n * `hs-crypto.target-keystores.read` \n * `hs-crypto.target-keystores.list` \n * `hs-crypto.key-templates.read` \n * `hs-crypto.key-templates.list` \n * `hs-crypto.vaults.read` \n * `hs-crypto.vaults.list` |
    | My reader | Performs read-only actions for auditing purposes. | * `hs-crypto.managed-keys.read` \n * `hs-crypto.managed-keys.list` \n * `hs-crypto.target-keystores.read` \n * `hs-crypto.target-keystores.list` \n * `hs-crypto.key-templates.read` \n * `hs-crypto.key-templates.list` \n * `hs-crypto.vaults.read` \n * `hs-crypto.vaults.list` |
    {: caption="Table 1. Custom roles and actions corresponding to the {{site.data.keyword.uko_full_notm}} operations" caption-side="bottom"}

8. Click **Create** after you select the appropriate actions for your custom role.

## Step 2: Assign IAM roles to users
{: #step2-assign-iam-roles-uko}

Before users can access {{site.data.keyword.uko_full_notm}} vaults, keystores, or keys, you need to grant users the appropriate IAM roles by completing the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select the user, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for that user.

    Click **Invite users** to add a user to your account if the user is not in the table. For more information, see [Inviting users to an account](/docs/account?topic=account-iamuserinv){: external}.
    {: tip}

3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select resources that you want to assign access to and click **Next**.

    - If you want to assign the user access to all the {{site.data.keyword.hscrypto}} instances under your account, select **All resources**.
    - If you want to assign the user access to part of the {{site.data.keyword.hscrypto}} resources under you account, select **Specific resources** and add the corresponding conditions based on your needs. For example, select the **Service Instance ID** and specify the instance from the list.

7. Under **Roles and actions**, choose a combination of platform and service access roles to assign access for the user and click **Next**. 

    - Check the box for at least the **Viewer** role under **Platform access**. For more information about the IAM platform roles, see [Platform access roles](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-platform-mgmt-roles).
    - Check the box for the corresponding custom role that you set up in [Step 1](#step1-create-custom-roles-uko) based on your needs.

    If you don't have any custom roles, you can select the existing IAM roles that cover the actions that you want to assign to the user. You can view the specific actions that correspond to the role by clicking the number.
    {: tip}

8. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
9. After confirmation, click **Add** &gt; **Assign**.


##  What's next
{: #uko-role-best-practices-next}

- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

