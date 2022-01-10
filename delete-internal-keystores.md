---

copyright:
  years: 2022
lastupdated: "2022-01-10"

keywords: Unified Key Orchestrator, keystore, delete keystore, internal keystore, external keystore

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

You can delete internal keystores in {{site.data.keyword.uko_full_notm}}  through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.

To delete an internal keystore, make sure that all the installed keys in this keystore are in _pre-active_ or _destroyed_ state.
{: shortdesc}

## Deleting internal keystores through the UI
{: #delete-internal-keystores-ui}

To delete an internal keystore through the UI, complete the following steps.

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. In the left navigation panel, go to **Vaults** &gt; **Target keystores** to view all the available keystores.
3. Click the keystore that you want to delete to view details.
4. Click **Delete** to delete the keystore and all the metadata. All the installed keys are to be uninstalled and associated resources are to be detached.
5. Click **Delete keystore** to confirm.



## What's next
{: #delete-internal-keystores-next}


  


