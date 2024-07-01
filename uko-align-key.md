---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-01"

keywords: Unified Key Orchestrator, align template, key template

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Realigning managed keys with key templates
{: #align-key}

After a managed key is created with a key template, you can still update the key template on general properties, key lifecycles, and assigned keystores. If it happens, an `Unaligned` flag can be displayed on the key details card for keys that are created with the key template. You can then manually realign your key with the key template with the {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API. You can either realign active or deactivated keys with the key template.  
{: shortdesc}

  
Currently, with the {{site.data.keyword.uko_full_notm}} with the UI, you can only realign assigned keystores with the key template. To realign general properties and key lifecycles, use the {{site.data.keyword.uko_full_notm}} API.  
{: note}


## Realigning managed keys with key templates through the UI
{: #align-key-ui}
{: ui}

To realign managed keys with key templates by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys. 
3. Click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") on the key that you want to realign, and select **Show details**.
4. To realign the key with key templates, click **Actions** and select **Realign with template**.
5. View the details on the confirmation page, check all boxes, and then click **Realign with template** to confirm.

Your key is now aligned again with the key template in terms of assigned keystores. 


 
If the key template is archived, you cannot realign the key with key templates.  
{: note}


## Realigning keys with key templates through the API
{: #align-key-api}
{: api}

To realign keys with key templates through the API, complete the following steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `POST` call to the following endpoint.

    
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/managed_keys/<id>/update_from_template
    
    ```
    {: codeblock}
    

    Replace `<id>` with the ID of your key.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#update-managed-key-from-template){: external}.


## What's next
{: #align-key-next}

- To find out instructions on editing a key template, check out [Editing key template details](/docs/hs-crypto?topic=hs-crypto-edit-template&interface=ui).

- To find out more about managing your key template, check out [Viewing a list of key templates](/docs/hs-crypto?topic=hs-crypto-view-key-template&interface=ui).




