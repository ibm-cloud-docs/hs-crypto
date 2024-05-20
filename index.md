---

copyright:
  years: 2018, 2024
lastupdated: "2024-05-20"

keywords: ibm cloud hyper protect crypto services, hyper protect crypto services, hpcs, crypto, crypto services, key management, kms, dedicated key management, hsm, hardware security module, cloud hsm, dedicated hsm, keep your own key, kyok, cryptographic operation, key storage, encryption key, cloud encryption, encryption at rest

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}



# Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) is a dedicated key management service and hardware security module (HSM) based on {{site.data.keyword.cloud_notm}}. With this service, you can take the ownership of the cloud HSM to fully manage your encryption keys and to perform cryptographic operations. {{site.data.keyword.hscrypto}} is also the only service in the cloud industry that is built on FIPS 140-2 Level 4-certified hardware. The {{site.data.keyword.uko_full_notm}} function provides the only cloud native single-point-of-control of encryption keys across hybrid multicloud environments of your enterprise.
{: shortdesc}

This tutorial shows you the high-level steps on how to set up your service instance by loading your master keys, create and manage encryption keys with the UI, and perform cryptographic operations with the PKCS #11 API or with the GREP11 API.

- [Step 1: Initialize your service instance](#initialize-crypto)
- [Step 2 (Standard Plan only): Create keys](#create-key-standard)
- [Step 2 ({{site.data.keyword.uko_full_notm}} Plan only): Manage your encryption keys](#manage-uko-key)
- [Step 3: Encrypt your data with cloud HSM](#encrypt-data-hsm)

## Before you begin
{: #get-started-prerequisites}
{: hide-dashboard}

In order to use {{site.data.keyword.hscrypto}}, make sure that you meet the following prerequisites:

1. You have a Pay-As-You-Go or Subscription [{{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-accounts){: external}.
    
    You can use promo code `HPCRYPTO30` to get two crypto units at no charge for 30 days.
    {: tip}

2. You have [provisioned a service instance](/docs/hs-crypto?topic=hs-crypto-provision) with either of the following plans:

    - [A standard plan with the Keep Your Own Key capability](/docs/hs-crypto?topic=hs-crypto-overview)
    - [An extended plan with both Keep Your Own Key and {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-overview)

## Step 1: Initialize your service instance
{: #initialize-crypto}

Depending on where your service instance locates and your security requirements, {{site.data.keyword.hscrypto}} provides you with the following three options to initialize your service instance:

- Option 1: [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)

    This option gives you the highest security, which enables you to store and manage master key parts by using smart cards.

- Option 2: [Initializing service instances using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)

    You can choose this option if you create your service instance in regions where the recovery crypto units are enabled. With this option, the master key is randomly generated within a recovery crypto unit and then automatically exported to other crypto units. You can manage the master key and complete the instance initialization with minimal effort.

- Option 3: [Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)

    You can also initialize your service instance using master key parts that are stored in files on your local workstation. You can use this approach regardless of whether or not your service instance includes recovery crypto units.

## Step 2 (Standard Plan only): Create keys
{: #create-key-standard}

With the Standard Plan, you can create root keys or standard keys for data encryption. Complete the following steps to create your first cryptographic key. To complete these steps, make sure that you are the {{site.data.keyword.cloud_notm}} account owner or are assigned the *writer* role. For details, see [Assigning access to {{site.data.keyword.hscrypto}} in the UI](/docs/hs-crypto?topic=hs-crypto-manage-access).

1. From the UI, click **KMS keys** &gt; **Add key**.
2. Select **Create a key**. 
3. Specify **[Root key](/docs/hs-crypto?topic=hs-crypto-understand-concepts&interface=ui#root-key-concept)** or **[Standard key](/docs/hs-crypto?topic=hs-crypto-understand-concepts&interface=ui#standard-key-concept)** as the key type and enter a unique name for your key. Ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location.
4. Click **Add key** to confirm.

The created key is a symmetric 256-bit key, supported by the AES-CBC algorithm. You can inspect the general characteristics of your keys in the **Key management service keys** table. You can also bring your own keys by [importing the base64-encoded key materials](/docs/hs-crypto?topic=hs-crypto-import-root-keys).

## Step 2 ({{site.data.keyword.uko_full_notm}} Plan only): Manage your encryption keys
{: #manage-uko-key}

Follow these steps to manage your encryption keys if you are using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}. To complete these steps, make sure that you are the {{site.data.keyword.cloud_notm}} account owner or are assigned the *Vault administrator* role. For details, see [Assigning access to {{site.data.keyword.hscrypto}} in the UI](/docs/hs-crypto?topic=hs-crypto-uko-manage-access).

### 1. Create vaults
{: #create-vault}

A vault is a single repository that controls a user's or an access group's access to managed keys and keystores through {{site.data.keyword.iamshort}} (IAM). 

Complete the following steps to create your first vault:

1. From your service instance UI, click **Vaults** from the navigation to view all the available vaults.
2. Click **Create vault**.
3. Enter a name in **Vault name**. The vault name can be of 1 to 100 characters. Optionally, you can add an extended description to your vault in the **Description** section.
4. Click **Create vault** to confirm.

### 2. Create keystores
{: #create-keystore}

A keystore is a repository that stores the cryptographic keys. You can create an internal keystore within the service instance or connect to an external keystore in another service instance or even in another cloud provider, such as Microsoft Azure Key Vault, Amazon Web Services (AWS) Key Management Service (KMS), and Google Cloud KMS.

Complete the following steps to create your first internal keystore:

1. From your service instance UI, click **Keystores** from the navigation to view all the available keystores.
2. Click **Add keystore**.
3. Under **Vault**, select the vault that you create, and click **Next**. If you want to assign the keystore to a new vault, click **Create vault**.
4. Under **Keystore type**, select **IBM Cloud KMS** and click **Next**.
5. Under **Keystore properties**, enter a name in **Keystore name**. The keystore name can be of 1 to 100 characters. And then, click **Next**.
6. Under **Summary**, you can view the summary of the keystore that you create, including the keystore type, the assigned vault, and general properties.
7. After you confirm the keystore details, click **Create keystore** to create the keystore. 

### 3. Create key templates
{: #create-key-template}

key template specifies the properties of the managed keys to be created, such as the naming convention, key algorithm, and key length. 

Complete the following steps to create your first key template:

1. From your service instance UI, click **Key templates** from the navigation.
2. Click **Create key template**.
3. Under **Vault**, select the vault that you've just created and then click **Next**. 
4. Under **Keystores**, select **IBM Cloud KMS** as the keystore type, select the keystore you've just created, and then click **Next**.
5. Under **Key template properties**, specify the following details of the key template. Click **Next** to continue.
6. Under **Summary**, view the summary of your key template, and then click **Create key template** to complete the key template creation.

### 4. Create managed keys
{: #create-managed-key}

You can use a managed key for encryption or decryption only after it is created and activated in at least one keystore. Complete the following steps to create your first IBM Cloud KMS key and activate the key in the keystore that you create:

1. From your service instance UI, click **Managed keys** from the navigation to view all the available keys.
2. Click **Create key**.
3. Under **Vault**, select the vault that you've just created and then click **Next**. 
4. Under **Key template**, select **Create from a key template** and then select the key template that you've just created and click **Next**. 
5. Under **Key properties**, specify details of the key. Click **Next** to continue when you are done. Note that `Pre-active` keys are not to be installed in keystores until you manually activate them. `Active` keys are to be automatically installed in the keystores. For more information about the key properties, see [Creating managed keys with a key template in the IBM Cloud UI](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=ui#create-managed-keys-template-ui).
6. Under **Summary**, view the summary of your key, and then click **Create key** to create the key.

## Step 3: Encrypt your data with cloud HSM
{: #encrypt-data-hsm}

You can remotely access {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations with the PKCS #11 API or with the GREP11 API. To complete these steps, make sure that you are the {{site.data.keyword.cloud_notm}} account owner or are assigned the *writer* role. For details, see [Assigning access to {{site.data.keyword.hscrypto}} in the UI](/docs/hs-crypto?topic=hs-crypto-manage-access&interface=ui#assign-access-console).

### Performing cryptographic operations with the PKCS #11 API
{: #cryptographic-operations-with-pkcs11}

To perform cryptographic operations with the PKCS #11 API, complete the following steps:

1. Set up PKCS #11 Service IDs, roles, and actions. For more information, see [Setting up PKCS #11 API user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access).
2. Download, install, and configure the PKCS #11 client library. For more information about configuring the PKCS #11 client library, see [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api).

### Performing cryptographic operations with the GREP11 API
{: #cryptographic-operations-with-grep11}

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
    - Replace `<grep11_server_address>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance UI, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**.
    - Replace `<ibm_cloud_apikey>` with the [service ID API key](/docs/account?topic=account-serviceidapikeys){: external} that you created.

4. From the `<your_repository_path>/hpcs-grep11-go/examples` directory, execute the examples by running the `go test -v -run Example` command.
