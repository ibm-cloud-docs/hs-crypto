---

copyright:
  years: 2021
lastupdated: "2021-11-19"

keywords: multicloud, key management, hyper protect, ekmf-web, uko, Unified Key Orchestrator

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}


# Introducing {{site.data.keyword.uko_full_notm}}
{: #introduce-uko}

{{site.data.keyword.uko_full_notm}} is a function based on IBM&reg; Enterprise Key Management Foundation - Web Edition (EKMF Web), a flexible and highly secure key management system for the enterprise.

As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, {{site.data.keyword.uko_full_notm}} is the first public cloud control plane for multicloud and hybrid cloud key orchestration. It provides NIST-defined states for cryptographic keys and secure transfer of keys to internal keystores on {{site.data.keyword.cloud_notm}}, and external keystores such as Microsoft Azure and Amazon Web Services (AWS).



## Why {{site.data.keyword.uko_full_notm}}?
{: #why-uko}

Many enterprises have the legal obligation to bring their own keys when they move sensitive workloads to the cloud. Enterprises are adopting native encryption and key management offerings from cloud providers.

Dealing with multiple clouds means dealing with keys in multiple key management services. This presents the following challenges:
- High manual effort and susceptibility to errors when enterprises operate different key management systems
- No control over the [master key](#x2908413){: term} in cloud key management
- Shortage of data centers and skilled staff to operate [hardware security module (HSM)](#x6704988){: term}


As a key management service from a third-party encryption provider, {{site.data.keyword.hscrypto}} alleviates the complexity of maintaining encryption across hybrid environments. 

With {{site.data.keyword.uko_full_notm}}, you can integrate all your key management use cases into one consistent approach, backed by a trusted IBM Z HSM. It provides you with the following features:
- Simple and consistent user experience
- Seamless integration into the existing cloud framework
- One point of control for multiple keys in multiple clouds 
- Secure backup of all keys and easy restoration across multiple clouds


![Unified Key Orchestrator](/images/unified-key-orchestrator.svg "Unified Key Orchestrator"){: caption="Unified Key Orchestrator"  caption-side="bottom"}


## Key components
{: #key-components}

{{site.data.keyword.uko_full_notm}} has the following components:

- **Vaults**

    Vaults are used to assign access control with Identity and Access Management (IAM). A vault contains managed keys, keystores, and key templates. You need to assign a managed key to a vault when you create the key. All the keys you created or provided are encrypted with customer-owned HSM master keys.

- **Keystores**
  
    - **KMS keystore**

        The {{site.data.keyword.keymanagementservicelong_notm}} key management service component within {{site.data.keyword.hscrypto}} provides the Keep Your Own Key (KYOK) feature for {{site.data.keyword.cloud_notm}} services to ensure that you have access to only the authorized keystores. 

        You can create up to five KMS keystores free of charge. If the number reaches the limit, an additional keystore is charged $60 per calendar month.

    - **EP11 keystore**

        The backing store for EP11 keys that are provided by the GREP11 API. The EP11 keystore has two purposes:
        - To serve as an internal keystore to store internal keys
        - To serve as a user keystore to store user keys that are to be exposed and used by GREP11 or PKCS #11 applications

    The KMS internal keystore is a separate database schema and cannot be accessed by users through the GREP11 API.



## Use cases
{: #use-cases}

You can use {{site.data.keyword.uko_full_notm}} to securely create and manage your keys and keystores across multiple clouds.


### Identity and Access Management (IAM)
{: #uko-iam}

You can grant and control access to keys and keystores, so that only a distinct set of users can manage the keys.


### Manage your keys through one user experience
{: #manage-keys}

You can create, manage, and delete your cryptographic keys from one point of control, without dealing with different user interfaces. When you install a managed key in multiple keystores, the vault keeps the installations in sync. This ensures an efficient and fully audited key lifecycle management.


### Connect to external keystores
{: #connect-to-keystores}

You can connect to external keystores to manage keys in other service instances, such as Microsoft Azure Key Vault or AWS Key Management Service. {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} connects to external keystores through REST APIs and retrieves all keys into the vault. You can create, edit, or delete the keys in vaults, and install the keys back in the external keystores. 


### Back up all keys of your enterprise centrally
{: #back-up-keys}

All keys are accessible and manageable on {{site.data.keyword.cloud_notm}}. When a fatal error occurs in the cloud, you can reinstall the keys to quickly recover from the error.



## What's next
{: #uko-next}



(To be updated)





