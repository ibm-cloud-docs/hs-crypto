---

copyright:
  years: 2022, 2023
lastupdated: "2023-06-12"

keywords: Unified Key Orchestrator, edit keys, key management, kms keys, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Editing key details
{: #edit-kms-keys}

You can edit your keys in {{site.data.keyword.uko_full_notm}} with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}


## Editing key details with the {{site.data.keyword.cloud_notm}} console
{: #edit-kms-keys-ui}
{: ui}

To edit the details of a managed key by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the Actions icon  ![Actions icon](../icons/action-menu-icon.svg "Actions")  on the key that you want to edit, and choose **Show details**.
4. Under **Key properties**, click **Edit** on each card to update the key properties. 

    
    1. You can update the general properties and lifecycle properties. Or, you can also view the key material properties, including algorithm, length, and key check value. The following are a few properties that you can edit.
 
        |       Property	     |                         Description                       |
        |----------------------|-------------------------------------------------------------|
        | Key name             | A unique, human-readable name for easy identification of your key. When you change the name of a managed key, the key is to be renamed in all target keystores where it is activated. \n \n Depending on the keystore type, name your key with the following rules:  \n - IBM Cloud KMS: 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces. \n - IBM {{site.data.keyword.keymanagementserviceshort}}: 2–50 characters in length. The characters can be letters (case-sensitive), digits (0–9), or spaces. \n - AWS Key Management Service: 1–255 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (/\_-). However, do not start the name with `AWS/`. \n - Azure Key Vault: 1–24 characters in length. The characters can be letters (case-sensitive), digits (0–9), or hyphens (-). \n - Google Cloud KMS: 1–63 characters in length. The characters can be letters (case-sensitive), digits (0–9), or symbols (\_-). |
        | Description          | (Optional) An extended description for your key, with up to 200 characters in length. |
        | State                | Key states include _Pre-active_, _Active_, _Deactivated_, and _Destroyed_. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). |
        | Activation date      | Plan a date to activate the key. Automatic state change is to be triggered on the planned date. |
        | Expiration date      | Plan a date to deactivate the key. Automatic state change is to be triggered on the planned date. |
        {: caption="Table 1. Key properties" caption-side="bottom"}

        You can edit one property card at a time. To make changes to another property card, save your changes first.
        {: note}
    

    

    2. In the **Target keystores** card, click **Edit** to add or remove the target keystores where the key is activated. You can use a key only for encryption and decryption after it is activated in at least one target keystore.  
        - Add target keystores
          
            If you want to activate the key in more target keystores, click **Edit** and check the corresponding target keystore cards. The _Active_ key state is synced across all target keystores.
        
        - Remove target keystores

            If you want to deactivate the key in some target keystores, click **Edit** and clear the checkbox in the corresponding target keystore cards. After the removal, the key material remains unless you destroy the key. The key state in the removed target keystores becomes _deactivated_ and cannot be synced with the managed key state in the future. However, you can reactivate the key by reassigning the key to these keystores so that the key state is synced again.

        - Sync keys

            If the key state in some target keystores is different from the managed key state, you receive a **Key out of sync** warning message. An **Out of sync** flag is also displayed in the corresponding keystore card. There can be multiple reasons why the key state is out of sync. For example, you have deactivated the key in this target keystore before, or you activate the key through the CLI and the console doesn't reflect the state timely. When you hover over this flag, you can see the specific reason. You can sync the key state by clicking **Sync keys**. 

            During master key rotation, you can activate {{site.data.keyword.cloud_notm}} KMS key in internal keystores. However, it will be shown as **Out of sync**. You can sync the key after the master key rotation is complete. 
            {: note} 

5. Under **Advanced properties**, click **Edit** to update or add new key tags to the key. Key tags are used as identifications of a key.
6. When you finish making changes, click **Save** to save the changes.

You can search for a specific key by using the search bar, or filter keys based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Managed keys** table. For more information, see [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
{: tip}


## Editing key details with the API
{: #edit-kms-keys-api}
{: api}

To edit key details through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Update the details of a managed key by making a `PATCH` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/managed_keys/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your managed key.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#update-managed-key){: external}.



## What's next
{: #edit-kms-keys-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).
  
- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).
  
- To find out how to activate an existing key in a keystore, check out [Setting target keystores for existing keys](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).

