---

copyright:
  years: 2018, 2023
lastupdated: "2023-07-05"

keywords: ibm cloud hyper protect crypto services, hyper protect crypto services, hpcs, crypto, crypto services, key management, kms, dedicated key management, hsm, hardware security module, cloud hsm, dedicated hsm, keep your own key, kyok, cryptographic operation, key storage, encryption key, cloud encryption, encryption at rest

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}




# Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) is a dedicated key management service and [hardware security module (HSM)](#x6704988){: term} based on {{site.data.keyword.cloud_notm}}. With this service, you can take the ownership of the cloud HSM to fully manage your encryption keys and to perform cryptographic operations. {{site.data.keyword.hscrypto}} is also the only service in the cloud industry that is built on FIPS 140-2 Level 4-certified hardware.
{: shortdesc}
{: hide-dashboard}

{{site.data.keyword.hscrypto}} integrates with {{site.data.keyword.keymanagementserviceshort}} application programming interface (API) to generate and manage keys. The Keep Your Own Key (KYOK) function is also enabled to provide access to cloud-based cryptographic HSMs. You can access the network addressable HSMs by making standard PKCS #11 API calls or Enterprise PKCS #11 over gRPC (GREP11) API calls to perform cryptographic operations.
{: hide-dashboard}


With the {{site.data.keyword.uko_full_notm}} function, you can manage and orchestrate all keys from a multicloud environment with {{site.data.keyword.hscrypto}}. {{site.data.keyword.uko_full_notm}} provides the only cloud native single-point-of-control of encryption keys across hybrid multicloud environments of your enterprise.
{: hide-dashboard}


This tutorial shows you the high-level steps on how to set up your service instance by loading your [master keys](#x2908413){: term}, create and manage encryption keys with the {{site.data.keyword.cloud_notm}} console, and perform cryptographic operations with the PKCS #11 API or with the GREP11 API.
{: hide-dashboard}



With {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} that is built on FIPS 140-2 Level 4-certified hardware, you can take the ownership of the cloud HSM to fully manage your encryption keys and to perform cryptographic operations. The {{site.data.keyword.uko_full_notm}} function provides the only cloud native single-point-of-control of encryption keys across hybrid multicloud environments of your enterprise.
{: hide-in-docs}

This tutorial guides you on how to initialize your service instance by loading your master key, create and manage encryption keys with the {{site.data.keyword.cloud_notm}} console, and perform cryptographic operations with the PKCS #11 API or with the Enterprise PKCS #11 over gRPC (GREP11) API.
{: hide-in-docs}

## Step 1: Initialize your service instance
{: #initialize-crypto-dashboard}
{: hide-in-docs}
{: notoc}

To manage your keys, you need to initialize your service instance first. Depending on where your service instance locates and your security requirements, {{site.data.keyword.hscrypto}} provides you with the following three options to initializing your service instance:

- Option 1: [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)

    This option gives you the highest security, which enables you to store and manage master key parts using smart cards.

- Option 2: [Initializing service instances using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)

    If you create your service instance in Dallas (`us-south`) or Washington DC (`us-east`) where the recovery crypto units are enabled, you can choose this approach where the master key is randomly generated within a recovery crypto unit and then exported to other crypto units. With this option, your manager key parts are safely stored in the recovery crypto units of IBM Cloud. You don't need additional hardware for master key management. 

- Option 3: [Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)

    You can also initialize your service instance using master key parts that are stored in files on your local workstation. You can use this approach regardless of whether or not your service instance includes recovery crypto units. 

## Step 2 (Standard Plan only): Manage your encryption keys with the key management service 
{: #manage-data-key-dashboard}
{: hide-in-docs}
{: notoc}

Follow these steps to manage your encryption keys if you are using {{site.data.keyword.hscrypto}} Standard Plan.

From the {{site.data.keyword.cloud_notm}} console, you can create new root keys or standard keys for data encryption, or you can import your existing keys.

### Creating new keys
{: #create-keys-dashboard}

Complete the following steps to create your first cryptographic key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To create a new key, select **Create a key**.

    Specify the key's details:

    | Setting | Description |
    | --- | --- |
    | Key type | The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select **Root key** or **Standard key**. |
    | Key name | A unique, human-readable alias for easy identification of your key. To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location. |
    {: caption="Table 1. Description of the settings to create a key" caption-side="bottom"}

3. When you finish filling out the key's details, click **Add key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-CBC algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified HSMs that are located in secure {{site.data.keyword.cloud_notm}} data centers.

### Importing your own keys
{: #import-keys-dashboard}

You can bring your existing keys to the service so that you can still use the same encryption keys to protect your applications or data.

Complete the following steps to add an existing key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To upload an existing key, select **Import a key**.

    Specify the key's details:

    | Setting | Description |
    | --- | --- |
    | Key type | The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select **Root key** or **Standard key**. |
    | Key name | A unique, human-readable alias for easy identification of your key. To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location. |
    | Key material | The key material, such as a symmetric key, that you want to store in the {{site.data.keyword.hscrypto}} service. The key that you provide must be base64 encoded. |
    {: caption="Table 2. Description of the settings to import your own key" caption-side="bottom"}

3. When you finish filling out the key's details, click **Import key** to confirm.

From the {{site.data.keyword.cloud_notm}} console, you can inspect the general characteristics of your new keys.


## Step 2 ({{site.data.keyword.uko_full_notm}} Plan only): Manage your encryption keys in a multicloud environment using {{site.data.keyword.uko_full_notm}}
{: #manage-uko-key-dashboard}
{: hide-in-docs}
{: notoc}

Follow these steps to manage your encryption keys if you are using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}.

### Creating vaults
{: #create-vault}

A vault is a single repository that controls a user's or an access group's access to managed keys and target keystores through {{site.data.keyword.iamshort}} (IAM). 

Complete the following steps to create your first vault:

1. From your service instance UI, click **Vaults** from the navigation to view all the available vaults.
2. To create a vault, click **Create vault**.
3. Enter a name in **Vault name**. The vault name can be of 1 to 100 characters. Optionally, you can add an extended description to your vault in the **Description** section.
4. Click **Create vault** to confirm.

### Creating target keystores
{: #create-keystore}

A target keystore is a repository that stores the cryptographic keys. You can create an internal target keystore within the service instance or connect to an external target keystore in another service instance or even in another cloud provider, such as Microsoft Azure Key Vault, Amazon Web Services (AWS) Key Management Service (KMS), and Google Cloud KMS.

Complete the following steps to create your first internal target keystore:

1. From your service instance UI, click **Target keystores** from the navigation to view all the available keystores.
2. To create a keystore, click **Add keystore**.
3. Under **Vault**, select the vault that you create, and click **Next**. 

   If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

4. Under **Keystore type**, select **KMS Keystore** and click **Next**.
5. Under **Keystore properties**, enter a name in **Keystore name**. The keystore name can be of 1 to 100 characters. And then, click **Next**.
6. Under **Summary**, you can view the summary of the keystore that you create, including the keystore type, the assigned vault, and general properties. 
7. After you confirm the keystore details, click **Create keystore** to create the keystore.

### Creating and installing managed keys
{: #create-managed-key}

You can use a managed key for encryption or decryption only after it is created and activated in at least one keystore. Complete the following steps to create your first managed key and activate the key in the keystore that you create:

1. From your service instance UI, click **Managed keys** from the navigation to view all the available keys.
2. To create a managed key, click **Create key**.
3. Under **Vault**, select the vault that you create, and click **Next**. 
4. Under **General**, select **IBM Cloud KMS** as the keystore type, and click **Next**.
5. Under **Key properties**, specify the following details of the key. Click **Next** to continue when you are done.

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | Pre-active keys are not to be installed in target keystores until you manually activate them. Active keys are to be automatically installed in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. Automatic state change is to be triggered on the planned date. |
    | Expiration date      | Plan a date to deactivate the key. Automatic state change is to be triggered on the planned date. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: caption="Table 3. Managed key properties" caption-side="bottom"}

6. Under **Target keystores**, select the keystore that you create. 
7. Under **Summary**, view the summary of your key, and then click **Create key** to confirm.

## Step 3: Encrypt your data with cloud HSM
{: #encrypt-data-hsm-dashboard}
{: hide-in-docs}
{: notoc}

You can remotely access {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations with the PKCS #11 API or with the GREP11 API.

### Performing cryptographic operations with the PKCS #11 API
{: #cryptographic-operations-with-pkcs11-dashboard}

To perform cryptographic operations with the PKCS #11 API, complete the following steps:

1. Setup PKCS #11 Service IDs, roles, and actions. See [Setting up PKCS #11 API user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access).
2. Download, install, and configure the PKCS #11 client library. See [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto/hs-crypto-set-up-pkcs-api).

### Performing cryptographic operations with the GREP11 API
{: #cryptographic-operations-with-grep11-dashboard}

To perform cryptographic operations with the GREP11 API, you need to make sure your applications are developed with programming languages that are supported by gRPC.

The following procedure uses Golang code as an example to test GREP11 functions.

1. Install Golang by following [the instruction](https://golang.org/doc/install){: external}.
2. Clone the [sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external} into a local directory of your choice. Go modules are used for this repository, so you don't need to place the cloned repository in your `GOPATH`. Refer to the repository's README file for more information about the GREP11 Go code examples.
3. Update the following code snippet in the `examples/server_test.go` file.

    ```Golang
    var (
        Address        = "<grep11_server_address>:<port>"
        APIKey         = "<ibm_cloud_apikey>"
    )
    ```
    {: codeblock}

    In the code example,
    - Replace `<grep11_server_address>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance console, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**.
    - Replace `<ibm_cloud_apikey>` with the service ID API key that you created. The service ID API Key can be created by following the instruction in [Managing service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.

4. From the `<your_repository_path>/hpcs-grep11-go/examples` directory, execute the examples by running the `go test -v -run Example` command.

    The sample program produces output similar to the following:

    ```
    === RUN   Example_getMechanismInfo
    --- PASS: Example_getMechanismInfo (0.11s)
    === RUN   Example_generateGenericKey
    --- PASS: Example_generateGenericKey (0.09s)
    === RUN   Example_encryptAndDecryptUsingAES
    --- PASS: Example_encryptAndDecryptUsingAES (0.28s)
    === RUN   Example_digest
    --- PASS: Example_digest (0.18s)
    === RUN   Example_signAndVerifyUsingRSAKeyPair
    --- PASS: Example_signAndVerifyUsingRSAKeyPair (0.21s)
    === RUN   Example_signAndVerifyUsingDSAKeyPair
    --- PASS: Example_signAndVerifyUsingDSAKeyPair (0.99s)
    === RUN   Example_deriveKeyUsingDHKeyPair
    --- PASS: Example_deriveKeyUsingDHKeyPair (0.64s)
    === RUN   Example_signAndVerifyUsingECDSAKeyPair
    --- PASS: Example_signAndVerifyUsingECDSAKeyPair (0.16s)
    === RUN   Example_signAndVerifyToTestErrorHandling
    --- PASS: Example_signAndVerifyToTestErrorHandling (0.16s)
    === RUN   Example_wrapAndUnwrapKey
    --- PASS: Example_wrapAndUnwrapKey (0.20s)
    === RUN   Example_deriveKey
    --- PASS: Example_deriveKey (0.22s)
    === RUN   Example_tls
    --- PASS: Example_tls (0.14s)
    PASS
    ok      github.com/IBM-Cloud/hpcs-grep11-go/examples    13.106s
    ```
    {: screen}





## Before you begin
{: #get-started-prerequisites}
{: hide-dashboard}

In order to use {{site.data.keyword.hscrypto}}, make sure that you have a Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account. For more information about the {{site.data.keyword.cloud_notm}} account types, see [Account types](/docs/account?topic=account-accounts).

1. To check your account type, go to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/login){: external} and click **Management** > **Account** > **Account settings**.
2. If you have a Lite account and want to use {{site.data.keyword.hscrypto}}, [upgrade your account](/docs/account?topic=account-upgrading-account) to a Pay-As-You-Go or Subscription account. You can also [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) if you have one.

## Step 1: Provision the service
{: #provision-service}
{: hide-dashboard}

You must first create an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console. 

{{site.data.keyword.hscrypto}} offers the following pricing plans. You can find the detailed pricing plans on the [service creation page](/catalog/services/hyper-protect-crypto-services){: external}. 

* [A standard plan with the Keep Your Own Key capability](/docs/hs-crypto?topic=hs-crypto-overview)
* [An extended plan with both the Keep Your Own Key and {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-overview)

For detailed steps, see [Provisioning the service](/docs/hs-crypto?topic=hs-crypto-provision).

## Step 2: Initialize your service instance
{: #initialize-crypto}
{: hide-dashboard}
{: help}
{: support}

To manage your keys, you need to initialize your service instance first. Depending on where your service instance locates and your security requirements, {{site.data.keyword.hscrypto}} provides you with the following three approaches to initializing your service instance:

- Option 1: [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)

    This option gives you the highest security, which enables you to store and manage master key parts using smart cards.

- Option 2: [Initializing service instances using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)

    If you create your service instance in Dallas (`us-south`) or Washington DC (`us-east`) where the recovery crypto units are enabled, you can choose this approach where the master key is randomly generated within a recovery crypto unit and then exported to other crypto units. With this option, your manager key parts are safely stored the recovery crypto units in IBM Cloud. You don't need additional hardware for master key management. 

- Option 3: [Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)

    You can also initialize your service instance using master key parts that are stored in files on your local workstation. You can use this approach regardless of whether or not your service instance includes recovery crypto units. 

## Step 3 (Standard Plan only): Manage your encryption keys with the key management service
{: #manage-data-key}
{: hide-dashboard}

Follow these steps to manage your encryption keys if you are using {{site.data.keyword.hscrypto}} Standard Plan.

### Creating new keys
{: #create-keys}
{: help}
{: support}

Complete the following steps to create your first cryptographic key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To create a new key, select **Create a key**.

    Specify the key's details:

    | Setting | Description |
    | --- | --- |
    | Key type | The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select **Root key** or **Standard key**. |
    | Key name | A unique, human-readable alias for easy identification of your key. To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location. |
    {: caption="Table 1. Description of the settings to create a key" caption-side="bottom"}

3. When you finish filling out the key's details, click **Add key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-CBC algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified HSMs that are located in secure {{site.data.keyword.cloud_notm}} data centers.

### Importing your own keys
{: #import-keys}
{: help}
{: support}

You can bring your existing keys to the service so that you can still use the same encryption keys to protect your applications or data.

Complete the following steps to add an existing key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To upload an existing key, select **Import a key**.

    Specify the key's details:

    | Setting | Description |
    | --- | --- |
    | Key type | The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select **Root key** or **Standard key**. |
    | Key name | A unique, human-readable alias for easy identification of your key. To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location. |
    | Key material | The key material, such as a symmetric key, that you want to store in the {{site.data.keyword.hscrypto}} service. The key that you provide must be base64 encoded. |
    {: caption="Table 2. Description of the settings to import your own key" caption-side="bottom"}

3. When you finish filling out the key's details, click **Import key** to confirm.

From the {{site.data.keyword.cloud_notm}} console, you can inspect the general characteristics of your new keys.

## Step 3 ({{site.data.keyword.uko_full_notm}} Plan only): Manage your encryption keys in a multicloud environment with {{site.data.keyword.uko_full_notm}}
{: #manage-uko-key}
{: hide-dashboard}

Follow these steps to manage your encryption keys if you are using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}.

### Creating vaults
{: #create-vault}
{: help}
{: support}

A vault is a single repository that controls a user's or an access group's access to managed keys and target keystores through {{site.data.keyword.iamshort}} (IAM). 

Complete the following steps to create your first vault. To do so, you need to be an account owner. 

1. From your service instance UI, click **Vaults** from the navigation to view all the available vaults.
2. To create a vault, click **Create vault**.
3. Enter a name in **Vault name**. The vault name can be of 1 to 100 characters. Optionally, you can add an extended description to your vault in the **Description** section.
4. Click **Create vault** to confirm.

### Creating target keystores
{: #create-keystore}
{: help}
{: support}

A target keystore is a repository that stores the cryptographic keys. You can create an internal target keystore within the service instance or connect to an external target keystore in another service instance or even in another cloud provider, such as Microsoft Azure Key Vault, Amazon Web Services (AWS) Key Management Service (KMS), and Google Cloud KMS.

Complete the following steps to create your first internal target keystore:

1. From your service instance UI, click **Target keystores** from the navigation to view all the available keystores.
2. To create a keystore, click **Add keystore**.
3. Under **Vault**, select the vault that you create, and click **Next**. 

   If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

4. Under **Keystore type**, select **KMS Keystore** and click **Next**.
5. Under **Keystore properties**, enter a name in **Keystore name**. And then, click **Next**.
6. Under **Summary**, you can view the summary of the keystore that you create, including the keystore type, the assigned vault, and general properties. 
7. After you confirm the keystore details, click **Create keystore** to create the keystore.

### Creating managed keys
{: #create-managed-key}
{: help}
{: support}

You can use a managed key for encryption or decryption only after it is created and activated in at least one keystore. Complete the following steps to create your first managed key and activate the key in the keystore that you create:

1. From your service instance UI, click **Managed keys** from the navigation to view all the available keys.
2. To create a managed key, click **Create key**.
3. Under **Vault**, select the vault that you create, and click **Next**. 
4. Under **General**, select **IBM Cloud KMS** as the keystore type, and click **Next**.
5. Under **Key properties**, specify the following details of the key. Click **Next** to continue when you are done.

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encrytion. Active keys are automatically activated in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. Automatic state change is to be triggered on the planned date. |
    | Expiration date      | Plan a date to deactivate the key. Automatic state change is to be triggered on the planned date. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: caption="Table 3. Managed key properties" caption-side="bottom"}

6. Under **Target keystores**, select the keystore that you create. 
7. Under **Summary**, view the summary of your key, and then click **Create key** to confirm.

## Step 4: Encrypt your data with cloud HSM
{: #encrypt-data-hsm}
{: hide-dashboard}

You can remotely access {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations with the PKCS #11 API or with the GREP11 API.

### Performing cryptographic operations with the PKCS #11 API
{: #cryptographic-operations-with-pkcs11-dashboard}
{: help}
{: support}

To perform cryptographic operations with the PKCS #11 API, complete the following steps:

1. Setup PKCS #11 Service IDs, roles, and actions. See [Setting up PKCS #11 API user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access).
2. Download, install, and configure the PKCS #11 client library. See [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto/hs-crypto-set-up-pkcs-api).

### Performing cryptographic operations with the GREP11 API
{: #cryptographic-operations-with-grep11-dashboard}
{: help}
{: support}

To perform cryptographic operations with the GREP11 API, you need to make sure your applications are developed with programming languages that are supported by gRPC.

The following procedure uses Golang code as an example to test GREP11 functions.

1. Install Golang by following [the instruction](https://golang.org/doc/install){: external}.
2. Clone the [sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external} into a local directory of your choice. Go modules are used for this repository, so you don't need to place the cloned repository in your `GOPATH`. Refer to the repository's README file for more information about the GREP11 Go code examples.
3. Update the following code snippet in the `examples/server_test.go` file.

    ```Golang
    var (
        Address        = "<grep11_server_address>:<port>"
        APIKey         = "<ibm_cloud_apikey>"
    )
    ```
    {: codeblock}

    In the code example,
    - Replace `<grep11_server_address>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance console, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**.
    - Replace `<ibm_cloud_apikey>` with the service ID API key that you created. The service ID API Key can be created by following the instruction in [Managing service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.

4. From the `<your_repository_path>/hpcs-grep11-go/examples` directory, execute the examples by running the `go test -v -run Example` command.

    The sample program produces output similar to the following:

    ```
    === RUN   Example_getMechanismInfo
    --- PASS: Example_getMechanismInfo (0.11s)
    === RUN   Example_generateGenericKey
    --- PASS: Example_generateGenericKey (0.09s)
    === RUN   Example_encryptAndDecryptUsingAES
    --- PASS: Example_encryptAndDecryptUsingAES (0.28s)
    === RUN   Example_digest
    --- PASS: Example_digest (0.18s)
    === RUN   Example_signAndVerifyUsingRSAKeyPair
    --- PASS: Example_signAndVerifyUsingRSAKeyPair (0.21s)
    === RUN   Example_signAndVerifyUsingDSAKeyPair
    --- PASS: Example_signAndVerifyUsingDSAKeyPair (0.99s)
    === RUN   Example_deriveKeyUsingDHKeyPair
    --- PASS: Example_deriveKeyUsingDHKeyPair (0.64s)
    === RUN   Example_signAndVerifyUsingECDSAKeyPair
    --- PASS: Example_signAndVerifyUsingECDSAKeyPair (0.16s)
    === RUN   Example_signAndVerifyToTestErrorHandling
    --- PASS: Example_signAndVerifyToTestErrorHandling (0.16s)
    === RUN   Example_wrapAndUnwrapKey
    --- PASS: Example_wrapAndUnwrapKey (0.20s)
    === RUN   Example_deriveKey
    --- PASS: Example_deriveKey (0.22s)
    === RUN   Example_tls
    --- PASS: Example_tls (0.14s)
    PASS
    ok      github.com/IBM-Cloud/hpcs-grep11-go/examples    13.106s
    ```
    {: screen}



## What's next
{: #get-started-next}

- {{site.data.keyword.hscrypto}} helps you meet compliance requirements and ensures the security of your data. Check out the [compliance standards and criteria](/docs/hs-crypto?topic=hs-crypto-security-and-compliance) {{site.data.keyword.hscrypto}} has been certified.

- {{site.data.keyword.hscrypto}} provides advanced encryption to your at-rest data with envelope encryption, check out [Protecting your data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to see how it works.

- You can use {{site.data.keyword.hscrypto}} as the encryption key provider for other services such as {{site.data.keyword.cos_full_notm}} to bring your own encryption to your applications or data. Check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services) for the full list of supported services.

- To learn more about {{site.data.keyword.hscrypto}} concepts and terminologies, check out [Components and concepts](/docs/hs-crypto?topic=hs-crypto-understand-concepts).

- If you are using the Standard Plan, manage your keys with [{{site.data.keyword.hscrypto}} key management service API](/apidocs/hs-crypto){: external} and [{{site.data.keyword.keymanagementserviceshort}} CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli).

 - If you are using the {{site.data.keyword.uko_full_notm}} Plan, manage your keys and keystores with [manage your keys with {{site.data.keyword.uko_full_notm}} API](/apidocs/uko){: external}. 

- Encrypt your data and perform cryptographic operations with the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) or the [GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
