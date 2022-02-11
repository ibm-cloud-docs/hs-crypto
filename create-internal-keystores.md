---

copyright:
  years: 2022
lastupdated: "2022-02-11"

keywords: Unified Key Orchestrator, UKO keystore, create keystore, internal keystore， KMS keystore

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


# Creating internal keystores
{: #create-internal-keystores}

An internal keystore is a repository that stores the cryptographic keys within your service instance. You can use {{site.data.keyword.uko_full_notm}} to create internal keystores through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

You can create up to five free internal keystores to manage your keys. If you need additional keystores for cross-region key distribution or specified access permissions, you are charged. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing). Other currencies are applied based on the region the service instance is provisioned in.
{: note}

## Creating internal keystores through the UI
{: #create-internal-keystores-ui}



### Creating internal KMS keystores
{: #create-internal-kms}


To create an internal KMS keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. To create a keystore, click **Add keystore**.
4. Under **Vault**, select a vault for the keystore for access control, and click **Next**. 

   If you want to assign the keystore to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

5. Under **Keystore type**, select **KMS Keystore** and click **Next**.
6. Under **Keystore properties**, enter a name in **Keystore name**. The keystore name can be of 2 to 100 characters. Optionally, you can add an extended description to your keystore in the **Description** section. And then, click **Next**.
7. Under **Summary**, you can view the summary of the keystore that you create, including the keystore type, the assigned vault, and general properties. 
8. After you confirm the keystore details, click **Create keystore** to create the keystore.

You have successfully created an internal KMS keystore.







## Creating internal keystores with the API
{: #create-internal-keystores-api}






## What's next
{: #create-internal-keystores-next}

- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out instructions on editing an internal keystore, check out [Editing internal keystores](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores).

- To find out how to delete an internal keystore, check out [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores).


