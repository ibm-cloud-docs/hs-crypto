---

copyright:
  years: 2022
lastupdated: "2022-01-10"

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

The following diagram shows how a key passes through states between the generation and the destruction.

![Key states and transitions](/images/uko-key-states.svg "Key states and transitions"){: caption="Figure 1. Key states and transitions" caption-side="bottom"}




| State       | Integer mapping | Description |
|-------------|-----------------|-------------|
| Pre-active  |        0        | A _Pre-active_ key is a created key that is not yet installed into keystores and is therefore not available for use by applications. New keys are initially created in the _Pre-active_ state. |
| Active      |        1        | An _Active_ key is installed in keystores and is available for use by applications. _Pre-Active_ keys are automatically moved to the _Active_ state upon the activation date or if they are manually activated. Keys that are created without an activation date become active immediately. |
| Deactivated |        3        | A _Deactivated_ key is no longer allowed for operations that generate new cryptographic data, such as encryption or signing, but can still be used for operations on existing data to do decryption or signature verification. _Active_ keys are automatically moved to the _Deactivated_ state upon the expiration date or if they are manually deactivated. |
| Destroyed   |        5        | A _Destroyed_ key is a key record for which the actual key material has been permanently erased. The record of the key is retained to be available for later queries or audits until you manually remove the key from the vault. Keys in the _Destroyed_ state cannot be restored. |
{: caption="Table 1. Key states and transitions" caption-side="bottom"}


## Key states and service actions
{: #uko-key-states-service-actions}

Key states affect whether an action that you perform on a key succeeds or fails. For example, if a key is in the _Active_ state, you cannot restore the key because the key wasn't deleted.

The following table shows how {{site.data.keyword.uko_full_notm}} handles service actions based on the state of a key. The column headers represent the key states, and the row headers represent the actions that you can perform on a key. The **Checkmark** icon ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") indicates that the action on a key is expected to succeed based on the key state.


| Action | Pre-active | Active | Deactivated | Destroyed |
| ------ | ------ | ----------- | ----------- | --------- |
| Get a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List keys. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Deactivate a key. |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Reactivate a key. |     |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Destroy a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Remove a key from vault. |     |     |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: caption="Table 2. How key states affect service actions" caption-side="bottom"}



## Monitoring for lifecycle changes
{: #uko-monitor-lifecycle-changes}

(To be updated)

After you add a root key to the service, use the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.hscrypto}} key management REST API to view your key's transition history and configuration.

For audit purposes, you can also monitor the activity trail for a root key by integrating {{site.data.keyword.hscrypto}} with the [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started){: external}. After both services are provisioned and running, activity events are generated and automatically collected in a {{site.data.keyword.at_full_notm}} log when you perform actions on keys in {{site.data.keyword.hscrypto}}.






