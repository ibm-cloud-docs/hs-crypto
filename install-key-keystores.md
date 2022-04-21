---

copyright:
  years: 2022
lastupdated: "2022-04-21"

keywords: Unified Key Orchestrator, install keys, key management, kms keys

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}


# Setting target keystores for existing keys
{: #install-key-keystores}

You can use a managed key in {{site.data.keyword.uko_full_notm}} for encryption and decryption only after it is installed in at least one keystore. You can install and uninstall existing keys in target keystores with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}


## Setting target keystores for existing keys with the {{site.data.keyword.cloud_notm}} console
{: #install-key-keystores-ui}
{: ui}

To install or uninstall a managed key in target keystores by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key that you want to edit, and choose **Show details**.
4. Click **Set target keystores** to see all possible keystores that you can select for the key.
5. Select one or multiple target keystores that you want to install the key in. Or, you can clear the checkbox to uninstall the key from a keystore.
   
   Installing a key in multiple keystores enables redundancy. If you want to install the key to a new keystore, click **Add keystore**. For more instructions, see [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
   
6. Click **Save** to save the changes.



## Setting target keystores for existing keys with the API
{: #install-key-keystores-api}

To install or uninstall a managed key in target keystores through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Add a keystore to or remove a keystore from a keystore group by making a `PATCH` call to the following endpoint. The keystore group should match the key template that is associated with the managed key.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/keystores/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your keystore.

3. Update the managed key to match the latest version of the associated key template by making a `POST` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/managed_keys/<id>/update_from_template
    ```
    {: codeblock}

    Replace `<id>` with the ID of your managed key.

    For detailed instructions and code examples about using the API method, check out how to [Update an internal keystore or a keystore connection](/apidocs/uko#update-keystore){: external} and [Update a managed key to match the key template](/apidocs/uko#update-managed-key-from-template){: external} in the {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc.



## What's next
{: #install-key-keystores-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).
  
- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  
- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).


