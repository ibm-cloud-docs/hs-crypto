---

copyright:
  years: 2020
lastupdated: "2020-09-18"

keywords: pkcs11 access, pkcs 11 authentication, set up PKCS 11 API, best practice for setting up pkcs11 users

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

# Best practices for setting up PKCS #11 user types
{: #best-practice-pkcs11-access}

To align with industry-standard security requirements and [Permitted object accesses by sessions](http://docs.oasis-open.org/pkcs11/pkcs11-ug/v2.40/cn02/pkcs11-ug-v2.40-cn02.html#_Toc406759993) that is defined in the PKCS #11 Usage Guide, it is recommended to set up the PKCS #11 user types in your {{site.data.keyword.hscrypto}} instance.

##  PKCS #11 user types
{: #pkcs11-user-types}

The PKCS #11 standard defines two user types: security officer and normal user. If a user does not perform a `C_Login` function call, the user is considered as an anonymous user.

There are two types of keystores that are defined in the PKCS #11 library that users can access:

* **Public keystore**: Stores keys that are less sensitive and that are to be accessed by any user types.
* **Private keystore**: Stores keys that encrypt sensitive data and that are to be accessed by normal users only.

For more information about keystores, see the keystore introduction in [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro).

In the {{site.data.keyword.hscrypto}} PKCS #11 library configuration file `grep11client.yaml`, the following user types are predefined, with each assigned a [service ID API key](/docs/account?topic=account-serviceidapikeys):

* **Security officer (SO)**: Manages both public and private keystores, and keys in the public keystore.

  An SO user can be a person who owns the SO API key in an enterprise. This person is able to initialize the PKCS #11 token and delete all key objects in public and private keystores. This person can be the one who sets up the {{site.data.keyword.hscrypto}} instance and the {{site.data.keyword.iamshort}} (IAM) roles. The PKCS #11 application can perform administrative Cryptoki function calls, such as `C_InitToken`, after it logs in as an SO user type.

* **Normal user**: Manages keys in both public and private keystores. Only normal users have access to keys in the private keystore.

  Normal users are the ones who have access to the normal user API key. The normal user API key should be distributed only to a limited group of people, who need access to the private token keystore where more sensitive keys are stored, such as keys for signing and encrypting contracts. In this case, the PKCS #11 application calls the `C_Login` function using the normal user API key as the PIN and becomes a normal user to access the private token keystore.

* **Anonymous user**: Manages keys in the public keystore only.

  The anonymous user API key can be distributed to anyone in the enterprise so that anonymous users can access the public keystore to perform daily work, such as signing a document. The confidentiality level of the keys in the public keystore is lower than keys in the private keystore. The API key is configured in the PKCS #11 library configuration file `grep11client.yaml` and the anonymous user does not need to call the `C_Login` function.

A PKCS #11 application works as only one of the three user types at any time, no matter how many sessions are opened. Each user type needs an API key for authentication. To create the API keys, you need to first create two custom IAM roles, and then create service IDs for the three user types, and then map the custom IAM roles to the service IDs.

To perform the following steps, you need to have the `Administrator` [platform access](/docs/account?topic=account-userroles#platformroles) in your {{site.data.keyword.cloud}} account.
{: tip}

## Step 1: Create custom IAM roles
{: #step1-create-custom-roles}

You need to create two custom roles, one for operating keys and one for operating keystores.

### 1. Create a custom role for operating keys
{: #create-key-operator}

This role is used to generate and manage keys in the PKCS #11 keystores. However, this role does not have permissions to manage PKCS #11 keystores.

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role; for example, `key operator`. This name must be unique within the account. Users see this role name in the console when they assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when assigning access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `KeyOperator`
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the console when a user assigns access to the service.
6. From the list of services, select **Hyper Protect Crypto Services**.
7. Select **Add** for the following actions:
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
  * hs-crypto.ep11.use
  * hs-crypto.keystore.deletekey
  * hs-crypto.keystore.listkeysbyattributes
  * hs-crypto.keystore.listkeysbyids
  * hs-crypto.keystore.storenewkey
  * hs-crypto.keystore.updatekey
8. Click **Create** when you're done adding actions.

### 2. Create a custom role for operating keystores
{: #create-keystore-operator}

This role is used to create and delete PKCS #11 keystores but does not have permissions to manage keys.

1. In the {{site.data.keyword.cloud}} console, go to **Manage** > **Access (IAM)**, and select **Roles**.
2. Click **Create**.
3. Enter a name for your role; for example, `keystore operator`. This name must be unique within the account. Users see this role name in the console when they assign access to the service.
4. Enter an ID for the role. This ID is used in the CRN, which is used when assigning access by using the API. The role ID must begin with a capital letter and use alphanumeric characters only; for example, `KeystoreOperator`
5. Optional: Enter a succinct and helpful description that helps the users who are assigning access know what level of access this role assignment gives a user. This description also shows in the console when a user assigns access to the service.
6. From the list of services, select **Hyper Protect Crypto Services**.
7. Select **Add** for the following actions:
  * hs-crypto.keystore.createkeystore
  * hs-crypto.keystore.deletekeystore
  * hs-crypto.keystore.listkeystoresbyattributes
  * hs-crypto.keystore.listkeystoresbyids
8. Click **Create** when you're done adding actions.

For more information about how to create custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

##  Step 2: Create service IDs and API keys for the SO user, normal user, and anonymous user
{: #step2-create-service-id-api-key}

### 1. Create service IDs and API keys for the SO user
{: #create-service-id-api-key-so-user}

To create a service ID for the SO user and the corresponding API key, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**.
2. To create the service ID for the SO user, follow these steps:
  1. Click **Create**.
  2. Create a name `SO user` and description for the SO user service ID.
  3. Click **Create**.
3. To create an API key for the service ID, follow these steps:
  1. Click the **API keys** tab on the `SO user` service ID page.
  2. Click **Create**.
  3. Add a name and description to easily identify the API key, for example, `SO user API key`.
  4. Click **Create**.
  5. Save your API key by copying or downloading it to secure location.

  The API key is to be used as the PIN for the SO user logins, and cannot be retrieved. Make sure to make a copy of it in this step.
  {: important}

### 2. Create service IDs and API keys for the normal user
{: #create-service-id-api-key-normal-user}

To create a service ID for the normal user and the corresponding API key, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**.
2. To create the service ID for the normal user, follow these steps:
  1. Click **Create**.
  2. Create a name `Normal user` and description for the normal user service ID.
  3. Click **Create**.
3. To create an API key for the service ID, follow these steps:
  1. Click the **API keys** tab on the `Normal user` service ID page.
  2. Click **Create**.
  3. Add a name and description to easily identify the API key, for example, `Normal user API key`.
  4. Click **Create**.
  5. Save your API key by copying or downloading it to secure location.

  The API key is to be used as the PIN for the normal user logins, and cannot be retrieved. Make sure to make a copy of it in this step.
  {: important}

### 3. Create service IDs and API keys for the anonymous user
{: #create-service-id-api-key-ananymous-user}

To create a service ID for the anonymous user and the corresponding API key, complete the following steps:

1. In the {{site.data.keyword.cloud_notm}} console, go to **Manage** &gt; **Access (IAM)**, and select **Service IDs**.
2. To create the service ID for the anonymous user, follow these steps:
  1. Click **Create**.
  2. Create a name `Anonymous user` and description for the anonymous user service ID.
  3. Click **Create**.
3. To create an API key for the service ID, follow these steps:
  1. Go to the **API keys** tab.
  2. Click the **API keys** tab on the `Anonymous user` service ID page.
  3. Add a name and description to easily identify the API key, for example, `Anonymous user API key`.
  4. Click **Create**.
  5. Save your API key by copying or downloading it to secure location.

  The API key is to be used as the PIN for the anonymous user logins, and cannot be retrieved. Make sure to make a copy of it in this step.
  {: important}

For more information about creating services IDs, see [Creating and working with service IDs](/docs/account?topic=account-serviceids). For detailed instructions on creating service ID API keys, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).

## Step 3: Assign IAM roles to the service IDs
{: #step3-assign-iam-roles}

You can grant access to service IDs within a {{site.data.keyword.hscrypto}} service instance by using the {{site.data.keyword.cloud_notm}} console.

The following table shows the custom role that each type of user should be assigned.

| Keystore type | SO user | Normal user | Anonymous user |
|-----|-----|-----|-----|
| Public keystore | Keystore operator, Key operator | Key operator |Key operator|
| Private keystore | Keystore operator | Key operator |N/A |
{: caption="Table 1. Lists PKCS #11 keystore user types and corresponding custom roles" caption-side="bottom"}

### 1. Assign the custom roles to the SO user service ID

To assign the custom roles that are defined in [Step 1](#step1-create-custom-roles) to the SO user service ID that are created in the previous step, follow these steps:

#### Assign access to the public keystore
{: #assign-access-public-keystore-so-user}

To assign access to the public keystore for the SO user, follow these steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
1. Hover your mouse over the `SO user` service ID, and click the overflow (...) icon located to the right of the `SO user` row to open a list of options.
1. From the options menu, click **Assign access**.
1. Click **Assign service ID additional access**, and then click the **IAM services** button.
1. Click **No service access** under **What type of access do you want to assign?** and select **Hyper Protect Crypto Services**.
1. Click **Service Instance ID** and select the {{site.data.keyword.hscrypto}} service instance that you want to grant access to.
<!-- 1. Enter the identifying information about the key.
   * For **Resource type**, enter `keystore`.
   * For **Resource ID**, enter a Universally Unique Identifier (UUID) that uniquely identifies the keystore. For example, `21000000-0000-0000-0200-000000000222`. For more information about UUID, see [Generate a UUID compliant with RFC 4122](https://www.cryptosys.net/pki/uuid-rfc4122.html){: external}.
     The UUID is to be used in the `grep11client.yaml` file when defining the PKCS #11 user type in the `tokenspaceID` field.
     {: tip} -->
1. Under **Custom access**, check the boxes for the following roles:
  * `Keystore operator`
  * `Key operator`
1. Click **Add**, and then click **Assign** after confirmation.

#### Assign access to the private keystore
{: #assign-access-private-keystore-so-user}

To assign access to the private keystore for the SO user, follow these steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
1. Hover your mouse over the `SO user` service ID, and click the overflow (...) icon located to the right of the `SO user` row to open a list of options.
1. From the options menu, click **Assign access**.
1. Click **Assign service ID additional access**, and then click the **IAM services** button.
1. Click **No service access** under **What type of access do you want to assign?** and select **Hyper Protect Crypto Services**.
1. Click **Service Instance ID** and select the {{site.data.keyword.hscrypto}} service instance that you want to grant access to.
<!--1. Enter the identifying information about the key.
   * For **Resource type**, enter `keystore`.
   * For **Resource ID**, enter a Universally Unique Identifier (UUID) that uniquely identifies the keystore. For example, `11000000-0000-0000-0200-000000000111`. For more information about UUID, see [Generate a UUID compliant with RFC 4122](https://www.cryptosys.net/pki/uuid-rfc4122.html){: external}.
     The UUID is to be used in the `grep11client.yaml` file when defining the PKCS #11 user type in the `tokenspaceID` field.
     {: tip} -->
1. Under **Custom access**, check the box for `Keystore operator`.
1. Click **Add**, and then click **Assign** after confirmation.

### 2. Assign the custom roles to the normal user service ID

To assign the custom roles that are defined in [Step 1](#step1-create-custom-roles) to the normal user service ID that are created in the previous step, follow these steps:

#### Assign access to the public keystore
{: #assign-access-public-keystore-normal-user}

To assign access to the public keystore for the normal user, follow these steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
1. Hover your mouse over the `Normal user` service ID, and click the overflow (...) icon located to the right of the `Normal user` row to open a list of options.
1. From the options menu, click **Assign access**.
1. Click **Assign service ID additional access**, and then click the **IAM services** button.
1. Click **No service access** under **What type of access do you want to assign?** and select **Hyper Protect Crypto Services**.
1. Click **Service Instance ID** and select the {{site.data.keyword.hscrypto}} service instance that you want to grant access to.
<!-- 1. Enter the identifying information about the key.
   * For **Resource type**, enter `keystore`.
   * For **Resource ID**, enter a Universally Unique Identifier (UUID) that uniquely identifies the keystore. For example, `21000000-0000-0000-0200-000000000222`. For more information about UUID, see [Generate a UUID compliant with RFC 4122](https://www.cryptosys.net/pki/uuid-rfc4122.html){: external}.
     The UUID is to be used in the `grep11client.yaml` file when defining the PKCS #11 user type in the `tokenspaceID` field.
     {: tip} -->
1. Under **Custom access**, check the box for `Key operator`.
1. Click **Add**, and then click **Assign** after confirmation.

#### Assign access to the private keystore
{: #assign-access-private-keystore-normal-user}

To assign access to the private keystore for the normal user, follow these steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
1. Hover your mouse over the `Normal user` service ID, and click the overflow (...) icon located to the right of the `Normal user` row to open a list of options.
1. From the options menu, click **Assign access**.
1. Click **Assign service ID additional access**, and then click the **IAM services** button.
1. Click **No service access** under **What type of access do you want to assign?** and select **Hyper Protect Crypto Services**.
1. Click **Service Instance ID** and select the {{site.data.keyword.hscrypto}} service instance that you want to grant access to.
<!--1. Enter the identifying information about the key.
   * For **Resource type**, enter `keystore`.
   * For **Resource ID**, enter a Universally Unique Identifier (UUID) that uniquely identifies the keystore. For example, `11000000-0000-0000-0200-000000000111`. For more information about UUID, see [Generate a UUID compliant with RFC 4122](https://www.cryptosys.net/pki/uuid-rfc4122.html){: external}.
     The UUID is to be used in the `grep11client.yaml` file when defining the PKCS #11 user type in the `tokenspaceID` field.
     {: tip} -->
1. Under **Custom access**, check the box for `Key operator`.
1. Click **Add**, and then click **Assign** after confirmation.

### 3. Assign the custom roles to the anonymous user service ID

To assign the custom roles that are defined in [Step 1](#step1-create-custom-roles) to the anonymous user service ID that are created in the previous step, follow these steps:

#### Assign access to the public keystore
{: #assign-access-public-keystore-anonymous-user}

To assign access to the public keystore for the anonymous user, follow these steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Service IDs** to browse the existing service IDs in your account.
1. Hover your mouse over the `Anonymous user` service ID, and click the overflow (...) icon located to the right of the `Anonymous user` row to open a list of options.
1. From the options menu, click **Assign access**.
1. Click **Assign service ID additional access**, and then click the **IAM services** button.
1. Click **No service access** under **What type of access do you want to assign?** and select **Hyper Protect Crypto Services**.
1. Click **Service Instance ID** and select the {{site.data.keyword.hscrypto}} service instance that you want to grant access to.
<!-- 1. Enter the identifying information about the key.
   * For **Resource type**, enter `keystore`.
   * For **Resource ID**, enter a Universally Unique Identifier (UUID) that uniquely identifies the keystore. For example, `21000000-0000-0000-0200-000000000222`. For more information about UUID, see [Generate a UUID compliant with RFC 4122](https://www.cryptosys.net/pki/uuid-rfc4122.html){: external}.
     The UUID is to be used in the `grep11client.yaml` file when defining the PKCS #11 user type in the `tokenspaceID` field.
     {: tip} -->
1. Under **Custom access**, check the box for `Key operator`.
1. Click **Add**, and then click **Assign** after confirmation.

##  What's next
{: #pkcs11-best-practices-next}

You have successfully set up the PKCS #11 user types. Continue to read [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api) on how to use the PKCS #11 API.
