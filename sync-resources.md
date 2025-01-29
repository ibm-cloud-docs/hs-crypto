---

copyright:
  years: 2021, 2024
lastupdated: "2024-10-09"

keywords: sync resources, sync registrations, key registration, notify key state to resources

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Synchronizing associated resources
{: #sync-associated-resources}

You can initiate a manual data synchronization request between root keys and the associated cloud resources, such as {{site.data.keyword.cos_full_notm}} buckets or Cloud Databases deployments, by using the {{site.data.keyword.hscrypto}} key management service API.
{: shortdesc}

When you perform a key lifecycle action on a root key that is associated with other IBM cloud services, those IBM cloud services are notified of the key lifecycle event and are encouraged to respond. However, if the cloud services do not respond to the key lifecycle notification, use the sync API to initiate a renotification of the key lifecycle event to those associated cloud services.

For example, you might delete a root key that has an association with {{site.data.keyword.cos_full_notm}}. After you wait for 4 hours for changes to take effect, you notice that you are still able to access the key's resources despite expecting to be blocked from accessing those resources. In this case, you need to call the sync API to renotify {{site.data.keyword.cos_full_notm}} of the deleted key lifecycle event, so that {{site.data.keyword.cos_full_notm}} can block access to the resources.

The sync API initiates only a request for synchronization. The IBM services that are associated with the key are responsible for managing all related associated resources and ensuring that the key state and key versions are up to date.
{: important}

## Syncing associated resources with the UI
{: #sync-associated-resources-ui}
{: ui}

You can renotify associated resources of your {{site.data.keyword.hscrypto}} root key's lifecycle event by using the UI.

1. [Log in to the UI](https://cloud.ibm.com/){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, use the **Keys** table to browse the keys in your service.
5. To renotify the protected resources of a specific root key, click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key and select **Synchronize associated resources**.
6. On the **View associated resources** page, click **Synchronize**.

## Syncing associated resources with the API
{: #sync-associated-resources-api}
{: api}

You can renotify associated IBM cloud services of your {{site.data.keyword.hscrypto}} root key's lifecycle event by using the {{site.data.keyword.hscrypto}} API.

You can initiate the renotification of a key lifecycle event by making a `POST` call to the following endpoint.

 

```
https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/actions/sync
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Initiate a manual data synchronization request by running the following `curl` command.

    ```sh
    $ curl -X POST \
        "https://<instance_ID>.api.<region>.hs-crypto.appdomain.cloud/api/v2/keys/<key_ID>/actions/sync" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The region abbreviation, such as `us-south`, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides. For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints). |
    | `key_ID` | **Required.** The identifier for the root key that is associated with the cloud resources that you want to view. For more information, see [View Keys](/docs/hs-crypto?topic=hs-crypto-view-keys). |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the `IAM` token, including the Bearer value, in the `curl` request. For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token). |
    | `instance_ID` | **Required.** The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID). |
    {: caption="Describes the variables needed to initiate a renotification of a key lifecycle event" caption-side="bottom"}

    A successful sync API request returns an HTTP `204 No Content` response, which indicates that the IBM cloud service that is associated with the specified key is notified.

The sync API can be initialized only when it is longer than an hour since the last notification to the associated cloud services of the key. If you send a request to this API and the key is synced or a key lifecycle action is taken within the past hour, the API returns a `409 Conflict` response.
{: important}
