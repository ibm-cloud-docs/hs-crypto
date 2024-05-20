---

copyright:
  years: 2022, 2024
lastupdated: "2024-05-20"

keywords: Unified Key Orchestrator, view key templates, key management, kms keys, UKO

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Viewing a list of key templates
{: #view-key-template}

You can view a list of your key templates in {{site.data.keyword.uko_full_notm}} with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}


## Viewing a list of key templates with the UI
{: #view-key-template-ui}
{: ui}

To view a list of your key templates by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Key templates** from the navigation to view all the available key templates.
3. Browse the general characteristics of your key templates in the table. 
   
    
   To customize how the table is to be presented, click the **Settings icon** ![Settings icon](../icons/settings.svg "Settings") and check the columns to be displayed. You can also view archived key templates by clicking the **Show archived templates** icon ![Show archived templates icon](/images/archive.svg "Show archived templates") on the table. For more information, see [Archiving and unarchiving key templates](/docs/hs-crypto?topic=hs-crypto-archive-template&interface=ui).
   {: tip} 

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Name                 | The unique, human-readable name that is assigned to your key template. |
    | ID                   | A string that uniquely identifies the key template. The key template ID is truncated and displayed with a copy icon. |
    | Vault                | The vault that controls access to the key template.           |
    | Last modified        | The date and time when the key template was last updated. This field gets updated when the key template is created, edited, or any part of the key template metadata is modified.   |
    | Key algorithm        | The encryption algorithm to encrypt data for the key to be created with the template.      |
    | Key length           | The number of bits that represents the encryption strength of the keys that are created or to be created with the template.  |
    | Key naming scheme    | The key naming conventions that are created based on the key template.     |
    | Keys                 | The number of keys that created based on the key template.                | 
    | Keystore type        | The type of keystore that the key template properties are compatible with.   |
    | Creation date        | Set a date range of when the key template was created.             |
    {: caption="Table 1. Key templates table" caption-side="bottom"}
    
     
    You can search for a specific key template by using the search bar, or filter key templates based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Key templates** table. 
    {: tip}



## Viewing a list of key templates with the API
{: #view-key-template-api}
{: api}

To view a list of key templates through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with key templates in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create a key template by making a `GET` call to the following endpoint.
    
    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/templates
    
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#list-key-templates){: external}.

## What's next
{: #view-key-template-next}

- To find out instructions on creating a key template, check out [Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template).

- To find out instructions on deleting a key template, check out [Deleting key templates](/docs/hs-crypto?topic=hs-crypto-delete-template).

- To continue to create keys with the key template created, follow the instruction in [Creating managed keys with a key template](/docs/hs-crypto?topic=hs-crypto-create-managed-keys&interface=ui#create-managed-keys-template).

- To find out instructions on archiving and unarchiving the key template, check out [Archiving and unarchiving key templates](/docs/hs-crypto?topic=hs-crypto-archive-template). 



