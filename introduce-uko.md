---

copyright:
  years: 2022
lastupdated: "2022-02-11"

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

{{site.data.keyword.uko_full_notm}} is a public cloud control plane for multicloud and hybrid cloud key orchestration. As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, it provides key lifecycle management according to NIST recommendations and secure transfer of keys to internal keystores in the service instance or external keystores.


## Why {{site.data.keyword.uko_full_notm}}?
{: #why-uko}

Many enterprises have the legal obligation to bring their own cryptographic keys when they move sensitive workloads to the cloud. Enterprises are adopting native encryption and key management offerings from cloud providers.

Dealing with multiple clouds means dealing with cryptographic keys in multiple key management services. This presents the following challenges:
- High manual effort and susceptibility to errors when enterprises operate different key management systems
- No control over the [master key](#x2908413){: term} in external cloud key management systems
- Shortage of data centers and skilled staff to operate [hardware security modules (HSMs)](#x6704988){: term} for KYOK or BYOK


{{site.data.keyword.uko_full_notm}} alleviates the complexity of maintaining encryption across hybrid environments. 

You can integrate all your key management use cases into one consistent approach, backed by a trusted IBM Z HSM. It provides you with the following features:
- Consistent user experience
- Seamless integration into the existing cloud framework
- One point of control for multiple keys in multiple clouds 
- Secure backup of all keys and easy restoration across multiple clouds


![Unified Key Orchestrator](/images/unified-key-orchestrator.svg "Unified Key Orchestrator"){: caption="Unified Key Orchestrator"  caption-side="bottom"}


## Components
{: #Components}

{{site.data.keyword.uko_full_notm}} has the following components:

- **Vaults**
    
    A vault is a single repository that controls a user's or an access group's access to managed keys and target keystores through Identity and Access Management (IAM). A managed key or internal target keystore can be created only in a vault. When you connect to an external keystore, you need to assign it to a vault. To use a managed key for encryption and decryption, you need to install in one or more keystores within the same vault. The vault keeps all installations of a managed key in sync.

    - **Managed keys**
        
        A managed key is a key that is created in and assigned to a vault. You can manage the lifecycle of a managed key and install it to multiple keystores in the same vault. You can use a managed key for encryption and decryption only when it is installed in at least one target keystore. Installing a managed key in multiple keystores in the same vault enables key redundancy.  

    - **Target keystores**
        
        A target keystore is keystore that is assigned to a vault. If it is an internal keystore, it can be created only in a vault. If it is an external keystore, you need to assign the external keystore to a vault when you connect your service instance to it. 

- **Target keystores**
    
    You need to install a key to a keystore before you can encrypt or decrypt data by using the key.
    
    - **Internal keystores**
        
        An internal keystore is a keystore that is created in your {{site.data.keyword.hscrypto}} instance. 

        - **KMS keystores**
            
            The {{site.data.keyword.keymanagementservicelong_notm}} key management service component within {{site.data.keyword.hscrypto}} provides the Keep Your Own Key (KYOK) feature for {{site.data.keyword.cloud_notm}} services to ensure that you have access to only the authorized keystores. 

            You can create up to five free KMS keystores to manage your keys. If you need additional keystores for cross-region key distribution or specified access permissions, you are charged. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing).

    - **External keystores**  
        
        External keystores are keystores that are not in your service instance. You can connect to keystores that are external to your service instance, such as another {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance, potentially in another region. Or, you can connect to external keystores from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS). 

        You can connect to one external keystore at no initial cost, regardless of the type. You are charged for additional external keystores. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing).

        - **{{site.data.keyword.hscrypto}}** 
            
            You can connect your {{site.data.keyword.hscrypto}} instance to the keystores of another {{site.data.keyword.hscrypto}} instance, and manage KMS keys and EP11 keys of another service instance using the current service instance.
            
        - **{{site.data.keyword.keymanagementserviceshort}}** 
            
            {{site.data.keyword.keymanagementserviceshort}} is a service encryption solution that allows data to be secured and stored in {{site.data.keyword.cloud}} using the envelope encryption techniques that leverage FIPS 140-2 Level 3 certified cloud-based hardware security modules.           
            
        - **Azure Key Vault**   
            
            Microsoft Azure Key Vault is a cloud service for you to create and manage cryptographic keys and other sensitive information.

        - **AWS KMS**        
            
            AWS KMS is a managed service for you to create and manage cryptographic keys across a wide range of AWS services.
        

## Use cases
{: #use-cases}

You can use {{site.data.keyword.uko_full_notm}} to securely create and manage your keys and internal keystores across multiple clouds. The following is a few use cases on how you can use {{site.data.keyword.uko_full_notm}} to manage your keys.


### Identity and Access Management (IAM)
{: #uko-iam}

With IAM, you can grant and control access to the vault, and therefore the keys and keystores that are assigned to the vault.


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

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

- To find out more about the {{site.data.keyword.uko_full_notm}} API, see [{{site.data.keyword.uko_full_notm}} API reference](/apidocs/uko){: external}.






