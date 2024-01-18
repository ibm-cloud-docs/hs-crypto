---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-18"

keywords: Unified Key Orchestrator, edit key templates, key management, kms keys, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Editing key template details
{: #edit-template}

You can edit your key templates in {{site.data.keyword.uko_full_notm}} with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

## Editing key templates with the {{site.data.keyword.cloud_notm}} console
{: #edit-key-template-ui}
{: ui}

To edit the details of a key template by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Key templates** from the navigation to view all the available key templates. 
3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key template that you want to edit, and select **Show details**.
4. Under **Key template properties**, click **Edit** on each card to update the properties. Note that you can edit one property card at a time. To edit another property card, save your changes first.
    
    1. You can update the General properties and Key lifecycle properties. Or, you can view the Key naming and Key material properties. The following are a few properties that you can edit.

    Because the key template is already created, you cannot make changes to key naming and key material properties that are marked with a Lock icon.
    {: note}

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|  
    | Key template name    | A unique, human-readable name for easy identification of your key template. It must be 1–100 characters in length.| 
    | Description          | (Optional) An extended description for your key template, with up to 200 characters in length. |
    | Initial key state        | States of keys that are to be created with the key template, including Pre-active and Active. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external}.  |
    | Activate keys after  | (Optional) Plan a date to activate the Pre-active keys to be created since the key creation. Automatic state change is to be triggered on the planned date.|
    | Deactivate keys after| (Optional) Plan a date to deactivate the keys to be created since the key creation. Automatic state change is to be triggered on the planned date. |
    {: caption="Table 1. Key template properties" caption-side="bottom"}

    2. In the **Keystores** card, click **Edit** to add or remove the keystores where keys are to be activated. All the displayed keystores belong to the same vault and the same keystore type:

         - Add keystores
    
           If you want to distribute keys to be created with this template to other keystores, click **Edit** and check the corresponding keystore cards. 

         - Remove keystores

           If you want to unlink keys to be created with this template from some of the keystores, click **Edit** and clear the checkbox in the corresponding keystore cards. 
        
         - Create a keystore
    
           If you want to activate keys to be created in a new keystore, click **Add keystore**. For more instructions, see [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
    
        If you have already created keys with this key template before making the changes, an `Unaligned` flag is displayed on the key details cards of the keys, indicating that those keys are no longer in sync with the key template. If you want to keep these changes, ignore the flag. Otherwise, realign your key with the key template again by selecting **Actions** > **Realign with template**. For more information, see [Realigning keys with key templates](/docs/hs-crypto?topic=hs-crypto-align-key). 
        {: tip}

        
        If you connect to an external keystore of type Azure Key Vault, you can distribute both HSM-protected keys and software-protected keys to Azure Key Vault (Premium). However, you can distribute only software-protected keys to Azure Key Vault (Standard). 
        {: note}
        

5. When you finish making changes, click **Save** to save the changes. 

7. Under **Managed Keys**, view the total number of managed keys that are created based on this key template. You can also edit the managed keys by clicking the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key that you want to edit, and select **Show details**. For more information, see [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys&interface=ui).

    To search for a specific key by using the search bar, or filter keys based on your needs, click the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the table. 
    {: tip}


## Editing key templates with the API
{: #edit-key-template-api}
{: api}

To edit key template details through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `PATCH` call to the following endpoint.
    
    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/templates/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your key template.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#update-key-template){: external}.

## Editing keystores for key templates with the API
{: #assign-keystores-api}
{: api}

To edit keystores for existing key templates through the API, complete the following steps:

1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Add a keystore to or remove a keystore from a keystore group by making a `PATCH` call to the following endpoint. The keystore group should match the key template that is associated with the managed key.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/keystores/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your keystore.

3. Update the managed key to match the latest version of the associated key template by making a `POST` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/managed_keys/<id>/update_from_template
    ```
    {: codeblock}

    Replace `<id>` with the ID of your managed key.

    For detailed instructions and code examples about using the API method, check out how to [Update an internal keystore or a keystore connection](/apidocs/uko#update-keystore){: external} and [Update a managed key to match the key template](/apidocs/uko#update-managed-key-from-template){: external} in the {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc.

## What's next
{: #edit-key-template-next}

- To find out instructions on creating a key template, check out [Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template).

- To find out more about managing your key template, check out [Viewing a list of key templates](/docs/hs-crypto?topic=hs-crypto-view-template).
  
- To find out instructions on deleting a key template, check out [Deleting key templates](/docs/hs-crypto?topic=hs-crypto-delete-template).

- To find out instructions on archiving and unarchiving the key template, check out [Archiving and unarchiving key templates](/docs/hs-crypto?topic=hs-crypto-archive-template). 

- To find out more about realigning keys with the key templates, check out [Realigning keys with key templates](/docs/hs-crypto?topic=hs-crypto-align-key).

- To continue to create keys with the key template created, follow the instruction in [Creating managed keys with a key template](/docs/hs-crypto?topic=hs-crypto-create-managed-keys#create-managed-keys-template).

