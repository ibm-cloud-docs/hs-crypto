---

copyright:
  years: 2022
lastupdated: "2022-01-14"

keywords: Unified Key Orchestrator, keystore, connect keystore, external keystore

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


# Connecting to external keystores
{: #connect-external-keystores}

You can use {{site.data.keyword.uko_full_notm}} to connect to external keystores through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

## Connecting to external keystores through the UI
{: #connect-external-keystores-ui}

You can connect to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS).

### Connecting to Azure Key Vaults
{: #connect-azure-key-vault}

To connect to an Azure Key Vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** on the left navigation pane to view all the available keystores.
3. To connect to a new Azure Key Vault, click **Add keystore.**
4. Under **Vault,** assign the keystore to a vault for access control. You can also click **Create vault** to create a new vault.
5. Under **Keystore type,** select **Azure Key Vault (Premium).**
6. Under **Keystore properties,** specify the details of the keystore:
   
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

7. Click **Test connection** to check the availability of the current keystore.
8. View the summary of your Azure Key Vault, then **Connect to keystore** to confirm.



### Connecting to AWS Key Management Services
{: #connect-aws-kms}

To connect to an AWS keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** on the left navigation pane to view all the available keystores.
3. To connect to a new AWS keystore, click **Add keystore.**
4. Under **Vault,** assign the keystore to a vault for access control. You can also click **Create vault** to create a new vault.
5. Under **Keystore type,** select **AWS keystore.**
6. Under **Keystore properties,** specify the details of the keystore:
   
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Keystore description        | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               |                                                           |
    | Access key ID on AWS        |                                                           |
    | Secret access key on AWS    |                                                           |

7. Click **Test connection** to check the availability of the current keystore.
8. View the summary of your AWS keystore, then **Connect to keystore** to confirm.



### Connecting to {{site.data.keyword.keymanagementservicelong_notm}} 
{: #connect-key-protect}






### Connecting to another {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} instance
{: #connect-hp-crypto}







## What's next
{: #connect-external-keystores-next}


  


