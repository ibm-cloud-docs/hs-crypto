---

copyright:
  years: 2021
lastupdated: "2021-12-09"

keywords: Unified Key Orchestrator, create keys, key management, kms keys

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

You can use {{site.data.keyword.uko_full_notm}} to create internal KMS keys in the UI or with the API.
{: shortdesc}


## Creating internal KMS keys in the UI
{: #create-kms-keys-ui}

Complete the following steps to create an internal KMS key in the UI.

1. [Log in to the {{site.data.keyword.uko_full_notm}} service instance](https://cloud.ibm.com/login){: external}.
2. In the left navigation panel, go to **Vaults** &gt; **Managed keys** to view all the available keys.
3. To create a new key, click **Add key**.
4. Under **Vault,** assign the key to a vault for access control. You can also click **Create vault** to create a new vault.
5. Under **Keystore type,** select **Internal KMS.**
6. In the **Key properties** table, specify the details of the key:

    |       Property	     |                         Description                       |
    |----------------------|-----------------------------------------------------------|
    | Name                 |                                                           |
    | Description          | (Optional)                                                |
    | Key algorithm        |                                                           |
    | Key length           |                                                           |
    | State                |                                                           |
    | Activation date      |                                                           |
    | Deactivation date    |                                                           |
    | Key tags             | (Optional)                                                |

7. Optionally, you can select one or multiple **Target keystores** to install the key in.
8. View the summary of your key.
9. Click **Create key** to confirm.




## Creating internal KMS keys with the API
{: #create-kms-keys-api}






## What's next
{: #create-kms-keys-next}


  


