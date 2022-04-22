---

copyright:
  years: 2022
lastupdated: "2022-04-21"

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}


# Editing vault details
{: #edit-vaults}

You can edit your vaults in {{site.data.keyword.uko_full_notm}} with the {{site.data.keyword.cloud}} console, or programmatically with the {{site.data.keyword.uko_full_notm}} API. With a vault, you can not only create managed keys or add target keystores, but also manage resources that are contained in the vault.
{: shortdesc}


## Editing vault details with the {{site.data.keyword.cloud_notm}} console
{: #edit-vaults-ui}
{: ui}

To edit vault details by using the console, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Vaults** from the navigation to view all the available vaults.
3. Click the vault that you want to edit. The Details side panel is displayed.
4. Click **Edit** to update the **Vault name** and **Description**.
5. Click **Save** to save the property changes.
6. The keys and keystores that are assigned to this vault are displayed in tables. 
7. Optionally, you can add additional keys to the vault by clicking **Create key** under **Keys**, or add a keystore by clicking **Add keystores** under **Target keystores**.



## Editing vault details with the API
{: #edit-vaults-api}
{: api}

To edit a vault through the API, follow these steps:

1. [Retrieve your service and authentication credentials to work with keys in the service](/docs/hs-crypto?topic=hs-crypto-set-up-uko-api).
   
2. Edit a vault by making a `PATCH` call to the following endpoint.

    ```
    https://uko.<region>.hs-crypto.cloud.ibm.com:<port>/api/v4/vaults/<vault_id>
    ```
    {: codeblock}

    Replace `<vault_id>` with the ID of your vault.

    For detailed instructions and code examples about using the API method, check out the [{{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko#update-vault){: external}.



## What's next
{: #edit-vaults-next}

- To find out how to create a vault, check out [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
  
- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

