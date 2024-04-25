---

copyright:
  years: 2024, 2024
lastupdated: "2024-04-25"

keywords: Unified Key Orchestrator, UKO keystore, connect keystore, external keystore, KMS keystore, azure key vault

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Connecting to Azure Key Vault through private endpoint
{: #connect-azure-key-vault-private-endpoint}

You can use {{site.data.keyword.uko_full_notm}} to connect to Azure Key Vault through the private endpoint with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API. With establishing a private connection between {{site.data.keyword.uko_full_notm}} and Azure Key Vault, exposing your service to the public internet is no longer necessary.
{: shortdesc}

## Before you begin
{: #prerequisite}
{: ui}

Before you connect to an Azure Key Vault through the private endpoint, make sure you complete the following tasks:

- Set up user access before you use {{site.data.keyword.uko_full_notm}} to access keystores in third-party clouds.
- [Create a service principal](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external} in Azure.
- [Create an Azure Key Vault](https://learn.microsoft.com/en-us/azure/key-vault/general/quick-create-portal){: external}.
- [Set up access policy](https://docs.microsoft.com/en-us/azure/key-vault/general/assign-access-policy-portal){: external} for the Key Vault, granting access to that service principal.
- [Create a satellite connector](/docs/satellite?topic=satellite-create-connector).
- [Create a connector agent](/docs/satellite?topic=satellite-run-agent-locally).

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


## Step 1: Create a private endpoint in Azure portal
{: #step1-create-private-endpoint-ui}
{: ui}

To create a private endpoint in the Azure portal, complete the following steps:
1. Log in to your [Azure Tenant Portal](https://portal.azure.com/){: external} and select an Azure Key Vault. 

2. Under **Settings**, click **Networking**. 

3. To create the private endpoint, under **Private endpoint connections**, click **+ Create**.

4. Under **Basics**, enter the following information and click **Next: Resource**.
    |           Setting	      |               Value                       |
    |-----------------------------|-------------------------------|
    | Subscription	| Select the subscription.  |
    | Resource group	| Select the resource group. |
    | Name	 | Enter the instance name.   | 
    | Network Interface Name | The default network interface name is automatically generated. |
    | Region |	Select the region.  | 
    {: caption="Table 1. Private endpoint basics properties" caption-side="bottom"}

5. Under **Resource**, enter the following information and click **Next: Virtual Network**
    |           Setting	      |               Value                       |
    |-----------------------------|-------------------------------|
    | Connection method |	Select **Connect to an Azure resource in my directory**. |   
    | Subscription	| Select the subscription. |
    | Resource type |	Select the vault. | 
    | Resource   |	Select the key vault. |
    | Target     | Select the vault. |
    {: caption="Table 2. Private endpoint resource properties" caption-side="bottom"}

6. Under **Virtual Network**, enter the following information and click **Next: DNS**.
    |           Setting	      |               Value                       |
    |-----------------------------|-------------------------------|
    | Virtual network |	Select the network. |
    | Subnet | Select the subnet. |
    | Private IP configuration | Select Dynamically allocate IP address. |
    {: caption="Table 3. Private endpoint virtual network properties" caption-side="bottom"}

7. Under **DNS**, confirm the information and click **Next: Tags**.

8. Under **Tags**, click **Next: Review + create**.

9. After you confirm the information about creating a private endpoint, click **Create**.
    Now, you can verify the new private endpoint by clicking the key vault under the **Private endpoint connections**.  

10. To enable the private endpoint, go to **Firewalls and virtual network** and select **Disable public access**. 
    For more information, see [Create a private endpoint](https://learn.microsoft.com/en-us/azure/private-link/create-private-endpoint-portal?tabs=dynamic-ip#create-a-private-endpoint){: external}.

## Step 2: Create and manage connector endpoint
{: #step2-create-manage-endpoint-ui}
{: ui}

To connect {{site.data.keyword.cloud_notm}} to the Azure private endpoint created, you need to create a connector endpoint in IBM Satellite. To create a connector endpoint, complete the following steps: 
1. Log in to the [satellite UI](https://cloud.ibm.com/satellite/connectors){: external}, select the Connector that you want to use to create a connector endpoint.

2. From the Connector UI, click **User endpoints** and click **Create endpoint**.

3. Under **Resource details**, enter the following details and click **Next**. 

    |           Setting	      |               Value                       |
    |-----------------------------|-------------------------------|
    | Endpoint name |	Specify the endpoint name. |
    | Destination FQDN or IP  | Enter the fully qualified domain name. For example, `<Azure-key-vault-name>.privatelink.vaultcore.azure.net`, where `Azure-key-vault-name` is the key vault name you used in Step 1. |
    | Destination port | Enter the port that your destination resource listens for incoming requests, for example `443`.|
    {: caption="Table 4. Connector endpoint resource properties" caption-side="bottom"}

4. Under **Protocol**, select `TCP` as the source protocol and click **Next**.

5. Under **Access Control list**, do not select any rules and click **Next** to continue.

6. Under **Connection settings**, set an inactivity timeout, for example `60`.

7. Click **Create endpoint**.

Now, you have successfully created the connector endpoint and make sure to note the endpoint address.  


## Step 3: Connect Azure Key Vault to the UI
{: #step3-connect-azure-key-vault-ui}
{: ui}

To connect to an Azure Key Vault by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Keystores** from the navigation to view all the available keystores.
3. To connect to the Azure Key Vault, click **Add keystore**.
4. Under **Vault**, select a vault for the keystore for access control, and click **Next**. 

   If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Keystore type**, select **Azure Key Vault (Premium)** and click **Next**.

6. Under **Keystore properties**, specify the details:

    |           Property	      |               Description                       |
    |-----------------------------|-------------------------------|
    | Keystore name               | A unique, human-readable name for easy identification of your keystore, with 1–100 characters in length. The first character must be a letter (case-sensitive) or digit (0–9). The rest can also be symbols (.-_) or spaces. |
    | Description                 | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Service name on Azure       | The name must match the name of the Key Vault in Azure.   |
    | Resource group on Azure     | A logical construct that groups multiple resources. Obtain it from the Azure portal. |
    | Service principal client ID on Azure | Application ID that identifies the application of service principal.|
    | Service principal password on Azure | Only password-based authentication is supported for service principals.       |
    | Tenant ID on Azure          |  A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. Use Microsoft Entra ID for authenticating requests to the Key Vault.     |
    | Subscription ID on Azure    |  A GUID that uniquely identifies your subscription to use Azure services.    |
    | Private endpoint URL of TLS proxy | (Optional) Copy and paste the endpoint address in Step 2. For more information, see [Creating and managing Connector endpoints](/docs/satellite?topic=satellite-connector-create-endpoints).   | 
    {: caption="Table 5. Azure Key Vault properties" caption-side="bottom"}

    You cannot make further changes to identifying properties that are marked with a Lock icon after the keystore is connected.
    {: note}

7. Optionally, click **Test connection** to test the connection to the Azure Key Vault that you configure. When completed, click **Next** to continue.

    You can complete the subsequent steps even if the test fails. To adjust the connection settings in case of a connection failure, check and adjust the connection properties.
    {: note}

8. Under **Summary**, view the summary of your Azure Key Vault and the estimated additional cost.
9. After you confirm the keystore details, click **Add keystore**.

If you connect to the Azure Key Vault, a key that is named `EKMF-BYOK-KEK-FOR-IMPORT` is automatically created in the Azure Key Vault instance that you connect to. You can view the key from the Azure Key Vault instance UI. Don't delete this key. Otherwise, you will not be able to create and distribute managed keys to the Azure Key Vault instance. For more information, see [Why can't I distribute keys in Azure Key Vault](/docs/hs-crypto?topic=hs-crypto-troubleshoot-import-azure-key).
{: important}

You have successfully connected to the Azure Key Vault through private endpoint。

## Connecting to Azure Key Vault with API
{: #connect-azure-key-vault-api}
{: api}

To connect to an Azure Key Vault through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keystores in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Connect to an external keystore by making a `POST` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/keystores
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-keystore){: external}.

If you connect to the Azure Key Vault, a key that is named `EKMF-BYOK-KEK-FOR-IMPORT` is automatically created in the Azure Key Vault instance that you connect to. You can view the key from the Azure Key Vault instance UI. Don't delete this key. Otherwise, you will not be able to create and distribute managed keys to the Azure Key Vault instance. For more information, see [Why can't I distribute keys in Azure Key Vault](/docs/hs-crypto?topic=hs-crypto-troubleshoot-import-azure-key).
{: important}


## What's next
{: #connect-azure-key-vault-private-endpoint-next}

- To watch a use case video on using {{site.data.keyword.uko_full_notm}} to manage Azure Key Vault, see [Managing compliance of a Microsoft Office 365 environment using Hyper Protect Crypto Services with Unified Key Orchestrator](https://mediacenter.ibm.com/media/1_1pzzhrb8){: external}.

- To find out how to update the connection to an external keystore, check out [Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection).

- To find out how to disconnect from an external keystore, check out [Disconnecting from external keystores](/docs/hs-crypto?topic=hs-crypto-disconnect-external-keystores).

