---

copyright:
  years: 2022, 2024
lastupdated: "2024-07-01"

keywords: Unified Key Orchestrator, UKO keystore, create keystore, internal keystore， KMS keystore

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}






# Creating internal KMS keystores
{: #create-internal-keystores}

An internal keystore is a repository that stores the cryptographic keys within your service instance. You can use {{site.data.keyword.uko_full_notm}} to create internal KMS keystores with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

Before you create an internal KMS keystore, keep in mind the following considerations:

- You can create up to five internal KMS keystores to manage your keys for free. The maximum number of internal KMS keystores for a service instance is 50. 
- To enable cross-region key distribution or specified access permissions, you might want to create additional keystores. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Other currencies are applied based on the region that the service instance is provisioned in.
- A managed key can be used for encryption and decryption only after you activate it in at least one keystore. 
- A keystore can be assigned to only one vault.

## Creating internal KMS keystores with the UI
{: #create-internal-keystores-ui}
{: ui}



To create an internal KMS keystore by using the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Keystores** from the navigation to view all the available keystores.
3. To create a keystore, click **Add keystore**.

   

4. Under **Vault**, select a vault for the keystore for access control, and click **Next**. 

   If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Keystore type**, select **IBM Cloud KMS Keystore** and click **Next**.
    You can change the currency that is displayed by selecting your country or location.
    {: tip}
    
6. Under **Keystore properties**, enter a name in **Keystore name**. Optionally, you can add an extended description to your keystore in the **Description** section. And then, click **Next**.
  
    The keystore name must be of 1 to 100 characters in length. The first character must be a letter (case-sensitive) or digit (0-9). The rest can also be symbols (.-_) or spaces. The description can be up to 200 characters in length.

7. Under **Summary**, you can view the summary of the keystore that you create, including the keystore type, the assigned vault, and general properties. 
8. After you confirm the keystore details, click **Create keystore** to create the keystore.

You have successfully created an internal KMS keystore.



## Creating internal KMS keystores with the API
{: #create-internal-keystores-api}
{: api}

To create an internal keystore through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keystores in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Create an internal keystore by making a `POST` call to the following endpoint.

     

    ```
    https://<instance_ID>.uko.<region>.hs-crypto.appdomain.cloud/api/v4/keystores
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-keystore){: external}.





## What's next
{: #create-internal-keystores-next}

- To find out instructions on editing an internal keystore, check out [Editing internal keystores](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores).

- To find out how to delete an internal keystore, check out [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores).


