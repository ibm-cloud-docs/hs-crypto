---

copyright:
  years: 2022
lastupdated: "2022-02-08"

keywords: Unified Key Orchestrator, key management, UKO keystore, edit keystore, external keystore, KMS keystore

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


# Editing connection to external keystores
{: #edit-external-keystore-connection}

You can use {{site.data.keyword.uko_full_notm}} to edit connection to external keystores through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

You can edit the connection to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS).

## Editing connection to external keystores through the UI
{: #edit-external-keystore-connection-ui}

You cannot change keystore name and connection properties at the same time.
{: note}

### Editing connection to Azure Key Vaults
{: #edit-azure-key-vault-connection}

To edit the connection to an Azure Key Vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the Azure Key Vault that you want to edit. The Details side panel is displayed.
4. Click **Edit** in each property card to update keystore properties.
   
    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Keystore description        | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       | The name must match the name of the Key Vault in Azure.   |
    | Resource group on Azure     | A logical construct that groups multiple resources together. Obtain it from the Azure portal. |
    | Location on Azure           | Geographical location where the Key Vault is located in.   |
    | Environment on Azure        | The Azure environment to authenticate with.               |
    | Service principal password on Azure | Only password based authentication is supported for service principals.       |
    | Tenant ID on Azure          |  A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. Use Azure Active Directory tenant ID for authenticating requests to the key vault.     |
    | Subscription ID on Azure    |   A GUID that uniquely identifies your subscription to use Azure services.    |
    {: caption="Table 1. Azure Key Vault properties" caption-side="bottom"}    

5. Click **Test connection** to check the availability of the current keystore, and click **Next**.
6. Click **Save** to save the changes.



### Editing connection to AWS Key Management Service
{: #edit-aws-kms-connection}

To edit the connection to an AWS keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the AWS keystore that you want to edit. The Details side panel is displayed.
4. Click **Edit** in each property card to update keystore properties.
   
    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               | Geographical location where the AWS KMS is located in.    |
    | Access key ID on AWS        | Part of your access key for AWS.                          |
    | Secret access key on AWS    | Part of your access key for AWS. The secret access key is available for download only when you create it.     |
    {: caption="Table 2. AWS Key Management Service properties" caption-side="bottom"}
    
5. Click **Test connection** to check the availability of the current keystore, and click **Next**.
6. Click **Save** to save the changes.



### Editing connection to {{site.data.keyword.keymanagementservicelong_notm}} 
{: #edit-key-protect-connection}

To edit the connection to an {{site.data.keyword.keymanagementservicelong_notm}} keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the {{site.data.keyword.keymanagementserviceshort}} keystore that you want to edit. The Details side panel is displayed.
4. Click **Edit** in each property card to update keystore properties.

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.keymanagementserviceshort}} API endpoint  | A digital location where the API handles requests.  |
    | {{site.data.keyword.cloud_notm}} Identity Management endpoint   |    |
    | Instance ID                 | A string to identify your service instance.  |
    | API key                     | A unique code that is passed to an API to identify the calling application or user. |
    {: caption="Table 3. {{site.data.keyword.keymanagementservicelong_notm}} keystore properties" caption-side="bottom"}

5. Click **Test connection** to check the availability of the current keystore, and click **Next**.
6. Click **Save** to save the changes.



### Editing connection to another {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} instance
{: #edit-hp-crypto-connection}

To edit the connection to a {{site.data.keyword.hscrypto}} keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the {{site.data.keyword.hscrypto}} keystore that you want to edit. The Details side panel is displayed.
4. Click **Edit** in each property card to update keystore properties.

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on IBM Cloud         | Geographical location where the service instance is located in.   |
    | Resource group on IBM Cloud | A group that you use to organize resources across regions and manage access to the resources.  |
    | Service instance ID on IBM Cloud  | A string to identify your service instance.   |
    | API key on IBM Cloud        | A unique code that is passed to an API to identify the calling application or user.  |
    {: caption="Table 4. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} keystore properties" caption-side="bottom"}

5. Click **Test connection** to check the availability of the current keystore, and click **Next**.
6. Click **Save** to save the changes.



## What's next
{: #edit-external-keystore-connection-next}

- To find out how to connect to an external keystore, check out [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).

- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).
