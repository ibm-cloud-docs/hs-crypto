---

copyright:
  years: 2021
lastupdated: "2021-10-22"

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

As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, Multicloud Key Orchestrator is the first public cloud control plane for multicloud and hybrid cloud key orchestration. It provides NIST-defined states for cryptographic keys and secure transfer of keys to internal keystores on {{site.data.keyword.cloud_notm}}, and external keystores such as Microsoft Azure and Amazon Web Services (AWS).



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


![Multicloud Key Orchestrator](/images/multicloud-key-orchestrator.svg "Multicloud Key Orchestrator"){: caption="Figure 1. Multicloud Key Orchestrator"}

![Multicloud Key Orchestrator](/images/multicloud-key-orchestrator-with-logo.svg "Multicloud Key Orchestrator"){: caption="Figure 2. Multicloud Key Orchestrator with logo"}


## Key components
{: #key-components}

Multicloud Key Orchestrator has the following components:

- **Vault**

    The vault is a centralized key repository in Multicloud Key Orchestrator and backed by a separate datastore. All the keys you created or provided are listed in the vault, and are encrypted with customer-owned HSM master keys.

- **Keystores**
  
    - **KMS keystore**

        The key management service component within {{site.data.keyword.hscrypto}} provides the Keep Your Own Key KMS feature for {{site.data.keyword.cloud_notm}} services to make sure that you have access to only authorized keystores. 
        
        The service is built on FIPS 140-2 Level 4-certified hardware, the highest security level that is offered in the industry.

    - **EP11 keystore**

        The backing store for EP11 keys that are provided by the GREP11 API. The EP11 keystore has two purposes:
        - To serve as an internal keystore to store KMS internal keys
        - To serve as a user keystore to store user keys that are to be exposed and used by GREP11 or PKCS #11 applications

        The KMS internal keystore is a separate database schema and cannot be accessed by users through the GREP11 API.

- **Key templates**

(To be updated)




## Use cases
{: #use-cases}



### Manage your keys through one user experience
{: #manage-keys}

You can create, manage, and delete your cryptographic keys from one point of control in the vault, without dealing with different user interfaces. When you install a managed key in multiple keystores, the vault keeps the installations in sync. This ensures an efficient and fully audited key lifecycle management.


### Connect to external keystores
{: #connect-keystores}

You can connect to external keystores to manage keys in other service instances, such as Microsoft Azure Key Vault or AWS Key Management Service. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} connects to external keystores through REST APIs and retrieves all keys into the vault. You can create, edit, deactivate, or delete the keys in the vault, and distribute the keys back to the external keystores. 


### Back up all keys of your enterprise centrally
{: #back-up-keys}

All keys are accessible and manageable on {{site.data.keyword.cloud_notm}}. When a fatal error occurs in the cloud, you can redistibute keys to quickly recover from the error.


### IAM
{: #iam}




## What's next
{: #mcko-next}



(To be updated)





