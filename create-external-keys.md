---

copyright:
  years: 2022
lastupdated: "2022-01-20"

keywords: Unified Key Orchestrator, create key, key management, kms key, UKO key

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


# Creating and storing external keys
{: #create-external-keys}

You can use {{site.data.keyword.uko_full_notm}} to create keys for external keystores through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

To protect your privacy, do not store your personal data as metadata for your key.
{: important}

## Creating external keys through the UI
{: #create-external-keys-ui}

To create an external key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. To create a key, click **Add key**.
4. Under **Vault**, select a vault for the key for access control, and click **Next**. 

  If you want to assign the key to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).
  
5. Under **General**, select **AWS Key Management Service**, **Azure Key Vault**, or **IBM Key Protect**, depending on which type of external keystore you want to install the key in. And then, click **Next**. 
6. Under **Key properties**, specify the following details of the key. Click **Next** to continue when you are done.

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key, with 2 - 100 characters in length. |
    | Description          | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | _Pre-active_ keys are not to be installed in target keystores until they are activated. _Active_ keys are to be automatically installed in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external} |
    | Activation date      | (Optional) Set the date when the _Pre-active_ key gets activated. You can also manually activate the key later. |
    | Deactivation date    | (Optional) Set the date when the key gets expired. After the expiration date, the key moves into the _Deactivated_ state.  |
    | Key tags             | (Optional) Add pairs of names and values to mark your key.  |
    {: caption="Table 1. Key properties" caption-side="bottom"}

7. Under **Target keystores**, you can select one or multiple target keystores to install the key in. You can also install the key later by following instructions in [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

    You can use the key for encryption or decryption only after it is installed in at least one keystore.
    {: important}

    Installing a key in multiple keystores enables redundancy. You can install a key in one internal keystore and at least one external keystore as a backup.
    {: tip} 
8. Under **Summary**, view the summary of your key, and then click **Create key** to confirm.

You have successfully created an external key. 


## Creating external keys with the API
{: #create-external-keys-api}






## What's next
{: #create-external-keys-next}

- To find out how to create a key for internal keystores, check out [Creating internal keys](/docs/hs-crypto?topic=hs-crypto-create-internal-keys).
  
- To find out instructions on editing your key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  
- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
  
- To find out how to delete a key, check out [Deleting external keys](/docs/hs-crypto?topic=hs-crypto-delete-external-keys).
  


