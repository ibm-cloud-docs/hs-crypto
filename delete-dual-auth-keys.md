---

copyright:
  years: 2020
lastupdated: "2020-09-24"

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

# Deleting root keys or standard keys using dual authorization
{: #delete-dual-auth-keys}

You can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to safely delete root keys or standard keys by using a dual authorization process.
{: shortdesc}

When you delete an encryption key, you shred its contents and associated data. Only imported root keys can be restored after deletion. Any data that is encrypted by the key becomes inaccessible.
[Destroying resources](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#data-deletion) is not recommended for production environments, but might be useful for temporary environments such as testing or QA.
{: important}

Keep in mind the following considerations before you delete a key:

- {{site.data.keyword.hscrypto}} blocks the deletion of any key
that's actively protecting a cloud resource. Before you delete a key,
[review the resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources)
that are associated with the key.
- You can [force deletion on a key](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-key-force)
that's protecting a cloud resource. However, the action won't succeed if the key's associated resource is non-erasable due to a retention policy. You can verify whether a key is associated with a non-erasable resource by [checking the registration details](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources-api) for the key.

## Deleting a key using dual authorization
{: #delete-dual-auth-keys-api}

Deleting a key that has a
[dual authorization policy](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) requires an authorization from two users. With the
{{site.data.keyword.hscrypto}} key management API, you can provide the first authorization by [setting the key for deletion](#set-key-deletion-api). Then, a different user provides a second authorization by using the {{site.data.keyword.hscrypto}} GUI or key management API to delete the key.

Before you delete a key by using dual authorization:

- **Determine who can authorize deletion of your {{site.data.keyword.hscrypto}} resources.**
To use dual authorization, be sure to identify a user who can set the key for
deletion, and another user who can delete the key. Users with a _Writer_ or  _Manager_ access policy can set keys for deletion. Users with a _Manager_ access policy can delete keys.
- **Plan to delete the key within a 7-day waiting period.**
When the first user authorizes a key for deletion,
{{site.data.keyword.hscrypto}} sets a 7-day waiting period on
the key. During this period, the key remains in the
[_Active_ state](/docs/hs-crypto?topic=hs-crypto-key-states)
and all key operations are allowed on the key. To complete the deletion, the
second user with a _Manager_ access policy can use the
{{site.data.keyword.hscrypto}} GUI or key management API to delete the key.

### Step 1. Authorize deletion for a key
{: #set-key-deletion-api}

After you enable dual authorization [for an instance](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) or [for a key](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy),
you can provide the first authorization to delete a key by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=setKeyForDeletion
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
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=setKeyForDeletion' \
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
          <p>
            For more information, see
            [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
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
          <p>
            For more information, see
            [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
          </p>
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
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <caption style="caption-side:bottom;">
        Table 1. Describes the variables that are needed to set a key for
        deletion.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which
    indicates that your key was authorized for deletion. Another user with a
    _Manager_ access policy can now
    [delete the key](/docs/hs-crypto?topic=hs-crypto-delete-keys)
    by using the {{site.data.keyword.hscrypto}} GUI or key management API.

    If you need to prevent the deletion of a key that's already authorized for
    deletion, you can remove the existing authorization by calling
    `POST /api/v2/keys/<key_ID>?action=unsetKeyForDeletion`.
    {: tip}

### Step 2. Delete the key
{: #delete-dual-auth-key-api}

After you set a key for deletion, a second user with a _Manager_ access policy
can safely delete the key by using the
{{site.data.keyword.hscrypto}} GUI or key management API.

{{site.data.keyword.hscrypto}} sets a 7-day waiting period that
starts after you provide the first authorization to delete the key. During this
7-day period, the key remains in the
[_Active_ state](/docs/hs-crypto?topic=hs-crypto-key-states)
and all key operations are allowed on the key. If no action is taken by the
second user and the 7-day period expires, you must
[restart the dual authorization process](#set-key-deletion-api)
 to delete the key.
{: note}

Delete a key and its contents by making a `DELETE` call to the following
endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Retrieve the ID of the key that you would like to delete.

    You can retrieve the ID for a specified key by making a `GET /v2/keys`
    request, or by viewing your keys in the
    {{site.data.keyword.hscrypto}} dashboard.

3. Run the following cURL command to delete the key and its contents.

    ```cURL
    curl -X DELETE \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
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
          <p>
            For more information, see
            [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>key_ID</varname>
        </td>
        <td>
          <strong>Required.</strong> The unique identifier for the key that you
          would like to delete.
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
          <p>
            For more information, see
            [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
          </p>
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
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>return_preference</varname>
        </td>
        <td>
          <p>
            A header that alters server behavior for <code>POST</code> and
            <code>DELETE</code> operations.
          </p>
          <p>
            When you set the <em>return_preference</em> variable to
            <code>return=minimal</code>, the service returns a successful
            deletion response. When you set the variable to
            <code>return=representation</code>, the service returns both the key
            material and the key metadata.
          </p>
        </td>
      </tr>

      <caption style="caption-side:bottom;">
        Table 2. Describes the variables that are needed to delete keys with the
        {{site.data.keyword.hscrypto}} key management API.
      </caption>
    </table>

    If the `return_preference` variable is set to `return=representation`, the
    details of the `DELETE` request are returned in the response entity-body.

    The following JSON object shows an example returned value.

    ```json
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "type": "application/vnd.ibm.kms.key+json",
          "id": "02fd6835-6001-4482-a892-13bd2085f75d",
          "name": "test-root-key",
          "state": 5,
          "extractable": false,
          "crn": "crn:v1:bluemix:public:hs-crypto:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
          "imported": false,
          "creationDate": "2020-03-10T20:41:27Z",
          "createdBy": "...",
          "algorithmType": "AES",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "CBC_PAD"
          },
          "algorithmBitSize": 256,
          "algorithmMode": "CBC_PAD",
          "lastUpdateDate": "2020-03-16T20:41:27Z",
          "dualAuthDelete": {
            "enabled": false
          },
          "deleted": true,
          "deletionDate": "2020-03-16T21:46:53Z",
          "deletedBy": "..."
        }
      ]
    }
    ```
    {: screen}

    For a detailed description of the available parameters, see the
    {{site.data.keyword.hscrypto}}
    [Key management REST API reference doc](/apidocs/hs-crypto){: external}.

### Removing an existing authorization
{: #unset-key-deletion-api}

If you need to cancel an authorization for a key before the 7-day waiting period
expires, you can remove the existing authorization by making a `POST` call to
the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=unsetKeyForDeletion
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
      'https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=setKeyForDeletion' \
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
          <p>
            For more information, see
            [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
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
          <p>
            For more information, see
            [Retrieving an access token](/docs/hs-crypto?topic=hs-crypto-retrieve-access-token).
          </p>
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
          <p>
            For more information, see
            [Retrieving an instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).
          </p>
        </td>
      </tr>

      <caption style="caption-side:bottom;">
        Table 3. Describes the variables that are needed to unset a key for
        deletion.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which
    indicates that your key is no longer authorized for deletion. If you need to
    restart the dual authorization process, you can issue another authorization
    to
    [set the key for deletion](#set-key-deletion-api).
