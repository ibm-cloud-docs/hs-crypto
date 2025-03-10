---

copyright:
  years: 2022, 2024
lastupdated: "2024-11-29"

keywords: Unified Key Orchestrator, search keys, key management, kms keys

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Filtering and searching managed keys
{: #search-key-list}

You can filter and search for your managed keys in {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}}.
{: shortdesc}


## Filtering managed keys with the UI
{: #filter-key-list-ui}
{: ui}

To filter managed keys by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the table.
4. Specify the filter criteria as you need, and click **Apply**.
   
   
   You can set the following filter criteria. 

   |       Property	     |                         Description                        |
   |----------------------|-----------------------------------------------------------|
   | Vault                | The vault that controls access to the managed key.        |
   | Key template         | The key template with which the key is created.  |
   | Key template flags   | The keys that are unaligned with the key template. |
   | Activation           | Set a date range of when you activate the key.  |
   | Expiration           | Set a date range of when you deactivate the key.  |
   | Creation             | Set a date range of when the key was created.             |
   | Keystore types       | The type of keystore where the key is stored. |
   | Algorithm            | The encryption algorithm to encrypt data for the key.     |
   | Minimum key length   | The minimum number of bits that represents the encryption strength of the key.   |
   | Maximum key length   | The maximum number of bits that represents the encryption strength of the key.   |
   | State                | Key states include Pre-active, Active, Deactivated, and Destroyed. |
   | State flags          | Key state flags include `Out of sync` and `pending`. \n \n If your key state is different from the key state in its keystores, an **Out of sync** flag is displayed beside the state. There can be multiple reasons why the key state is out of sync. For example, there is an issue in relinking the key in the keystore, the key is failed to be destroyed in some of the distributed keystores, or the key is modified in the target keystore outside of {{site.data.keyword.uko_full_notm}}. When you hover over this flag, you can see the specific reason. You can sync the key state by selecting **Show details** on the Actions ![Actions icon](../icons/action-menu-icon.svg "Actions") menu and clicking **Sync key**. For more information, see [Syncing keys in keystores with managed keys manually](/docs/hs-crypto?topic=hs-crypto-uko-sync-keys&interface=ui).\n \n  A `pending` flag is displayed beside the state after you move a key from Deactivated to Destroyed state, the key will be pending on destruction in a time period defined by the destruction policies of the external cloud providers. For Azure Key Vault and Google Cloud KMS keystore, the pending destruction time period can also be customized on the external cloud provider side. When you hover over the `pending` flag, you can see the date which it will end the pending state. You cannot cancel pending destruction using the {{site.data.keyword.uko_full_notm}} UI or API. However, you might still do so through the third-party keystores that the keys are created in. For more information, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states).|
   | Last rotated         | The time range when the key was last rotated. |
   {: caption="Filter managed keys" caption-side="bottom"}
   



##  Searching for keys with the UI
{: #search-key-list-ui}
{: ui}

To search for a key by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. To search for key name or description, type a word in the search bar.



## Searching keys with the API
{: #search-key-list-api}
{: api}

To search for a managed key by ID through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Retrieve a managed key and its details by making a `GET` call to the following endpoint.

    

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/managed_keys/<id>
    
    ```
    {: codeblock}

    Replace `<id>` with the ID of your managed key.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#get-managed-key){: external}.



## What's next
{: #search-key-list-next}

- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list).
  
- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).

- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).
