---

copyright:
  years: 2021
lastupdated: "2021-08-10"

keywords: pkcs11 ui access, pkcs 11 account authentication

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

# Granting users access to manage EP11 keystores and keys through UI
{: #grant-pkcs11-ui-access}

To enable users to manage Enterprise PKCS #11 (EP11) keystores and keys with the {{site.data.keyword.cloud_notm}} console, you need to assign users the appropriate access.
{: shortdesc}

## (Optional) Step 1: Create custom IAM roles
{: #step1-create-custom-roles-pkcs11-ui}

With the integration with {{site.data.keyword.iamshort}} (IAM), {{site.data.keyword.hscrypto}} provides you with multiple [existing IAM service roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles) to assign and control access. For more granular access management, you can create custom roles based on your own needs. For example, if you want to assign a group of users only the access to view the EP11 keystores, you can create a custom role that covers only the action of `hs-crypto.keystore.listkeystoresbyids` and then assign these users with this custom role.

To create a custom role, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role; for example, `EP11 keystore UI operator`. This name must be unique within the account. You can see this role name in the console when you assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when you assign access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `EPKeystoreUIOperator`
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the console when you assign access to the service.
6. From the list of services, select **Hyper Protect Crypto Services**.
7. Select **Add** to add actions for the role. The following table lists the actions that correspond to the EP11 keystore or key operations with the console:

    <table>
    <tr>
      <th>Operations</th>
      <th>Actions</th>
    </tr>
    <tr>
      <td>View EP11 keystores.</td>
      <td>
        <ul>
          <li>`hs-crypto.keystore.listkeystoresbyids`</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Create EP11 keystores.</td>
      <td>
        <ul>
          <li>`hs-crypto.keystore.listkeystoresbyids`</li>
          <li>`hs-crypto.keystore.createkeystore`</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Delete EP11 keystores.</td>
      <td>
        <ul>
          <li>`hs-crypto.keystore.listkeystoresbyids`</li>
          <li>`hs-crypto.keystore.deletekeystore`</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>View EP11 keys.</td>
      <td>
        <ul>
          <li>`hs-crypto.keystore.listkeystoresbyids`</li>
          <li>`hs-crypto.keystore.listkeysbyids`</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>Create EP11 keys.</td>
      <td>
        <ul>
          <li>`hs-crypto.keystore.listkeystoresbyids`</li>
          <li>`hs-crypto.keystore.listkeysbyids`</li>
          <li>`hs-crypto.crypto.generatekey`</li>
          <li>`hs-crypto.crypto.generatekeypair`</li>
          <li>`hs-crypto.keystore.storenewkey`</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td>View EP11 keys.</td>
      <td>
        <ul>
          <li>`hs-crypto.keystore.listkeystoresbyids`</li>
          <li>`hs-crypto.keystore.listkeysbyids`</li>
          <li>`hs-crypto.keystore.deletekey`</li>
        </ul>
      </td>
    </tr>
    <caption>Table 1. Actions corresponding to the EP11 keystore or key operations with the console</caption>
    </table>

8. Click **Create** after you select the appropriate actions for your custom role.

## Step 2: Assign IAM roles to users
{: #step2-assign-iam-roles-pkcs-ui}

Before users can access EP11 keystores or keys with the {{site.data.keyword.cloud_notm}} console, you need to grant users the appropriate IAM roles by completing the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Click the **User** name and select the **Access policies** tab.

    Click **Invite users** to add a user to your account if the user is not in the table. For more information, see [Inviting users to an account](/docs/account?topic=account-iamuserinv){: external}.
    {: tip}

3. Click **Assign access**.
4. Select **Hyper Protect Crypto Services** from the list under **What type of access do you want to assign?**.
5. Select services that you want to assign access to:

    - If you want to assign the user access to all the {{site.data.keyword.hscrypto}} instances under your account, select **All services**.
    - If you want to assign the user access to part of the {{site.data.keyword.hscrypto}} resources under you account, select **Services based on attributes** and check the corresponding conditions based on your needs. For example, check the **Service Instance ID** and specify the instance from the list.

6. Check the box for at least the **Viewer** role under **Platform access**. For more information about the IAM platform roles, see [Platform access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#platform-mgmt-roles).
7. Check the box for the corresponding custom role that you set up in [Step 1](#step1-create-custom-roles-pkcs11-ui) based on your needs.

    If you don't have any custom roles, you can select the existing IAM roles that cover the actions that you want to assign to the user. You can view the specific actions that correspond to the role by clicking the number.
    {: tip}

8. Click **Add**, and then click **Assign** after confirmation.

##  What's next
{: #pkcs11-ui-best-practices-next}

Continue to read [Managing EP11 keystores with the IBM Cloud console](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui) and [Managing EP11 keys with the IBM Cloud console](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui) on detailed operations.
