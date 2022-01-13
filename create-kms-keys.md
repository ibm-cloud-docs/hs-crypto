---

copyright:
  years: 2022
lastupdated: "2022-01-13"

keywords: Unified Key Orchestrator, create key, key management, kms key

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


# Creating internal KMS keys
{: #create-kms-keys}

You can use {{site.data.keyword.uko_full_notm}} to create internal KMS keys through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}


## Creating internal KMS keys through the UI
{: #create-kms-keys-ui}

To create an internal KMS key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. In the left navigation panel, go to **Vaults** &gt; **Managed keys** to view all the available keys.
3. To create a new key, click **Add key**.
4. Under **Vault,** assign the key to a vault for access control. You can also click **Create vault** to create a new vault.
5. Under **Keystore type,** select **Internal KMS.**
6. Under **Key properties,** specify the details of the key:

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Name                 | A unique, human-readable name for easy identification of your key, with 2 - 100 characters in length. |
    | Description          | (Optional) An extended description for your keystore, with up to 200 characters in length. |
    | Key algorithm        |                                                           |
    | Key length           |                                                           |
    | State                |                                                           |
    | Activation date      |                                                           |
    | Deactivation date    |                                                           |
    | Key tags             | (Optional)                                                |

7. Optionally, you can select one or multiple **Target keystores** to install the key in.
8. View the summary of your key, then click **Create key** to confirm.




## Creating internal KMS keys with the API
{: #create-kms-keys-api}






## What's next
{: #create-kms-keys-next}


  


