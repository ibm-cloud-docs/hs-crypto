---

copyright:
  years: 2022
lastupdated: "2022-02-14"

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


# Creating managed keys
{: #create-managed-keys}

You can use {{site.data.keyword.uko_full_notm}} to create KMS keys through the user interface (UI), or programmatically with the {{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

To protect your privacy, do not store your personal data as metadata for your key.
{: important}

## Creating managed keys through the UI
{: #create-managed-keys-ui}

To create a managed key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. To create a managed key, click **Create key**.
4. Under **Vault**, select a vault for the key for access control, and click **Next**. 
   
   If you want to assign the key to a new vault, click **Create vault**. For more instructions, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults). 

5. Under **General**, select **IBM KMS**, **IBM Key Protect**, **AWS Key Management Service**, or **Azure Key Vault**, depending on which type of keystore you want to install the key in. And then, click **Next**.
   
   After a keystore type is selected, you can install the key to keystores of this type only.
   {: note}

6. Under **Key properties**, specify the following details of the key. Click **Next** to continue when you are done.

    |       Property	      |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Key name             | A unique, human-readable name for easy identification of your key, with 2 - 100 characters in length. |
    | Description          | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Algorithm            | The encryption algorithm to encrypt data for the key.     |
    | Length               | The number of bits that represents the encryption strength of the key.   |
    | State                | _Pre-active_ keys are not to be installed in target keystores until you manually activate them. _Active_ keys are to be automatically installed in the target keystores. For more information about key states, see [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states){: external} |
    | Activation date      | Plan a date to activate the _Pre-active_ key. No automatic state change is triggered. |
    | Expiration date      | Plan a date to deactivate the key. No automatic state change is triggered. |
    | Key tags             | (Optional) Add pairs of names and values to identify your key.  |
    {: caption="Table 1. Key properties" caption-side="bottom"}

7. Under **Target keystores**, you can select one or multiple target keystores to install the managed key in. Installing a key in multiple keystores enables redundancy. You can also install the key later by following instructions in [Installing existing keys to keystores](/docs/hs-crypto?topic=hs-crypto-install-key-keystores).

   You can use the key for encryption or decryption only after it is installed in at least one keystore.
   {: important}

8. Under **Summary**, view the summary of your key, and then click **Create key** to confirm.

You have successfully created a managed key. 


## Creating managed keys with the API
{: #create-managed-keys-api}






## What's next
{: #create-managed-keys-next}

- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  
- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).
  
- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).

