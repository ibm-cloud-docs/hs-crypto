---

copyright:
  years: 2022
lastupdated: "2022-02-11"

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

You can connect to one external keystore at no initial cost, regardless of the type. You are charged for additional external keystores. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Other currencies are applied based on the region the service instance is provisioned in.
{: note}

## Connecting to external keystores through the UI
{: #connect-external-keystores-ui}

To connect to an external keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. To connect to an external keystore, click **Add keystore**.
4. Under **Vault**, select a vault for the keystore for access control, and click **Next**. 

   If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Keystore type**, select one of the following types and click **Next**:

    - **Azure Key Vault (Premium)**
    - **AWS Key Management Service**
    - **{{site.data.keyword.keymanagementserviceshort}}**
    - **KMS keystore in another instance**

6. Under **Keystore properties**, specify the details of based on the keystore type that you want to connect to, and click **Next** to continue when you are done.
   
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
    {: #table-1}
    {: caption="Table 1. Azure Key Vault properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault properties"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               | Geographical location where the AWS KMS is located in.    |
    | Access key ID on AWS        | Part of your access key for AWS.                          |
    | Secret access key on AWS    | Part of your access key for AWS. The secret access key is available for download only when you create it.     |
    {: #table-2}
    {: caption="Table 2. AWS Key Management Service properties" caption-side="bottom"}
    {: tab-title="AWS Key Management Service properties"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.keymanagementserviceshort}} API endpoint  | The service endpoint of your {{site.data.keyword.keymanagementserviceshort}} instance. For more information, see [/docs/key-protect?topic=key-protect-regions#service-endpoints].  |
    | {{site.data.keyword.cloud_notm}} Identity Management endpoint **Tiffany: Is it IAM endpoint? If yes, the title needs to be changed**  |  The endpoint of IAM, which is `https://iam.cloud.ibm.com`.  |
    | Instance ID                 | The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. For more information, see [Retrieving your instance ID and cloud resource name](/docs/key-protect?topic=key-protect-retrieve-instance-ID).  |
    | API key    **Tiffany: Need to be changed to `Service ID API key` to avoidn confusion**                  | A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).|
    {: #table-3}
    {: caption="Table 3. {{site.data.keyword.keymanagementservicelong_notm}} keystore properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.keymanagementservicelong_notm}} keystore properties"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 2 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service instance ID on {{site.data.keyword.cloud_notm}}   | The unique identifier that is assigned to your  service instance. For more information, see [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).   |
    | API key on {{site.data.keyword.cloud_notm}}   **Tiffany: The naming patterns for KP and HPCS instances are different. Is there any specific reason?**      |  A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys). |
    {: #table-4}
    {: caption="Table 4. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} keystore properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.hscrypto}} keystore properties"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

7. Under **Summary**, view the summary of your Azure Key Vault and the total estimated cost.
8. After you confirm the keystore details, click  **Connect to keystore** to connect to the keystore.

You have successfully connected to the external keystore that you select. 

## What's next
{: #connect-external-keystores-next}

- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out how to update the connection to an external keystore, check out [Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).
  


