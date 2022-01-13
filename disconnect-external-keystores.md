---

copyright:
  years: 2022
lastupdated: "2022-01-13"

keywords: Unified Key Orchestrator, keystore, disconnect keystore, external keystore

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


# Disconnecting from external keystores
{: #disconnect-external-keystores}

You can disconnect from keystores that are external to your service instance on {{site.data.keyword.cloud}}, or from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS).
{: shortdesc}

To disconnect from an external keystore, make sure that all the installed keys in this keystore are in _pre-active_ or _destroyed_ state.
{: note}


## Disconnecting external keystores through the UI
{: #disconnect-external-keystores-ui}

To disconnect from an external keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. In the left navigation panel, go to **Vaults** &gt; **Target keystores** to view all the available keystores.
3. Click the keystore that you want to disconnect to view details.
4. Click **Disconnect** to disconnect the keystore and remove it from the keystore list. All the installed keys are to be uninstalled and be inaccessible to their resources.
5.  Click **Disconnect keystore** to confirm.



## What's next
{: #disconnect-external-keystores-next}


  


