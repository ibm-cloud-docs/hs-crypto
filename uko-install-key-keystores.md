---

copyright:
  years: 2022, 2023
lastupdated: "2023-06-12"

keywords: Unified Key Orchestrator, install keys, activate key, key management, kms keys

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Reassigning target keystores for existing keys
{: #install-key-keystores}

You can reassigning target keystores for keys after they are created through the {{site.data.keyword.cloud_notm}} console or the API.
{: shortdesc}


## Reassigning target keystores for existing keys with the {{site.data.keyword.cloud_notm}} console
{: #install-key-keystores-ui}
{: ui}

To reassigning target keystores for existing keys by using the {{site.data.keyword.cloud_notm}} console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. Click the Actions icon  ![Actions icon](../icons/action-menu-icon.svg "Actions")  on the key that you want to edit, and choose **Show details**.
4. In the **Target keystores** card, click **Edit** to see all possible keystores that you can select for the key.
5. Activate or deactivate the key in keystores by adding or removing target keystores. You can use a key only for encryption and decryption after it is activated in at least one target keystore.

    - Add target keystores
    
        If you want to activate the key in more target keystores, check the corresponding target keystore cards. The _Active_ key state is synced across all target keystores.

    - Remove target keystores

        If you want to deactivate the key in some target keystores, clear the checkbox in the corresponding target keystore cards. After the removal, the key material remains unless you destroy the key. The key state in the removed target keystores becomes _deactivated_ and cannot be synced with the managed key state in the future. However, you can reactivate the key by reassigning the key to these keystores so that the key state is synced again.
        
        A managed keys is cynced across multiple target keystores that it is assigned to. You can fully remove a key from a target keystore only after the key is destroyed. However, you can deactivate the key or remove the target keystores at any time.

    - Sync keys

        If the key state in some target keystores is different from the managed key state, you receive a **Key out of sync** warning message. An **Out of sync** flag is also displayed in the corresponding keystore card. There can be multiple reasons why the key state is out of sync. For example, you have deactivated the key in this target keystore before, or you activate the key through the CLI and the console doesn't reflect the state timely. When you hover over this flag, you can see the specific reason. You can sync the key state by clicking **Sync keys**. 
    
   
    Activating a key in multiple keystores enables redundancy. If you want to activate the key in a new keystore, click **Add keystore**. For more instructions, see [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

   
6. Click **Save** to save the changes.


## Reassigning target keystores for existing keys with the API
{: #install-key-keystores-api}
{: api}

To reassigning target keystores for existing keys by using API, complete the following steps:

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


