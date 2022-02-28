---

copyright:
  years: 2022
lastupdated: "2022-02-28"

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

You can use {{site.data.keyword.uko_full_notm}} to edit connection to external keystores through the user interface (UI).
{: shortdesc}

You can edit the connection to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS).

## Editing connection to external keystores through the UI
{: #edit-external-keystore-connection-ui}

You can only change the keystore name and connection properties one by one.
{: tip}

To edit the connection to an external keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the external keystore that you want to edit. The Details side panel is displayed.
4. Click **Edit** in each property card to update keystore properties.
   
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       | The name must match the name of the Key Vault in Azure.   |
    | Resource group name on Azure     | A logical construct that groups multiple resources together. Obtain it from the Azure portal. |
    | Location on Azure           | The geographical location where the Key Vault is located in.   |
    | Environment on Azure        | The Azure environment to authenticate with.      |
    | Service principal client ID on Azure | Application ID that identifies the application of service principal. |    
    | Service principal password on Azure | Only password based authentication is supported for service principals.       |
    | Tenant ID on Azure          |  A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. Use Azure Active Directory tenant ID for authenticating requests to the key vault.     |
    | Subscription ID on Azure    |  A GUID that uniquely identifies your subscription to use Azure services.    |
    {: #table-1}
    {: caption="Table 1. Azure Key Vault properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}
    {: caption="Table 1. Azure Key Vault properties" caption-side="bottom"}    

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               | The geographical location where the AWS keystore is located in.    |
    | Access key ID on AWS        | All requests to AWS KMS must be signed by using an access key ID and a secret access key. For more information, see [Understanding and getting your AWS credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html).   |
    | Secret access key on AWS    | All requests to AWS KMS must be signed by using an access key ID and a secret access key. The secret access key is available for download only when you create it.    |
    {: #table-2}
    {: caption="Table 2. AWS Key Management Service properties" caption-side="bottom"}
    {: tab-title="AWS keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.keymanagementserviceshort}} API endpoint  | The service endpoint of your {{site.data.keyword.keymanagementserviceshort}} instance in the format of `https://<region>.kms.cloud.ibm.com`. For more information, see [Regions and endpoints](/docs/key-protect?topic=key-protect-regions).  |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  The endpoint of IAM, which is `https://iam.cloud.ibm.com`.  |
    | Service instance ID on {{site.data.keyword.cloud_notm}}   | The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. For more information, see [Retrieving your instance ID and cloud resource name](/docs/key-protect?topic=key-protect-retrieve-instance-ID).  |
    | Service ID API key          | A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys). |
    {: #table-3}
    {: caption="Table 3. {{site.data.keyword.keymanagementserviceshort}} keystore properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.keymanagementserviceshort}} keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.hscrypto}} API endpoint  | The service endpoint of your {{site.data.keyword.hscrypto}} instance in the format of `https://uko.<region>.hs-crypto.cloud.ibm.com:<port>`. You can get the `<region>` and `<port>` in your provisioned service instance UI dashboard through **Overview** &gt; **Connect** &gt; **{{site.data.keyword.uko_full_notm}} endpoint URL**.  |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  The endpoint of IAM, which is `https://iam.cloud.ibm.com`.  |
    | Service instance ID on {{site.data.keyword.cloud_notm}}  | The unique identifier that is assigned to your service instance. For more information, see [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).  |
    | Service ID API key          | A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).  |
    {: #table-4}
    {: caption="Table 4. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} KMS keystore properties" caption-side="bottom"}
    {: tab-title="KMS keystore in another instance"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}


5. Click **Save** to save the changes.

You can search for a specific keystore by using the search bar, or filter keystores based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Target keystores** table.
{: tip}



## What's next
{: #edit-external-keystore-connection-next}

- To find out how to connect to an external keystore, check out [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).

- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

