---

copyright:
  years: 2021
lastupdated: "2021-11-05"

keywords: encryption key states, encryption key lifecycle, manage key lifecycle, MCKO, multicloud key orchestrator

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:term: .term}


# Monitoring the lifecycle of encryption keys in Multicloud Key Orchestrator
{: #mcko-key-states}


## Key states and transitions
{: #mcko-key-transitions}

Cryptographic keys, in their lifetime, transition through several states that are a function of how long the keys are in existence and whether data is protected.

The following diagram shows how a key is created in the vault, passes through states, and gets removed from the vault.

![Key states and transitions in the vault](/images/mcko-key-states.svg "Key states and transitions in the vault")
{: caption="Figure 1. Key states and transitions in the vault." caption-side="bottom"}


| State       | Integer Mapping | Description |
|-------------|-----------------|-------------|
| Pre-active  |        0        | Keys are initially created in the _Pre-active_ state. A pre-active key cannot be used to cryptographically protect data. |
| Active      |        1        | Keys move immediately into the _Active_ state on the activation date. This transition marks the beginning of a key's cryptoperiod. Keys with no activation date become active immediately and remain active until they expire or are destroyed. |
| Suspended   |        2        | A key moves into the _Suspended_ state when it is [disabled for encrypt and decrypt operations](/docs/hs-crypto?topic=hs-crypto-disable-keys). In this state, the key is unable to cryptographically protect data and can be moved only to the _Active_ or _Destroyed_ states. |
| Deactivated |        3        | A key moves into the _Deactivated_ state on the expiration date, if one is assigned. In this state, the key is unable to cryptographically protect data and can be moved only to the _Destroyed_ state. |
| Compromised |        4        | A key's material has been disclosed to an unauthorised person. |
| Destroyed   |        5        | Deleted keys are in the _Destroyed_ state. Keys in this state are not recoverable. Metadata that is associated with a key, such as the key's transition history and name, is kept in the {{site.data.keyword.hscrypto}} database. |
{: caption="Table 1. Describes key states and transitions." caption-side="bottom"}


## Key states and service actions
{: #mcko-key-states-service-actions}

Key states affect whether an action that is performed on a key succeeds or fails. For example, if a key is in the _Active_ state, you can't restore the key because the key wasn't previously deleted.

The following table shows how Multicloud Key Orchestrator handles service actions based on the state of a key. The column headers represent the key states, and the row headers represent the actions that you can perform on a key. The **Checkmark** icon ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") indicates that the action on a key is expected to succeed based on the key state.


(To be updated)

| Action | Active | Suspended | Deactivated | Compromised |Destroyed |
| --- | --- | --- | --- | --- | --- |
| Get key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |  |![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List keys. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Rotate key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |     |   |
| Wrap key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |     |   |
| Unwrap key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Rewrap key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Disable key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |     |   |
| Enable key. |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |   |
| Destroy key. |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Restore key. |     |     |     |  |   |
{: caption="Table 2. Describes how key states affect service actions." caption-side="bottom"}



## Monitoring for lifecycle changes
{: #mcko-monitor-lifecycle-changes}







