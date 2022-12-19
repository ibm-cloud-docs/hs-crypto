---

copyright:
  years: 2022
lastupdated: "2022-12-19"

keywords: Unified Key Orchestrator, UKO keystore, connect keystore, external keystore, KMS keystore

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
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

- You can connect to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault, Amazon Web Services (AWS) Key Management Service (KMS), and Google Cloud KMS.
- You can connect to one external keystore at no initial cost, regardless of the type. You are charged for additional external keystores. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Other currencies are applied based on the region the service instance is provisioned in.
- A managed key can be used for encryption and decryption only after you activate it in at least one target keystore. 
- A target keystore can be assigned to only one vault.

## Setting up required user access in external keystores
{: #connect-external-keystores-access}

You need to set up user access before you use {{site.data.keyword.uko_full_notm}} to access keystores in third-party clouds.

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



### Setting up required user access in Google Cloud KMS
{: #connect-external-keystores-access-google-cloud}

To set up user access to Google Cloud KMS, complete the following steps:

1. [Create a service account](https://cloud.google.com/iam/docs/creating-managing-service-accounts#creating){: external} in your Google Cloud project.

2. [Create a service account key](https://cloud.google.com/iam/docs/creating-managing-service-account-keys#creating){: external} to establish the identity of the service account. Select `JSON` for the key type. The private JSON key file will be downloaded directly on your workstation. You need to provide the JSON key file when you use the {{site.data.keyword.uko_full_notm}} to connect to your Google Cloud KMS keystore.
   
3. Create a [principal](https://cloud.google.com/iam/docs/overview#concepts_related_identity){: external} and associate it with the service account, and [assign the required IAM roles to the principal](https://cloud.google.com/iam/docs/granting-changing-revoking-access#grant-single-role){: external}. {{site.data.keyword.uko_full_notm}} requires the following IAM roles to be able to manage keys in Google Cloud KMS:

    - `Cloud KMS Admin`
    - `Cloud KMS Crypto Operator`


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

    - **AWS keystore**: Create a keystore that can store AWS KMS keys.
    - **Azure Key Vault (Premium)**: Create a keystore that can store Azure Key Vault keys.
    - **Google Cloud KMS keystore**: Create a keystore that can store Google Cloud KMS keys.
    - **{{site.data.keyword.keymanagementserviceshort}}**: Create a keystore that can store {{site.data.keyword.keymanagementserviceshort}} keys.
    - **{{site.data.keyword.cloud_notm}} KMS keystore in another instance**: Create a keystore that can store KMS keys in another {{site.data.keyword.hscrypto}} instance.

    You can change the currency displayed by selecting your country or location.
    {: tip}

6. Under **Keystore properties**, specify the details of based on the keystore type that you want to connect to.

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. The first character must be a letter (case-sensitive) or digit (0 - 9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               | The geographical location where the AWS keystore is located in.    |
    | Access key ID on AWS        | All requests to AWS KMS must be signed by using an access key ID and a secret access key. For more information, see [Understanding and getting your AWS credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html).    |
    | Secret access key on AWS    | All requests to AWS KMS must be signed by using an access key ID and a secret access key. The secret access key is available for download only when you create it.     |
    {: #table-1}
    {: caption="Table 1. AWS Key Management Service properties" caption-side="bottom"}
    {: tab-title="AWS keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}
   
    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. The first character must be a letter (case-sensitive) or digit (0 - 9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       | The name must match the name of the Key Vault in Azure.   |
    | Resource group name on Azure     | A logical construct that groups multiple resources. Obtain it from the Azure portal. |
    | Location on Azure           | The geographical location where the Key Vault is located in.   |
    | Environment on Azure        | The Azure environment to authenticate with.               |
    | Service principal client ID on Azure | Application ID that identifies the application of service principal. |    
    | Service principal password on Azure | Only password based authentication is supported for service principals.       |
    | Tenant ID on Azure          |  A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. Use Azure Active Directory tenant ID for authenticating requests to the Key Vault.     |
    | Subscription ID on Azure    |  A GUID that uniquely identifies your subscription to use Azure services.    |
    {: #table-2}
    {: caption="Table 2. Azure Key Vault properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}


    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. The first character must be a letter (case-sensitive) or digit (0 - 9). The rest can also be symbols (.-_) or spaces. |
    | Keystore description        | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Upload JSON key file        | The private key file that is downloaded from your service account on Google Cloud in step 2 of [Setting up required user access in Google Cloud KMS](#connect-external-keystores-access-google-cloud). The file type must be `.json` and the maximum file size is 4 KB. |
    | Project on Google Cloud     | Read only. The name of your Google Cloud project. It is automatically extracted from the JSON key file that you upload.  |
    | Location on Google Cloud    | The geographical region where you want to store your Google Cloud KMS resources. For more details about the location, see [Google Cloud KMS locations](https://cloud.google.com/kms/docs/locations){: external}.     |
    | Key ring on Google Cloud | A human-readable name of the key ring that organizes your keys. The name must be unique within a location. For more information about key rings, see [Key rings](https://cloud.google.com/kms/docs/resource-hierarchy#key_rings){: external}.  |
    | Private key ID on Google Cloud | Read only. The ID of the public/private RSA key pair in Google. It is used for establishing a secure connection to Google Cloud Platform. It is automatically extracted from the JSON key file that you upload. |
    {: #table-3}
    {: caption="Table 3. Google Cloud KMS keystore properties" caption-side="bottom"}
    {: tab-title="Google Cloud KMS keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    

    

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. The first character must be a letter (case-sensitive) or digit (0 - 9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service instance ID on {{site.data.keyword.cloud_notm}}   | The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. For more information, see [Retrieving your instance ID and cloud resource name](/docs/key-protect?topic=key-protect-retrieve-instance-ID).  |
    | Key ring ID on {{site.data.keyword.cloud_notm}}   | The unique identifier of the key ring in the {{site.data.keyword.keymanagementserviceshort}} instance that you want to connect to. For more information, see [Grouping keys together using key rings](/docs/key-protect?topic=key-protect-grouping-keys). If you are not sure which key ring to connect to, specify `default` to connect to the default key ring. |
    | {{site.data.keyword.keymanagementserviceshort}} API endpoint  | The service endpoint of your {{site.data.keyword.keymanagementserviceshort}} instance in the format of `https://<region>.kms.cloud.ibm.com`. For more information, see [Regions and endpoints](/docs/key-protect?topic=key-protect-regions). |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  The endpoint of IAM, which is `https://iam.cloud.ibm.com`.  |
    | Service ID API key          | A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys). |
    {: #table-4}
    {: caption="Table 4. {{site.data.keyword.keymanagementserviceshort}} keystore properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.keymanagementserviceshort}} keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}
    
    
    
    
    
    

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1 - 100 characters in length. The first character must be a letter (case-sensitive) or digit (0 - 9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service instance ID on {{site.data.keyword.cloud_notm}}   | The unique identifier that is assigned to your service instance. For more information, see [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).   |
    | Key ring ID on {{site.data.keyword.cloud_notm}}   | The unique identifier of the key ring in the {{site.data.keyword.hscrypto}} instance Standard Plan that you want to connect to. For more information, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings). If you are not sure which key ring to connect to, specify `default` to connect to the default key ring. |
    | Key management endpoint  | The service endpoint of your {{site.data.keyword.hscrypto}} instance in the format of `https://api.<region>.hs-crypto.cloud.ibm.com:<port>`. You can get the `<region>` and `<port>` in your provisioned service instance UI dashboard through **Overview** &gt; **Connect** &gt; Key managment endpoint URL**.   |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  The endpoint of IAM, which is `https://iam.cloud.ibm.com`.  |
    | Service ID API key          |  A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys). |
    {: #table-5}
    {: caption="Table 5. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} KMS keystore properties" caption-side="bottom"}
    {: tab-title="KMS keystore in another instance"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}
    
    

    You cannot make further changes to identifying properties that are marked with a Lock icon after the keystore is connected.
    {: note}

7. Optionally, click **Test connection** to test the connection to the external keystore that you configure. When completed, click **Next** to continue.

    **Test connection** is an optional step. You can complete the subsequent steps even if the test fails. To adjust the connection settings in case of a connection failure, check and adjust the connection properties.
    {: tip}
8. Under **Summary**, view the summary of your Azure Key Vault and the total estimated cost.
9. After you confirm the keystore details, click  **Connect to keystore** to connect to the keystore.

If you connect to an external keystore of type Azure Key Vault, a key named `EKMF-BYOK-KEK-FOR-IMPORT` is automatically created in the Azure Azure Key Vault instance that you connect to. You can view the key from the Azure Key Vault instance UI. Don't delete this key. Otherwise, you will not be able to create and assign managed keys to the Azure Key Vault instance. For more information, see [Why can't I assign keys in Azure Key Vault](/docs/hs-crypto?topic=hs-crypto-troubleshoot-import-azure-key).
{: important}

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

If you connect to an external keystore of type Azure Key Vault, a key named `EKMF-BYOK-KEK-FOR-IMPORT` is automatically created in the Azure Azure Key Vault instance that you connect to. You can view the key from the Azure Key Vault instance UI. Don't delete this key. Otherwise, you will not be able to create and assign managed keys to the Azure Key Vault instance. For more information, see [Why can't I assign keys in Azure Key Vault](/docs/hs-crypto?topic=hs-crypto-troubleshoot-import-azure-key).
{: important}


## What's next
{: #connect-external-keystores-next}

- To watch a use case video on using {{site.data.keyword.uko_full_notm}} to manage Azure Key Vault, see [Managing compliance of a Microsoft Office 365 environment using Hyper Protect Crypto Services with Unified Key Orchestrator](https://mediacenter.ibm.com/media/1_1pzzhrb8){: external}.

- To watch a use case video on using {{site.data.keyword.uko_full_notm}} to manage AWS Key Management Service, see [Securely managing AWS S3 encryption keys using Hyper Protect Crypto Services with Unified Key Orchestrator](https://mediacenter.ibm.com/media/1_1a6c6vub){: external}.

- To find out how to activate an existing key in a keystore, check out [Setting target keystores for existing keys](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out how to update the connection to an external keystore, check out [Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).
  


