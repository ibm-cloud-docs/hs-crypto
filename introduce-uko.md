---

copyright:
  years: 2021
lastupdated: "2021-11-26"

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

{{site.data.keyword.uko_full_notm}} is the first public cloud control plane for multicloud and hybrid cloud key orchestration. As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, it provides key lifecycle management according to NIST recommendations and secure transfer of keys to internal keystores in {{site.data.keyword.cloud_notm}}, and external keystores in Microsoft Azure and Amazon Web Services (AWS).


## Why {{site.data.keyword.uko_full_notm}}?
{: #why-uko}

Many enterprises have the legal obligation to bring their own keys when they move sensitive workloads to the cloud. Enterprises are adopting native encryption and key management offerings from cloud providers.

Dealing with multiple clouds means dealing with keys in multiple key management services. This presents the following challenges:
- High manual effort and susceptibility to errors when enterprises operate different key management systems
- No control over the [master key](#x2908413){: term} in external cloud key management systems
- Shortage of data centers and skilled staff to operate [hardware security module (HSM)](#x6704988){: term} for KYOK or BYOK


{{site.data.keyword.uko_full_notm}} alleviates the complexity of maintaining encryption across hybrid environments. 

You can integrate all your key management use cases into one consistent approach, backed by a trusted IBM Z HSM. It provides you with the following features:
- Simple and consistent user experience
- Seamless integration into the existing cloud framework
- One point of control for multiple keys in multiple clouds 
- Secure backup of all keys and easy restoration across multiple clouds


![Unified Key Orchestrator](/images/unified-key-orchestrator.svg "Unified Key Orchestrator"){: caption="Unified Key Orchestrator"  caption-side="bottom"}


## Key components
{: #key-components}

{{site.data.keyword.uko_full_notm}} has the following components:

- **Vaults**

    A vault is a single unit that controls a user's or an access group's access to keys and keystores through Identity and Access Management (IAM). A managed key or internal keystore can be created only in a vault. When you connect to an external keystore, you need to assign it to a vault. You can install a managed key in one or more keystores in the same vault for encryption and decryption. The vault keeps all the managed keys in sync.

- **Keystores**

    {{site.data.keyword.uko_full_notm}} can manage both internal keystores, such as KMS keystores or EP11 keystores, and external keystores from an external cloud provider, such as Microsoft Azure Key Vault and AWS Key Management Service. You need to install a key to a keystore before you can encrypt or decrypt data by using the key.
    
    - **KMS keystore**

        The {{site.data.keyword.keymanagementservicelong_notm}} key management service component within {{site.data.keyword.hscrypto}} provides the Keep Your Own Key (KYOK) feature for {{site.data.keyword.cloud_notm}} services to ensure that you have access to only the authorized keystores. 

        You can create up to five free KMS keystores to manage your keys. If you need additional keystores for cross-region key distribution or specified access permissions, you are charged $60 per calendar month for an additional keystore. 

    - **EP11 keystore**

        The backing store for EP11 keys that are provided by the GREP11 API. The EP11 keystore has the following purposes:
        - To serve as an internal keystore to store internal keys.
        - To serve as a user keystore to store user keys that are to be exposed and used by GREP11 or PKCS #11 applications.


    - **External keystore**
       
        {{site.data.keyword.uko_full_notm}} supports connecting to external keystores, such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS), and creating and installing keys into these keystores.


## Use cases
{: #use-cases}

You can use {{site.data.keyword.uko_full_notm}} to securely create and manage your keys and internal keystores across multiple clouds.


### Identity and Access Management (IAM)
{: #uko-iam}

You can grant and control access to keys and keystores in a vault, so that only distinct users or access groups can manage the keys.


### Manage your keys through one user experience
{: #manage-keys}

You can create, manage, and delete your cryptographic keys from one point of control, without dealing with different user interfaces. When you install a managed key in multiple keystores in a vault, the system keeps the installations in sync. This ensures an efficient and fully audited key lifecycle management.


### Connect to external keystores
{: #connect-to-keystores}

You can connect to external keystores to manage keys in other service instances, such as Microsoft Azure Key Vault or AWS KMS.


### Back up all keys of your enterprise centrally
{: #back-up-keys}

All keys are accessible and manageable on {{site.data.keyword.cloud_notm}}. When a fatal error occurs in the cloud, you can reinstall the keys to quickly recover from the error.



## What's next
{: #uko-next}



(To be updated)





