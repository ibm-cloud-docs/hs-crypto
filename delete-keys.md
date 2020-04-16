---

copyright:
  years: 2018, 2020
lastupdated: "2020-02-18"

keywords: details of the DELETE request, delete encryption key, deleting keys, Variable Description region, delete key API examples

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}

# Deleting keys
{: #delete-keys}

If you are an administrator of the {{site.data.keyword.cloud_notm}} space or {{site.data.keyword.hscrypto}} service instance, you are authorized to delete an encryption key and the associated data in {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

When you delete a key, you permanently shred its contents and associated data. The action cannot be reversed. Destroying resources is not recommended in a production environment.
{: important}

## Deleting keys with the GUI
{: #delete-keys-gui}

[After you create or import your existing keys into the service](/docs/hs-crypto?topic=hs-crypto-create-root-keys), complete the following steps to delete a key:

1. [Log in to the {{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource List** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}}.
4. Use the **Keys** table to browse the keys in your service.
5. Select the key that you want to delete and click the overflow icon to open a list of options for the key.
6. From the options menu, click **Delete key** and confirm the key deletion in the next screen.

After you delete a key, the key transitions to the _Destroyed_ state. Keys in this state are no longer recoverable. Metadata that is associated with the key, such as the key's deletion date, is kept in the {{site.data.keyword.hscrypto}} database.

## Deleting keys with the API
{: #delete-keys-api}
{: help}
{: support}

To delete a key and its contents, make a `DELETE` call to the following endpoint.

```
https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api).

2. Retrieve the ID of the key that you would like to delete.

    You can retrieve the ID for a specified key by making a `GET /v2/keys/` request, or by viewing your keys in the {{site.data.keyword.hscrypto}} dashboard.

3. Run the following cURL command to permanently delete the key and its contents.

    ```cURL
    curl -X DELETE \
      https://api.<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>The region abbreviation, such as <code>us-south</code> or <code>au-syd</code>, that represents the geographic area where your {{site.data.keyword.hscrypto}} service instance resides. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints">Regional service endpoints</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>The unique identifier for the key that you would like to delete.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Your {{site.data.keyword.cloud_notm}} access token. Include the full contents of the <code>IAM</code> token, including the Bearer value, in the cURL request. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-access-token">Retrieving an access token</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>The unique identifier that is assigned to your {{site.data.keyword.hscrypto}} service instance. For more information, see <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">Retrieving an instance ID</a>.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>A header that alters server behavior for <code>POST</code> and <code>DELETE</code> operations.</p><p>When you set the <em>return_preference</em> variable to <code>return=minimal</code>, the service returns a successful deletion response. When you set the variable to <code>return=representation</code>, the service returns both the key material and the key metadata.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Describes the variables that are needed to delete keys with the {{site.data.keyword.hscrypto}} key management API.</caption>
    </table>

    If the _return_preference_ variable is set to `return=representation`, the details of the `DELETE` request are returned in the response entity-body. The following JSON object shows an example returned value.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
        "collectionTotal": 1
      },
      "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    For a detailed description of the available parameters, see the {{site.data.keyword.hscrypto}} [key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.

    ## What's next
    {: #delete-key-next}

    - To create another root key, check out [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
    - To delete the service instance, check out [Deleting service instances](/docs/hs-crypto?topic=hs-crypto-delete-instance)
    - To find out more about programmatically managing your keys, [check out the {{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
