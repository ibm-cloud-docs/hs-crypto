---

copyright:
  years: 2021
lastupdated: "2021-07-26"

keywords: disable key, enable key, suspend key, suspend operations on a key

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

# Disabling root keys
{: #disable-keys}

You can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to disable or enable a root key and temporarily revoke access to the key's associated data on the cloud.
{: shortdesc}

As an admin, you might need to temporarily disable a root key if you suspect a possible security exposure, compromise, or breach with your data. When you disable a root key, you suspend the encrypt and decrypt operations. After you confirm that a security risk is no longer active, you can restore access to your data by enabling the disabled root key.

If you are using a cloud service that is integrated with {{site.data.keyword.hscrypto}}, your data might not be accessible after you disable a root key. To determine whether an [integrated service](/docs/hs-crypto?topic=hs-crypto-integrate-services) supports revoking access to data by disabling a {{site.data.keyword.hscrypto}} root key, see the service documentation.
{: note}

When you disable a root key, the key moves to the
[_Suspended_ state](/docs/hs-crypto?topic=hs-crypto-key-states),
and it can no longer be used to cryptographically protect data.

When you enable a root key that was previously disabled, the key moves
from the _Suspended_ to the _Active_ key state. This action restores the key's
encrypt and decrypt operations.

You must wait 30 seconds after you disable a root key before you are able to enable it again.

For an integrated Cloud Service that supports revoking access to a
disabled root key, the service can take up to 4 hours to revoke or restore access
to the associated data of the root key. After access to the associated
data is revoked or restored, a corresponding enable event is displayed in the Activity
Tracker web UI.
{: note}

## Disabling and enabling root keys with the console
{: #disable-enable-ui}

If you prefer to enable or disable your root keys by using a graphical interface, you can use the {{site.data.keyword.cloud_notm}} console.

### Disabling a root key
{: #disable-ui}

[After you create or import your existing keys into the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys),
complete the following steps to disable a key:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your
provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, use the **Keys** table to browse the keys in
your service instance.
5. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key that you want to
disable.
6. From the options menu, click **Disable key**, enter the key name to confirm the key to be disabled, and click **Disable key**.

After the key is disabled, the **State** of the key is moved to `Suspended` in the **Keys** table.

### Enabling a root key
{: #enable-ui}

If you want to reenable a root key that is [disabled](#disable-ui),
complete the following steps:

You must wait 30 seconds after you disable a root key before you are able to enable it again.
{: note}

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://{DomainName}/){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your
provisioned instance of {{site.data.keyword.hscrypto}}.
4. On the **KMS keys** page, use the **Keys** table to browse the keys in
your service.
5. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key that you want to
enable.
6. From the options menu, click **Enable key**.

 After the key is enabled, the **State** of the key is transferredto `Active` in the **Keys** table.

## Disabling and enabling root keys with the API
{: #disable-enable-api}

### Disabling a root key
{: #disable-api}

When you disable a root key, the key moves to the [_Suspended_ state](/docs/hs-crypto?topic=hs-crypto-key-states), and it can no longer be used to encrypt data.

For an integrated cloud service that supports revoking access to a disabled root key, the service can take up to 4 hours to revoke access to the associated data of the root key. After access to the associated data is revoked, a corresponding disable event is displayed in the Activity Tracker web UI.
{: note}

You can disable a root key that's in the _Active_ key state by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/disable
```

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api#retrieve-kms-credentials).

    To disable a root key, you must be assigned a _Manager_ service access role for the instance or key. To learn how IAM roles map to {{site.data.keyword.hscrypto}} service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Retrieve the key management API endpoint URL.

    You can get the API endpoint from your provisioned service instance dashboard through **Overview** &gt; **Connect** &gt; **Key management endpoint URL**. Or, you can dynamically [retrieve the API endpoint URL](https://{DomainName}/apidocs/hs-crypto#getinstance){: external} with an API call. Select the public or private key manage endpoint URL based on your needs.

3. Retrieve the ID of the root key that you want to disable.

    You can retrieve the ID for a specified key by making a [list keys API request](https://{DomainName}/apidocs/hs-crypto#getkeys){: external}, or by viewing your keys in the {{site.data.keyword.cloud_notm}} console.

4. Disable the root key and suspend the encrypt and decrypt operations by making the following API call.

    ```sh
    curl -X POST \
      "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/disable" \
      -H "authorization: Bearer <IAM_token>" \
      -H "bluemix-instance: <instance_ID>" \
      -H "x-kms-key-ring: <key_ring_ID>"
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
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>eu-de</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides.
          </p>
          <p>
            For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
        </td>
      </tr>

      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>

      <tr>
        <td>
          <varname>key_ID</varname>
        </td>
        <td>
          <strong>Required.</strong> The unique identifier for the root key that you want to disable.
        </td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request.
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
      <tr>
        <td>
          <varname>key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. It is therefore suggested to specify the key ring ID for a more optimized request.
          </p>
          <p>
            Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default.
          </p>
          <p>
            For more information, see
            [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings).
          </p>
        </td>
      </tr>
      <caption>
        Table 1. Describes the variables that are needed to disable root keys with the {{site.data.keyword.hscrypto}} API.
      </caption>
    </table>

    A successful disable request returns an HTTP `204 No Content` response, which indicates that the root key was disabled for encrypt and decrypt operations.

5. Optional: Verify that the root key was disabled by retrieving details about the key.

    ```cURL
    curl -X GET \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_id>/metadata \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.key+json'
    ```
    {: codeblock}

    Review the `state` field in the response body to verify that the key moved to the _Suspended_ key state. The following JSON output shows the metadata details for a disabled root key.

    The integer mapping for the _Suspended_ key state is 2. Key States are based on NIST SP 800-57.
    {: note}

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
                "name": "...",
                "description": "...",
                "tags": [
                    "..."
                ],
                "state": 2,
                "extractable": false,
                "crn": "crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
                "imported": true,
                "creationDate": "2020-03-10T20:41:27Z",
                "createdBy": "...",
                "algorithmType": "AES",
                "algorithmMetadata": {
                    "bitLength": "128",
                    "mode": "CBC_PAD"
                },
                "algorithmBitSize": 128,
                "algorithmMode": "CBC_PAD",
                "lastUpdateDate": "2020-03-16T20:41:27Z",
                "keyVersion": {
                    "id": "30372f20-d9f1-40b3-b486-a709e1932c9c",
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
    {: screen}

### Enabling a disabled root key
{: #enable-api}

When you enable a root key that was previously disabled, the key moves from the _Suspended_ to the _Active_ key state. This action restores the key's encrypt and decrypt operations.

For an integrated cloud service that supports revoking access to a disabled root key, the service can take up to 4 hours to restore access to the associated data of the root key. After access to the associated data is restored, a corresponding enable event is displayed in the Activity Tracker web UI.
{: note}

You can enable a root key that's in the _Suspended_ key state by making a `POST` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/enable
```

1. [Retrieve your authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api#retrieve-kms-credentials).

    To enable a root key, you must be assigned a _Manager_ service access role for the instance or key. To learn how IAM roles map to {{site.data.keyword.hscrypto}} service actions, check out [Service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
    {: note}

2. Retrieve the key management API endpoint URL.

    You can get the API endpoint from your provisioned service instance dashboard by clicking **Manage** &gt; **Key management endpoint URL**, or you can dynamically [retrieve the API endpoint URL](https://{DomainName}/apidocs/hs-crypto#getinstance){: external} with an API call. Select the public or private key manage endpoint URL based on your needs.

3. Retrieve the ID of the disabled root key that you want to enable.

    You can retrieve the ID for a specified key by making a [list keys API request](https://{DomainName}/apidocs/hs-crypto#getkeys){: external}, or by viewing your keys in the {{site.data.keyword.hscrypto}} dashboard.

4. Enable the root key and restore the encrypt and decrypt operations by making the following API call.

    You must wait 30 seconds after you disable a root key before you are able to enable it again.
    {: note}

    ```sh
    curl -X POST \
      "https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>/actions/enable" \
      -H "authorization: Bearer <IAM_token>" \
      -H "bluemix-instance: <instance_ID>" \
      -H "x-kms-key-ring: <key_ring_ID>"
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
            <strong>Required.</strong> The region abbreviation, such as <code>us-south</code> or <code>eu-de</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides.
          </p>
          <p>
            For more information, see [Regional service endpoints](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints).
          </p>
        </td>
      </tr>

      <tr>
        <td><varname>port</varname></td>
        <td><strong>Required.</strong> The port number of the API endpoint.</td>
      </tr>
      
      <tr>
        <td>
          <varname>key_ID</varname>
        </td>
        <td>
          <strong>Required.</strong> The unique identifier for the root key that you want to enable.
        </td>
      </tr>

      <tr>
        <td>
          <varname>IAM_token</varname>
        </td>
        <td>
          <p>
            <strong>Required.</strong> Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request.
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
      <tr>
        <td>
          <varname>key_ring_ID</varname>
        </td>
        <td>
          <p>
            <strong>Optional.</strong> The unique identifier of the key ring that the key belongs to. If unspecified, {{site.data.keyword.hscrypto}} will search for the key in every key ring that is associated with the specified instance. It is therefore suggested to specify the key ring ID for a more optimized request.
          </p>
          <p>
            Note: The key ring ID of keys that are created without an `x-kms-key-ring` header is: default.
          </p>
          <p>
            For more information, see
            [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings).
          </p>
        </td>
      </tr>
      <caption>
        Table 2. Describes the variables that are needed to enable root keys with the {{site.data.keyword.hscrypto}} API.
      </caption>
    </table>

    A successful enable request returns an HTTP `204 No Content` response, which indicates that the root key was reinstated for encrypt and decrypt operations.

5. Optional: Verify that the root key was enabled by retrieving details about the key.

    ```cURL
    curl -X GET \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_id>/metadata \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'accept: application/vnd.ibm.kms.key+json'
    ```
    {: codeblock}

    Review the `state` field in the response body to verify that the root key moved to the _Active_ key state. The following JSON output shows the metadata details for an active key.

    The integer mapping for the _Active_ key state is 1. Key States are based on NIST SP 800-57.
    {: note}

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
          "name": "...",
          "description": "...",
          "tags": [
            "..."
          ],
          "state": 1,
          "extractable": false,
          "crn": "crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:12e8c9c2-a162-472d-b7d6-8b9a86b815a6:key:02fd6835-6001-4482-a892-13bd2085f75d",
          "imported": true,
          "creationDate": "2020-03-10T20:41:27Z",
          "createdBy": "...",
          "algorithmType": "AES",
          "algorithmMetadata": {
            "bitLength": "128",
            "mode": "CBC_PAD"
          },
          "algorithmBitSize": 128,
          "algorithmMode": "CBC_PAD",
          "lastUpdateDate": "2020-03-16T20:41:27Z",
          "keyVersion": {
            "id": "30372f20-d9f1-40b3-b486-a709e1932c9c",
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
    {: screen}
