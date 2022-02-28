---

copyright:
  years: 2022
lastupdated: "2022-02-28"

keywords: UKO access, UKO account authentication, UKO custom roles, Unified Key Orchestrator

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:table: .aria-labeledby="caption"}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}

# Setting up custom roles for {{site.data.keyword.uko_full_notm}} 
{: #uko-role-best-practices}

To manage users and access to {{site.data.keyword.uko_full_notm}} keys, keystores, and vaults, {{site.data.keyword.hscrypto}} provides [default service-level IAM access roles](/docs/hs-crypto?topic=hs-crypto-uko-manage-access#uko-service-access-roles) to assign and control access. If you want to set up more granular custom roles to manage user access to meet the requirements of your enterprise, here are some best practices you can follow.

{: shortdesc}

## Step 1: Create custom IAM roles
{: #step1-create-custom-roles-uko}

To create a custom role, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** &gt; **Access (IAM)**, and select **Roles**.

2. Click **Create**.

3. Enter a name for your role. This name must be unique within the account. You can see this role name in the console when you assign access to the service.

4. Enter an ID for the role. This ID is used in the CRN, which is used when you assign access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `MyVaultAdministrator`.

5. Optionally, you can enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description is also displayed in the console when you assign access to the service.

6. From the list of services, select **{{site.data.keyword.hscrypto}}**.

7. Select **Add** to add actions for the role. 

    The following table lists the suggested custom roles and corresponding actions for your reference:
    

    <table>
    <tr>
      <th>Role</th>
      <th>Description</th>
      <th>Actions</th>
    </tr>
    <tr>
      <td>My vault administrator</td>
      <td>Manages vaults.</td>
      <td>
        <ul>
          <li><code>hs-crypto.managed-keys.read</code></li>
          <li><code>hs-crypto.managed-keys.list</code></li>
          <li><code>hs-crypto.target-keystores.read</code></li>
          <li><code>hs-crypto.target-keystores.list</code></li>
          <li><code>hs-crypto.key-templates.read</code></li>
          <li><code>hs-crypto.key-templates.list</code></li>
          <li><code>hs-crypto.vaults.read</code></li>
          <li><code>hs-crypto.vaults.list</code></li>
          <li><code>hs-crypto.vaults.write</code></li>
          <li><code>hs-crypto.vaults.delete</code></li>
          <li><code>hs-crypto.uko.initiate-paid-upgrade</code></li>
          <li><code>hs-crypto.uko.add-paid-keystore</code></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>My keystore administrator</td>
      <td>Manages keystores.</td>
      <td>
        <ul>
          <li><code>hs-crypto.managed-keys.read</code></li>
          <li><code>hs-crypto.managed-keys.list</code></li>
          <li><code>hs-crypto.target-keystores.read</code></li>
          <li><code>hs-crypto.target-keystores.list</code></li>
          <li><code>hs-crypto.target-keystores.write</code></li>
          <li><code>hs-crypto.target-keystores.delete</code></li>
          <li><code>hs-crypto.key-templates.read</code></li>
          <li><code>hs-crypto.key-templates.list</code></li>
          <li><code>hs-crypto.vaults.read</code></li>
          <li><code>hs-crypto.vaults.list</code></li>
          <li><code>hs-crypto.uko.initiate-paid-upgrade</code></li>
          <li><code>hs-crypto.uko.add-paid-keystore</code></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>My key administrator</td>
      <td>Manages special permissions for administrative tasks, such as destructive actions.</td>
      <td>
        <ul>
          <li><code>hs-crypto.managed-keys.deactivated-destroy</code></li>
          <li><code>hs-crypto.managed-keys.destroyed-remove</code></li>
          <li><code>hs-crypto.managed-keys.read</code></li>
          <li><code>hs-crypto.managed-keys.list</code></li>
          <li><code>hs-crypto.managed-keys.delete</code></li>
          <li><code>hs-crypto.target-keystores.read</code></li>
          <li><code>hs-crypto.target-keystores.list</code></li>
          <li><code>hs-crypto.key-templates.read</code></li>
          <li><code>hs-crypto.key-templates.list</code></li>
          <li><code>hs-crypto.key-templates.write</code></li>
          <li><code>hs-crypto.key-templates.delete</code></li>
          <li><code>hs-crypto.vaults.read</code></li>
          <li><code>hs-crypto.vaults.list</code></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>My key custodian - creator</td>
      <td>Manages and creates keys. For a complete key lifecycle, both Creator and Deployer roles are needed. To implement separaton of duties, assign Creator and Deployer role to different people. </td>
      <td>
        <ul>
          <li><code>hs-crypto.managed-keys.preactivation-destroy</code></li>
          <li><code>hs-crypto.managed-keys.active-install</code></li>
          <li><code>hs-crypto.managed-keys.active-uninstall</code></li>
          <li><code>hs-crypto.managed-keys.deactivated-install</code></li>
          <li><code>hs-crypto.managed-keys.deactivated-uninstall</code></li>
          <li><code>hs-crypto.managed-keys.read</code></li>
          <li><code>hs-crypto.managed-keys.list</code></li>
          <li><code>hs-crypto.managed-keys.write</code></li>
          <li><code>hs-crypto.managed-keys.generate</code></li>
          <li><code>hs-crypto.managed-keys.distribute</code></li>
          <li><code>hs-crypto.managed-keys.write-dates</code></li>
          <li><code>hs-crypto.managed-keys.write-tags</code></li>
          <li><code>hs-crypto.target-keystores.read</code></li>
          <li><code>hs-crypto.target-keystores.list</code></li>
          <li><code>hs-crypto.key-templates.read</code></li>
          <li><code>hs-crypto.key-templates.list</code></li>
          <li><code>hs-crypto.key-templates.write</code></li>
          <li><code>hs-crypto.vaults.read</code></li>
          <li><code>hs-crypto.vaults.list</code></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>My key custodian - deployer</td>
      <td>Manages and deploys keys. For a complete key lifecycle, both Creator and Deployer roles are needed. To implement separaton of duties, assign Creator and Deployer role to different people. </td>
      <td>
        <ul>
          <li><code>hs-crypto.managed-keys.preactivation-activate</code></li>
          <li><code>hs-crypto.managed-keys.preactivation-destroy</code></li>
          <li><code>hs-crypto.managed-keys.active-deactivate</code></li>
          <li><code>hs-crypto.managed-keys.active-install</code></li>
          <li><code>hs-crypto.managed-keys.active-uninstall</code></li>
          <li><code>hs-crypto.managed-keys.deactivated-install</code></li>
          <li><code>hs-crypto.managed-keys.deactivated-reactivate</code></li>
          <li><code>hs-crypto.managed-keys.deactivated-uninstall</code></li>
          <li><code>hs-crypto.managed-keys.read</code></li>
          <li><code>hs-crypto.managed-keys.list</code></li>
          <li><code>hs-crypto.managed-keys.write</code></li>
          <li><code>hs-crypto.managed-keys.distribute</code></li>
          <li><code>hs-crypto.managed-keys.write-dates</code></li>
          <li><code>hs-crypto.managed-keys.write-tags</code></li>
          <li><code>hs-crypto.target-keystores.read</code></li>
          <li><code>hs-crypto.target-keystores.list</code></li>
          <li><code>hs-crypto.key-templates.read</code></li>
          <li><code>hs-crypto.key-templates.list</code></li>
          <li><code>hs-crypto.vaults.read</code></li>
          <li><code>hs-crypto.vaults.list</code></li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>My reader</td>
      <td>Performs read-only actions for auditing purposes.</td>
      <td>
        <ul>
          <li><code>hs-crypto.managed-keys.read</code></li>
          <li><code>hs-crypto.managed-keys.list</code></li>
          <li><code>hs-crypto.target-keystores.read</code></li>
          <li><code>hs-crypto.target-keystores.list</code></li>
          <li><code>hs-crypto.key-templates.read</code></li>
          <li><code>hs-crypto.key-templates.list</code></li>
          <li><code>hs-crypto.vaults.read</code></li>
          <li><code>hs-crypto.vaults.list</code></li>
        </ul>
      </td>
    </tr>
    <caption>Table 1. Custom roles and actions corresponding to the {{site.data.keyword.uko_full_notm}} operations</caption>
    </table>

8. Click **Create** after you select the appropriate actions for your custom role.

## Step 2: Assign IAM roles to users
{: #step2-assign-iam-roles-uko}

Before users can access {{site.data.keyword.uko_full_notm}} vaults, keystores, or keys, you need to grant users the appropriate IAM roles by completing the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
   
2. Click the **User** name and select the **Access policies** tab.

    Click **Invite users** to add a user to your account if the user is not in the table. For more information, see [Inviting users to an account](/docs/account?topic=account-iamuserinv){: external}.
    {: tip}

3. Click **Assign access**.

4. Select **{{site.data.keyword.hscrypto}}** from the list under **Which service do you want to assign access to?**.

5. Select services that you want to assign access to:

    - If you want to assign the user access to all the {{site.data.keyword.hscrypto}} instances under your account, select **All resources**.
    - If you want to assign the user access to part of the {{site.data.keyword.hscrypto}} resources under you account, select **Resources based on selected attributes**, and check the corresponding conditions based on your needs. For example, check the **Service Instance ID** and specify the instance from the list.

6. Check the box for at least the **Viewer** role under **Platform access**. For more information about the IAM platform roles, see [Platform access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#platform-mgmt-roles).

7. Check the box for the corresponding custom role that you set up in [Step 1](#step1-create-custom-roles-uko) based on your needs.

8. Click **Add**, and then click **Assign** after confirmation.

##  What's next
{: #uko-role-best-practices-next}

- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

