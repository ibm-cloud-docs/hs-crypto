---

copyright:
  years: 2021
lastupdated: "2021-12-09"

keywords: Unified Key Orchestrator, keystore, connect to keystore, key management, external keystore

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


# Managing external keystores
{: #manage-external-keystores}

You can use {{site.data.keyword.uko_full_notm}} to manage external keystores that are external to your service instance on {{site.data.keyword.cloud}}. Or, you can connect to external keystores from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS).
{: shortdesc}


## Connecting to external keystores
{: #connect-external-keystores}

Complete the following steps to connect to an external keystore in the UI.


### Connecting to Azure Key Vaults
{: #connect-azure-key-vault}

1. [Log in to the {{site.data.keyword.uko_full_notm}} service instance](https://cloud.ibm.com/login){: external}.
2. In the left navigation panel, go to **Vaults** &gt; **Target keystores** to view all the available keystores.
3. To connect to a new Azure Key Vault, click **Add keystore.**
4. Under **Vault,** assign the keystore to a vault for access control. You can also click **Create vault** to create a new vault.
5. Under **Keystore type,** select **Azure Key Vault (Premium).**
6. In the **Keystore properties** table, specify the details of the keystore:
   
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               |                                                           |
    | Keystore description        | (Optional)                                                |
    | Service name on Azure       |                                                           |
    | Resource group on Azure     |                                                           |
    | Location on Azure           |                                                           |
    | Environment on Azure        |                                                           |
    | Service principal password on Azure |                                                   |
    | Tenant ID on Azure          |                                                           |
    | Subscription ID on Azure    |                                                           |

7. Click **Test connection** to check the availability of the current keystore.
8. View the summary of your Azure Key Vault keystore and the total estimated cost.
9. Click **Connect to keystore** to confirm.



### Connecting to AWS Key Management Services
{: #connect-aws-kms}





### Granting access to external keystores
{: #access-external-keystores}




## Disconnecting from external keystores
{: #disconnect-external-keystores}






## What's next
{: #manage-external-keystores-next}


  


