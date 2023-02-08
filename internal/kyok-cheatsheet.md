---

copyright:
  years: 2020, 2023
lastupdated: "2023-02-08"

keywords: enable KYOK, onboard to Hyper Protect Crypto Services, HPCS onboarding, service onboarding, internal registration, key registration, KYOK, kms onboarding

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Keep Your Own Key cheat sheet
{: #kyok-cheatsheet}

A consolidated list to help your service properly enable Keep Your Own Key (KYOK) with your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance.
{: shortdesc}

## Core concepts
{: #kyok-core-concepts}

Although you don't necessarily need to understand the details of each topic, they are there for your awareness. The important thing to know is that if your service addresses each concept, you will have enabled key management service.

- You must have a basic understanding of IAM concepts, such as [granting service to service access](/docs/get-coding?topic=get-coding-servicetoservice){: external}.
- You must have a basic understanding of the [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) process.
- You must have a basic understanding of how the platform uses [Global Search and Tagging (GhoST)](/docs/get-coding?topic=get-coding-ghost_overview){: external}.
- You must have a basic understanding of [key registration](/docs/hs-crypto?topic=hs-crypto-register-protected-resources).

## Required actions
{: #kyok-required-actions}

If you complete all the following steps, your service will meet all the Keep Your Own Key (KYOK) requirements. When you plan to adopt key management service, follow the steps that are listed in order. You can also use these steps to estimate and group the effort that is required to become KYOK ready.

| Actions | Steps   |
| ---------- | ------- |
| [Onboard your service to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-onboard-service) | <ol><li>[Submit a request to onboard your service](/docs/hs-crypto?topic=hs-crypto-onboard-service#submit-request)</li><li>[Create a CRN token](/docs/hs-crypto?topic=hs-crypto-onboard-service#submit-request)</li><li>[Discover KMS instances](/docs/hs-crypto?topic=hs-crypto-onboard-service#discover-kms-instances)</li><li>[Submit a request to integrate with Hyperwarp](/docs/hs-crypto?topic=hs-crypto-onboard-service#integrate-hyperwarp)</li></ol> |
| [Set up the {{site.data.keyword.hscrypto}} key management service API](/docs/hs-crypto?topic=hs-crypto-configure-api-test) | <ol><li>[Create a test instance](/docs/hs-crypto?topic=hs-crypto-configure-api-test#provision-instance-test)</li><li>[Create a root key](/docs/hs-crypto?topic=hs-crypto-configure-api-test#create-root-key-test)</li><li>[Wrap a data encryption key](/docs/hs-crypto?topic=hs-crypto-configure-api-test#wrap-key-test)</li><li>[Unwrap the data encryption key](/docs/hs-crypto?topic=hs-crypto-configure-api-test#unwrap-key-test)</li></ol> |
| [Map cloud resources to a root key](/docs/hs-crypto?topic=hs-crypto-register-protected-resources)  | <ol><li>[Register cloud resources](/docs/hs-crypto?topic=hs-crypto-register-protected-resources#create-registration)</li><li>[Unregister cloud resources](/docs/hs-crypto?topic=hs-crypto-register-protected-resources#delete-registration)</li></ol> |

## Features
{: #kyok-features}

The following features are available for KYOK enabled services. For up-to-date information, reach out to us in the [`#hp-crypto-kms` Slack channel](https://app.slack.com/client/T02J3DPUE/CFFC7M3B3){: external}.

Use the [adopter's guide](https://github.ibm.com/kms/BYOK_Adopter_services){: external} for more information on KYOK requirements, features, and use cases.
{: note}

| Actions | Steps |
| --- | --- |
| [Plan for crypto erasure](/docs/hs-crypto?topic=hs-crypto-key-erasure) | 1.  [Delete a root key](/docs/hs-crypto?topic=hs-crypto-delete-keys) \n 2.  [Check for a Hyperwarp deletion event from {{site.data.keyword.hscrypto}}](https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure) \n 3.  [Process Hyperwarp deletion event](https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go) \n 4.  [Notify {{site.data.keyword.hscrypto}} that the event was processed](/apidocs/hs-crypto#eventacknowledge) \n 5.  [Verify end to end deletion flow in {{site.data.keyword.cloudaccesstrailshort}} logs](/docs/observability?topic=observability-pattern1#pattern1_step4) |
| [Plan for key rotation](/docs/hs-crypto?topic=hs-crypto-dek-rewrap) | 1.  [Rotate a root key](/docs/hs-crypto?topic=hs-crypto-rotate-keys) \n 2.  [Check for a Hyperwarp rotation event from {{site.data.keyword.hscrypto}}](https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure) \n 3.  [Process Hyperwarp rotation event](https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go) \n 4.  [Notify {{site.data.keyword.hscrypto}} that the event was processed](/apidocs/hs-crypto#eventacknowledge) \n 5.  [Verify end to end rotation flow in {{site.data.keyword.cloudaccesstrailshort}} logs](/docs/observability?topic=observability-pattern1#pattern1_step4) |
| [Enable or Disable a root key](/docs/hs-crypto?topic=hs-crypto-disable-keys) | 1.  [Disable or Enable a root key](/apidocs/hs-crypto#actiononkey) \n 2.  [Check for a Hyperwarp event from {{site.data.keyword.hscrypto}}](https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure) \n 3.  [Process Hyperwarp enable or disable event](https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go) \n 4.  [Notify {{site.data.keyword.hscrypto}} that the event was processed](/apidocs/hs-crypto#eventacknowledge) \n 5.  [Verify end to end enable or disable flow in {{site.data.keyword.cloudaccesstrailshort}} logs](/docs/observability?topic=observability-pattern1#pattern1_step4) |
| [Restore a root key](/docs/hs-crypto?topic=hs-crypto-restore-keys) | 1.  [Restore a root key](/apidocs/hs-crypto#actiononkey) \n 2.  [Check for a Hyperwarp restoration event from {{site.data.keyword.hscrypto}}](https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure) \n 3.  [Process Hyperwarp restoration event](https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go) \n 4.  [Notify {{site.data.keyword.hscrypto}} that the event was processed](/apidocs/hs-crypto#eventacknowledge) \n 5.  [Verify end to end restoration flow in {{site.data.keyword.cloudaccesstrailshort}} logs](/docs/observability?topic=observability-pattern1#pattern1_step4) |
| Encryption Key Location | 1.  Your service needs to allow keys from any region to protect resources in the region where service is deployed. \n 2.  Your service needs to not enforce that the key needs to be allocated in the same region where the resource is located. |
