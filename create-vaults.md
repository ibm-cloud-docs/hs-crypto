---

copyright:
  years: 2022
lastupdated: "2022-02-11"

keywords: Unified Key Orchestrator, vaults, keys, keystores, key management, UKO

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


# Creating vaults
{: #create-vaults}

A vault is a single repository that controls a user's or an access group's access to managed keys and target keystores through {{site.data.keyword.iamshort}} (IAM). You can create vaults in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{{site.data.keyword.uko_full_notm}} API.
{: shortdesc}

For more information about granting access, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).


## Creating vaults through the UI
{: #create-vaults-ui}

To create a vault through the UI, complete the following steps through the **Vaults** page. Optionally, you can create a vault when you [create a key](/docs/hs-crypto?topic=hs-crypto-create-internal-keys) or [add a keystore](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores).

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. To create a vault, click **Create vault**.
4. Enter a name in **Vault name**. The vault name can be of 2 to 100 characters. Optionally, you can add an extended description to your vault in the **Description** section.
5. Click **Create vault** to confirm.

You have successfully created a vault. 

## Creating vaults through the API
{: #create-vaults-api}

To create a vault through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
2. Create a vault by making a `POST` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v3/vaults
    ```
    {: codeblock}

    For detailed instructions and code examples about using the API method, [check out the {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#create-vault-v3){: external}.

## What's next
{: #create-vaults-next}

- To find out instructions on editing a vault, check out [Editing vault details](/docs/hs-crypto?topic=hs-crypto-edit-vaults).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
  
- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

- To find out more about programmatically managing your keys and keystores, [check out the {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external}.

