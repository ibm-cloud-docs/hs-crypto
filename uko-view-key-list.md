---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-21"

keywords: Unified Key Orchestrator, view managed keys, key management, kms keys, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Viewing a list of managed keys
{: #view-key-list}

You can view a list of your managed keys in {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}


## Viewing a list of managed keys with the UI
{: #view-key-list-ui}
{: ui}

To view a list of your managed keys by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Browse the general characteristics of your keys in the table. By default, only `active` and `pre-active` keys are displayed.
   
    
   To customize how the table is to be presented, click the **Settings icon** ![Settings icon](../icons/settings.svg "Settings") and check the columns to be displayed.
   {: tip} 

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Name                 | The unique, human-readable name that is assigned to your key. |
    | Version              | The version of the managed key. It is in the format of `V` plus the version number. For example, `V2` means that [the key was rotated](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys) once and this is the second version of the key material. |
    | ID                   | A string that uniquely identifies the key. |
    | Vault                | The vault that controls access to the managed key.           |
    | State                | Key states include Pre-active, Active, Deactivated, and Destroyed. For more information, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). \n \n If your key state is different from the key state in its keystores, an **Out of sync** flag is displayed beside the state. There can be multiple reasons why the key state is out of sync. For example, there is an issue in relinking the key in the keystore, the key is failed to be destroyed in some of the distributed keystores, or the key is modified in the target keystore outside of {{site.data.keyword.uko_full_notm}}. You can sync the key state by selecting **Show details** on the Actions ![Actions icon](../icons/action-menu-icon.svg "Actions") menu and clicking **Sync key**. For more information, see [Syncing keys in keystores with managed keys manually](/docs/hs-crypto?topic=hs-crypto-uko-sync-keys&interface=ui).\n \n  A `pending` flag is displayed beside the state after you move a key from Deactivated to Destroyed state, the key will be pending on destruction for a time period defined by the default destruction policies of the external cloud providers. For Azure Key Vault and Google Cloud KMS keystore, the pending destruction time period can also be customized on the external cloud provider side. You cannot cancel pending destruction using the {{site.data.keyword.uko_full_notm}} UI or API. However, you might still do so through the third-party keystores that the keys are created in. For more information, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states).  |
    | Key template         | The key template that the key is created with. For more information, see [Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template&interface=ui).| 
    | Activation date      | The date when the key gets activated, or the date on which you plan to activate the key. |
    | Expiration date      | The date when the key gets deactivated, or the date on which you plan to deactivate the key. |
    | Last updated         | The date and time when the key was last updated. This field gets updated when the key is created, edited, or any part of the key metadata is modified.   |
    | Last rotated         | The date and time when the key was last rotated. If the key was not rotated before, it shows `Never`. |
    | Creation date        | Set a date range of when the key was created.             |
    | Keystores            | The keystores where the key is activated.               |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | Keystore type        | The type of keystore where the key is stored. |
    {: caption="Table 1. Managed keys table" caption-side="bottom"}  

    You can search for a specific key by using the search bar, or filter keys based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Managed keys** table. For more information, see [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
    {: tip} 



## Viewing a list of keys with the API
{: #view-key-list-api}
{: api}

To view a list of managed keys through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. View a list of managed keys by making a `GET` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/managed_keys
    
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#list-managed-keys){: external}.



## What's next
{: #view-key-list-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- To find out more about managing your keys, check out [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list) or [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).

- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).


