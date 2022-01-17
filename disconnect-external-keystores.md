---

copyright:
  years: 2022
lastupdated: "2022-01-17"

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

You can reconnect to the keystores at any time. For more instructions, see [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores){: external}.

To disconnect from an external keystore, make sure that all the installed keys in this keystore are in _Pre-active_ or _Destroyed_ state.
{: note}


## Disconnecting from external keystores through the UI
{: #disconnect-external-keystores-ui}

To disconnect from an external keystore through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Target keystores** on the left navigation pane to view all the available keystores.
3. Click on the keystore that you want to disconnect to open the side panel.
4. Click **Disconnect** to disconnect the keystore and remove it from the keystore list. All the installed keys are to be uninstalled and inaccessible to their resources.
5. Click **Disconnect keystore** to confirm.



## What's next
{: #disconnect-external-keystores-next}


  


