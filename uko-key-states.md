---

copyright:
  years: 2021
lastupdated: "2021-11-18"

keywords: encryption key states, encryption key lifecycle, manage key lifecycle, Unified Key Orchestrator

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


# Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}
{: #uko-key-states}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} follows the security guidelines by [NIST SP 800-57 for key states](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0){: external}.
{: shortdesc}

## Key states and transitions
{: #uko-key-transitions}

Cryptographic keys, in their lifetime, transition through several states that are a function of how long the keys are in existence and whether data is protected.

The following diagram shows how a key passes through states in the vault between the generation and the destruction.

![Key states and transitions in the vault](/images/uko-key-states.svg "Key states and transitions in the vault"){: caption="Figure 1. Key states and transitions in the vault" caption-side="bottom"}




| State       | Integer mapping | Description |
|-------------|-----------------|-------------|
| Pre-active  |        0        | Keys are initially created in the _Pre-active_ state. A _Pre-active_ key cannot be used to cryptographically protect data. |
| Active      |        1        | Keys move immediately into the _Active_ state on the activation date. You can also manually activate the keys. This transition marks the beginning of the crypto period of the keys. Keys with no activation date become active immediately and remain active until they expire or are destroyed. |
| Deactivated |        3        | Keys move into the _Deactivated_ state on the scheduled expiration date. You can also manually deactivate or reactivate the keys. In this state, a key is not able to cryptographically protect data. Deactivate a key first before you move the key to the _Destroyed_ state. |
| Compromised |        4        | Mark a key as _Compromised_ when the information of the key is disclosed to an unauthorized third party. You can still decrypt the data in the _Compromised_ keys, but you cannot use the key to encrypt new data. |
| Destroyed   |        5        | Destroyed keys are in the _Destroyed_ state. Keys in this state cannot be restored. Metadata that is associated with a key remains in the vault until you manually remove the key from the vault. |
{: caption="Table 1. Key states and transitions" caption-side="bottom"}


## Key states and service actions
{: #uko-key-states-service-actions}

Key states affect whether an action that you perform on a key succeeds or fails. For example, if a key is in the _Active_ state, you cannot restore the key because the key wasn't deleted.

The following table shows how {{site.data.keyword.uko_full_notm}} handles service actions based on the state of a key. The column headers represent the key states, and the row headers represent the actions that you can perform on a key. The **Checkmark** icon ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") indicates that the action on a key is expected to succeed based on the key state.


(To be updated)

| Action | Active | Deactivated | Compromised | Destroyed |
| ------ | ------ | ----------- | ----------- | --------- |
| Get a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |  |![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List keys. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Deactivate a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |   |
| Reactivate a key. |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Destroy a key. |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Remove a key from vault. |     |     |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: caption="Table 2. How key states affect service actions" caption-side="bottom"}



## Monitoring for lifecycle changes
{: #uko-monitor-lifecycle-changes}

(To be updated)

After you add a root key to the service, use the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.hscrypto}} key management REST API to view your key's transition history and configuration.

For audit purposes, you can also monitor the activity trail for a root key by integrating {{site.data.keyword.hscrypto}} with the [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started){: external}. After both services are provisioned and running, activity events are generated and automatically collected in a {{site.data.keyword.at_full_notm}} log when you perform actions on keys in {{site.data.keyword.hscrypto}}.







