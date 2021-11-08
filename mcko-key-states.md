---

copyright:
  years: 2021
lastupdated: "2021-11-08"

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

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} follows the security guidelines by [NIST SP 800-57 for key states](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0){: external}.
{: shortdesc}

## Key states and transitions

{: #mcko-key-transitions}

Cryptographic keys, in their lifetime, transition through several states that are a function of how long the keys are in existence and whether data is protected.

The following diagram shows how a key passes through states in the vault between the generation and the destruction.

![Key states and transitions in the vault](/images/mcko-key-states.svg "Key states and transitions in the vault"){: caption="Figure 1. Key states and transitions in the vault" caption-side="bottom"}




| State       | Integer Mapping | Description |
|-------------|-----------------|-------------|
| Pre-active  |        0        | Keys are initially created in the _Pre-active_ state. A pre-active key cannot be used to cryptographically protect data. |
| Active      |        1        | Keys move immediately into the _Active_ state on the activation date or when you manually activate them. This transition marks the beginning of a key's cryptoperiod. Keys with no activation date become active immediately and remain active until they expire or are destroyed. |
| Deactivated |        3        | A key moves into the _Deactivated_ state on the expiration date, if one is assigned. You can also manually deactivate or reactivate a key. In this state, the key is unable to cryptographically protect data. A key should be deactivated first before it can be moved to the _Destroyed_ state. |
| Compromised |        4        | You should mark a key as being _Compromised_ when the key's information is disclosed to an unauthorised third party. Data in the _Compromised_ keys can still be decrypted, but you should not use the key to encrypt new data. |
| Destroyed   |        5        | Destroyed keys are in the _Destroyed_ state. Keys in this state are not recoverable. Metadata that is associated with a key remains in the vault until you manually remove the key from the vault. |
{: caption="Table 1. Describes key states and transitions." caption-side="bottom"}


## Key states and service actions
{: #mcko-key-states-service-actions}

Key states affect whether an action that is performed on a key succeeds or fails. For example, if a key is in the _Active_ state, you can't restore the key because the key wasn't previously deleted.

The following table shows how Multicloud Key Orchestrator handles service actions based on the state of a key. The column headers represent the key states, and the row headers represent the actions that you can perform on a key. The **Checkmark** icon ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") indicates that the action on a key is expected to succeed based on the key state.


(To be updated)

| Action | Active | Deactivated | Compromised | Destroyed |
| --- | --- | --- | --- | --- |
| Get key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |  |![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List keys. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Deactivate key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |   |
| Reactivate key. |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Destroy key. |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Remove key from vault. |     |     |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: caption="Table 2. Describes how key states affect service actions." caption-side="bottom"}



## Monitoring for lifecycle changes
{: #mcko-monitor-lifecycle-changes}

(To be updated)

After you add a root key to the service, use the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.hscrypto}} key management REST API to view your key's transition history and configuration.

For audit purposes, you can also monitor the activity trail for a root key by integrating {{site.data.keyword.hscrypto}} with the [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started){: external}. After both services are provisioned and running, activity events are generated and automatically collected in a {{site.data.keyword.at_full_notm}} log when you perform actions on keys in {{site.data.keyword.hscrypto}}.







