---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-09"

keywords: Unified Key Orchestrator, create key, key management, kms key, UKO key

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Creating managed keys
{: #create-managed-keys}


You can use {{site.data.keyword.uko_full_notm}} to create a managed key with a key template to have predefined key properties, or you can create a managed key with custom properties to have full customized control.
{: shortdesc}

Before you create a managed key, keep in mind the following considerations:

- For access management, you need to assign a managed key to a vault upon creation.
- A managed key can be assigned to only one vault.
- A managed key can be used for encryption and decryption only after you activate it in at least one keystore. 
- You need to select the keystore type when you create a managed key. The keystore type that you select determines where the managed key is to be stored. The keystore type cannot be changed later.
- Distributing a managed key in multiple keystores enables redundancy.
- To protect your privacy, do not store your personal data as metadata for your managed key.
- You can create a managed key with only one key template. 
- Currently, importing managed keys is not supported. You can create managed keys with {{site.data.keyword.uko_full_notm}} only.


## Creating managed keys with a key template in the UI
{: #create-managed-keys-template-ui}
{: ui}

When you select the **Create with a key template** option, you are creating a managed key with key properties that are predefined by your administrator. This option ensures that your key is compliant with the predefined standards. To create a managed key with a key template by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. To create a managed key, click **Create key**. 

   

4. Under **Vault**, select a vault for the key for access control, and click **Next**. 
   
   If you want to assign the key to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Key template**, select **Create from a key template** to create a key by following predefined properties.

6. Select a key template for the key and click **Next**. You can select only one key template for a key. 

7. Under **Key properties**, specify the following details of the key. 

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1–250 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (/_-). However, do not start the name with `AWS/`. \n \n **Important:** If the key naming scheme is defined in the key template, you need to enter values for each custom placeholder. Each placeholder must be at least 2 characters in length. The characters can be letters (case-sensitive), digits (0-9), or spaces. An example of the managed key name must not exceed 50 characters in length. You can also specify the extended description for your key. Note that you cannot modify the key name after the key creation.  |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | State                | The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      | Plan a date to deactivate the key. It is for planning purpose only. |
    | Key algorithm            |  (Read only) The encryption algorithm to encrypt data for the key.           | 
    | Key length           | (Read only) The number of bits that represents the encryption strength of the key.   |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-1}
    {: caption="AWS Key Management Service keys properties" caption-side="bottom"}
    {: tab-title="AWS Key Management Service keys"}
    {: tab-group="Managed key properties with templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1–127 characters in length. The characters can be letters (case-sensitive), digits (0–9), or hyphens (-). \n \n **Important:** If the key naming scheme is defined in the key template, you need to enter values for each custom placeholder. Each placeholder must be at least 2 characters in length. The characters can be letters (case-sensitive), digits (0-9), or spaces. An example of the managed key name must not exceed 50 characters in length. You can also specify the extended description for your key. Note that you cannot modify the key name after the key creation.   |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Protection level     | (Read only) Data protection level of keys to be created with the key template. \n \n **HSM-protected key** is stored and generated in a FIPS-certified Hardware Security Module. It is available in Azure Key Vault (Premium) only. This type of keys ensures the highest security. \n \n **Software-protected key** is available in both Azure Key Valut (Standard) and Key Vault (Premium). You can choose this level to [reduce cost](https://azure.microsoft.com/en-us/pricing/details/key-vault/){: external}.  |
    | Key algorithm        | (Read only) The encryption algorithm to encrypt data for the key.     |
    | Key length           | (Read only) The number of bits that represents the encryption strength of the key.   |
    | State                |  The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). |
    | Activation date      |  Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      |  Plan a date to deactivate the key. It is for planning purpose only. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-2}
    {: caption="Azure Key Vault keys properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault keys"}
    {: tab-group="Managed key properties with templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1–63 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (_-).  \n \n **Important:** If the key naming scheme is defined in the key template, you need to enter values for each custom placeholder. Each placeholder must be at least 2 characters in length. The characters can be letters (case-sensitive), digits (0-9), or spaces. An example of the managed key name must not exceed 50 characters in length. You can also specify the extended description for your key. Note that you cannot modify the key name after the key creation.  |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Key state                |  The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). |
    | Activation date      |  Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      |  Plan a date to deactivate the key. It is for planning purpose only. |
    | Protection level     |  (Read only) **HSM-protected key** protection level applies to keys that are protected by FIPS 140-2 Level 3 Hardware Security Modules (HSMs) in Google Cloud. This type of keys ensures the higher security. **Software-protected key** protection level applies to keys that are protected by software. You can choose this level to [reduce cost](https://cloud.google.com/kms/pricing){: external}. For more information, see [Cloud KMS software backend: SOFTWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#software-protection-level){: external} and [Cloud KMS HSM backend: HARDWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#hardware-protection-level){: external}. \n \n **Note:** Software-protected keys don't support the Elliptic curve `secp256k1` algorithm.  |
    | Purpose               |  (Read only) The cryptographic capabilities of the key, which is what you are going to do with this key. The purpose also determines the available key algorithms. The supported key purposes are **Symmetric encrypt/decrypt**, **Asymmetric sign**, **Asymmetric decrypt**, and **MAC signing/verification**. For more information, see [Key purpose](https://cloud.google.com/kms/docs/algorithms#key_purposes){: external}.   |
    | Key algorithm |   (Read only) The corresponding key algorithms that are supported for each key purpose. Algorithms define what parameters are needed for cryptographic operations. For the list of available key algorithms, see [Key purposes and algorithms](https://cloud.google.com/kms/docs/algorithms){: external}.  |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-3}
    {: caption="Google Cloud KMS keys properties" caption-side="bottom"}
    {: tab-title="Google Cloud KMS keys"}
    {: tab-group="Managed key properties with templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces. \n \n **Important:** If the key naming scheme is defined in the key template, you need to enter values for each custom placeholder. Each placeholder must be at least 2 characters in length. The characters can be letters (case-sensitive), digits (0-9), or spaces. An example of the managed key name must not exceed 50 characters in length. You can also specify the extended description for your key. Note that you cannot modify the key name after the key creation. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Key state                |  The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). |
    | Activation date      |  Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      |  Plan a date to deactivate the key. It is for planning purpose only. |
    | Key algorithm            |  (Read only) The encryption algorithm to encrypt data for the key.           | 
    | Key length           | (Read only) The number of bits that represents the encryption strength of the key.   |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-4}
    {: caption="IBM Cloud KMS keys properties" caption-side="bottom"}
    {: tab-title="IBM Cloud KMS keys"}
    {: tab-group="Managed key properties with templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces. \n \n **Important:** If the key naming scheme is defined in the key template, you need to enter values for each custom placeholder. Each placeholder must be at least 2 characters in length. The characters can be letters (case-sensitive), digits (0-9), or spaces. An example of the managed key name must not exceed 50 characters in length. You can also specify the extended description for your key. Note that you cannot modify the key name after the key creation.|
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Key state                |  The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). |
    | Activation date      |  Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      |  Plan a date to deactivate the key. It is for planning purpose only. |
    | Key algorithm |   (Read only) The encryption algorithm to encrypt data for the key.           | 
    | Key length           | (Read only) The number of bits that represents the encryption strength of the key.   |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-5}
    {: caption="{{site.data.keyword.keymanagementserviceshort}} keys properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.keymanagementserviceshort}} keys"}
    {: tab-group="Managed key properties with templates"}
    {: class="comparison-tab-table"}  



8. View the key properties defined by the selected key template and click **Next** to continue.

9. Under **Summary**, view the summary of your key, and then click **Create key** to confirm.

You have successfully created a managed key. 

If you are creating internal KMS keys during the master key rotation, internal KMS keys can still be created successfully. However, an **Out of sync** flag is displayed next to the key state. For each of these keys, you can sync keys by selecting **Show details** on the Actions ![Actions icon](../icons/action-menu-icon.svg "Actions") menu and clicking **Sync key** after the master key rotation is completed. 
{: note}

## Creating managed keys with a key template through the API
{: #create-managed-keys-template-api}
{: api}

You can create a managed key with key properties that are predefined by your administrator. This option ensures your key is compliant with the predefined standards. To create a managed key with a key template through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `POST` call to the following endpoint.

    
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/templates
    
    ```
    {: codeblock}

3. Create a managed key based on the supplied template by making a `POST` call to the following endpoint.

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/managed_keys
    
    ```
    {: codeblock}

    The managed key is to be activated in all keystores in the keystore group that is defined in the key template.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-managed-key){: external}. 

## Creating managed keys with custom properties in the UI
{: #create-managed-keys-ui}
{: ui}

When you select the **Create with custom properties** option, you are creating a managed key from scratch. This option gives you the flexibility to create a customized key with full control by yourself. To create a managed key with custom properties by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. To create a managed key, click **Create key**.
   
   
   
4. Under **Vault**, select a vault for the key for access control, and click **Next**. 
   
   If you want to assign the key to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Key template**, select **Create with custom properties** to create a key without a key template.

6. Under **Keystore type**, select one of the following keystore types depending on which type of keystore you want to create the key in. And then, click **Next**. 

    - **AWS Key Management Service**: Create a key to be used and stored in an AWS Key Management Service instance.
    - **Azure Key Vault**: Create a key to be used and stored in an Azure Key Vault.
    - **Google Cloud KMS**: Create a key to be used and stored in a Google Cloud KMS keystore.
    - **IBM Cloud KMS**: Create a key to be used and stored in an {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} keystore.
    - **IBM {{site.data.keyword.keymanagementserviceshort}}**: Create a key to be used and stored in an IBM {{site.data.keyword.keymanagementserviceshort}} key ring. 
    
   
     
   After a keystore type is selected, you can activate the key in keystores of this type only. If you select **IBM Cloud KMS**, the created key is a root key that can be used for [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) .
   {: note}

7. Under **Keystores**, you can select one or multiple keystores to activate the managed key in. Activating a key in multiple keystores enables redundancy.

    
    If there are no existing keystores, you can click **Add keystore** to [create internal KMS keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [connect to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores). The corresponding keystore type is selected for you. 

    

     
    You can use the key for encryption or decryption only after it is activated in at least one keystore. 
    {: important}

8. Under **Key properties**, specify the following details of the key. Click **Next** to continue when you are done. 

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1–250 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (/_-). However, do not start the name with `AWS/`. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Key algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Key length               | The number of bits that represents the encryption strength of the key.   |
    | Key state                | The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      | Plan a date to deactivate the key. It is for planning purpose only. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-6}
    {: caption="AWS Key Management Service keys properties" caption-side="bottom"}
    {: tab-title="AWS Key Management Service keys"}
    {: tab-group="Managed key properties without templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1–127 characters in length. The characters can be letters (case-sensitive), digits (0–9), or hyphens (-). \n \n **Important:** If the key naming scheme is defined in the key template, you need to enter values for each custom placeholder. Each placeholder must be at least 2 characters in length. The characters can be letters (case-sensitive), digits (0-9), or spaces. An example of the managed key name must not exceed 50 characters in length. You can also specify the extended description for your key. Note that you cannot modify the key name after the key creation.   |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Protection level     | Data protection level of keys to be created with the key template. \n \n **HSM-protected key** is stored and generated in a FIPS-certified Hardware Security Module. It is available in Azure Key Vault (Premium) only. This type of keys ensures the highest security. \n \n **Software-protected key** is available in both Azure Key Valut (Standard) and Key Vault (Premium). You can choose this level to [reduce cost](https://azure.microsoft.com/en-us/pricing/details/key-vault/){: external}. \n \n **Note:** If you connect to an external keystore of type Azure Key Vault, you can distribute both HSM-protected keys and software-protected keys to Azure Key Vault (Premium). However, you can distribute only software-protected keys to Azure Key Vault (Standard). |
    | Key algorithm        | The encryption algorithm to encrypt data for the key.     |
    | Key length           | The number of bits that represents the encryption strength of the key.   |
    | State                | The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      | Plan a date to deactivate the key. It is for planning purpose only. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-7}
    {: caption="Azure Key Vault keys properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault keys"}
    {: tab-group="Managed key properties without templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 1–63 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (_-). |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Protection level     | **HSM-protected key** protection level applies to keys that are protected by FIPS 140-2 Level 3 Hardware Security Modules (HSMs) in Google Cloud. This type of keys ensures the higher security. \n \n **Software-protected key** protection level applies to keys that are protected by software. You can choose this level to [reduce cost](https://cloud.google.com/kms/pricing){: external}. For more information, see [Cloud KMS software backend: SOFTWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#software-protection-level){: external} and [Cloud KMS HSM backend: HARDWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#hardware-protection-level){: external}. \n \n **Note:** Software-protected keys don't support the Elliptic curve `secp256k1` algorithm.  |
    | Purpose               | The cryptographic capabilities of the key, which is what you are going to do with this key. The purpose also determines the available key algorithms. The supported key purposes are **Symmetric encrypt/decrypt**, **Asymmetric sign**, **Asymmetric decrypt**, and **MAC signing/verification**. For more information, see [Key purpose](https://cloud.google.com/kms/docs/algorithms#key_purposes){: external}.   |
    | Key algorithm |  The corresponding key algorithms that are supported for each key purpose. Algorithms define what parameters are needed for cryptographic operations. For the list of available key algorithms, see [Key purposes and algorithms](https://cloud.google.com/kms/docs/algorithms){: external}.  |
    | State                | The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      | Plan a date to deactivate the key. It is for planning purpose only. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-8}
    {: caption="Google Cloud KMS keys properties" caption-side="bottom"}
    {: tab-title="Google Cloud KMS keys"}
    {: tab-group="Managed key properties without templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces.|
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Key algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Key length               | The number of bits that represents the encryption strength of the key.   |
    | State                | The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      | Plan a date to deactivate the key. It is for planning purpose only. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-9}
    {: caption="IBM Cloud KMS keys properties" caption-side="bottom"}
    {: tab-title="IBM Cloud KMS keys"}
    {: tab-group="Managed key properties without templates"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key. It must be 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces. |
    | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
    | Key algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Key length               | The number of bits that represents the encryption strength of the key.   |
    | State                | The initial state of the key, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activation date      | Plan a date to activate the Pre-active key. It is for planning purpose only. |
    | Expiration date      | Plan a date to deactivate the key. It is for planning purpose only. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: #table-10}
    {: caption="{{site.data.keyword.keymanagementserviceshort}} keys properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.keymanagementserviceshort}} keys"}
    {: tab-group="Managed key properties without templates"}
    {: class="comparison-tab-table"} 



9. Under **Summary**, view the summary of your key, and then click **Create key** to confirm.

You have successfully created a managed key. 

 
If you are creating internal KMS keys during the master key rotation, internal KMS keys can still be created successfully. However, an **Out of sync** flag is displayed next to the key state. For each of these keys, you can sync keys by selecting **Show details** on the Actions ![Actions icon](../icons/action-menu-icon.svg "Actions") menu and clicking **Sync key** after the master key rotation is completed. 
{: note}


## Creating managed keys with custom properties through the API
{: #create-managed-keys-api}
{: api}

You can create a managed key from scratch. This option gives you the flexibility to create a customized key with full control by yourself. To create a managed key with custom properties through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `POST` call to the following endpoint.
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/templates
    
    ```
    {: codeblock}

3. Create a managed key based on the supplied template by making a `POST` call to the following endpoint.

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/managed_keys
    
    ```
    {: codeblock}

    The managed key is to be activated in all keystores in the keystore group that is defined in the key template.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-managed-key){: external}.



## What's next
{: #create-managed-keys-next}

- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  
- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
  
- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).
