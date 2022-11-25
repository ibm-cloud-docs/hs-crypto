---

copyright:
  years: 2022
lastupdated: "2022-11-25"

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}
{:note: .note}


# Introducing {{site.data.keyword.uko_full_notm}}
{: #introduce-uko}

With {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}, you can manage keys not only for your internal keystores, but across multiple cloud providers, including Microsoft Azure, Amazon Web Services (AWS), and Google Cloud Platform. All your keys in all those places are protected by your own master key, which is stored in a FIPS 140-2 Level 4-certified hardware security module (HSM) for the highest security. You can manage the lifecycles of your keys from a single point of control, while the system keeps keys that are distributed in sync.

With {{site.data.keyword.uko_full_notm}}, you can organize everything in vaults. *Vaults* are secure repositories that bundle your managed keys and the target keystores to distribute managed keys to. You can use vaults to grant access to different Identity and Access Management (IAM) user groups.

## Use case example
{: #uko-use-case-example}

In the following example, your retail banking business unit, reflected as one user group, uses a vault called `Retail Banking BU`. Another business unit, reflected as another user group, uses their own vault to keep their managed keys and target keystores separate.

You connect vault `Retail Banking BU` to three external keystores in different locations, in this example, three Azure Key Vaults. You can also connect your vault to other external keystore types if needed, such as AWS Key Management Service, {{site.data.keyword.keymanagementservicelong}}, or other {{site.data.keyword.hscrypto}} instances. Then, you create managed keys in vault `Retail Banking BU` and distribute the keys to those three external keystores in Azure.

For development and test purposes, you create a few more keys in the same vault and an internal KMS keystore to distribute the keys to.

You activate a key in multiple internal or external keystores in the same vault. When you make changes to the key, for example, changing the key state from Active to Deactivated, the change is applied to all keystores that the key is activated in.

![{{site.data.keyword.uko_full_notm}} use case example](/images/uko-example.png "Illustration that explains how to use vault to manage access while connecting to external Azure Key Vaults"){: caption="Figure 1. {{site.data.keyword.uko_full_notm}} use case example"  caption-side="bottom"}

## Components
{: #Components}

The following list includes the key components of {{site.data.keyword.uko_full_notm}}. For an architectural diagram that includes key {{site.data.keyword.hscrypto}} components, see [Service architecture](/docs/hs-crypto?topic=hs-crypto-uko-architecture-workload-isolation).

- **Vaults**
    
    A vault is a repository that controls a user's or an access group's access to managed keys and target keystores through IAM. A vault keeps all activations of a managed key in sync. You can assign a managed key or target keystore only in one vault. When you connect to an external keystore, you also need to assign it to a vault first. 

    You can create different vaults based on your organizational or security needs. For example, you can create a vault for each business unit. In this way, you set access control policies at a vault level, and key administrators of each business unit have access only to the keys and keystores that are assigned to the vault of their business unit.

    For more information about creating and managing access to vaults, see [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults) and [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).

- **Managed keys**
        
    A managed key is a key that is created in and assigned to a vault. You can manage the lifecycle of a managed key and activate it in multiple keystores in the same vault. You can use a managed key for encryption and decryption only when it is activated in at least one target keystore. Activating a managed key in multiple keystores in the same vault enables key redundancy. To use a managed key for encryption and decryption, activate it in one or more keystores within the same vault first. 

    For more information about creating managed keys, see [Creating and activating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- **Target keystores**
        
    A target keystore is keystore that is assigned to a vault. You need to create an internal keystore in only one vault, or assign an external keystore to a vault when you connect your service instance to it. 

    You need to activate a key in a keystore before you can encrypt or decrypt data by using the key.       
    
    - **Internal keystores**
        
        An internal keystore is a keystore that is created in your {{site.data.keyword.hscrypto}} instance. 

        For more information about creating internal keystores, see [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores).

        - **KMS keystores**
            
            The key management service component within {{site.data.keyword.hscrypto}} provides the Keep Your Own Key (KYOK) feature for {{site.data.keyword.cloud_notm}} services to ensure that you have access to only the authorized keystores. 

            You can create up to five free KMS keystores to manage your keys. If you need additional keystores for cross-region key distribution or specified access permissions, you are charged. For more information about the pricing, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing).

    - **External keystores**  
        
        External keystores are keystores that are not in your service instance. You can connect to keystores that are external to your service instance, such as another {{site.data.keyword.hscrypto}} or {{site.data.keyword.keymanagementserviceshort}} instance, potentially in another region. Or, you can connect to external keystores from other cloud providers such as  Key Vault, AWS Key Management Service (KMS), and Google Cloud KMS. 

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
        
        - **Google Cloud KMS**

            Google Cloud KMS is a centralized cloud service for you to create and manage cryptographic keys. You can perform cryptographic operations by using keys in Google Cloud KMS, or by integrating with other Google Cloud services such as Cloud HSM.
        
        

## What's next
{: #uko-next}

- To find out instructions on creating a managed key, check out [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

- To find out instructions on adding a keystore, check out [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores) or [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores).

- To find out how to grant access to vaults, see [Granting access to vaults](/docs/hs-crypto?topic=hs-crypto-grant-access-vaults).


- To find out more about the {{site.data.keyword.uko_full_notm}} API, see [{{site.data.keyword.uko_full_notm}} API reference](/apidocs/uko){: external}.







