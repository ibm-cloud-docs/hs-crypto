---

copyright:
  years: 2022
lastupdated: "2022-01-14"

keywords: Unified Key Orchestrator, key management, keystore, edit keystore, external keystore

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

## Editing connection to external keystores through the UI
{: #edit-external-keystore-connection-ui}

You can edit the connection to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS).

You cannot change Keystore name and Connection properties at the same time.
{: note}

### Editing connection to Azure Key Vaults
{: #edit-azure-key-vault-connection}

To edit the connection to an Azure Key Vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** on the left navigation pane to view all the available keystores.
3. Click on the Azure Key Vault that you want to edit to open the sidepanel.
4. Click **Edit** to update keystore properties:
   
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Keystore description        | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       |                                                           |
    | Resource group on Azure     |                                                           |
    | Location on Azure           |                                                           |
    | Environment on Azure        |                                                           |
    | Service principal password on Azure |                                                   |
    | Tenant ID on Azure          |                                                           |
    | Subscription ID on Azure    |                                                           |

5. Click **Test connection** to check the availability of the current keystore.
6. Click **Save** to save the changes.



### Editing connection to AWS Key Management Services
{: #edit-aws-kms-connection}

To edit the connection to an AWS keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** on the left navigation pane to view all the available keystores.
3. Click on the AWS keystore that you want to edit to open the sidepanel.
4. Click **Edit** to update keystore properties:
   
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Keystore description        | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               |                                                           |
    | Access key ID on AWS        |                                                           |
    | Secret access key on AWS    |                                                           |

5. Click **Test connection** to check the availability of the current keystore.
6. Click **Save** to save the changes.



### Editing connection to {{site.data.keyword.keymanagementservicelong_notm}} 
{: #edit-key-protect-connection}






### Editing connection to another {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} instance
{: #edit-hp-crypto-connection}







## What's next
{: #edit-external-keystore-connection-next}


  


