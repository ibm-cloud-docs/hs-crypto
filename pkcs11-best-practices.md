---

copyright:
  years: 2020, 2025
lastupdated: "2025-02-24"

keywords: pkcs11 access, pkcs 11 authentication, set up PKCS 11 API, best practice for setting up pkcs11 users

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Setting up PKCS #11 API user types
{: #best-practice-pkcs11-access}

To align with industry-standard security requirements and [Permitted object accesses by sessions](http://docs.oasis-open.org/pkcs11/pkcs11-ug/v2.40/cn02/pkcs11-ug-v2.40-cn02.html#_Toc406759993), it is suggested to set up the PKCS #11 user types in your {{site.data.keyword.hscrypto}} instance when you use the PKCS #11 API.
{: shortdesc}

##  PKCS #11 user types
{: #pkcs11-user-types}

The PKCS #11 standard defines two user types: security officer and normal user. If a user does not perform a `C_Login` function call, the user is considered as an anonymous user.



In the {{site.data.keyword.hscrypto}} PKCS #11 library configuration file `grep11client.yaml`, the following user types are predefined, with each assigned a [service ID API key](/docs/account?topic=account-serviceidapikeys):

* **Security officer (SO)**: 
    An SO user can be a person who owns the SO API key in an enterprise. This person is able to initialize the PKCS #11 token and delete all key objects in keystores. This person can be the one who sets up the {{site.data.keyword.hscrypto}} instance and the {{site.data.keyword.iamshort}} (IAM) roles. The PKCS #11 application can perform administrative Cryptoki function calls, such as `C_InitToken`, after it logs in as an SO user type.

* **Normal user**: 
    Normal users are the ones who have access to the normal user API key. The normal user API key needs to be distributed only to a limited group of people, who need access to the keystore where more sensitive keys are stored, such as keys for signing and encrypting contracts. In this case, the PKCS #11 application calls the `C_Login` function by using the normal user API key as the PIN and becomes a normal user to access the keystore.

* **Anonymous user**: 
    The anonymous user API key can be distributed to anyone in the enterprise so that anonymous users can access the keystore to perform daily work, such as signing a document. The API key is configured in the PKCS #11 library configuration file `grep11client.yaml` and the anonymous user does not need to call the `C_Login` function.

A PKCS #11 application works as only one of the three user types at any time, no matter how many sessions are opened. Each user type needs an API key for authentication. To create the API keys, you need to first create three custom IAM roles. And then, create service IDs for the three user types, and map the custom IAM roles to the service IDs.

To perform the following steps, you need to have the `Administrator` [platform access](/docs/account?topic=account-userroles#platformroles) in your {{site.data.keyword.cloud}} account.
{: tip}

## Step 1: Create custom IAM roles
{: #step1-create-custom-roles}

You need to create three custom roles, one for performing crypto operations, one for managing keys, and the other for managing EP11 keystores.

### 1. Create a custom role for performing crypto operations
{: #create-crypto-operator}

This role is used to generate key objects for performing crypto operations. However, this role does not have permission to use or manage Enterprise PKCS #11 (EP11) keystores.

1. In the UI, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role; for example, `Crypto operator`. This name must be unique within the account. Users see this role name in the UI when they assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when you assign access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `CryptoOperator`.
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the UI when a user assigns access to the service.
6. From the list of services, select **Hyper Protect Crypto Services**.
7. Select **Add** for the following 19 actions:
    * hs-crypto.crypto.decrypt
    * hs-crypto.crypto.derivekey
    * hs-crypto.crypto.digest
    * hs-crypto.crypto.digestkey
    * hs-crypto.crypto.encrypt
    * hs-crypto.crypto.generatekey
    * hs-crypto.crypto.generatekeypair
    * hs-crypto.crypto.generaterandom
    * hs-crypto.crypto.getattributevalue
    * hs-crypto.crypto.getmechanisminfo
    * hs-crypto.crypto.getmechanismlist
    * hs-crypto.crypto.rewrapkeyblob
    * hs-crypto.crypto.setattributevalue
    * hs-crypto.crypto.sign
    * hs-crypto.crypto.unwrapkey
    * hs-crypto.crypto.verify
    * hs-crypto.crypto.wrapkey
    * hs-crypto.discovery.listservers
    * hs-crypto.ep11.use
8. Review the actions added under **Summary**, and then click **Create**.

### 2. Create a custom role for managing keys
{: #create-manage-key-operator}

This role is used to manage keys in the EP11 keystores. However, this role does not have permission to manage EP11 keystores or perform crypto operations.

1. In the UI, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role; for example, `Key operator`. This name must be unique within the account. Users see this role name in the UI when they assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when you assign access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `KeyOperator`.
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the UI when a user assigns access to the service.
6. From the list of services, select **Hyper Protect Crypto Services**.
7. Select **Add** for the following six actions:
    * hs-crypto.keystore.deletekey
    * hs-crypto.keystore.listkeysbyattributes
    * hs-crypto.keystore.listkeysbyids
    * hs-crypto.keystore.listkeystoresbyids
    * hs-crypto.keystore.storenewkey
    * hs-crypto.keystore.updatekey
8. Review the actions added under **Summary**, and then click **Create**.

### 3. Create a custom role for managing keystores
{: #create-keystore-operator}

This role is used to create and delete EP11 keystores but does not have permissions to manage keys.

1. In the UI, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role; for example, `Keystore operator`. This name must be unique within the account. Users see this role name in the UI when they assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when you assign access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `KeystoreOperator`.
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the UI when a user assigns access to the service.
6. From the list of services, select **Hyper Protect Crypto Services**.
7. Select **Add** for the following four actions:
    * hs-crypto.keystore.createkeystore
    * hs-crypto.keystore.deletekeystore
    * hs-crypto.keystore.listkeystoresbyattributes
    * hs-crypto.keystore.listkeystoresbyids
8. Review the actions added under **Summary**, and then click **Create**.

For more information about how to create custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

##  Step 2: Create service IDs and API keys for the SO user, normal user, and anonymous user
{: #step2-create-service-id-api-key}

### 1. Create service IDs and API keys for the SO user
{: #create-service-id-api-key-so-user}

To create a service ID for the SO user and the corresponding API key, complete the following steps:

1. In the UI, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**.
2. To create the service ID for the SO user, follow these steps:
    1. Click **Create**.
    2. Create a name `SO user` and description for the SO user service ID.
    3. Click **Create**.
3. To create an API key for the service ID, follow these steps:
    1. Click the **API keys** tab on the `SO user` service ID page.
    2. Click **Create**.
    3. Add a name and description to easily identify the API key. For example, `SO user API key`.
    4. Click **Create**.
    5. Save your API key by copying or downloading it to a secure location.

    The API key is to be used as the PIN for the SO user logins for and cannot be retrieved. Make sure to make a copy of it in this step.
    {: important}

### 2. Create service IDs and API keys for the normal user
{: #create-service-id-api-key-normal-user}

To create a service ID for the normal user and the corresponding API key, complete the following steps:

1. In the UI, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**.
2. To create the service ID for the normal user, follow these steps:
    1. Click **Create**.
    2. Create a name `Normal user` and description for the normal user service ID.
    3. Click **Create**.
3. To create an API key for the service ID, follow these steps:
    1. Click the **API keys** tab on the `Normal user` service ID page.
    2. Click **Create**.
    3. Add a name and description to easily identify the API key. For example, `Normal user API key`.
    4. Click **Create**.
    5. Save your API key by copying or downloading it to a secure location.

    The API key is to be used as the PIN for the normal user logins, and cannot be retrieved. Make sure to make a copy of it in this step.
    {: important}

### 3. Create service IDs and API keys for the anonymous user
{: #create-service-id-api-key-ananymous-user}

To create a service ID for the anonymous user and the corresponding API key, complete the following steps:

1. In the UI, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**.
2. To create the service ID for the anonymous user, follow these steps:
    1. Click **Create**.
    2. Create a name `Anonymous user` and description for the anonymous user service ID.
    3. Click **Create**.
3. To create an API key for the service ID, follow these steps:
    1. Click the **API keys** tab on the `Anonymous user` service ID page.
    2. Click **Create**.
    3. Add a name and description to easily identify the API key. For example, `Anonymous user API key`.
    4. Click **Create**.
    5. Save your API key by copying or downloading it to a secure location.

    The API key is to be used to perform crypto operations and access the public keystore for the anonymous user, which cannot be retrieved. Make sure to make a copy of it in this step.
    {: important}

For more information about creating service IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids). For detailed instructions on creating service ID API keys, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).

## Step 3: Assign IAM roles to the service IDs
{: #step3-assign-iam-roles}

You can grant access to service IDs within a {{site.data.keyword.hscrypto}} service instance by using the UI.

### 1. Assign the custom roles to the SO user service ID
{: #assign-custom-role-SO-user-service}

To assign the custom roles that are defined in [Step 1](#step1-create-custom-roles) to the SO user service ID, follow these steps:

To assign access to the keystores for the SO user, follow these steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
2. Hover your mouse over the `SO user` service ID, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options.
3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select **Specific resources**.
7. Select the **Service Instance ID** attribute type, enter the {{site.data.keyword.hscrypto}} service instance ID that you want to grant access to, and click **Next**.
8. Under **Roles and actions**, check the boxes for the following roles and click **Next**:
    * `Crypto operator`
    * `Key operator`
    * `Keystore operator`

9. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
10. Click **Add**.
11. Review the roles and actons added under **Summary**, and then click **Assign**.


### 2. Assign the custom roles to the normal user service ID
{: #assign-custom-role-normal-user-service}

To assign the custom roles that are defined in [Step 1](#step1-create-custom-roles) to the normal user service ID, follow these steps:

To assign access to the keystores for the normal user, follow these steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
2. Hover your mouse over the `Normal user` service ID, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options.
3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select **Specific resources**.
7. Select the **Service Instance ID** attribute type, enter the {{site.data.keyword.hscrypto}} service instance ID that you want to grant access to, and click **Next**.
8. Under **Roles and actions**, check the boxes for `Crypto operator` and `Key operator`, and then click **Next**.
9. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
10. Click **Add**.
11. Review the roles and actons added under **Summary**, and then click **Assign**.


### 3. Create access policies and assign custom roles to the anonymous user service ID
{: #create-policy-assign-custom-role-anonymous-user-service}

The anonymous user requires two access policies. The PKCS#11 specification specifies that the anonymous user can access the public keystore only. The following access policies are set up to restrict the anonymous user to the public keystore.

To assign the custom roles that are defined in [Step 1](#step1-create-custom-roles) to the anonymous user service ID, follow these steps:

#### Create access policy for crypto operations
{: #create-access-policy-crypto-operations}

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
2. Hover your mouse over the `Anonymous user` service ID, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options.
3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select **Specific resources**.
7. Select the **Service Instance ID** attribute type, enter the {{site.data.keyword.hscrypto}} service instance ID that you want to grant access to, and click **Next**.
8. Under **Roles and actions**, check the box for `Crypto operator` and click **Next**.
9. (Optional) Under **Conditions (optional)**, click **Review** to check the access policy.
10. Click **Add**.
11. Review the roles and actons added under **Summary**, and then click **Assign**.

#### Create access policy for public key store and key access
{: #create-access-policy-key-access}

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
2. Hover your mouse over the `Anonymous user` service ID, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options.
3. From the options menu, click **Assign access**.
4. Click **Access policy**.
5. Under **Service**, select **Hyper Protect Crypto Services** and click **Next**.
6. Under **Resources**, select **Specific resources**.
7. Select the **Service Instance ID** attribute, enter the {{site.data.keyword.hscrypto}} service instance ID that you want to grant access to, and click **Next**.
8. Under **Roles and actions**, check the box for `Key operator` and click **Next**.
10. Under **Conditions (optional)**, click **Add condition**.
11. Click **Advanced condition builder** and click **Next**.
12. Within the **Create a condition** dialog, click the down arrow to the right of **Service Instance ID** and select **Resource Type** from the drop-down list.
13. Enter **key** in the text box that is displaying **Enter a value**.
14. Click **Add condition group**.
15. Click the **OR** radio button located directly under the **JSON** text.  Do **NOT** select the **OR** radio button within the condition group.
16. Within the condition group, click the down arrow to the right of **Service Instance ID** and select **Resource Type** from the drop-down list.
17. Enter **keystore** for the value of the **Resource Type** attribute.
18. Within the condition group, click the down arrow to the right of **Region** and select **Resource ID** from the drop-down list.
19. Enter the value of the **Resource ID** in the text box to the right of the **Resource ID** and **string equals** text. 
     
    The value of the **Resource ID** attribute type must contain a valid [Universally Unique IDentifier (UUID)](https://www.cryptosys.net/pki/uuid-rfc4122.html){: external} of the PKCS#11 public keystore. You can generate the UUID with a third-party tool, such as [UUID generator](https://www.uuidgenerator.net/){: external}. The UUID string specified for the **Resource ID** attribute must match the UUID string specified for the anonymous user's **public_keystore_spaceid** configuration parameter within the `grep11client.yaml` [configuration file](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file) in the PKCS#11 client library.
    {: important}
20. Click **Create** to create the advanced condition.
21. Click **Review** to check the access policy.
22. Click **Add**.
23. Review the roles and actions added under **Summary**, and then click **Assign**.

##  What's next
{: #pkcs11-best-practices-next}

Continue to read [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api) on how to use the PKCS #11 API.
