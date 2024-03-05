---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-27"

keywords: managed key versions, get key versions, list key versions

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Viewing managed key versions
{: #uko-view-key-versions}

You can view the key versions that are associated with a rotated managed key by using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}.
{: shortdesc}

When you rotate a managed key, the service creates a new version of the key material. As a security administrator, you can audit the rotation history of a managed key by viewing the key version history. 

## Viewing manage key versions with the UI
{: #uko-view-key-versions-gui}
{: ui}

If you prefer to view your managed key versions by using a graphical interface, you can use the UI.

Complete the following steps to view the key versions:

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}.
4. Click **Managed keys** from the navigation to view all the available keys.
5. Select the key that you want to view and click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions") to open a list of options for the key.
6. Click **Show details** from the options menu to open the key details page.
7. Click the version number next to the key name to open a list of all the previous key versions. The latest version is always displayed at the top. Click the corresponding key version to view its details. You can also search for a specific key version by entering the version number or the rotation date in the search bar. For example, you can enter `11` to search for version 11, or enter `2014` to search for versions that were rotated in year 2014.

You can no longer edit pervious key versions.
{: note}

## Viewing managed key versions with the API
{: #uko-view-key-versions-api}
{: api}

To view managed key versions through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. View managed key versions by making a `GET` call based on the following example:

    ```
    curl --location --request GET 'https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/managed_keys/<id>/versions' \
    --header 'Authorization: Bearer <IAM_token>' \
    --header 'Accept: application/json'
    ```
    {: codeblock}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `region` | **Required.** The prefix that represents the geographic area where your service instance resides. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions). |
    | `port` | **Required.** The port number of the API endpoint. |
    | `id` | **Required.** The unique identifier for the managed key that you want to rotate. |
    | `IAM_token` | **Required.** Your {{site.data.keyword.cloud_notm}} IAM access token that you retrieve in step 1. Include the full contents of the `IAM` token, including the Bearer value. |
    {: caption="Table 1. Variables needed to view managed key versions" caption-side="bottom"}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#list-managed-key-versions){: external}.

## What's next
{: #uko-view-key-versions-next}

To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external}.
