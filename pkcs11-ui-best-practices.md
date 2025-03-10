---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-09"

keywords: pkcs11 ui access, pkcs 11 account authentication

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Granting users access to manage EP11 keystores and keys through UI
{: #grant-pkcs11-ui-access}

To enable users to manage Enterprise PKCS #11 (EP11) keystores and keys with the UI, you need to assign users the appropriate access.
{: shortdesc}

## (Optional) Step 1: Create custom IAM roles
{: #step1-create-custom-roles-pkcs11-ui}

With the integration with {{site.data.keyword.iamshort}} (IAM), {{site.data.keyword.hscrypto}} provides you with multiple [existing IAM service roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles) to assign and control access. For more granular access management, you can create custom roles based on your own needs. For example, if you want to assign a group of users only the access to view the EP11 keystores, you can create a custom role that covers only the action of `hs-crypto.keystore.listkeystoresbyids` and then assign these users with this custom role.

To create a custom role, complete the following steps:

1. In the UI, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role; for example, `EP11 keystore UI operator`. This name must be unique within the account. You can see this role name in the UI when you assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when you assign access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `EPKeystoreUIOperator`
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the UI when you assign access to the service.
6. From the list of services, select **Hyper Protect Crypto Services**.
7. Select **Add** to add actions for the role. The following table lists the actions that correspond to the EP11 keystore or key operations with the UI:

    | Operations | Actions |
    | --- | --- |
    | View EP11 keystores. | * `hs-crypto.keystore.listkeystoresbyids` |
    | Create EP11 keystores. | * `hs-crypto.keystore.listkeystoresbyids` \n * `hs-crypto.keystore.createkeystore` |
    | Delete EP11 keystores. | * `hs-crypto.keystore.listkeystoresbyids` \n * `hs-crypto.keystore.deletekeystore` |
    | View EP11 keys. | * `hs-crypto.keystore.listkeystoresbyids` \n * `hs-crypto.keystore.listkeysbyids` |
    | Create EP11 keys. | * `hs-crypto.keystore.listkeystoresbyids` \n * `hs-crypto.keystore.listkeysbyids` \n * `hs-crypto.crypto.generatekey` \n * `hs-crypto.crypto.generatekeypair` \n * `hs-crypto.keystore.storenewkey` |
    | View EP11 keys. | * `hs-crypto.keystore.listkeystoresbyids` \n * `hs-crypto.keystore.listkeysbyids` \n * `hs-crypto.keystore.deletekey` |
    {: caption="Actions corresponding to the EP11 keystore or key operations with the UI" caption-side="bottom"}

8. Click **Create** after you select the appropriate actions for your custom role.

## Step 2: Assign IAM roles to users
{: #step2-assign-iam-roles-pkcs-ui}

Before users can access EP11 keystores or keys with the UI, you need to grant users the appropriate IAM roles by completing the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select the user, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for that user.

    Click **Invite users** to add a user to your account if the user is not in the table. For more information, see [Inviting users to an account](/docs/account?topic=account-iamuserinv){: external}.
    {: tip}

3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select resources that you want to assign access to and click **Next**:

    - If you want to assign the user access to all the {{site.data.keyword.hscrypto}} instances under your account, select **All resources**.
    - If you want to assign the user access to part of the {{site.data.keyword.hscrypto}} resources under you account, select **Specific resources** and add the corresponding conditions based on your needs. For example, select the **Service Instance ID** and specify the instance from the list.

7. Under **Roles and actions**, choose a combination of [platform and service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#roles) to assign access for the user and click **Next**. 

    - Check the box for at least the **Viewer** role under **Platform access**.
    - Check the box for the corresponding custom role that you set up in [Step 1](#step1-create-custom-roles-pkcs11-ui) based on your needs.

    If you don't have any custom roles, you can select the existing IAM roles that cover the actions that you want to assign to the user. You can view the specific actions that correspond to the role by clicking the number.
    {: tip}

8. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
9. After confirmation, click **Add** &gt; **Assign**.

##  What's next
{: #pkcs11-ui-best-practices-next}

Continue to read [Managing EP11 keystores with the IBM Cloud UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui) and [Managing EP11 keys with the IBM Cloud UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui) on detailed operations.
