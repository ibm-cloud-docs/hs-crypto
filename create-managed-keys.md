---

copyright:
  years: 2022
lastupdated: "2022-11-24"

keywords: Unified Key Orchestrator, create key, key management, kms key, UKO key

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}


# Creating managed keys
{: #create-managed-keys}

You can use {{site.data.keyword.uko_full_notm}} to create managed keys with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

Before you create a managed key, keep in mind the following considerations:

- For access management, you need to assign a managed key to a vault upon creation.
- A managed key can be assigned to only one vault.
- A managed key can be used for encryption and decryption only after you activate it in at least one keystore. 
- You need to select the keystore type when you create a managed key. The keystore type that you select determines where the managed key is to be stored. The keystore type cannot be changed later.
- Activating a managed key in multiple keystores enables redundancy.
- To protect your privacy, do not store your personal data as metadata for your managed key.

## Creating managed keys with the {{site.data.keyword.cloud_notm}} console
{: #create-managed-keys-ui}
{: ui}

To create a managed key by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. To create a managed key, click **Create key**.
4. Under **Vault**, select a vault for the key for access control, and click **Next**. 
   
   If you want to assign the key to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults). 

5. Under **Keystore type**, select one of the following keystore types depending on which type of keystore you want to create the key in. And then, click **Next**. 

    - **AWS Key Management Service**: Create a key to be used and stored in an AWS Key Management Service instance.
    - **Azure Key Vault**: Create a key to be used and stored in an Azure Key Vault.
    - **Google Cloud KMS**: Create a key to be used and stored in a Google Cloud KMS keystore.
    - **IBM Cloud KMS**: Create a key to be used and stored in an {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} keystore.
    - **IBM {{site.data.keyword.keymanagementserviceshort}}**: Create a key to be used and stored in an IBM {{site.data.keyword.keymanagementserviceshort}} key ring.
    
   
   After a keystore type is selected, you can activate the key in keystores of this type only. If you select **IBM KMS**, the created key is a root key that can be used for [envelope encryption](/docs/hs-crypto?topic=hs-crypto-kms-envelope-encryption).
   {: note}

6. Under **Key properties**, specify the following details of the key. Click **Next** to continue when you are done.

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1 - 255 characters in length. The characters can be letters (case-sensitive), digits (0 - 9), or symbols (/_-). However, do not start the name with `AWS/`. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | _Pre-active_ keys are not to be activated in target keystores until you manually activate them. _Active_ keys are to be automatically activated in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the _Pre-active_ key. No automatic state change is triggered. |
    | Expiration date      | Plan a date to deactivate the key. No automatic state change is triggered. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-1}
    {: caption="Table 1. AWS Key Management Service keys properties" caption-side="bottom"}
    {: tab-title="AWS Key Management Service keys"}
    {: tab-group="Managed key properties"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1 - 24 characters in length. The characters can be letters (case-sensitive), digits (0 - 9), or hyphens (-). |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | _Pre-active_ keys are not to be activated in target keystores until you manually activate them. _Active_ keys are to be automatically activated in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the _Pre-active_ key. No automatic state change is triggered. |
    | Expiration date      | Plan a date to deactivate the key. No automatic state change is triggered. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-2}
    {: caption="Table 2. Azure Key Vault keys properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault keys"}
    {: tab-group="Managed key properties"}
    {: class="comparison-tab-table"}

    
    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1 - 63 characters in length. The characters can be letters (case-sensitive), digits (0 - 9), or symbols (_-). |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Protection level     | **HSM-protected key** protection level applies to keys that are protected by FIPS 140-2 Level 3 Hardware Security Modules (HSMs) in Google Cloud. This type of keys ensures the highest security. **Software-protected key** protection level applies to keys that are protected by software. You can choose this level to [reduce cost](https://cloud.google.com/kms/pricing){: external}. For more information, see [Cloud KMS software backend: SOFTWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#software-protection-level){: external} and [Cloud KMS HSM backend: HARDWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#hardware-protection-level){: external}.   |
    | Purpose               | The cryptographic capabilities of the key, which is what you are going to do with this key. The purpose also determines the available key algorithms. The supported key purposes are **Symmetric encrypt/decrypt**, **Asymmetric sign**, **Asymmetric decrypt**, and **MAC signing/verification**. For more information, see [Key purpose](https://cloud.google.com/kms/docs/algorithms#key_purposes){: external}.   |
    | Key algorithm |  The corresponding key algorithms that are supported for each key purpose. Algorithms define what parameters are needed for cryptographic operations. For the list of available key algorithms, see [Key purposes and algorithms](https://cloud.google.com/kms/docs/algorithms){: external}.  |
    | State                | _Pre-active_ keys are not to be activated in target keystores until you manually activate them. _Active_ keys are to be automatically activated in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the _Pre-active_ key. No automatic state change is triggered. |
    | Expiration date      | Plan a date to deactivate the key. No automatic state change is triggered. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-3}
    {: caption="Table 3. Google Cloud KMS keys properties" caption-side="bottom"}
    {: tab-title="Google Cloud KMS keys"}
    {: tab-group="Managed key properties"}
    {: class="comparison-tab-table"}
    

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must 2 - 50 characters in length. The characters can be letters (case-sensitive), digits (0 - 9), or spaces.|
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | _Pre-active_ keys are not to be activated in target keystores until you manually activate them. _Active_ keys are to be automatically activated in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the _Pre-active_ key. No automatic state change is triggered. |
    | Expiration date      | Plan a date to deactivate the key. No automatic state change is triggered. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-4}
    {: caption="Table 4. IBM Cloud KMS keys properties" caption-side="bottom"}
    {: tab-title="IBM Cloud KMS keys"}
    {: tab-group="Managed key properties"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 2 - 50 characters in length. The characters can be letters (case-sensitive), digits (0 - 9), or spaces. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | _Pre-active_ keys are not to be activated in target keystores until you manually activate them. _Active_ keys are to be automatically activated in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the _Pre-active_ key. No automatic state change is triggered. |
    | Expiration date      | Plan a date to deactivate the key. No automatic state change is triggered. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-5}
    {: caption="Table 5. {{site.data.keyword.keymanagementserviceshort}} keys properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.keymanagementserviceshort}} keys"}
    {: tab-group="Managed key properties"}
    {: class="comparison-tab-table"}

7. Under **Target keystores**, you can select one or multiple target keystores to activate the managed key in. Activating a key in multiple keystores enables redundancy. You can also activate the key later by following instructions in [Setting target keystores for existing keys](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

    If there are no existing keystores, you can click **Add keystore** to [create internal KMS keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [connect to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores). The corresponding keystore type is selected for you.

    You can use the key for encryption or decryption only after it is activated in at least one keystore.
    {: important}

8. Under **Summary**, view the summary of your key, and then click **Create key** to confirm.

You have successfully created a managed key. 


## Creating managed keys with the API
{: #create-managed-keys-api}
{: api}

To create a managed key through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `POST` call to the following endpoint.
    
    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/templates
    ```
    {: codeblock}

3. Create a managed key based on the supplied template by making a `POST` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/managed_keys
    ```
    {: codeblock}

    The managed key is to be activated in all keystores in the keystore group that is defined in the key template.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-managed-key){: external}.



## What's next
{: #create-managed-keys-next}

- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  
- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
  
- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).

