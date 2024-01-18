---

copyright:
  years: 2022, 2024
lastupdated: "2024-01-18"

keywords: encryption key states, encryption key lifecycle, manage key lifecycle, Unified Key Orchestrator, UKO keys

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}




# Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}
{: #uko-key-states}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} follows the security guidelines by [NIST SP 800-57 for key states](https://www.nist.gov/publications/recommendation-key-management-part-1-general-0){: external}.
{: shortdesc}

## Key states and transitions
{: #uko-key-transitions}

Managed keys in {{site.data.keyword.uko_full_notm}} transition through several states that indicate how long the keys are in existence and whether data is protected.

The following diagram shows how a managed key passes through states between the generation and the destruction.


![Key states and transitions](/images/uko-key-states.svg "Key states and transitions"){: caption="Figure 1. Key states and transitions" caption-side="bottom"}



The following table shows the details of each key state.

| State       | Integer mapping | Description |
|-------------|-----------------|-------------|
| Pre-active  |        0        | A Pre-active key is not yet activated in keystores and is therefore not available for use by applications. New keys are initially created in the Pre-active state. |
| Active      |        1        | An Active key is activated in keystores and is available for use by applications. If the key is used to protect associated resources, the key will be accessible to its associated resources and can be used for data protection. You can set a key to the Active state when you create the key, or manually activate a Pre-active key later. |
| Deactivated |        3        | A Deactivated key is no longer allowed for operations that generate new cryptographic data, such as encryption or signing, but can still be used for operations on existing data to do decryption or signature verification. When you deactivate a key, the key is unlinked from all the keystores, and not accessible to all associated resources and their data. However, you can still reactivate the key so that it is accessible to the resources again. |
| Destroyed<sup>1</sup>   |        5        | A Destroyed key is a key record for which the actual key material has been permanently erased. The record of the key is retained to be available for later queries or audits until you manually remove the key from the vault. Keys in the Destroyed state cannot be restored in {{site.data.keyword.uko_full_notm}}. However, you can still restore your keys in external keystores depending on the settings of the cloud providers. |
{: caption="Table 1. Key states and transitions" caption-side="bottom"}

If the key state in some keystores is different from the managed key state, you receive a **Key out of sync** warning message. An `Out of sync` flag is also displayed in the corresponding keystore card or the key list. There can be multiple reasons why the key is out of sync. For example, there is an issue in relinking the key in the keystore,  or the key is modified in the target keystore outside of {{site.data.keyword.uko_full_notm}}. When you hover over this flag, you can see the specific reason. You can sync the key state by clicking **Sync key** on the Key details page.

## Key states and service actions
{: #uko-key-states-service-actions}

Key states affect whether an action that you perform on a key succeeds or fails. For example, if a managed key is in the Active state, you cannot destroy the key before you deactivate it first.

The following table shows how {{site.data.keyword.uko_full_notm}} handles service actions based on the state of a key. The column headers represent the key states, and the row headers represent the actions that you can perform on a key. The **Checkmark** icon ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") indicates that the action on a key is expected to succeed based on the key state.

| Action | Pre-active | Active | Deactivated | Destroyed |
| ------ | ------ | ---------- | ----------- | --------- |
| Get a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |![checkmark icon](../icons/checkmark-icon.svg "Checkmark")|
| List keys. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Rotate a key. |   | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")  |    |    |
| Deactivate a key. |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |     |   |
| Reactivate a key. |     |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Destroy a key. | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |   |
| Remove a key from vault. |     |     |     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") |
{: caption="Table 3. How key states affect service actions" caption-side="bottom"}



## Monitoring for lifecycle changes
{: #uko-monitor-lifecycle-changes}

After you add a managed key to the service, use the {{site.data.keyword.cloud_notm}} UI or the {{site.data.keyword.uko_full_notm}} API to view your key's transition history and configuration.

For audit purposes, you can also monitor the activity trail for a managed key by integrating {{site.data.keyword.hscrypto}} with the [{{site.data.keyword.at_full_notm}}](/docs/activity-tracker?topic=activity-tracker-getting-started){: external}. After both services are provisioned and running, activity events are generated and automatically collected in an {{site.data.keyword.at_full_notm}} log when you perform actions on keys in {{site.data.keyword.hscrypto}}.


## What's next
{: #uko-key-states-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- To find out instructions on editing a managed key, check out [Editing key details](/docs/hs-crypto?topic=hs-crypto-edit-kms-keys).
  
- To find out more about managing your key list, check out [Viewing a list of keys](/docs/hs-crypto?topic=hs-crypto-view-key-list) or [Filtering and searching keys](/docs/hs-crypto?topic=hs-crypto-search-key-list).

- To find out instructions on deleting a managed key, check out [Deleting managed keys](/docs/hs-crypto?topic=hs-crypto-delete-managed-keys).

 
- To find out more about the UKO API, see [{{site.data.keyword.uko_full_notm}} API reference](/apidocs/uko){: external}. 





