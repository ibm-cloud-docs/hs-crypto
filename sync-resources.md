---

copyright:
  years: 2021
lastupdated: "2021-03-15"

keywords: sync resources, sync registrations, key registration, notify key state to resources

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:preview: .preview}

# Synchronizing associated resources
{: #sync-associated-resources}

You can initiate a manual data synchronization request between root keys and the associated cloud resources, such as {{site.data.keyword.cos_full_notm}} buckets or Cloud Databases deployments, by using the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

When you perform a key lifecycle action (for example `rotation`, `restore`, `disable`, `enable`, `deletion`) on a root key that is associated with other IBM cloud services, those IBM cloud services are notified of the key lifecycle event and are encouraged to respond accordingly. However, in the case where the cloud services do not respond to the key lifecycle notification, you can use the sync API to initiate a renotification of the key lifecycle event to those associated cloud services.

For example, you might delete a root key that has an association with {{site.data.keyword.cos_full_notm}} (COS). After waiting four hours for changes to take effect, you notice that you are still able to access the key's resources despite expecting to be blocked from accessing those resources. In this case, you should call the sync API to renotify COS of the deleted key lifecycle event, so that COS can block access to the resources.

The sync API only initiates a request for synchronization. The IBM services associated with the key are responsible for managing all related associated resources and ensuring that the key state and key versions are up to date.
{: important}

## Syncing associated resources with the console
{: #sync-associated-resources-ui}

You can renotify associated resources of your {{site.data.keyword.hscrypto}} root key's lifecycle event by using the console.

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **Key management service keys** page, use the **Keys** table to browse the keys in your service.
5. To renotify the protected resources of a specific root key, click the overflow (⋯) icon to open a list of options for the key and select **Synchronize associated resources**.
6. On the **View associated resources** page, click **Synchronize**.

## Syncing associated resources with the API
{: #sync-associated-resources-api}

You can renotify associated IBM cloud services of your {{site.data.keyword.hscrypto}} root key's lifecycle event by using the {{site.data.keyword.hscrypto}} API.

You can initiate the renotification of a key lifecycle event by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/sync
```
{: codeblock}

1. [Retrieve your authentication credentials to work with the API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Initiate a manual data synchronization request by running the following `curl` command.

    ```sh
    $ curl -X POST \
        "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/sync" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>"
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>

      <tr>
        <td>
          <varname>region</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code>, that represents the
            geographic area where your {{site.data.keyword.hscrypto}} instance resides.
          </p>
          <p>
            For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>key_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The identifier for the root key that is associated with the cloud resources that you want to view.
          </p>
          <p>
            For more information, see [View Keys](/docs/hs-crypto?topic=hs-crypto-view-keys).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the <code>curl</code> request.
          </p>
          <p>
            For more information, see [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance.
          </p>
          <p>
            For more information, see [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <caption style="caption-side:bottom;">
        Table 1. Describes the variables that are needed to initiate a renotification of a key lifecycle event.
      </caption>
    </table>

    A successful sync API request returns an HTTP `204 No Content` response, which indicates that the IBM cloud service that is associated with the specified key has been notified.

The sync API can only be initialized if it has been longer than an hour since the last notification to the associated cloud services of the key. If you send a request to this API and the key has been synced or a key lifecycle action has been taken within the past hour, the API returns a `409 Conflict` response.
{: important}
