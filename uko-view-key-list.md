---

copyright:
  years: 2022, 2023
lastupdated: "2023-12-05"

keywords: Unified Key Orchestrator, view keys, key management, kms keys, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Viewing a list of keys
{: #view-key-list}

You can view a list of your managed keys in {{site.data.keyword.uko_full_notm}} with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}


## Viewing a list of keys with the {{site.data.keyword.cloud_notm}} console
{: #view-key-list-ui}
{: ui}

To view a list of your keys by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Browse the general characteristics of your keys in the table. 
   
   To customize how the table is to be presented, click the **Settings icon** ![Settings icon](../icons/settings.svg "Settings") and check the columns to be displayed.
   {: tip}

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Name                 | The unique, human-readable name that is assigned to your key. |
    | Version              | The version of the managed key. It is in the format of `V` plus the version number. For example, `V2` means that [the key was rotated](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys) once and this is the second version of the key material. |
    | ID                   | A string that uniquely identifies the key. |
    | Vault                | The vault that controls access to the managed key.           |
    | State                | Key states include Pre-active, Active, Deactivated, and Destroyed. For more information, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states). \n \n If your key state is different from the key state in its keystores, an **Out of sync** flag is displayed beside the state. There can be multiple reasons why the key state is out of sync. For example, you have deactivated the key in this keystore before, or you activate the key through the CLI and the console doesn't reflect the state timely. When you hover over this flag, you can see the specific reason. You can sync keys by selecting **Show details** on the Actions ![Actions icon](../icons/action-menu-icon.svg "Actions") menu and clicking **Sync keys**.  |
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

