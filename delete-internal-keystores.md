---

copyright:
  years: 2022
lastupdated: "2022-01-18"

keywords: Unified Key Orchestrator, UKO keystore, delete keystore, internal keystore, KMS keystore

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


# Deleting internal keystores
{: #delete-uko-keystores}

You can delete internal keystores in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API. After you delete an internal keystore, all the installed keys are uninstalled and associated resources are detached.
{: shortdesc}

If you want to delete an internal keystore, delete any installed keys first. In other words, all keys with this keystore as a target are in _Pre-active_ or _Destroyed_ state. For more information about deleting keys, see [Deleting internal keys](/docs/hs-crypto?topic=hs-crypto-delete-internal-keys).
{: important}


## Deleting internal keystores through the UI
{: #delete-internal-keystores-ui}

To delete an internal keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** from the navigation to view all the available keystores.
3. Click the keystore that you want to delete to open the side panel.
4. Click **Delete** to delete the keystore and all the metadata. 
5. Click **Delete keystore** to confirm.

The internal keystore has been deleted with all the installed keys uninstalled and associated resources detached.

## What's next
{: #delete-internal-keystores-next}


  


