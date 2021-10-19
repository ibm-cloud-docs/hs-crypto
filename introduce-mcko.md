---

copyright:
  years: 2021
lastupdated: "2021-10-19"

keywords: multicloud, key management, hyper protect, ekmf-web

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}


# Introducing Multicloud Key Orchestrator
{: #introduce-mcko}

The Multicloud Key Orchestrator (MCKO) is a feature based on IBM Enterprise Key Management Foundation - Web Edition (EKMF Web), a flexible and highly secure key management system for the enterprise.

As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, MCKO is the first public cloud control plane for multicloud and hybrid cloud key orchestration. It provides NIST defined states for cryptopraphic keys and secure transfer of keys to {{site.data.keyword.cloud_notm}}, and external keystores such as Microsoft Azure, Amazon AWS, and Google Cloud.


## Why Multicloud Key Orchestrator?
{: #why-mcko}

Many enterprises have the legal obligation to bring their own keys when they move sensitive workloads to the cloud. They are adopting native encryption and key management offerings from their cloud providers.

Dealing with multiple clouds means dealing with keys in multiple key management services. This presents the following challenges:
- Manual effort: High effort and susceptibility to errors when operating different key management systems
- Loss of control: No control over the [master key](#x2908413){: term} when using the hyperscalers' cloud key management solutions
- Resource intensity: Shortage of data centers and skilled staff to operate [hardware security module (HSM)](#x6704988){: term}


Key management service from third-party encryption providers alleviates the complexity of maintaining encryption across hybrid environments. 

With MCKO, you can integrate all your key management use cases into one consistent approach, and orchestrate your keys from one point of control, backed by a trusted Z HSM. It provides you with the following features:
- Simple and consistent user experience
- Seamless integration into the existing cloud framework
- One point of control for all keys in all clouds 
- Secure backup of all keys and easy restoration across multiple clouds



## How does the Multicloud Key Orchestrator work?
{: #how-mcko-work}


1. Push keys to external key store (e.g. Azure Key Vault or Key Protect) 
- Bring your own keys to Azure Key Vault (Office365®)
- Distribute with a fingertip
- Restful API interface

2. Backup all keys of the enterprise centrally
- All keys are accessible and manageable on {{site.data.keyword.cloud_notm}}
- Redistibute keys to quickly recover from fatal cloud errors
- Own your Keys


3. Orchestrate keys through one user experience across multiple clouds
- No dealing with different UIs any more
- Efficient and full audited key lifecycle management


4. Automate key orchestration across your enterprise
- Use of a certified device for Key Creation
- Keys are generated in the customer exclusively owned service
- Automate operations (e.g. Azure Key Rotation) 



## Key features
{: #key-features}


- **KMS keystore**

    The Keyprotect component within HPCS provides the BYOK KMS feature for {{site.data.keyword.cloud_notm}} services. The KP-API will be used to export/sync CRKs to the KMS keystore (internal to HPCS instance).

    The connection to KP-API passes your IAM token to do authorization checks on KP. You can have access to a specific keystore only, and not others.

- **EP11 keystore**

    The backing store for EP11 keys (provided via GREP11 API) has two purposes:
    - as an internal keystore (to store MCKO internal keys)
    - as a user keystore (to store user keys, to be exposed/used by grep11 or pkcs11 applications)

    The keys for the MCKO internal keystore is a separate DB schema and will not be accessibile by users via GREP11 API.

- **Vault**

    The Vault is the central key repository in MCKO and backed by a separate datastore. All the keys you created or provided are persisted in there, and are encrypted with customers own HSM Master Key.

    All users cryptographic keys are generated within the HSM via GREP11. As GREP11 provides a gRPC API for external users to provide Cloud HSM functionality, for MCKO internal usage an extra port is provided to be configured for the MCKO path only (mutual TLS).




## What's next
{: #mcko-next}



(To be updated)





