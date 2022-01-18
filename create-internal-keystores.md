---

copyright:
  years: 2022
lastupdated: "2022-01-18"

keywords: Unified Key Orchestrator, keystore, create keystore, internal keystore

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

You can use {{site.data.keyword.uko_full_notm}} to create internal keystores through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

An internal keystore is a repository that stores the cryptographic keys within your service instance. You can create up to five free internal keystores to manage your keys with the Keep Your Own Key (KYOK) support. If additional keystores are needed, you are charged $225 per calendar month for any additional keystore. 
{: note}

## Creating internal keystores through the UI
{: #create-internal-keystores-ui}

You can create both internal KMS keystores and EP11 keystores through the UI.

### Creating internal KMS keystores
{: #create-internal-kms}

To create an internal KMS keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** on the left navigation pane to view all the available keystores.
3. To create a new keystore, click **Add keystore.**
4. Under **Vault,** assign the keystore to a vault for access control. You can also click **Create vault** to create a new vault. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults){: external}.
5. Under **Keystore type,** select **Internal KMS**.
6. Under **Keystore properties,** enter a **Keystore name** of 2 to 100 characters. Optionally, you can add an extended description to your keystore in the **Description** section.
7. View the summary of your KMS keystore, then click **Create keystore** to confirm.



### Creating EP11 keystores
{: #create-ep11}





## Creating internal keystores with the API
{: #create-internal-keystores-api}






## What's next
{: #create-internal-keystores-next}

- To find out how to install an existing key to a keystore, check out [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

- To find out instructions on editing an internal keystore, check out [Editing internal keystores](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores).

- To find out how to delete an internal keystore, check out [Deleting internal keystores](/docs/hs-crypto?topic=hs-crypto-delete-internal-keystores).


