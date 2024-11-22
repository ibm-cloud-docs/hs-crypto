# Deleting key templates
{: #delete-template}

You can delete your key templates in {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API. After you delete the key template, you can no longer create managed keys based on this key template.
{: shortdesc}


## Deleting key templates with the UI
{: #delete-key-template-ui}
{: ui}

 
To delete a key template, you need to destroy all keys that are created with the template and remove them from the vault first. For more information, see [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).
{: note}
 

Follow these steps to complete the process:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Key templates** from the navigation to view all the available key templates.

    You can also view archived key templates by clicking the **Show archived templates** icon ![Show archived templates icon](../images/archive.svg "Show archived templates") on the table.

3. Locate the key template that you want to delete, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and select **Delete** to remove the key template.
4. Click **Delete key template** to confirm the deletion.

   Alternatively, locate the key template that you want to delete, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then click **Show details**. A side panel is displayed to show the key template properties, click **Actions** > **Delete**.
   
The key template is deleted from the vault. You can no longer create managed keys based on this key template. 


## Deleting key templates with the API
{: #delete-key-template-api}
{: api}

To delete a key template through the API, follow these steps:

 
To delete a key template, you need to destroy all keys that are created with the template and remove them from the vault first. For more information, see [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys&interface=api).
{: note}


1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Delete a key template by making a `DELETE` call to the following endpoint.

    
    
    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/templates/<id>
    
    ```
    {: codeblock}

    Replace `<id>` with the ID of your key template.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#delete-key-template){: external}.


## What's next
{: #delete-key-template-next}

- To create another key template, check out [Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template).

- To find out instructions on managing a key template, check out [Editing key template details](/docs/hs-crypto?topic=hs-crypto-edit-template).


