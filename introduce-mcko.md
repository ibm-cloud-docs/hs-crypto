---

copyright:
  years: 2021
lastupdated: "2021-10-21"

keywords: multicloud, key management, hyper protect, ekmf-web, mcko, Multicloud Key Orchestrator

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

Multicloud Key Orchestrator is a function based on IBM&reg; Enterprise Key Management Foundation - Web Edition (EKMF Web), a flexible and highly secure key management system for the enterprise.

As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, Multicloud Key Orchestrator is the first public cloud control plane for multicloud and hybrid cloud key orchestration. It provides NIST-defined states for cryptographic keys and secure transfer of keys to {{site.data.keyword.cloud_notm}}, and external keystores such as Microsoft Azure, Amazon Web Services, and Google Cloud.



## Why Multicloud Key Orchestrator?
{: #why-mcko}

Many enterprises have the legal obligation to bring their own keys when they move sensitive workloads to the cloud. Enterprises are adopting native encryption and key management offerings from cloud providers.

Dealing with multiple clouds means dealing with keys in multiple key management services. This presents the following challenges:
- High manual effort and susceptibility to errors when enterprises operate different key management systems
- No control over the [master key](#x2908413){: term} in cloud key management
- Shortage of data centers and skilled staff to operate [hardware security module (HSM)](#x6704988){: term}


As a key management service from a third-party encryption provider, {{site.data.keyword.hscrypto}} alleviates the complexity of maintaining encryption across hybrid environments. 

With Multicloud Key Orchestrator, you can integrate all your key management use cases into one consistent approach, and orchestrate your keys from one point of control, backed by a trusted IBM Z HSM. It provides you with the following features:
- Simple and consistent user experience
- Seamless integration into the existing cloud framework
- One point of control for all keys in all clouds 
- Secure backup of all keys and easy restoration across multiple clouds


## Key components
{: #key-components}


- **KMS keystore**

    The key management service component within {{site.data.keyword.hscrypto}} provides the Keep Your Own Key KMS feature for {{site.data.keyword.cloud_notm}} services to make sure that you have access to only authorized keystores.

- **EP11 keystore**

    The backing store for EP11 keys that are provided by the GREP11 API. The EP11 keystore has two purposes:
    - To serve as an internal keystore to store KMS internal keys
    - To serve as a user keystore to store user keys that are to be exposed and used by GREP11 or PKCS #11 applications

    The KMS internal keystore is a separate database schema and cannot be accessed by users through the GREP11 API.


- **Vault**

    The vault is a centralized key repository in Multicloud Key Orchestrator and backed by a separate datastore. All the keys you created or provided are persisted in the vault, and are encrypted with customer-owned HSM master keys. All user cryptographic keys are generated within the HSM with GREP11.



## Use cases
{: #use-cases}


### Push keys to external keystores
{: #push-keys}

You can bring your own keys to external keystores, such as Microsoft Azure Key Vault. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} connects to external keystores through REST APIs and retrieves all keys into the vault. You can assign, deactivate, or delete the keys, and distribute the keys back to the keystores. 


### Back up all keys of your enterprise centrally
{: #back-up-keys}

All keys are accessible and manageable on {{site.data.keyword.cloud_notm}}. When a fatal error occurs in the cloud, you can redistibute keys to quickly recover from the error.


### Orchestrate keys through one user experience across multiple clouds
{: #orchestrate-keys}

You can create and manage your keys from one point of control on {{site.data.keyword.cloud_notm}} without dealing with different user interfaces. This ensures an efficient and fully audited key lifecycle management.


### Automate key orchestration across your enterprise
{: #automate-orchestration}

Keys are created in the customer-owned service through a certified device. You can automate your key operations, for example, through the key rotation function in Azure Key Vault.



## What's next
{: #mcko-next}



(To be updated)





