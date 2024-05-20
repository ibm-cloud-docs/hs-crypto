---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-20"

keywords: rotate managed key, rotate key, managed key rotation, key rotation, key rewrap

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Rotating managed keys manually
{: #uko-rotate-keys}

You can rotate your managed keys on demand by using {{site.data.keyword.uko_full_notm}} with the UI.
{: shortdesc}

To learn how managed key rotation works, see [Managed key rotation](/docs/hs-crypto/concepts?topic=hs-crypto-managed-key-rotation-intro).

## Rotating managed keys with the UI
{: #uko-rotate-managed-key-gui}
{: ui}

If you prefer to rotate your managed keys by using a graphical interface, you can use the UI.

Complete the following steps to rotate a key:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}.
4. Click **Managed keys** from the navigation to view all the available keys.
5. Select the key that you want to rotate and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key.
6. Click **Rotate** from the options menu. Alternatively, you can click **Show details** from the options menu and then click **Rotate** on the key details page.
7. Click **Rotate key** to confirm.

## Rotating managed keys with the API
{: #uko-rotate-managed-key-api}
{: api}

To rotate a managed key through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Rotate a managed key by making a `POST` call based on the following example:

    ```
    curl --location --request POST 'https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/managed_keys/<id>/rotate'
    --header 'Authorization: Bearer <IAM_token>' \
    --header 'Accept: application/json' \
    --header 'UKO-Vault: <vault_id>' \
    --header 'If-Match: <ETag>'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table. 

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The prefix that represents the geographic area where your service instance resides. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `id` | **Required.** The unique identifier for the managed key that you want to rotate. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} IAM access token that you retrieve in step 1. Include the full contents of the `IAM` token, including the Bearer value. |
    | `vault_id` | **Required.** The Universally Unique Identifier (UUID) of the vault that your manage key is assigned to. |
    | `ETag` | **Required.** The precondition of the update, which is the value of ETag from the header on a GET request. |
    {: caption="Table 1. Variables needed to rotate a managed key" caption-side="bottom"} 

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#rotate-managed-key){: external}.
    
    A successful rotation request returns an HTTP `204 No Content` response, which indicates that your managed key is replaced by the new key material.  
    


## What's next
{: #uko-rotate-keys-next}

- To confirm whether the key rotation is successfully proceeded, you can [view managed key versions](/docs/hs-crypto?topic=hs-crypto-uko-view-key-versions).
- After you rotate a managed key, new cryptographic key material becomes available for encryption. To learn how to rewrap data by using the latest key material, see [Rewrapping data after rotating a managed key](/docs/hs-crypto?topic=hs-crypto-managed-key-rotation-intro#rewrap-data-after-managed-key-rotation).
- To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external}.


