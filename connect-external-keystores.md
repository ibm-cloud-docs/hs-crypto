---

copyright:
  years: 2022
lastupdated: "2022-04-21"

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}


# Connecting to external keystores
{: #connect-external-keystores}

You can use {{site.data.keyword.uko_full_notm}} to connect to external keystores with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

Before you connect to an external keystore, keep in mind the following considerations:

- You can connect to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS). 
- You can connect to one external keystore at no initial cost, regardless of the type. You are charged for additional external keystores. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Other currencies are applied based on the region the service instance is provisioned in.
- A managed key can be used for encryption and decryption only after you install it in at least one target keystore. 
- A target keystore can be assigned to only one vault.

## Setting up required user access in external keystores
{: #connect-external-keystores-access}

You need to set up user access before you use {{site.data.keyword.uko_full_notm}} to access keystores in third-party cloud.

### Setting up required user access in Azure Key Vault
{: #connect-external-keystores-access-azure}

To set up user access to Azure Key Vault, complete the following steps:

1. [Create a service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} in Azure.
   
2. [Set up access policy](https://docs.microsoft.com/en-us/azure/key-vault/general/assign-access-policy-portal){: external} for the Key Vault, granting access to that service principal.

{{site.data.keyword.uko_full_notm}} requires the following access to be able to manage keys in Azure Key Vault:

- `create`
- `import`
- `update`
- `list`
- `delete`
- `get`
- `recover`
- `purge`
- `backup`
- `restore`

For more information, check out [Assign a Key Vault access policy](https://docs.microsoft.com/en-us/azure/key-vault/general/assign-access-policy?tabs=azure-portal){: external}.


### Setting up required user access in AWS keystore
{: #connect-external-keystores-access-aws}

{{site.data.keyword.uko_full_notm}} requires the following access to be able to manage keys in AWS KMS:

- `ListKeys`
- `CreateKey`
- `GetParametersForImport`
- `ImportKeyMaterial`
- `DeleteAlias`
- `CreateAlias`
- `TagResource`
- `UntagResource`
- `DescribeKey`
- `DeleteImportedKeyMaterial`
- `ListResourceTags`
- `ListAliases`
- `ScheduleKeyDeletion`

For more information, check out [AWS KMS permissions](https://docs.aws.amazon.com/kms/latest/developerguide/kms-api-permissions-reference.html){: external}.

## Connecting to external keystores with the {{site.data.keyword.cloud_notm}} console
{: #connect-external-keystores-ui}
{: ui}

To connect to an external keystore by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. To connect to an external keystore, click **Add keystore**.
4. Under **Vault**, select a vault for the keystore for access control, and click **Next**. 

   If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Keystore type**, select one of the following types and click **Next**:

    - **Azure Key Vault (Premium)**
    - **AWS keystore**
    - **{{site.data.keyword.keymanagementserviceshort}}**
    - **KMS keystore in another instance**

6. Under **Keystore properties**, specify the details of based on the keystore type that you want to connect to, and click **Next** to continue when you are done.
   
    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       | The name must match the name of the Key Vault in Azure.   |
    | Resource group name on Azure     | A logical construct that groups multiple resources. Obtain it from the Azure portal. |
    | Location on Azure           | The geographical location where the Key Vault is located in.   |
    | Environment on Azure        | The Azure environment to authenticate with.               |
    | Service principal client ID on Azure | Application ID that identifies the application of service principal. |    
    | Service principal password on Azure | Only password based authentication is supported for service principals.       |
    | Tenant ID on Azure          |  A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. Use Azure Active Directory tenant ID for authenticating requests to the Key Vault.     |
    | Subscription ID on Azure    |  A GUID that uniquely identifies your subscription to use Azure services.    |
    {: #table-1}
    {: caption="Table 1. Azure Key Vault properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               | The geographical location where the AWS keystore is located in.    |
    | Access key ID on AWS        | All requests to AWS KMS must be signed by using an access key ID and a secret access key. For more information, see [Understanding and getting your AWS credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html).    |
    | Secret access key on AWS    | All requests to AWS KMS must be signed by using an access key ID and a secret access key. The secret access key is available for download only when you create it.     |
    {: #table-2}
    {: caption="Table 2. AWS Key Management Service properties" caption-side="bottom"}
    {: tab-title="AWS keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.keymanagementserviceshort}} API endpoint  | The service endpoint of your {{site.data.keyword.keymanagementserviceshort}} instance in the format of `https://<region>.kms.cloud.ibm.com`. For more information, see [Regions and endpoints](/docs/key-protect?topic=key-protect-regions). |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  The endpoint of IAM, which is `https://iam.cloud.ibm.com`.  |
    | Service instance ID on {{site.data.keyword.cloud_notm}}   | The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. For more information, see [Retrieving your instance ID and cloud resource name](/docs/key-protect?topic=key-protect-retrieve-instance-ID).  |
    | Service ID API key          | A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys). |
    {: #table-3}
    {: caption="Table 3. {{site.data.keyword.keymanagementserviceshort}} keystore properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.keymanagementserviceshort}} keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.hscrypto}} API endpoint  | The service endpoint of your {{site.data.keyword.hscrypto}} instance in the format of `https://uko.<region>.hs-crypto.cloud.ibm.com:<port>`. You can get the `<region>` and `<port>` in your provisioned service instance UI dashboard through **Overview** &gt; **Connect** &gt; **{{site.data.keyword.uko_full_notm}} endpoint URL**.   |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  The endpoint of IAM, which is `https://iam.cloud.ibm.com`.  |
    | Service instance ID on {{site.data.keyword.cloud_notm}}   | The unique identifier that is assigned to your service instance. For more information, see [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).   |
    | Service ID API key          |  A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys). |
    {: #table-4}
    {: caption="Table 4. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} KMS keystore properties" caption-side="bottom"}
    {: tab-title="KMS keystore in another instance"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

7. Under **Summary**, view the summary of your Azure Key Vault and the total estimated cost.
8. After you confirm the keystore details, click  **Connect to keystore** to connect to the keystore.

You have successfully connected to the external keystore that you select. 

## Connecting to external keystores with the API
{: #connect-external-keystores-api}
{: api}

To connect to an external keystore through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Connect to an external keystore by making a `POST` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/keystores
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-keystore){: external}.

## What's next
{: #connect-external-keystores-next}

- To find out how to install an existing key to a keystore, check out [Setting target keystores for existing keys](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out how to update the connection to an external keystore, check out [Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).
  


