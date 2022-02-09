---

copyright:
  years: 2022
lastupdated: "2022-02-08"

keywords: Unified Key Orchestrator, UKO keystore, disconnect keystore, external keystore, KMS keystore

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


# Disconnecting from external keystores
{: #disconnect-external-keystores}

You can disconnect from keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS). After you disconnect from an external keystore, all the installed keys are uninstalled and resources that are managed are not accessible.
{: shortdesc}

If you want to disconnect from an external keystore, delete all installed keys first. In other words, all keys with this keystore as a target are in _Pre-active_ or _Destroyed_ state. For more information about deleting keys, see [Deleting internal keys](/docs/hs-crypto?topic=hs-crypto-delete-internal-keys).
{: note}


## Disconnecting from external keystores through the UI
{: #disconnect-external-keystores-ui}

When you disconnect from an external keystore, all keys are to be uninstalled from the keystore and inaccessible to the {{site.data.keyword.cloud_notm}} associated resources. This action is permanent and cannot be undone.
{: important}

To disconnect from an external keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the keystore that you want to disconnect. The Details side panel is displayed.
4. Click **Disconnect** to disconnect the keystore and remove it from the keystore list. 
5. Click **Disconnect keystore** to confirm.

The external keystore has been disconnected with all the installed keys uninstalled and resources that are managed inaccessible.

After you disconnect from an external keystore, you can reconnect to the keystores at any time. For more instructions, see [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
{: tip}

## What's next
{: #disconnect-external-keystores-next}

- To find out how to update the connection to an external keystore, check out [Editing connection to external keystores](/docs/hs-crypto?topic=hs-crypto-edit-external-keystore-connection).
  
- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).
