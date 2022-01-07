---

copyright:
  years: 2020, 2022
lastupdated: "2022-01-07"

keywords: delete keys with dual authorization, dual authorization, policy-based, key deletion

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:preview: .preview}
{:term: .term}

# Deleting keys by using dual authorization
{: #delete-dual-auth-keys}

You can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to safely delete root keys or standard keys by using a dual authorization process.
{: shortdesc}


When you delete an encryption key, you shred the contents and associated data. Any data that is encrypted by the key becomes inaccessible. Only imported root keys can be restored after deletion.
[Destroying resources](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#data-deletion) is not suggested for production environments, but might be useful for temporary environments such as testing or QA.
{: important}

Keep in mind the following considerations before you delete a key:

- {{site.data.keyword.hscrypto}} blocks the deletion of any key
that's actively protecting a cloud resource. Before you delete a key,
[review the resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)
that are associated with the key.
- You can [force deletion on a key](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-key-force)
that's protecting a cloud resource. However, the action won't succeed if the key's associated resource is non-erasable due to a retention policy. You can verify whether a key is associated with a non-erasable resource by [checking the registration details](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources-api) for the key.




## Considerations for deleting a key using dual authorization
{: #dual-auth-deletion-considerations}

Deleting a key that has a
[dual authorization policy](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth)
requires an authorization from two users. With the
{{site.data.keyword.hscrypto}} key management API, you can provide the
first authorization by
[setting the key for deletion](#set-key-deletion-api).
Then, a different user provides a second authorization by using the
{{site.data.keyword.cloud_notm}} console or key management API to delete the key.

Before you delete a key by using dual authorization:

- **Determine who can authorize deletion of your {{site.data.keyword.hscrypto}} resources.**
To use dual authorization, be sure to identify a user who can set the key for
deletion, and another user who can delete the key. Users with a _Writer_ or
 _Manager_ access policy can set keys for deletion. Users with a _Manager_
 access policy can delete keys.
- **Plan to delete the key within a 7-day waiting period.**
When the first user authorizes a key for deletion,
{{site.data.keyword.hscrypto}} sets a 7-day waiting period on
the key. During this period, the key remains in the
[_Active_ state](/docs/hs-crypto?topic=hs-crypto-key-states)
and all key operations are allowed on the key. To complete the deletion, the
second user with a _Manager_ access policy can use the
{{site.data.keyword.cloud_notm}} console or API to delete the key.
- **The key and its associated data become inaccessible 90 days after the key is deleted.** When you delete a key, the key can be restored within 30 days after the deletion. You are able to retrieve associated data such as key metadata, registrations, and policies for up to 90 days. After 90 days, the key becomes eligible to be automatically purged and its associated data will be permanently removed from the your instance.

## Authorize deletion for a key with the console
{: #set-key-deletion-console}

### Step 1. Authorize deletion for a key
{: #set-dual-auth-key-gui}

After you [enable dual authorization for an instance](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) or [for a key](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy), you can provide the first authorization to delete a key by using the {{site.data.keyword.cloud_notm}} console.

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your
provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, use the **Keys** table to browse the keys in
your service.
5. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key that you want to
delete.
6. From the options menu, click **Schedule key deletion** and review the key's
associated resources.
7. Enter the name of the key that is to be deleted, and click **Schedule key deletion**.
8. Contact the second approver to complete the deletion of the key.

### Step 2. Delete the key
{: #delete-dual-auth-key-gui}

To delete the key, the second approver must have _Manager_ access policy for the instance or key in
order to authorize the key for deletion.

1. In the **Keys** table of the **KMS keys** page, you can find keys that are authorized for deletion with the following indicators:
    * The `Set for deletion` column has a value of `True`. The authorization expiration time is displayed in the `Deletion expiration` column.
    * A **Trash can** icon ![Trash can icon](../icons/icon_trash.svg "Trash can") is displayed in the `State` column. Hover over the icon to view the deletion expiration date.

2. To delete the key, follow the instructions in [Deleting keys with the console](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-keys-gui).

{{site.data.keyword.hscrypto}} sets a 7-day waiting period that
starts after you provide the first authorization to delete the key. During this
7-day period, the key remains in the
[_Active_ state](/docs/hs-crypto?topic=hs-crypto-key-states)
and all key operations are allowed on the key. If no action is taken by the
second user and the 7-day period expires, you must
[restart the dual authorization process](#set-key-deletion-api)
 to delete the key.
{: note}

## Authorize deletion for a key with the API
{: #set-key-deletion-api}

### Step 1. Authorize deletion for a key
{: #set-dual-auth-key-api}

After you enable dual authorization [for an instance](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) or [for a key](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy),
you can provide the first authorization to delete a key by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/setKeyForDeletion
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To set a key for deletion, you must be assigned a _Manager_ or _Writer_
    access policy for the instance or key. To learn how IAM roles map to
    {{site.data.keyword.hscrypto}} actions, check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Copy the ID of the key that you want to set or authorize for deletion.

3. Provide the first authorization to delete the key.

    ```cURL
    curl -X POST \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/setKeyForDeletion' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following
    table.

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
            <strong>Required.</strong> The region abbreviation, such as
            <code>us-south</code> or <code>eu-de</code>, that represents the
            geographic area where your
            {{site.data.keyword.hscrypto}} instance
            resides.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>key_ID</varname>
        </td>
        <td>
          <strong>Required.</strong> The unique identifier for the root key that
          you want to delete.
        </td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}}
            access token. Include the full contents of the <code>IAM</code>
            token, including the Bearer value, in the cURL request.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to
            your {{site.data.keyword.hscrypto}}
            instance.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</p>
        </td>
      </tr>

      <caption>
        Table 1. Describes the variables that are needed to set a key for
        deletion.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which
    indicates that your key was authorized for deletion. Another user with a
    _Manager_ access policy can now
    [delete the key](/docs/hs-crypto?topic=hs-crypto-delete-keys)
    by using the {{site.data.keyword.cloud_notm}} console or key management API.

    If you need to prevent the deletion of a key that's already authorized for
    deletion, you can remove the existing authorization by calling
    `POST /api/v2/keys/<key_ID>/actions/unsetKeyForDeletion`.
    {: tip}

### Step 2. Delete the key
{: #delete-dual-auth-key-api}

After you set a key for deletion, a second user with a _Manager_ access policy
can safely delete the key.

{{site.data.keyword.hscrypto}} sets a 7-day waiting period that
starts after you provide the first authorization to delete the key. During this
7-day period, the key remains in the
[_Active_ state](/docs/hs-crypto?topic=hs-crypto-key-states)
and all key operations are allowed on the key. If no action is taken by the
second user and the 7-day period expires, you must
[restart the dual authorization process](#set-key-deletion-api)
 to delete the key.
{: note}

To delete a key and the contents, make a `DELETE` call to the service
endpoint by following instructions in [Deleting keys with the API](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-keys-api).

### Removing an existing authorization
{: #unset-key-deletion-api}

If you need to cancel an authorization for a key before the 7-day waiting period
expires, you can remove the existing authorization by making a `POST` call to
the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/unsetKeyForDeletion
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To remove an authorization to delete a key, you must be assigned a _Manager_
    or _Writer_ access policy for the instance or key. To learn how IAM roles
    map to {{site.data.keyword.hscrypto}} actions,
    check out
    [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Copy the ID of the key that you want to unset or deauthorize for deletion.

3. Remove an existing authorization to delete the key.

    ```cURL
    curl -X POST \
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/setKeyForDeletion' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following
    table.

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
            <strong>Required.</strong> The region abbreviation, such as
            <code>us-south</code> or <code>eu-de</code>, that represents the
            geographic area where your
            {{site.data.keyword.hscrypto}} instance
            resides.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>key_ID</varname>
        </td>
        <td>
          <strong>Required.</strong> The unique identifier for the root key that
          you want to delete.
        </td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}}
            access token. Include the full contents of the <code>IAM</code>
            token, including the Bearer value, in the cURL request.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to
            your {{site.data.keyword.hscrypto}}
            instance.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</p>
        </td>
      </tr>

      <caption>
        Table 2. Describes the variables that are needed to unset a key for
        deletion.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which
    indicates that your key is no longer authorized for deletion. If you need to
    restart the dual authorization process, you can issue another authorization
    to
    [set the key for deletion](#set-key-deletion-api).

## What's next
{: #delete-daul-auth-keys-next}

- To restore a previously deleted key, check out [Restoring keys](/docs/hs-crypto?topic=hs-crypto-restore-keys).
- To create another root key, check out [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
- To delete the service instance, check out [Deleting service instances](/docs/hs-crypto?topic=hs-crypto-delete-instance)
- To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management API reference doc](/apidocs/hs-crypto){: external}.
