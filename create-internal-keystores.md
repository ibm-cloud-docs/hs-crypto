---

copyright:
  years: 2021
lastupdated: "2021-12-09"

keywords: Unified Key Orchestrator, keystore, create keystore, key management, internal keystore

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

You can use {{site.data.keyword.uko_full_notm}} to create internal keystores in the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}


## Creating internal keystores in the UI
{: #create-internal-keystores-ui}

Complete the following steps to create an internal keystore in the UI.


### Creating an internal KMS keystore
{: #create-internal-kms}

1. [Log in to the {{site.data.keyword.uko_full_notm}} service instance](https://cloud.ibm.com/login){: external}.
2. In the left navigation panel, go to **Vaults** &gt; **Target keystores** to view all the available keystores.
3. To create a new keystore, click **Add keystore.**
4. Under **Vault,** assign the keystore to a vault for access control. You can also click **Create vault** to create a new vault.
5. Under **Keystore type,** select **Internal KMS**.
6. Under **Keystore properties,** enter the **Keystore name**. Optionally, you can add an extended description to your keystore in the **Keystore description** section.
7. View the summary of your KMS keystore.
8. Click **Create keystore** to confirm.

An internal keystore is a repository that stores the cryptographic keys within your service instance. You can create up to five free KMS keystores to manage your keys with the Keep Your Own Key (KYOK) support. If additional keystores are needed, you are charged $60 per calendar month for any additional keystore. 
{: note}



### Creating an EP11 keystore
{: #create-ep11}





## Creating internal keystores with the API
{: #create-internal-keystores-api}






## What's next
{: #create-internal-keystores-next}

- To find out how to manage external keystores, check out [Managing external keystores](/docs/hs-crypto?topic=hs-crypto-manage-external-keystore).
  


