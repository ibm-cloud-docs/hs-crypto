---

copyright:
  years: 2021, 2022
lastupdated: "2022-03-01"

keywords: key rings, group keys, IAM access to keys group, IAM permissions for key rings

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

# Managing key rings
{: #managing-key-rings}

You can use {{site.data.keyword.hscrypto}} to create a group of keys for a target group of users that require the same {{site.data.keyword.iamshort}} (IAM) access permissions.
{: shortdesc}

As an account admin, you can bundle the keys in your {{site.data.keyword.hscrypto}} instance into groups called _key rings_. A key ring is a collection of keys in your service instance that require the same IAM access permissions. For example, if you have a group of team members who need a particular type of access to a specific group of keys, you can create a key ring for those keys and assign the appropriate IAM access policy to the target user group. The users that are assigned access to the key ring can create and manage the resources that exist within the key ring.

Key rings are also useful in cases where it is important for one business unit to have access to a set of keys that another business unit cannot have. An account admin can create key rings for each business unit and [assign the appropriate level of access](#grant-access-key-ring) to the appropriate users. In the case where the account admin would like to delegate platform management of a specific key ring to someone else, they can assign a user a [platform administrator role at the key ring level](/docs/account?topic=account-userroles#platformroles). The sub administrator will then be able to manage the key ring and grant access to the appropriate users.

You can grant access to key rings within a {{site.data.keyword.hscrypto}} instance by using the {{site.data.keyword.cloud_notm}} console, IAM API, or IAM CLI.
{: note}

Before you create a key ring for your {{site.data.keyword.hscrypto}} instance, keep in mind the following considerations:

- Every {{site.data.keyword.hscrypto}} instance comes with a default key ring.

    Each newly created {{site.data.keyword.hscrypto}} instance comes with a generated key ring with an ID of `default`. All keys that are not associated with a specified key ring exist within the default key ring.

- Key rings can hold root keys and standard keys, but not EP11 keys.

    Key rings can contain both root and standard keys. There is no limit on how many keys can exist within a key ring. Key rings don't apply to Enterprise PKCS #11 (EP11) keys.

- A key only can belong to one key ring at a time.

    A key can belong to only one key ring. Key ring assignment happens upon key creation. If a key ring ID is not passed in upon creation, the key will belong to the default key ring. You can update the key ring after the key creation.
- You can create up to five key rings for a service instance.

    The maximum number of key rings for a service instance is five. If the number reaches the limit, you are no longer able to create a key ring.

## Creating key rings
{: #create-key-ring}

Before you can group keys into a key ring, you need to create a key ring first. You can use either the console or the key management service API to create a key ring.

You can have up to five key rings for a service instance.
{: note}

### Creating key rings with the console
{: #create-key-ring-ui}

Create a key ring with the console by completing the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. To create a new key ring, select the **KMS key rings** tab in the side menu.
5. In the **Key management service key rings** table, click **Add key ring**.

    If the number of key rings reaches the limit of five, the **Add key ring** button is disabled.
    {: note}
6. Enter the **Key ring ID** and click **Add key ring**.

### Creating key rings with the API
{: #create-key-ring-api}

Create a key ring by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/key_rings
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Create a key ring by running the following `curl` command.

    ```sh
    $ curl -X POST \
        "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/key_rings/<key_ring_id>" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "correlation-id: <correlation_ID>"
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
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</p>
        </td>
      </tr>

      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>

      <tr>
        <td>
          <varname>key_ring_id</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier for the key ring that you would like to create.
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
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</p>
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
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>correlation_ID</varname>
        </td>
        <td>
          The unique identifier that is used to track and correlate transactions.
        </td>
      </tr>

      <caption>
        Table 1. Describes the variables that are needed to create a key ring with the key management service API
      </caption>
    </table>

    A successful `POST api/v2/key_rings` request returns an HTTP `201 Created` response, which indicates that the key ring is created and is now available for holding standard and root keys.


## Transferring a key to a different key ring
{: #transfer-key-key-ring}

As requirements change and new team members are brought into an org, you might create new key rings to reflect these organizational changes. After creating the key rings, it might be necessary to move a key from an existing key ring to a
new key ring that has different IAM permissions. For example, you might be onboarding a team that will need specific access to a key that belongs to a custom, non-default key ring. You can create a new key ring that is dedicated to the onboarding team and, since keys can only be associated with one key ring at a time, you need to move the key to the new key ring.

After transferring a key to a different key ring, it can take up to ten minutes for the change to take effect.
{: important}

### Transferring a key to a different key ring with the console
{: #transfer-key-ring-ui}

You can transfer a key to a different key ring with the console by completing the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. Select the **KMS keys** tab in the side menu to open the **Keys** table.
5. Find the key that you want to transfer from the list and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open the option list.
6. Click **Change key ring**.
7. Select the key ring ID that you want to move the key to and click **Change key ring**.

### Transferring a key to a different key ring with the API
{: #transfer-key-ring-api}

Transfer a key to a different key ring by making a `PATCH` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

    To update the key ring of a key, you must have at least _Manager_ service access to the key and the target key ring. To learn how IAM roles map to {{site.data.keyword.hscrypto}} service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Update the key ring of a key by running the following `curl` command.

    ```sh
    $ curl -X PATCH \
      "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>" \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H "x-kms-key-ring: <original_key_ring_ID>" \
      -H "correlation-id: <correlation_ID>" \
      -d '{
        "keyRingID": "<new_key_ring_ID>"
      }'
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
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</p>
        </td>
      </tr>

      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the <code>curl</code> request.
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
            <strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>original_key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. Therefore, it is suggested to specify the key ring ID for a more optimized request.
          </p>
          <p>
            Note: If you create a key without an <code>x-kms-key-ring</code> header, the key ring for the key is: <code>default</code>.
          </p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>correlation_ID</varname>
        </td>
        <td>
          The unique identifier that is used to track and correlate transactions.
        </td>
      </tr>

      <tr>
        <td>
          <varname>new_key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier for the target key ring that you want to move the key to.
          </p>
        </td>
      </tr>

      <caption>
        Table 2. Describes the variables that are needed to update a key's key ring with the key management service API
      </caption>
    </table>

    A successful `PATCH api/v2/keys/key_ID` request returns the key's metadata, including the ID of the key ring that the key now belongs to.

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
             "aliases": [
                 "alias-1",
                 "alias-2"
               ],
             "description": "A test root key",
             "state": 1,
             "extractable": false,
             "keyRingID": "new-key-ring",
             "crn": "crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
             "imported": false,
             "creationDate": "2020-03-12T03:37:32Z",
             "createdBy": "...",
             "algorithmType": "AES",
             "algorithmMetadata": {
                 "bitLength": "256",
                 "mode": "CBC_PAD"
             },
             "algorithmBitSize": 256,
             "algorithmMode": "CBC_PAD",
             "lastUpdateDate": "2020-03-12T03:37:32Z",
             "keyVersion": {
                 "id": "2291e4ae-a14c-4af9-88f0-27c0cb2739e2",
                 "creationDate": "2020-03-12T03:37:32Z"
             },
             "dualAuthDelete": {
                 "enabled": false
             },
             "deleted": false
         }
     ]
    }
    ```


## Granting access to a key ring
{: #grant-access-key-ring}

You can grant access to a key ring within a {{site.data.keyword.hscrypto}} instance by using the
{{site.data.keyword.cloud_notm}} console, [IAM API](/apidocs/iam-policy-management#create-policy){: external}, or [CLI](/docs/cli?topic=cli-ibmcloud_commands_iam#ibmcloud_iam_user_policy_create){: external}.

Review [roles and permissions](/docs/hs-crypto?topic=hs-crypto-manage-access) to learn how {{site.data.keyword.cloud_notm}} IAM roles map to {{site.data.keyword.hscrypto}} actions.
{: tip}

To assign access to a key ring with the console, complete the following steps:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Users** to browse the existing users in your account.
2. Select the user that you want to assign access to in the table, and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions")to open a list of options for that user.
3. From the options menu, click **Assign access**.
4. Click **Assign users additional access**.
5. Click the **IAM services** button.
6. From the list of services, select **{{site.data.keyword.hscrypto}}**.
7. Select **Services based on attributes**.
8. Select the **Instance ID** attribute and select the instance where the key ring resides.
9. Select the **Key Ring ID** attribute and enter the ID associated with the key ring.
8. Choose a combination of [platform and service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#roles)
   to assign access for the user.
9. Click **Add**.
10. Continue to add platform and service access roles as needed. When you finish all the access assignment, click **Assign**.

    You must assign the user must at least _Reader_ access to the entire instance in order for them to list, create, and delete key rings within the instance.
    {: note}

## Listing key rings
{: #list-key-ring}

You can browse the key rings that are managed in your provisioned instance of {{site.data.keyword.hscrypto}} with the console or the key management KPI.

### Listing key rings with the console
{: #list-key-ring-ui}

To browse the key rings with the console, complete the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. To browse the key rings, select the **KMS key rings** tab in the side menu.

The key rings table contains the following information:

| Column | Description |
| ------ | ----------- |
| Key ring ID   | The unique identifier that you specify when you create the key ring. |
| Last updated  | The date and time that the key ring was last updated. This field gets updated when the keyring is created or modified.  |
| Created   | The date and time that the key ring was created. |
{: caption="Table 3. Describes the columns for the key ring table" caption-side="bottom"}

### Listing key rings with the API
{: #list-key-ring-api}

You can browse the key rings by making a GET call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/key_rings
```
{: codeblock}

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. View general characteristics about your key rings by running the following `curl` command.

    ```sh
    $ curl -X GET \
        "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/key_rings" \
        -H "accept: application/vnd.ibm.kms.key_ring+json" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "correlation-id: <correlation_ID>"
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
          <strong>Required.</strong> The region abbreviation, such as <code>us-south</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides.
        </p>
        <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</p>
      </td>
    </tr>
    <tr>
      <td><varname>port</varname></td>
      <td><strong>Required.</strong> The port number of the API endpoint.</td>
    </tr>
    <tr>
      <td>
        <varname>IAM_token</varname>
      </td>
      <td>
        <p>
        <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the <code>curl</code> request.
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
        <strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} instance.
        </p>
        <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</p>
      </td>
    </tr>
    <tr>
      <td>
        <varname>correlation_ID</varname>
      </td>
      <td>
        <p>
          The unique identifier that is used to track and correlate transactions.
        </p>
      </td>
    </tr>
    <caption>
    Table 4. Describes the variables that are needed to view key rings with the key management service API.
    </caption>
    </table>

    A successful `GET api/v2/key_rings` request returns a collection of key rings that are available in your {{site.data.keyword.hscrypto}} service instance.

    ```json
    {
        "metadata": {
            "collectionType": "application/vnd.ibm.kms.key_ring+json",
            "collectionTotal": 2
        },
        "resources": [
            {
                "id": "default"
            },
            {
                "id": "Sample Key Ring 2",
                "creationDate": "2020-03-12T11:00:06Z",
                "createdBy": "..."
            }
        ]
    }
    ```
    {: codeblock}

## Deleting key rings
{: #delete-key-ring}

You can delete a key ring with the console or with the key management service API.

The `default` key ring cannot be deleted. You are also not able to delete a key ring if the key ring contains at least one key, regardless of the key state (including keys in the _Destroyed_ state).
{: important}

### Deleting key rings with the console
{: #delete-key-ring-ui}

To delete a key ring with the console, complete the following steps:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. Select the **KMS key rings** tab in the side menu to browse the key rings.
5. Find the key ring that you want to delete and click the **Deletion** icon ![Deletion icon](../icons/delete.svg "Deletion") at the end of the row.
6. Confirm the deletion and click **Delete key ring**.

### Deleting key rings with the API
{: #delete-key-ring-api}

You can delete a key ring by making a `DELETE` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/key_rings/<key_ring_id>
```

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).
2. Retrieve the ID of the key ring that you want to delete.

    You can find the ID for a key ring in your {{site.data.keyword.hscrypto}} instance by [retrieving a list of your key rings](#list-key-ring).

3. Run the following `curl` command to delete the key ring.

    ```sh
    $ curl -X DELETE \
        "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/key_rings/<key_ring_id>" \
        -H "authorization: Bearer <IAM_token>" \
        -H "bluemix-instance: <instance_ID>" \
        -H "prefer: <return_preference>"
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
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} instance resides.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</p>
        </td>
      </tr>

      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>

      <tr>
        <td>
          <varname>key_ring_id</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier for the key ring that you would like to delete.
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
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</p>
        </td>
      </tr>

      <tr>
        <td>
          <varname>instance_ID</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service
            instance.
          </p>
          <p>For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</p>
        </td>
      </tr>

      <caption>
        Table 5. Describes the variables that are needed to delete keys with the key management service API.
      </caption>
    </table>

    A successful request returns an HTTP `204 No Content` response, which indicates that the key ring is successfully deleted.
