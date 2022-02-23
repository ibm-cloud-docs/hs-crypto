---

copyright:
  years: 2020, 2022
lastupdated: "2022-02-16"

keywords: enable KYOK, onboard to Hyper Protect Crypto Services, HPCS onboarding, service onboarding, internal registration, key registration, KYOK, kms onboarding

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:external: target="_blank" .external}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Keep Your Own Key cheatsheet
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
| [Set up the {{site.data.keyword.hscrypto}} key management API](/docs/hs-crypto?topic=hs-crypto-configure-api-test) | <ol><li>[Create a test instance](/docs/hs-crypto?topic=hs-crypto-configure-api-test#provision-instance-test)</li><li>[Create a root key](/docs/hs-crypto?topic=hs-crypto-configure-api-test#create-root-key-test)</li><li>[Wrap a data encryption key](/docs/hs-crypto?topic=hs-crypto-configure-api-test#wrap-key-test)</li><li>[Unwrap the data encryption key](/docs/hs-crypto?topic=hs-crypto-configure-api-test#unwrap-key-test)</li></ol> |
| [Map cloud resources to a root key](/docs/hs-crypto?topic=hs-crypto-register-protected-resources)  | <ol><li>[Register cloud resources](/docs/hs-crypto?topic=hs-crypto-register-protected-resources#create-registration)</li><li>[De-register cloud resources](/docs/hs-crypto?topic=hs-crypto-register-protected-resources#delete-registration)</li></ol> |

## Features
{: #kyok-features}

The following features are available for KYOK enabled services. For up-to-date information, reach out to us in the [`#hp-crypto-kms` Slack channel](https://app.slack.com/client/T02J3DPUE/CFFC7M3B3){: external}.

Use the [adopter's guide](https://github.ibm.com/kms/BYOK_Adopter_services){: external} for more information on KYOK requirements, features, and use cases.
{: note}

<table>
    <thead>
    <tr>
      <th>Actions</th>
      <th>Steps</th>
    </tr>
    </thead>
    <tbody>
    <tr>
      <td><a href="/docs/hs-crypto?topic=hs-crypto-key-erasure">Plan for crypto erasure</a></td>
      <td>
        <ol>
          <li><a href="/docs/hs-crypto?topic=hs-crypto-delete-keys">Delete a root key</a></li>
          <li><a href="https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure">Check for a Hyperwarp deletion event from {{site.data.keyword.hscrypto}}</a></li>
          <li><a href="https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go">Process Hyperwarp deletion event</a></li>
          <li><a href="/apidocs/hs-crypto#eventacknowledge">Notify {{site.data.keyword.hscrypto}} that the event was processed</a></li>
          <li><a href="/docs/observability?topic=observability-pattern1#pattern1_step4">Verify end to end deletion flow in {{site.data.keyword.cloudaccesstrailshort}} logs</a></li>
        </ol>
      </td>
    </tr>
    <tr>
      <td><a href="/docs/hs-crypto?topic=hs-crypto-dek-rewrap">Plan for key rotation</a></td>
      <td>
        <ol>
          <li><a href="/docs/hs-crypto?topic=hs-crypto-rotate-keys">Rotate a root key</a></li>
          <li><a href="https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure">Check for a Hyperwarp rotation event from {{site.data.keyword.hscrypto}}</a></li>
          <li><a href="https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go">Process Hyperwarp rotation event</a></li>
          <li><a href="/apidocs/hs-crypto#eventacknowledge">Notify {{site.data.keyword.hscrypto}} that the event was processed</a></li>
          <li><a href="/docs/observability?topic=observability-pattern1#pattern1_step4">Verify end to end rotation flow in {{site.data.keyword.cloudaccesstrailshort}} logs</a></li>
        </ol>
      </td>
    </tr>
    <tr>
      <td><a href="/docs/hs-crypto?topic=hs-crypto-disable-keys">Enable or Disable a root key</a></td>
      <td>
        <ol>
          <li><a href="/apidocs/hs-crypto#actiononkey">Disable or Enable a root key</a></li>
          <li><a href="https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure">Check for a Hyperwarp event from {{site.data.keyword.hscrypto}}</a></li>
          <li><a href="https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go">Process Hyperwarp enable or disable event</a></li>
          <li><a href="/apidocs/hs-crypto#eventacknowledge">Notify {{site.data.keyword.hscrypto}} that the event was processed</a></li>
          <li><a href="/docs/observability?topic=observability-pattern1#pattern1_step4">Verify end to end enableor disable flow in {{site.data.keyword.cloudaccesstrailshort}} logs</a></li>
        </ol>
      </td>
    </tr>
    <tr>
      <td><a href="/docs/hs-crypto?topic=hs-crypto-restore-keys">Restore a root key</a></td>
      <td>
        <ol>
          <li><a href="/apidocs/hs-crypto#actiononkey">Restore a root key</a></li>
          <li><a href="https://github.ibm.com/kms/BYOK_Adopter_services/blob/master/How_to_subscribe_to_hyperwarp.md#event-structure">Check for a Hyperwarp restoration event from {{site.data.keyword.hscrypto}}</a></li>
          <li><a href="https://github.ibm.com/kms/Adopter_services/blob/master/src/github.ibm.com/skms/key-protect/event_processor.go">Process Hyperwarp restoration event</a></li>
          <li><a href="/apidocs/hs-crypto#eventacknowledge">Notify {{site.data.keyword.hscrypto}} that the event was processed</a></li>
          <li><a href="/docs/observability?topic=observability-pattern1#pattern1_step4">Verify end to end restoration flow in {{site.data.keyword.cloudaccesstrailshort}} logs</a></li>
        </ol>
      </td>
    </tr>
    <tr>
      <td>Encryption Key Location</td>
      <td>
        <ol>
          <li>Your service needs to allow keys from any region to protect resources in the region where service is deployed.</li>
          <li>Your service needs to not enforce that the key needs to be allocated in the same region where the resource is located.</li>
        </ol>
      </td>
    </tr>
    </tbody>
</table>