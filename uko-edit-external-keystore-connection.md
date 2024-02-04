---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-01"

keywords: Unified Key Orchestrator, key management, UKO keystore, edit keystore, external keystore, KMS keystore

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Editing connection to external keystores
{: #edit-external-keystore-connection}

You can use {{site.data.keyword.uko_full_notm}} to edit connection to external keystores with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

You can edit the connection to keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault, Amazon Web Services (AWS) Key Management Service (KMS), and Google Cloud KMS.

## Editing connection to external keystores with the {{site.data.keyword.cloud_notm}} console
{: #edit-external-keystore-connection-ui}
{: ui}

You can only change the keystore name and connection properties one by one.
{: tip}

To edit the connection to an external keystore by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Keystores** from the navigation to view all the available keystores.
3. Click the external keystore that you want to edit. The Details side panel is displayed.
4. Click **Edit** in each property card to update keystore properties.

    Because the keystore connection is already established, you cannot make changes to identifying properties that are marked with a Lock icon.
    {: note}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1–100 characters in length. The first character must be a letter (case-sensitive) or digit (0–9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Region on AWS               | Read only. The geographical location where the AWS keystore is located in. You cannot edit this property after the keystore is connected.    |
    | Access key ID on AWS        | All requests to AWS KMS must be signed by using an access key ID and a secret access key. For more information, see [Understanding and getting your AWS credentials](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html).   |
    | Secret access key on AWS    | All requests to AWS KMS must be signed by using an access key ID and a secret access key. The secret access key is available for download only when you create it.    |
    {: #table-1}
    {: caption="Table 1. AWS Key Management Service properties" caption-side="bottom"}
    {: tab-title="AWS keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    
    
    
    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1–100 characters in length. The first character must be a letter (case-sensitive) or digit (0–9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       | Read only. The name must match the name of the Key Vault in Azure. You cannot edit this property after the keystore is connected.   |
    | Resource group name on Azure     | Read only. A logical construct that groups multiple resources together. Obtain it from the Azure portal. You cannot edit this property after the keystore is connected. |
    | Service principal password on Azure | Only password based authentication is supported for service principals.       |
    | Service principal client ID on Azure | Application ID that identifies the application of service principal. | 
    | Subscription ID on Azure    |  Read only. A GUID that uniquely identifies your subscription to use Azure services. You cannot edit this property after the keystore is connected.    |
    | Tenant ID on Azure          |  Read only. A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. Use Microsoft Entra ID for authenticating requests to the key vault. You cannot edit this property after the keystore is connected.    |
    {: #table-2}
    {: caption="Table 2. Azure Key Vault properties" caption-side="bottom"}
    {: tab-title="Azure Key Vault"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}
    

    |           Property	      |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1–100 characters in length. The first character must be a letter (case-sensitive) or digit (0–9). The rest can also be symbols (.-_) or spaces. |
    | Keystore description        | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Upload JSON key file        | The private key file that is downloaded from your service account on Google Cloud in step 2 of [Setting up required user access in Google Cloud KMS](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores#connect-external-keystores-access-google-cloud). The file type must be `.json` and the maximum file size is 4 KB. |
    | Project on Google Cloud     | Read only. The name of your Google Cloud project. It is automatically extracted from the JSON key file that you upload. You cannot edit this property after the keystore is connected.    |
    | Location on Google Cloud    | The geographical region where you want to store your Google Cloud KMS resources. You cannot edit this property after the keystore is connected.  For more details about the location, see [Google Cloud KMS locations](https://cloud.google.com/kms/docs/locations){: external}.     |
    | Key ring on Google Cloud | A human-readable name of the key ring that organizes your keys. The name must be unique within a location. You cannot edit this property after the keystore is connected.  For more information about key rings, see [Key rings](https://cloud.google.com/kms/docs/resource-hierarchy#key_rings){: external}.  |
    | Private key ID on Google Cloud | Read only. The ID of the public/private RSA key pair in Google. It is used for establishing a secure connection to Google Cloud Platform. It is automatically extracted from the JSON key file that you upload. You cannot edit this property after the keystore is connected. |
    {: #table-3}
    {: caption="Table 3. Google Cloud KMS keystore properties" caption-side="bottom"}
    {: tab-title="Google Cloud KMS keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1–100 characters in length. The first character must be a letter (case-sensitive) or digit (0–9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.keymanagementserviceshort}} API endpoint  | Read only. The service endpoint of your {{site.data.keyword.keymanagementserviceshort}} instance in the format of `https://<region>.kms.cloud.ibm.com`. You cannot edit this property after the keystore is connected. For more information, see [Regions and endpoints](/docs/key-protect?topic=key-protect-regions).  |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  Read only. The endpoint of IAM, which is `https://iam.cloud.ibm.com`. You cannot edit this property after the keystore is connected.   |
    | Service instance ID on {{site.data.keyword.cloud_notm}}   | Read only. The unique identifier that is assigned to your {{site.data.keyword.keymanagementserviceshort}} service instance. You cannot edit this property after the keystore is connected. For more information, see [Retrieving your instance ID and cloud resource name](/docs/key-protect?topic=key-protect-retrieve-instance-ID).  |
    | Service ID API key          | A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys). |
    {: #table-4}
    {: caption="Table 4. IBM {{site.data.keyword.keymanagementserviceshort}} keystore properties" caption-side="bottom"}
    {: tab-title="IBM {{site.data.keyword.keymanagementserviceshort}} keystore"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

    |           Property	        |                         Description                       |
    |-----------------------------|-----------------------------------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1–100 characters in length. The first character must be a letter (case-sensitive) or digit (0–9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | {{site.data.keyword.hscrypto}} API endpoint  | Read only. The service endpoint of your {{site.data.keyword.hscrypto}} instance in the format of `https://uko.<region>.hs-crypto.cloud.ibm.com:<port>`. You can get the `<region>` and `<port>` in your provisioned service instance UI dashboard through **Overview** &gt; **Connect** &gt; **{{site.data.keyword.uko_full_notm}} endpoint URL**. You cannot edit this property after the keystore is connected.  |
    | {{site.data.keyword.cloud_notm}} Identity and Access Management endpoint  |  Read only. The endpoint of IAM, which is `https://iam.cloud.ibm.com`. You cannot edit this property after the keystore is connected.  |
    | Service instance ID on {{site.data.keyword.cloud_notm}}  | Read only. The unique identifier that is assigned to your service instance. You cannot edit this property after the keystore is connected. For more information, see [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).  |
    | Service ID API key          | A unique code that is passed to an API to identify the calling application. For more information, see [Managing service ID API keys](/docs/account?topic=account-serviceidapikeys).  |
    {: #table-5}
    {: caption="Table 5. {{site.data.keyword.cloud_notm}} KMS keystore properties" caption-side="bottom"}
    {: tab-title="{{site.data.keyword.cloud_notm}} KMS keystore in another instance"}
    {: tab-group="External keystore properties"}
    {: class="comparison-tab-table"}

5. Click **Save** to save the changes.

You can search for a specific keystore by using the search bar, or filter keystores based on your needs by clicking the **Filter** icon ![Filter icon](../icons/filter.svg "Filter") in the **Keystores** table.
{: tip}



## Editing connection to external keystores with the API
{: #edit-external-keystore-connection-api}
{: api}

To edit the connection to an external keystore through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keystores in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Edit the connection to an external keystore by making a `PATCH` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/keystores/<id>
    ```
    {: codeblock}

    Replace `<id>` with the ID of your keystore.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#update-keystore){: external}.



## What's next
{: #edit-external-keystore-connection-next}

- To find out how to connect to an external keystore, check out [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).


