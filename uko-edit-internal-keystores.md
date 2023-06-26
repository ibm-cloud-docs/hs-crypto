---

copyright:
  years: 2022, 2023
lastupdated: "2023-06-26"

keywords: Unified Key Orchestrator, UKO keystore, edit keystore, key management, internal keystore, KMS keystore

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Editing internal keystores
{: #edit-internal-keystores}

You can edit your internal keystores in {{site.data.keyword.uko_full_notm}} with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

## Editing internal keystores with the {{site.data.keyword.cloud_notm}} console
{: #edit-internal-keystores-ui}
{: ui}

To edit the details of an internal KMS keystore by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the internal keystore that you want to edit. The Details side panel is displayed.
4. Click **Edit** to update the **Keystore name** and **Description**. 

  The keystore name must be of 1 to 100 characters in length. The first character must be a letter (case-sensitive) or digit (0-9). The rest can also be symbols (.-_) or spaces. The description can be up to 200 characters in length.
  
  You can filter and search the keys that are assigned to this keystore, but you cannot edit key details or change key states from the side panel. To edit the details of the keys, see [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  {: tip}

5. Click **Save** to save the changes.

You can search for a specific keystore by using the search bar, or filter keystores based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Target keystores** table.
{: tip}



## Editing internal keystores with the API
{: #edit-internal-keystores-api}
{: api}

To edit the details of an internal keystore through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keystores in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Update an internal keystore by making a `PATCH` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/keystores/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your keystore.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#update-keystore){: external}.



## What's next
{: #edit-internal-keystores-next}

- To find out instructions on adding an internal keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores).

- To find out how to delete an internal keystore, check out [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores).
  
