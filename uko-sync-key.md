---

copyright:
  years: 2023, 2024
lastupdated: "2024-07-01"

keywords: Unified Key Orchstrator, sync managed key, out of sync

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Syncing keys in keystores with managed keys manually
{: #uko-sync-keys}

If the key state in some keystores is different from the managed key state, you receive a **Key out of sync** warning message. You can sync the key state by using {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

An `Out of sync` flag is also displayed in the corresponding keystore card or the key list. There can be multiple reasons why the key is out of sync. For example, there is an issue in relinking the key in the keystore, the key is failed to be destroyed in some of the distributed keystores, or the key is modified in the target keystore outside of {{site.data.keyword.uko_full_notm}}. Take the following steps to munually sync the state of keys in keystores with the managed key.


## Syncing keys with the UI
{: #uko-sync-managed-key-gui}
{: ui}

To sync the key in keystores with managed keys manually, you need to verify the key state first and then sync keys. Complete the following steps to sync a managed key:

### Step 1: Verify key state
{: #verify-key-state-gui}

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. Select your provisioned instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} from your {{site.data.keyword.cloud_notm}} resource list.
4. Click **Managed keys** from the navigation to view all the available keys.
5. Select the key that you want to verify the key state and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key.
6. Click **Verify sync** from the options menu. 

### Step 2: Sync key state
{: #sync-key-state-gui}

After you verify the key state, if an **Out of sync** flag is displayed next to the key state, you can sync the key state by performing the following steps:

1. Select the key that you want to sync and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key.
2. Click **Sync key** from the options menu. Alternatively, you can sync keys by selecting **Show details** on the Actions ![Actions icon](../icons/action-menu-icon.svg "Actions") menu and clicking **Sync key** in the key details page. 
3. Confirm the keystores where you want to sync the key and click **Sync key**.


## Syncing with the API
{: #uko-sync-managed-key-api}
{: api}

To sync a managed key through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Sync a managed key by making a `POST` call based on the following example:

     

    ```
    curl --location --request POST 'https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/managed_keys/<id>/sync_status_in_keystores' 
    --header 'Authorization: Bearer <IAM_token>' \
    --header 'Accept: application/json' \
    --header 'If-Match: <ETag>'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The prefix that represents the geographic area where your service instance resides. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `id` | **Required.** The unique identifier for the managed key that you want to sync. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} IAM access token that you retrieve in step 1. Include the full contents of the `IAM` token, including the Bearer value. |
    | `ETag` | **Required.** The precondition of the update, which is the value of ETag from the header on a GET request. |
    {: caption="Table 1. Variables needed to sync a managed key" caption-side="bottom"}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#sync-managed-key){: external}.

## What's next
{: #uko-sync-keys-next}

- To find out more about managing your keys, check out [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list) or [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
- To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external}.
