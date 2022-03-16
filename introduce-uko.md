---

copyright:
  years: 2022
lastupdated: "2022-03-16"

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
{:note: .note}


# Introducing {{site.data.keyword.uko_full_notm}}
{: #introduce-uko}

{{site.data.keyword.uko_full_notm}} is a public cloud control plane for multicloud and hybrid cloud key orchestration. As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, it provides key lifecycle management according to NIST recommendations and secure transfer of keys to internal keystores in the service instance or external keystores.


{{site.data.keyword.uko_full_notm}} is a limited available feature for customer accounts with special approvals. If you can’t find the {{site.data.keyword.uko_full_notm}} pricing plan when you provision a service instance, it means the plan is not currently available to you. To find more information, contact the {{site.data.keyword.cloud_notm}} Sales team.
{: note}



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
    
    A vault is a repository that controls a user's or an access group's access to managed keys and target keystores through Identity and Access Management (IAM). A vault keeps all installations of a managed key in sync. You can assign a managed key or internal target keystore only in one vault. When you connect to an external keystore, you also need to assign it to a vault first. 

    You can create different vaults based on your organizational or security needs. For example, you can create a vault for each business unit. In this way, you set access control policies at a vault level, and key administrators of each business unit have access only to the keys and keystores that are assigned to the vault of their business unit.

    For more information about creating and managing access to vaults, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults) and [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

- **Managed keys**
        
    A managed key is a key that is created in and assigned to a vault. You can manage the lifecycle of a managed key and install it to multiple keystores in the same vault. You can use a managed key for encryption and decryption only when it is installed in at least one target keystore. Installing a managed key in multiple keystores in the same vault enables key redundancy. To use a managed key for encryption and decryption, install in one or more keystores within the same vault first. 

    For more information about creating managed keys, see [Creating and installing managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- **Target keystores**
        
    A target keystore is keystore that is assigned to a vault. If it is an internal keystore, it can be created only in a vault. If it is an external keystore, you need to assign the external keystore to a vault when you connect your service instance to it. 

    You need to install a key to a keystore before you can encrypt or decrypt data by using the key.       
    
    - **Internal keystores**
        
        An internal keystore is a keystore that is created in your {{site.data.keyword.hscrypto}} instance. 

        For more information about creating internal keystores, see [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores).

        - **KMS keystores**
            
            The {{site.data.keyword.keymanagementservicelong_notm}} key management service component within {{site.data.keyword.hscrypto}} provides the Keep Your Own Key (KYOK) feature for {{site.data.keyword.cloud_notm}} services to ensure that you have access to only the authorized keystores. 

            You can create up to five free KMS keystores to manage your keys. If you need additional keystores for cross-region key distribution or specified access permissions, you are charged. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing).

    - **External keystores**  
        
        External keystores are keystores that are not in your service instance. You can connect to keystores that are external to your service instance, such as another {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance, potentially in another region. Or, you can connect to external keystores from other cloud providers such as Microsoft Azure Key Vault and Amazon Web Services (AWS) Key Management Service (KMS). 

        You can connect to one external keystore at no initial cost, regardless of the type. You are charged for additional external keystores. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing).

        For more information about connecting to keystores, see [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

        - **{{site.data.keyword.hscrypto}}** 
            
            You can connect your {{site.data.keyword.hscrypto}} instance to the keystores of another {{site.data.keyword.hscrypto}} instance, and manage KMS keys and EP11 keys of another service instance using the current service instance.
            
        - **{{site.data.keyword.keymanagementserviceshort}}** 
            
            {{site.data.keyword.keymanagementserviceshort}} is a service encryption solution that allows data to be secured and stored in {{site.data.keyword.cloud}} using the envelope encryption techniques that leverage FIPS 140-2 Level 3 certified cloud-based hardware security modules.           
            
        - **Azure Key Vault**   
            
            Microsoft Azure Key Vault is a cloud service for you to create and manage cryptographic keys and other sensitive information.

        - **AWS KMS**        
            
            AWS KMS is a managed service for you to create and manage cryptographic keys across a wide range of AWS services.



## What's next
{: #uko-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).








