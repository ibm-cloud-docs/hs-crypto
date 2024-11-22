# Archiving and unarchiving key templates
{: #archive-template}


You can archive your key templates if they are not to be used, and unarchive them later if needed. You can perform archive or unarchive a key template in {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

 
You can view archived key templates by clicking the **Show archived templates** icon ![Show archived templates icon](../images/archive.svg "Show archived templates") on the table. After the template is archived, you cannot edit the distribution of keys created with the template, and you can no longer create managed keys with the archived key template. However, you can still use the keys for cryptographic operations. 
 {: important}


## Archiving key templates with the UI
{: #archive-key-template-ui}
{: ui}

To archive the key template, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Key templates** from the navigation to view all the available unarchived key templates.
3. Locate the key template that you want to archive, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and select **Archive**. 
  
   Alternatively, locate the key template that you want to archive, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then click **Show details**. A side panel is displayed to show the key template properties, select **Actions** > **Archive**.

4. Check the box for **Key template will not be accessible** and click **Archive key template**.
   
After the template is archived, you cannot edit the distrubution of existing key that are created with the template, and you can no longer create managed keys with this key template. However, you can activate the key template again by unarchiving it. 


## Archiving key templates with the API
{: #archive-key-template-api}
{: api}

To archive the key template through the API, complete the following steps: 

1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Archive a key template by making a `POST` call to the following endpoint.

    
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/templates/<id>/archive
    
    ```
    {: codeblock}

    Replace `<id>` with the ID of your key template.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#archive-key-template){: external}.

## Unarchiving key templates with the UI
{: #unarchive-key-template-ui}
{: ui}

To unarchive the key template, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Key templates** from the navigation to view all the available unarchived key tamplates.
3. View archived key templates by clicking the **Show archived templates** icon ![Show archived templates icon](../images/archive.svg "Show archived templates") on the table.
4. Locate the key template that you want to unarchive, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and choose **Unarchive**. 

    Alternatively, locate the key template that you want to unarchive, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then click **Show details**. A side panel is displayed to show the key template properties, select **Actions** > **Unarchive**.

5. Click **Unachive key template**.

You can then use the key template to create keys and edit the key template properties again.
   

## Unarchiving key templates with the API
{: #unarchive-key-template-api}
{: api}

To unarchive the key template through the API, complete the following steps: 

1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Unarchive a key template by making a `POST` call to the following endpoint.
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/templates/<id>/unarchive
    
    ```
    {: codeblock}

    Replace `<id>` with the ID of your key template.

    
    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#unarchive-key-template){: external}.



## What's next
{: #archive-key-template-next}

- To find out instructions on creating a key template, check out [Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template).
  
- To find out instructions on managing a key template, check out [Editing key template details](/docs/hs-crypto?topic=hs-crypto-edit-template).

- To continue to create keys with the key template created, follow the instruction in [Creating managed keys with a key template](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=ui#create-managed-keys-template-ui).

- To find out instructions on deleting a key template, check out [Deleting key templates](/docs/hs-crypto?topic=hs-crypto-delete-template).


