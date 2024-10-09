---

copyright:
  years: 2022, 2024
lastupdated: "2024-10-09"

keywords: Unified Key Orchestrator, create, key templates, keys, keystores, key management, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Creating key templates
{: #create-template}

A key template specifies the properties of the managed keys to be created, such as the naming convention, key algorithm, and key length. You can create a key template from scratch or make a copy from an existing key template. After you create the key template, you can then create a group of keys with the same key properties that are defined in the key template. You can use {{site.data.keyword.uko_full_notm}} to create key templates with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API. 
{: shortdesc}

## Creating key templates from scratch with the UI
{: #create-template-ui}
{: ui}

You can create a key template from scratch with full control by yourself. To create a key template by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Key templates** from the navigation to view all the available key templates.
3. To create a key template, click **Create key template**. 

   

4. To control access to keys that are to be created with the key template, under **Vault**, select a vault and then click **Next**. All keys to be created with the key template will be managed in the selected vault.
   
   If you want to manage key access in a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Keystores**, perform the following steps: 

    * Under **Keystore type**, select one of the following keystore types, which determines the available [key template properties](#key-template-properties) and the type of key that you are going to create with the key template:

        - **AWS Key Management Service**: Create a key template for keys to be used and stored in an AWS Key Management Service instance.
        - **Azure Key Vault**: Create a key template for keys to be used and stored in an Azure Key Vault.
        - **Google Cloud KMS**: Create a key template for keys to be used and stored in a Google Cloud KMS keystore.
        - **IBM Cloud KMS**: Create a key template for keys to be used and stored in an {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} keystore.
        - **IBM {{site.data.keyword.keymanagementserviceshort}}**: Create a key template for keys to be used and stored in an IBM {{site.data.keyword.keymanagementserviceshort}} key ring.

        For more information about the keystores, see [Components](/docs/hs-crypto?topic=hs-crypto-introduce-uko&interface=ui#Components).
        
    * (Optional) Decide where your keys to be created with the key template are going to be activated or stored under **Keystores** by setting keystore group. Activating a key in multiple keystores enables redundancy. 

        If there are no existing keystores, click **Add keystore** to [create internal KMS keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [connect to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores). 

        
        After a keystore type is selected, you can create keys in keystores of this type only.
        {: note}

6. Click **Next** to continue.{: #key-template-properties}

7. Under **Key template properties**, specify the following details of the key template. Click **Next** to continue when you are done. By default, some configurations are pre-selected. However, you can change it according to your needs.


    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key template name    | A unique, human-readable name for easy identification of your key template. It must be 1–100 characters in length.  |
    | Description          | (Optional) An extended description for your key template, with up to 200 characters in length. |
    | Naming scheme        | (Optional) Enter strings or placeholders to enforce the key naming scheme. After defining the key naming scheme, you can then create a group of keys with the same key naming conventions but you cannot edit the key naming scheme any more. For more information, see [Defining key naming schemes](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#define-naming-scheme).    | 
    | Managed key name example | Read only. An example of the managed key name based on the key naming scheme is populated automatically for your reference.       |
    | Algorithm            | The encryption algorithm to encrypt data for the key to be created with the template.     |
    | Length               | The number of bits that represents the encryption strength of the key to be created with the template.   |
    | State                | The initial key state to be created with the key template, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activate keys after      | (Optional) Plan a date to activate the Pre-active keys to be created since the key creation. It is for planning purpose only. |
    | Deactivate keys after     | (Optional) Plan a date to deactivate the keys to be created since the key creation. It is for planning purpose only. |
    {: #table-1}
    {: caption="AWS Key templates properties" caption-side="bottom"}
    {: tab-title="AWS Key templates"}
    {: tab-group="Key templates from scratch properties"}
    {: class="comparison-tab-table"}


    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key template name    | A unique, human-readable name for easy identification of your key template. It must be 1–100 characters in length.  |
    | Description          | (Optional) An extended description for your key template, with up to 200 characters in length.|
    | Naming scheme        | (Optional) Enter strings or placeholders to enforce the key naming scheme. After defining the key naming scheme, you can then create a group of keys with the same key naming conventions but you cannot edit the key naming scheme any more. For more information, see [Defining key naming schemes](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#define-naming-scheme).    | 
    | Managed key name example | Read only. An example of the managed key name based on the key naming scheme is populated automatically for your reference.       |
    | Protection level     | Data protection level of keys to be created with the key template. \n \n **HSM-protected key** is stored and generated in a FIPS-certified Hardware Security Module. It is available in Azure Key Vault (Premium) only. This type of keys ensures the highest security. \n \n **Software-protected key** is available in both Azure Key Valut (Standard) and Key Vault (Premium). You can choose this level to [reduce cost](https://azure.microsoft.com/en-us/pricing/details/key-vault/){: external}. \n \n **Note:** If you connect to an external keystore of type Azure Key Vault, you can distribute both HSM-protected keys and software-protected keys to Azure Key Vault (Premium). However, you can distribute only software-protected keys to Azure Key Vault (Standard). |
    | Algorithm            | The encryption algorithm to encrypt data for the key to be created with the template.     |
    | Length               | The number of bits that represents the encryption strength of the key to be created with the template.   |
    | State                | The initial key state to be created with the key template, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activate keys after      | (Optional) Plan a date to activate the Pre-active keys to be created since the key creation. It is for planning purpose only. |
    | Deactivate keys after     | (Optional) Plan a date to deactivate the keys to be created since the key creation. It is for planning purpose only. |
    {: #table-2}
    {: caption="Azure Key templates properties" caption-side="bottom"}
    {: tab-title="Azure Key templates"}
    {: tab-group="Key templates from scratch properties"}
    {: class="comparison-tab-table"}


    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key template name    | A unique, human-readable name for easy identification of your key template. It must be 1–100 characters in length.  |
    | Description          | (Optional) An extended description for your key template, with up to 200 characters in length.|
    | Naming scheme        | (Optional) Enter strings or placeholders to enforce the key naming scheme. After defining the key naming scheme, you can then create a group of keys with the same key naming conventions but you cannot edit the key naming scheme any more. For more information, see [Defining key naming schemes](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#define-naming-scheme).    | 
    | Managed key name example | Read only. An example of the managed key name based on the key naming scheme is populated automatically for your reference.       |
    | Protection level     | Data protection level of keys to be created with the key template. \n \n **HSM-protected key** protection level applies to keys that are protected by FIPS 140-2 Level 3 Hardware Security Modules (HSMs) in Google Cloud. This type of keys ensures the higher security. \n \n **Software-protected key** protection level applies to keys that are protected by software. You can choose this level to [reduce cost](https://cloud.google.com/kms/pricing){: external}. For more information, see [Cloud KMS software backend: SOFTWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#software-protection-level){: external} and [Cloud KMS HSM backend: HARDWARE protection level](https://cloud.google.com/docs/security/key-management-deep-dive#hardware-protection-level){: external}. \n \n **Note:** Software-protected keys don't support the Elliptic curve `secp256k1` algorithm.  |
    | Purpose               |The cryptographic capabilities of the key, which is what you are going to do with this key. The purpose also determines the available key algorithms. The supported key purposes are **Symmetric encrypt/decrypt**, **Asymmetric sign**, **Asymmetric decrypt**, and **MAC signing/verification**. For more information, see [Key purpose](https://cloud.google.com/kms/docs/algorithms#key_purposes){: external}.   |
    | State                | The initial key state to be created with the key template, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activate keys after      | (Optional) Plan a date to activate the Pre-active keys to be created since the key creation. It is for planning purpose only. |
    | Deactivate keys after     | (Optional) Plan a date to deactivate the keys to be created since the key creation. It is for planning purpose only. |
    {: #table-3}
    {: caption="Google Key templates properties" caption-side="bottom"}
    {: tab-title="Google Key templates"}
    {: tab-group="Key templates from scratch properties"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key template name    | A unique, human-readable name for easy identification of your key template. It must be 1–100 characters in length.  |
    | Description          | (Optional) An extended description for your key template, with up to 200 characters in length.|
    | Naming scheme        | (Optional) Enter strings or placeholders to enforce the key naming scheme. After defining the key naming scheme, you can then create a group of keys with the same key naming conventions but you cannot edit the key naming scheme any more. For more information, see [Defining key naming schemes](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#define-naming-scheme).    | 
    | Managed key name example | Read only. An example of the managed key name based on the key naming scheme is populated automatically for your reference.       |
    | Algorithm            | The encryption algorithm to encrypt data for the key to be created with the template.     |
    | Length               | The number of bits that represents the encryption strength of the key to be created with the template.   |
    | State                | The initial key state to be created with the key template, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activate keys after      | (Optional) Plan a date to activate the Pre-active keys to be created since the key creation. It is for planning purpose only. |
    | Deactivate keys after     | (Optional) Plan a date to deactivate the keys to be created since the key creation. It is for planning purpose only. |
    {: #table-4}
    {: caption="IBM Cloud KMS Key templates properties" caption-side="bottom"}
    {: tab-title="IBM Cloud KMS Key templates"}
    {: tab-group="Key templates from scratch properties"}
    {: class="comparison-tab-table"}

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key template name    | A unique, human-readable name for easy identification of your key template. It must be 1–100 characters in length.  |
    | Description          | (Optional) An extended description for your key template, with up to 200 characters in length. |
    | Naming scheme        | (Optional) Enter strings or placeholders to enforce the key naming scheme. After defining the key naming scheme, you can then create a group of keys with the same key naming conventions but you cannot edit the key naming scheme any more. For more information, see [Defining key naming schemes](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#define-naming-scheme).    | 
    | Managed key name example | Read only. An example of the managed key name based on the key naming scheme is populated automatically for your reference.       |
    | Algorithm            | The encryption algorithm to encrypt data for the key to be created with the template.     |
    | Length               | The number of bits that represents the encryption strength of the key to be created with the template.   |
    | State                | The initial key state to be created with the key template, including Pre-active and Active. Pre-active keys are not activated in keystores for encryption. Active keys are automatically activated in the keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}. |
    | Activate keys after      | (Optional) Plan a date to activate the Pre-active keys to be created since the key creation. It is for planning purpose only. |
    | Deactivate keys after     | (Optional) Plan a date to deactivate the keys to be created since the key creation. It is for planning purpose only. |
    {: #table-5}
    {: caption="IBM Key Protect Key templates properties" caption-side="bottom"}
    {: tab-title="IBM Key Protect Key templates"}
    {: tab-group="Key templates from scratch properties"}
    {: class="comparison-tab-table"}   

 

8. Under **Summary**, view the summary of your key template, and then click **Create key template** to confirm.

You have successfully created a key template. 

## Creating key templates from scratch through the API
{: #create-template-api}
{: api}

To create a key template from scratch through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `POST` call to the following endpoint.

    
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/templates
    
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-key-template){: external}.



## Creating a copy of an existing key template with the UI
{: #copy-template-ui}
{: ui}

If you want to customize a key template based on an existing template, create a copy of the key template, and then edit the template properties. You can copy from either an active or archived key template. To do so through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Key templates** from the navigation to view all the available key templates.

    You can view archived key templates by clicking the **Show archived templates** icon ![Show archived templates icon](/images/archive.svg "Show archived templates") on the table.

3. Locate the key template that you want to copy from the list, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and select **Copy**.

    Alternatively, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and select **Show details**. And then, on the template details page, select **Actions** > **Copy**.  

4. All properties are preconfigured based on the copied key template. You can still make the following changes if needed: 
    - Vault
    - Keystore type
    - Keystores
    - Key template properties

    Refer to [Creating key templates from scratch with the UI](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui#create-template-ui) for detailed explanations.

7. Under **Summary**, view the summary of your key template, and then click **Create key template** to confirm.

You have successfully created a copy of an existing key template. 


## Creating key templates from an existing key template through the API
{: #copy-template-api}
{: api}

To make a copy from an existing key template through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `POST` call to the following endpoint.
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/templates
    
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-key-template){: external}.



## Defining key naming schemes
{: #define-naming-scheme}
{: ui}

By defining the key naming scheme for the key template, you can create a group of keys with the same key naming conventions. You can specify different naming scheme placeholders. The naming schemes consist of fixed strings, custom placeholders, and system placeholders, which will be populated during the creation of each key.

When you define a key naming scheme, an example of a managed key name based on the key naming scheme is populated automatically for your reference under **Managed key naming example**. For example, if you enter `akms-<PROJECT>-<LOCATION>-<ENV>-appdata` for your key naming scheme, an example of a managed key name is displayed `akms-XYZ-XYZ-XYZ-appdata`. In this example, `akms` and `appdata` are the fixed strings, and `XYZ` is the value for `PROJECT`, `LOCATION`, and `ENV` that you need to provide each time during the key creation with this key template.

Note that you need to keep in mind of the following considerations: 

- Depending on the keystore type, key naming requirements can be different:
    - **AWS Key Management Service**: It must be 1–250 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (/_-). However, do not start the name with `AWS/`.
    - **Azure Key Vault**: It must be 1–127 characters in length. The characters can be letters (case-sensitive), digits (0–9), or hyphens (-). 
    - **Google Cloud KMS**: It must be 1–63 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (_-).
    - **IBM Cloud KMS**: It must be 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces.
    - **IBM Key Protect**: It must be 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces. 

- Enter fixed strings or placeholders for the key naming scheme. Each placeholder must be within 1-20 characters in length. Note that you need to use the angle brackets (<>) to insert placeholders. 

- Enter an opening angle bracket (<) or click the system placeholder tag to insert a system placeholder. Each system placeholder consists of letters (case-sensitive), digits (0-9), or a forward slash (/). The following table lists the system placeholders: 

      
    If the key names contain system placeholders, keys to be created cannot be rotated.
    {: note} 

    |       System placeholder	      |    Alternative spelling      |                     Description                       |
    |----------------------|---------------------------| ----------------------------------------|
    | `lastActiveYear`    | `lay`\n \n `lastActiveYear/yyyy`\n \n`lay/yyyy`\n \n `lastActiveYear/4`\n \n `lay/4`    | A 4-digit format of the year when the key is expired.  |
    | `lastActiveYear/yy`    | `lay/2`\n \n `lastActiveYear/2` \n \n `lay/yy`    | A 2-digit format of the year when the key is expired.  |
    | `lastActiveMonth`    | `lam`                        | A 2-digit format of the month when the key is expired.  |
    | `yy`                 |                           | A 2-digit format of the year when the key is created.     | 
    | `yyyy`               |                           | A 4-digit format of the year when the key is created.     | 
    | `mm`                 |                           | A 2-digit format of the month when the key is created.     | 
    {: caption="System placeholders for naming scheme" caption-side="bottom"}

-  Do not use the following reserved placeholders for your key naming scheme.

    |       Reserved placeholder	      |    Alternative spelling      |     
    |----------------------|-------------------|
    | `SEQUENCENUMBER`    | `seqno`\n \n `sqn`\n \n `sequenceNumber`\n \n `SEQNO`\n \n `SQN`    | 
    | `hierarchy`         | `h`\n \n `hier`| 
    | `keyType`           | `kt`    | 
    | `institutionId`     | `iid` | 
    {: caption="Reserved placeholders for naming scheme" caption-side="bottom"}

 


- You can enter an opening angle bracket (<) to insert a custom placeholder. Each custom placeholder consists of letters (case-sensitive) or digits (0-9). To apply the naming scheme to multiple keys, make sure to use at least one custom placeholder.

- If you define a custom placeholder, you need to provide a value for the placeholder during the key creation. 

- You cannot edit the key name after the managed key is created with key naming schemes. 


## What's next
{: #create-template-next}

- To continue to create keys with the key template created, follow the instruction in [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- To find out instructions on editing a key template, check out [Editing key template details](/docs/hs-crypto?topic=hs-crypto-edit-template). 

- To find out instructions on archiving and unarchiving the key template, check out [Archiving and unarchiving key templates](/docs/hs-crypto?topic=hs-crypto-archive-template). 

- To find out instructions on deleting a key template, check out [Deleting key templates](/docs/hs-crypto?topic=hs-crypto-delete-template).
