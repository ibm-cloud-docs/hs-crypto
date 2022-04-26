---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-26"

keywords: encryption key states, encryption key lifecycle, manage key lifecycle

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Monitoring the lifecycle of encryption keys
{: #kms-key-states}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} key management service (KMS) follows the security guidelines by [NIST SP 800-57 for key states](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0){: external}.
{: shortdesc}

## Key states and transitions
{: #kms-key-transitions}

KMS keys, in their lifetime, transition through several states that are a function of how long the keys are in existence and whether data is protected.

{{site.data.keyword.hscrypto}} KMS provides a graphical user interface and a REST API for tracking keys as they move through several states in their lifecycle. The following diagram shows how a key passes through states between the generation and the destruction.

![Encryption key states and transitions](/images/key-states.svg "Encryption key states and transitions"){: caption="Figure 1. KMS key states and transitions" caption-side="bottom"}

| State       | Integer Mapping | Description |
|-------------|-----------------|-------------|
| Pre-active  |       0        | Keys are initially created in the _Pre-active_ state. A pre-active key cannot be used to cryptographically protect data. |
| Active      |       1        | Keys move immediately into the _Active_ state on the activation date. This transition marks the beginning of a key's cryptoperiod. Keys with no activation date become active immediately and remain active until they expire or are destroyed. |
| Suspended   |       2        | A key moves into the _Suspended_ state when it is [disabled for encrypt and decrypt operations](/docs/hs-crypto?topic=hs-crypto-disable-keys). In this state, the key is unable to cryptographically protect data and can be moved only to the _Active_ or _Destroyed_ states. |
| Deactivated |       3        | A key moves into the _Deactivated_ state on the expiration date, if one is assigned. In this state, the key is unable to cryptographically protect data and can be moved only to the _Destroyed_ state. |
| Destroyed   |       5        | Deleted keys are in the _Destroyed_ state. Keys in this state are not recoverable. Metadata that is associated with a key, such as the key's transition history and name, is kept in the {{site.data.keyword.hscrypto}} database. |
{: caption="Table 1. Describes KMS key states and transitions." caption-side="bottom"}

## KMS key states and service actions
{: #kms-key-states-service-actions}

KMS key states affect whether an action that is performed on a key succeeds or fails. For example, if a key is in the _Active_ state, you can't restore the key because the key wasn't previously deleted.

The following table shows how {{site.data.keyword.hscrypto}} handles service actions based on the state of a KMS key. The column headers represent the key states, and the row headers represent the actions that you can perform on a key. The **Checkmark** icon ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") indicates that the action on a key is expected to succeed based on the key state.

| Action | Active | Suspended | Deactivated | Destroyed |
| --- | --- | --- | --- | --- |
| Get key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
| List keys. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |
| Rotate key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |     |
| Wrap key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |     |
| Unwrap key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |
| Rewrap key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |
| Disable key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |     |
| Enable key. |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |     |
| Delete key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |
| Restore key. |     |     |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: caption="Table 2. Describes how key states affect service actions." caption-side="bottom"}

## Monitoring for lifecycle changes
{: #kms-monitor-lifecycle-changes}

After you add a KMS key to the service, use the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.hscrypto}} key management REST API to view your key's transition history and configuration.

For audit purposes, you can also monitor the activity trail for a root key by integrating {{site.data.keyword.hscrypto}} with the [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started){: external}. After both services are provisioned and running, activity events are generated and automatically collected in a {{site.data.keyword.at_full_notm}} log when you perform actions on keys in {{site.data.keyword.hscrypto}}.
