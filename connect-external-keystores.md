---

copyright:
  years: 2022
lastupdated: "2022-01-19"

keywords: Unified Key Orchestrator, UKO keystore, connect keystore, external keystore, KMS keystore

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

You can connect to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS).

For each external keystore, you are charged $6.25 per hour as base price for {{site.data.keyword.uko_full_notm}}. You can connect to one external keystore at no initial cost, regardless of the type. If additional keystores are needed, you are charged $225 per calendar month for each keystore. 
{: note}

## Connecting to external keystores through the UI
{: #connect-external-keystores-ui}

### Connecting to Azure Key Vaults
{: #connect-azure-key-vault}

To connect to an Azure Key Vault through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. To connect to an Azure Key Vault, click **Add keystore**.
4. Under **Vault**, select a vault for the keystore for access control, and click **Next**. 

  If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults){: external}
5. Under **Keystore type**, select **Azure Key Vault (Premium)** and click **Next**.
6. Under **Keystore properties**, specify the details of the keystore.
   
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Keystore description        | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       | The name must match the name of the Key Vault in Azure.   |
    | Resource group on Azure     | A logical construct that groups multiple resources. Obtain it from the Azure portal. |
    | Location on Azure           | Geographical location where the Key Vault is located in.   |
    | Environment on Azure        | The Azure environment to authenticate with.               |
    | Service principal password on Azure | Only password based authentication is supported for service principals.       |
    | Tenant ID on Azure          |  A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. Use Azure Active Directory tenant ID for authenticating requests to the Key Vault.     |
    | Subscription ID on Azure    |   A GUID that uniquely identifies your subscription to use Azure services.    |
    {: caption="Table 1. Azure Key Vault properties" caption-side="bottom"}

7. Click **Test connection** to check the availability of the current keystore, and then click **Next** to continue.<!--What can users do if the test connection fails?>
8. Under **Summary**, view the summary of your Azure Key Vault and the total estimated cost.
9. After you confirm the keystore details, click  **Connect to keystore** to connect to the keystore.

You have successfully connected to the Azure Key Vault keystore. 

### Connecting to AWS Key Management Services
{: #connect-aws-kms}

To connect to an AWS keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. To connect to a AWS keystore, click **Add keystore**.
4. Under **Vault**, select a vault for the keystore for access control, and click **Next**. 

  If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults){: external}
5. Under **Keystore type**, select **AWS Key Management Service**.
6. Under **Keystore properties**, specify the details of the keystore.
   
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               | Geographical location where the AWS KMS is located in.    |
    | Access key ID on AWS        | Part of your access key for AWS.                          |
    | Secret access key on AWS    | Part of your access key for AWS. The secret access key is available for download only when you create it.     |
    {: caption="Table 2. AWS Key Management Services properties" caption-side="bottom"}

7. Click **Test connection** to check the availability of the current keystore, and click **Next**.
8. Under **Summary**, view the summary of your AWS keystore and the total estimated cost.
9. After you confirm the keystore details, click **Connect to keystore** to connect to the keystore.

You have successfully connected to the AWS Key Management Servinces keystore. 

### Connecting to {{site.data.keyword.keymanagementservicelong_notm}} 
{: #connect-key-protect}






### Connecting to another {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} instance
{: #connect-hp-crypto}







## What's next
{: #connect-external-keystores-next}

- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out how to update the connection to an external keystore, check out [Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).
  


