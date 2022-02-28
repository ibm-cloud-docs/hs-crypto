---

copyright:
  years: 2022
lastupdated: "2022-02-28"

keywords: Unified Key Orchestrator, UKO keystore, delete keystore, internal keystore, KMS keystore

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

# Deleting internal keystores
{: #delete-internal-keystores}

You can delete internal keystores in {{site.data.keyword.uko_full_notm}} through the user interface (UI). After you delete an internal keystore, all the installed keys are uninstalled and associated resources are detached.
{: shortdesc}

To delete an internal keystore, [delete all installed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys) first. The key metadata remains in the keystore for 90 days before it gets removed automatically. You can delete the keystore only after the key metadata gets removed. If you want to delete the keystore immediately, [manually remove all key metadata using the KMS API](/apidocs/hs-crypto#purgekey){: external} in 4 hours after you destroy the key. Make sure that you have the **KMS Key Purge** role assigned. For more information about roles, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).
{: note}

## Deleting internal keystores through the UI
{: #delete-internal-keystores-ui}

When you delete an internal keystore, all keys are to be uninstalled from the keystore and inaccessible to the {{site.data.keyword.cloud_notm}} associated resources. The deletion is permanent and cannot be undone.
{: important}

To delete an internal keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the keystore that you want to delete. The side panel is displayed.
4. Click **Delete** to delete the keystore and all the metadata. 
5. Click **Delete keystore** to confirm the deletion.

The internal keystore has been deleted with all the installed keys uninstalled and associated resources detached.



## What's next
{: #delete-internal-keystores-next}

- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).
  
- To find out instructions on editing an internal keystore, check out [Editing internal keystores](/docs/hs-crypto?topic=hs-crypto-edit-internal-keystores).

- To find out how to delete a vault, check out [Deleting vaults](/docs/hs-crypto?topic=hs-crypto-delete-vaults).

