---

copyright:
  years: 2018, 2025
lastupdated: "2025-07-11"

keywords: release note, new, changelog, what's new, service updates, service bulletin

subcollection: hs-crypto

content-type: release-note

---


{{site.data.keyword.attribute-definition-list}}




# Release notes for {{site.data.keyword.hscrypto}}
{: #what-new}

Stay up to date with the new features that are available for {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}



## 18 July 2024
{: #hs-crypto-july182024}
{: release-note}

Updated: Transition to VPC data centers in Dallas, Washington D.C, and Frankfurt
:   {{site.data.keyword.hscrypto}} will be transitioning out of {{site.data.keyword.cloud_notm}} classic data centers in Dallas (`DAL`), Washington D.C (`WDC`), and Frankfurt (`FRA`) to {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) data centers in those respective locations allowing you to take advantage of the new product features and capabilities that VPC offers.

    Implications for current users:    
    
    The transition to VPC data centers will be a service/technology upgrade with the user experience remaining unchanged. Minimal customer interaction is required to complete the transition. There is minimal impact to clients.  
    
    Support from the IBM Team is available to ensure the successful deployment of your instances in the VPC data centers, contact your local sales representative or send an email to [zaas.client.acceleration@ibm.com](mailto:zaas.client.acceleration@ibm.com) for more information.
    {: note}

    Key dates for this transition:
    
    - For existing instances in `DAL` and `WDC`, customer migration will be **August 22, 2024** – **January 31, 2025**. Support remains uninterrupted throughout migration process. After **January 31, 2025**, the services in `DAL` and `WDC` data centers will be decommissioned and no longer available. All non-migrated instances and existing data still present in the `DAL` and `WDC` data centers will be terminated after this date.

    - For existing instances in `FRA`, customer migration will be **August 15, 2024** – **January 31, 2025**. Support remains uninterrupted throughout migration process. After **January 31, 2025**, the services in `FRA` data center will be decommissioned and no longer available. All non-migrated instances and existing data still present in the `FRA` data center will be terminated after this date.

## 15 July 2024
{: #hs-crypto-july152024}
{: release-note}

Updated: New API endpoints in Frankfurt
:   If you create your instances in Frankfurt after July 15, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).

## 2 July 2024
{: #hs-crypto-july22024}
{: release-note}

Updated: New API endpoints in Madrid
:   If you create your instances in Madrid after July 2, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).

## 19 June 2024
{: #hs-crypto-june192024}
{: release-note}

Updated: New API endpoints in Tokyo
:   If you create your instances in Tokyo after June 19, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).

## 18 June 2025
{: hs-crypto-june182025}
{: release-note}
[New]{: tag-new}: Context Based Restrictions support  
:   Context Based Restrictions (CBR) enables extra protection on {{site.data.keyword.cloud_notm}} resources. Essentially, it wraps around IAM polices allowing an admin or account owner configure network rules for the resource/endpoint and network zones to allow/disallow IPs for end user access. With added support of CBR in {{site.data.keyword.hscrypto}}, you can enforce these rules while utilizing your {{site.data.keyword.hscrypto}} instance. For more information, see [Protecting {{site.data.keyword.hscrypto}} resources with context-based restrictions](/docs/hs-crypto?topic=hs-crypto-cbr).

## 5 June 2024
{: #hs-crypto-june2024}
{: release-note}



Updated: New API endpoints in London
:   If you create your instances in London after June 5, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).

## 29 May 2024
{: #hs-crypto-may292024}
{: release-note}

Updated: New API endpoints in Toronto
:   If you create your instances in Toronto after May 29, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).


## 15 May 2024
{: #hs-crypto-may152024}
{: release-note}

Updated: New API endpoints in S&atilde;o-Paulo
:   If you create your instances in S&atilde;o-Paulo after May 15, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).

## 8 May 2024
{: #hs-crypto-may2024}
{: release-note}

Updated: New API endpoints in Dallas
:   If you create your instances in Dallas after May 8, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).

## 12 April 2024
{: #hs-crypto-apr2024}
{: release-note}

Updated: New API endpoints in Washington DC
:   If you create your instances in Washington DC after April 12, you need to use the new API endpoints for operations against your new instances. For more information about the supported regions and the new endpoint URLs, see [New endpoints](/docs/hs-crypto?topic=hs-crypto-regions#new-service-endpoints).

## 29 February 2024
{: #hs-crypto-feb2024}

Added: New key state `pending destruction` 
:   After you move a key from Deactivated to Destroyed state, the key will first be pending on destruction for a time period defined by the destruction policies of the external cloud providers. When the time period ends, the key will be moved to Destroyed state. For any pending destruction keys, a pending flag is displayed in the corresponding key card or the key list. For more information, see [Monitoring the lifecycle of encryption keys in Unified Key Orchestrator](/docs/hs-crypto?topic=hs-crypto-uko-key-states).

Added: Connecting to Azure Key Vault through private endpoint
:   You can use {{site.data.keyword.uko_full_notm}} to connect to Azure Key Vault through the private endpoint with the UI, or programmatically with the {{site.data.keyword.uko_full_notm}} API. With establishing a private connection between {{site.data.keyword.uko_full_notm}} and Azure Key Vault, exposing your service to the public internet is no longer necessary. For more information, see [Connecting to Azure Key Vault through private endpoint](/docs/hs-crypto?topic=hs-crypto-connect-azure-key-vault-private-endpoint&interface=ui).

## 18 January 2024
{: #hs-crypto-jan2024}
{: release-note}

Added: Azure software-protected key support for {{site.data.keyword.cloud_notm}}
:   Besides HSM-protected keys, software-protected keys can now also be created in Azure Key Vault (Premium) keystores of {{site.data.keyword.uko_full_notm}}. However, you can still create and distribute only software-protected keys to Azure Key Vault (Standard). For more information, see [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys) and [Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template).

## 09 November 2023
{: #hs-crypto-nov2023}
{: release-note}

Added: {{site.data.keyword.hscrypto}} adds support for Bring Your Own HSM (BYOHSM)
:   BYOHSM extends your local key management capability to the cloud and creates a scalable, unified, and secure hybrid cloud ecosystem for your regulated workloads. By connecting your own HSMs to your {{site.data.keyword.hscrypto}} instance, you have complete physical control over your keys to meet the data sovereignty regulations.

    The following topics can help you get started with the BYOHSM function:
    
    * [Introducing Bring Your Own HSM](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm)
    * [Managing your keys with BYOHSM in IBM Cloud Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-tutorial-byohsm)
    * [Setting up BYOHSM](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm)
    * [Provisioning an instance with BYOHSM](/docs/hs-crypto?topic=hs-crypto-provision&interface=ui#provision-standard)

## 26 October 2023
{: #hs-crypto-26oct2023}
{: release-note}

Deprecated: {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} in Sydney
:   {{site.data.keyword.hscrypto}} and [{{site.data.keyword.hpvs}} for Classic](/docs/hp-virtual-servers?topic=hp-virtual-servers-whats-new#hp-virtual-servers-oct2623) will be deprecated from the IBM Cloud data center in `Sydney`. New instances of Hyper Protect Services can no longer be deployed in the IBM Cloud data center in `Sydney` after **30 November 2023**, and existing Hyper Protect services and support in the IBM Cloud data center in Sydney will be decommissioned and discontinued on **31 March 2024**.

:   This announcement does not impact any other services running in the IBM Cloud data center in Sydney, or any other Hyper Protect Services, including support, running in any other data centers where Hyper Protect is supported.
{: note}

:   Review the following details for this deprecation:

    - Effective **30 November 2023**, no new instances of {{site.data.keyword.hscrypto}} or Hyper Protect Virtual Servers for Classic can be provisioned in `Sydney`.
    - Effective **31 March 2024**, {{site.data.keyword.hscrypto}} and {{site.data.keyword.hpvs}} for Classic will no longer be supported, and the services will be decommissioned from the IBM Cloud data center in `Sydney`. It is recommended that all instances and data be migrated to an IBM Cloud VPC data center.
    - Any Hyper Protect Services instances and data still present in the IBM Cloud data center in `Sydney` will be stopped and terminated on this date. The data center infrastructure will be decommissioned and data and services no longer available. To avoid the risk of data loss, ensure a backup or transfer of any required data is taken before the service is decommissioned on **31 March 2024**. 

:   For existing customers, migration to an IBM Cloud VPC data center is recommended:

    - To continue using {{site.data.keyword.hscrypto}}, it is recommended to migrate to an IBM Cloud VPC data center. The recommended region for migration within APAC is `Tokyo`.
    - For {{site.data.keyword.hpvs}} for Classic instances, it is recommended to migrate to an IBM Cloud VPC data center, as well as deploy the latest version of the service, [{{site.data.keyword.hpvs}} for VPC](https://www.ibm.com/cloud/hyper-protect-virtual-servers){: external} ({{site.data.keyword.hpvs}} for Classic is not available in IBM Cloud VPC data centers). The recommended region for migration within APAC is `Tokyo`.
    - To migrate to an IBM Cloud VPC Data center, support from IBM Team will be available. Contact your local sales representative or send an email to [zaas.client.acceleration@ibm.com](mailto:zaas.client.acceleration@ibm.com) for more information.

:   The following table lists the supported {{site.data.keyword.cloud_notm}} VPC data centers for {{site.data.keyword.hscrypto}} and Hyper Protect Virtual Servers for Classic:

    | Data center | {{site.data.keyword.hscrypto}} | Hyper Protect Virtual Servers for Classic |
    |--------------|--------------|--------------|
    | Tokyo (Recommended region within APAC) `jp-tok` | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark") | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | 
    | S&atilde;o-Paulo `br-sao` | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | 
    | London `eu-gb`  | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | 
    | Toronto `ca-tor`   | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | 
    | Madrid `eu-es`     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")     | 
    | Washington DC `us-east`   | N/A    |  ![checkmark icon](../icons/checkmark-icon.svg "Checkmark")    |  
    {: caption="Supported {{site.data.keyword.cloud_notm}} VPC data centers" caption-side="bottom"}

## 22 Sept 2023
{: #hs-crypto-sept2023}
{: release-note}

Added: {{site.data.keyword.hscrypto}} expands into the Madrid region 
:   You can now create {{site.data.keyword.hscrypto}} instances in the Madrid (`eu-es`) region where the infrastructure is based on {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 3 August 2023
{: #hs-crypto-august2023}
{: release-note}

Added: Key template support for {{site.data.keyword.uko_full_notm}} 
:   You are now able to create key templates which specify the properties of the managed keys to be created. After you create the key template, you can then create a group of managed keys with the same key properties that are defined in the key template.

    The following topics can help you get started with key templates:

    * [Creating key templates](/docs/hs-crypto?topic=hs-crypto-create-template)
    * [Viewing a list of key templates](/docs/hs-crypto?topic=hs-crypto-view-key-template)
    * [Editing key template details](/docs/hs-crypto?topic=hs-crypto-edit-template)
    * [Archiving and unarchiving key templates](/docs/hs-crypto?topic=hs-crypto-archive-template)
    * [Deleting key templates](/docs/hs-crypto?topic=hs-crypto-delete-template)
    * [Realigning keys with key templates](/docs/hs-crypto?topic=hs-crypto-align-key)

## 1 June 2023
{: #hs-crypto-june2023}
{: release-note}

Updated: Pricing plan for {{site.data.keyword.uko_full_notm}} 
:   The pricing plan has been updated for {{site.data.keyword.uko_full_notm}}. You can find more details on the [service catalog page](/catalog/services/hyper-protect-crypto-services){: external}.  

    For a detailed pricing sample, see [How am I charged for my use of {{site.data.keyword.hscrypto}} with Unified Key Orchestrator?](/docs/hs-crypto?topic=hs-crypto-faq-pricing&interface=ui#faq-how-charge-hpcs-uko). 

## 24 May 2023
{: #hs-crypto-may2023}
{: release-note}

Updated: Master key rotation support for all regions
:   You are now able to rotate master keys when you are using the Unified Key Orchestrator service plan or your service instance that has EP11 keystores enabled in all supported regions. Previously, it was only available in Frankfurt, Germany.

    For a list of supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions&interface=ui). For more information about how master key rotation works, see [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro). 
    

## 24 March 2023
{: #hs-crypto-march2023}
{: release-note}

Added: Master key rotation for {{site.data.keyword.uko_full_notm}}
:   You can now rotate master keys on demand to meet industry standards and cryptographic best practices in your {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} instance. You can understand how keys are protected during master key rotation and use the UI to view the progress. For more information about how master key rotation works, see [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro).


Added: Master key rotation for EP11 keystores
:   You are now able to rotate master keys when your service instance has EP11 keystores enabled. Previously, this function is not available.

## 1 Feb 2023
{: #hs-crypto-feb2023}
{: release-note}

Added: {{site.data.keyword.hscrypto}} key management functions 
:   The {{site.data.keyword.hscrypto}} key management service API is updated to version `22.11`. The following functions are added:

    - [List Keys with sorting](/apidocs/hs-crypto#:~:text=values%3A%20length%20≤%20256-,sort,-string){: external} to include lastRotateDate sorting.
    - [List Keys with advanced filtering](/apidocs/hs-crypto#:~:text=Default%3A%20id-,filter,-string){: external} to including lastRotateDate filtering.
    - [Create key with policy overrides](https://cloud.ibm.com/apidocs/hs-crypto#createkeywithpoliciesoverrides){: external} to enable users with Manager role to create keys with policies in a single call, overriding instance level policies.
    - [Disable a key rotation policy](/apidocs/hs-crypto#:~:text=policy%2Bjson%22%2C%0A%20%20%20%20%20%20%20%20%22rotation%22%3A%20%7B%0A%20%20%20%20%20%20%20%20%20%20%22-,enabled,-%22%3A%20%3Ctrue%7Cfalse%3E%2C%0A%20%20%20%20%20%20%20%20%20%20%22interval_month){: external} to allow an automatic key rotation policy to be paused temporarily.

Added: Activity Tracker event names
:    Find the latest event names and mapping in [Historical information regarding events](/docs/hs-crypto?topic=hs-crypto-at-events&interface=ui#historical-mapping-events).


## 19 December 2022
{: #hs-crypto-dec2022}
{: release-note}

Added: Managed key rotation support for {{site.data.keyword.uko_full_notm}}
:   You can now manually rotate a managed key in your {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} instance. Managed key rotation shortens the cryptoperiod of the keys and reduces the probability for a security breach. For more information about how managed key rotation works, see [Managed key rotation](/docs/hs-crypto?topic=hs-crypto-managed-key-rotation-intro). For more information about the detailed instructions, see [Rotating managed keys manually](/docs/hs-crypto?topic=hs-crypto-uko-rotate-keys).


## 21 November 2022
{: #hs-crypto-nov2022}
{: release-note}

Added: Management Utilities support for Red Hat Enterprise Linux 9.0 and Ubuntu 22.04.1 LTS
:    To manage your master keys by using smart cards, you can now install the smart card reader driver Identiv SPR332 V2 on Red Hat Enterprise Linux 9.0 and Ubuntu 22.04.1 LTS besides the already supported Red Hat Enterprise Linux 8.0 operating system. For more detailed steps, see [Installing the smart card reader driver](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver).

    You can also find the latest Management Utilities installation files in [Github](https://github.com/IBM-Cloud/hpcs-management-utilities/releases/tag/v1.0.3.8){: external}.


## 31 October 2022
{: #hs-crypto-31oct2022}
{: release-note}

Added: Google Cloud KMS support
:   You can now use {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} to create and manage Google Cloud KMS keys. For more information, see [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores) and [Creating managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).

## 20 October 2022
{: #hs-crypto-20oct2022}
{: release-note}

Added: EP11 activity tracker events
:   Both {{site.data.keyword.hscrypto}} Standard Plan and {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} now support Enterprise PKCS #11 (EP11) events tracking. You can use IBM Cloud Activity Tracker to monitor EP11 activities and analyze successful events. For more information, see [Auditing events for {{site.data.keyword.hscrypto}} - Standard Plan](/docs/hs-crypto?topic=hs-crypto-at-events) and [Auditing events for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-at-events).

## 24 June 2022
{: #hs-crypto-24june2022}
{: release-note}

Added: Go SDK and Terraform support for {{site.data.keyword.uko_full_notm}}
:  You can now manage your keys by using the {{site.data.keyword.uko_full_notm}} API with the Go software development kit (SDK) enabled. For more code examples in Go, see [{{site.data.keyword.uko_full_notm}} API reference](/apidocs/uko?code=go).

    With the Terraform support for {{site.data.keyword.uko_full_notm}}, you can now automate actions, such as managing vaults, keystores, key templates, and keys, by using Terraform. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-terraform-setup-for-hpcs).

## 8 June 2022
{: #hs-crypto-8june2022}
{: release-note}

Added: Post-quantum cryptography support {: #add-pqc}
:   With the GREP11 API and the PKCS #11 API, you can now perform [post-quantum cryptographic](https://en.wikipedia.org/wiki/Post-quantum_cryptography){: external} operations to protect your data against attacks from quantum computers. Currently, we support the Dilithium algorithm. For more information, see [Post-quantum cryptography support in GREP11](/docs/hs-crypto?topic=hs-crypto-grep11-intro#grep11-support-post-quantum) and [Post-quantum cryptography support in PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro#grep11-support-post-quantum).

## 3 June 2022
{: #hs-crypto-3june2022}
{: release-note}

Added: {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} CLI plug-in {: #add-uko-cli}
:   With the command-line interface (CLI) support for {{site.data.keyword.hscrypto}} with the {{site.data.keyword.uko_full_notm}} plan, you can now manage vaults, keystores, and keys by using CLI commands. For more information about these commands, see [{{site.data.keyword.uko_full_notm}} CLI plug-in reference](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#uko-cli-plugin).


## 1 April 2022
{: #hs-crypto-1april2022}
{: release-note}

Updated: Pricing model of the {{site.data.keyword.hscrypto}} standard plan {: #update-pricing-model}
:   The pricing model of the {{site.data.keyword.hscrypto}} standard plan is now changed from monthly billing to hourly billing with each crypto unit charged $2.13 USD per hour. 

    The first five keystores, including KMS key rings and EP11 keystores, are free of charge. Each additional key ring or EP11 keystore is charged with a tiered pricing starting at $225 USD per month. For keystores that are created or connected less than a month, the cost is prorated based on actual days within the month.

    For more information, see the [pricing plan](/catalog/services/hyper-protect-crypto-services){: external}. A [billing example](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-how-charge-hpcs) is also available for your reference.

Updated: Process of ordering smart cards and smart card readers {: #update-smartcard-procurement}
:   To order smart cards and smart card readers, you can now email IBM at `zcat@ibm.com@ibm.com` and provide necessary information. For detailed steps, see [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#order-smart-card-and-reader).

## 25 March 2022
{: #hs-crypto-25mar2022}
{: release-note}

Added: {{site.data.keyword.hscrypto}} expands into the Toronto region {: #add-toronto-region}
:   You can now create {{site.data.keyword.hscrypto}} instances in the Toronto (`ca-tor`) region where the infrastructure is based on {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 22 March 2022
{: #hs-crypto-march2022}
{: release-note}

General availability: Using {{site.data.keyword.uko_full_notm}} to manage and orchestrate keys in a multicloud environment 
:   {{site.data.keyword.uko_full_notm}} is a public cloud control plane for multicloud and hybrid cloud key orchestration. As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, it provides key lifecycle management according to NIST recommendations and secure transfer of keys to internal keystores in the service instance or external keystores.

    With {{site.data.keyword.uko_full_notm}}, you can connect your service instance to keystores in IBM Cloud and third-party cloud providers, back up and manage keys by using a unified system, and orchestrate keys across multiple clouds.

    The following topics can help you get started with {{site.data.keyword.uko_full_notm}}:

    * [Introducing {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-introduce-uko)
    * [FAQs: {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-faq-uko)
    * [Getting started with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started)
    * [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states)
    * [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults)
    * [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores)
    * [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores)
    * [Creating and installing managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys)


## 28 February 2022
{: #hs-crypto-28feb2022}
{: release-note}

Limited availability: Using {{site.data.keyword.uko_full_notm}} to manage and orchestrate keys in a multicloud environment {: #add-uko} 
:   {{site.data.keyword.uko_full_notm}} is a public cloud control plane for multicloud and hybrid cloud key orchestration. As part of the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, it provides key lifecycle management according to NIST recommendations and secure transfer of keys to internal keystores in the service instance or external keystores.

    With {{site.data.keyword.uko_full_notm}}, you can connect your service instance to keystores in IBM Cloud and third-party cloud providers, back up and manage keys by using a unified system, and orchestrate keys across multiple clouds.

    The following topics can help you get started with {{site.data.keyword.uko_full_notm}}:

    * [Introducing {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-introduce-uko)
    * [FAQs: {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-faq-uko)
    * [Getting started with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-get-started)
    * [Monitoring the lifecycle of encryption keys in {{site.data.keyword.uko_full_notm}}](/docs/hs-crypto?topic=hs-crypto-uko-key-states)
    * [Creating vaults](/docs/hs-crypto?topic=hs-crypto-create-vaults)
    * [Creating internal keystores](/docs/hs-crypto?topic=hs-crypto-create-internal-keystores)
    * [Connecting to external keystores](/docs/hs-crypto?topic=hs-crypto-connect-external-keystores)
    * [Creating and installing managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys)


## 23 February 2022
{: #hs-crypto-23feb2022}
{: release-note}

Added: Using {{site.data.keyword.mon_full_notm}} to measure {{site.data.keyword.hscrypto}} metrics {: #add-monitoring-metrics}
:   By enabling metrics instance policy, you can now use {{site.data.keyword.mon_full_notm}} to measure how users and applications interact with {{site.data.keyword.hscrypto}}. For more information, see [Managing metrics](/docs/hs-crypto?topic=hs-crypto-manage-monitoring-metrics) and [Monitoring operational metrics](/docs/hs-crypto?topic=hs-crypto-operational-metrics).

## 15 February 2022
{: #hs-crypto-15feb2022}
{: release-note}

Added: {{site.data.keyword.hscrypto}} expands into the S&atilde;o-Paulo region {: #add-sao-region}
:   You can now create {{site.data.keyword.hscrypto}} instances in the S&atilde;o-Paulo (`br-sao`) region where the infrastructure is based on {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 21 January 2022
{: #hs-crypto-jan2022}
{: release-note}

Updated: {{site.data.keyword.hscrypto}} key management functions {: #update-kms-api-v282}
:   The {{site.data.keyword.hscrypto}} key management service API is updated to version `2.82`. The following functions are added:
    1. **Purge a deleted key**: 
        By default, a deleted key becomes purged automatically after 90 days of the deletion. Now you can manually purge a key to permanently remove the key from your instance before 90 days. After a key is deleted, there is a wait period of up to 4 hours before you can perform the action. Make sure that you are assigned the _KMS Key Purge_ role before you purge a key. For more information, see [Purging keys manually](/docs/hs-crypto?topic=hs-crypto-purge-keys).
    2. **Update the key ring of a key**: 
        After you create a key, you can move the key to a different key ring. For more information, see [Transferring a key to a different key ring](/docs/hs-crypto?topic=hs-crypto-managing-key-rings#transfer-key-key-ring).

## 30 July 2021
{: #hs-crypto-july2021}
{: release-note}

Added: Exclusive control on the execution of cryptographic operations {: #add-cert-manager}
:   To ensure the exclusive control on the execution of cryptographic operations, you can use the {{site.data.keyword.hscrypto}} certificate manager CLI to enable the second layer of authentication for EP11 (GREP11 or PKCS #11 API) connections. By enabling this function, you enable an extra layer of access control on top of the Identity and Access Management (IAM) token to the EP11 applications. A mutual TLS connection is established to ensure that only EP11 applications with a valid client certificate can perform EP11 operations. For more information, see [Enabling the second layer of authentication for EP11 connections](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11)

Added: {{site.data.keyword.hscrypto}} expands into the Tokyo region {: #add-tokyo-region}
:   You can now create {{site.data.keyword.hscrypto}} instances in the Tokyo (`jp-tok`) region where the infrastructure is based on {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

Added: Using Terraform to initialize the {{site.data.keyword.hscrypto}} instance {: #add-terraform-automation}
:   With the integration with Terraform, now you can initialize your service instance by using Terraform, and then automate actions by using Terraform. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs) and the [Terraform documentation - Hyper Protect Crypto Services](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs/resources/hpcs){: external}.

Added: Using a signing service to manage signature keys for instance initialization {: #add-signing-service}
:   If you are using Terraform or key part files to initialize a service instance, you can now choose to use a third-party signing service to create, store, and manage the administrator signature keys that are used by Terraform or the Trusted Key Entry (TKE) CLI plug-in. For more information, see [Using a signing service to manage signature keys for instance initialization](/docs/hs-crypto?topic=hs-crypto-signing-service-signature-key).

## 30 June 2021
{: #hs-crypto-june2021}
{: release-note}

Added: Authenticated PKCS #11 keystore {: #add-authenticated-pkcs11-keystore}
:   The PKCS #11 database-backed keystores can now be encrypted and authenticated. For each service instance, a maximum of five authenticated PKCS #11 keystores are supported. You can enable the `sessionauth` parameter to encrypt the generated keys into the keystore or to decrypt the key before you use it. For more information, see [Set up the PKCS #11 configuration file](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file).

Added: Enabling cross-region recovery with failover crypto units {: #add-failover-crypto-units}
:   Failover crypto units back up the operational crypto units and keystores in another region. When a regional disaster occurs, you can use failover crypto units instead to reduce the downtime and data loss. Failover crypto units [charge extra fees](/docs/hs-crypto?topic=hs-crypto-faq-pricing) and this option is now available only in regions of `us-south` and `us-east`. For more information, see [Enabling or adding failover crypto units](/docs/hs-crypto?topic=hs-crypto-enable-add-failover) and [Cross-region disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr#cross-region-disaster-recovery).

Added: {{site.data.keyword.hscrypto}} expands into the London region {: #add-london-region}
:   You can now create {{site.data.keyword.hscrypto}} instances in the London (`eu-gb`) region where the infrastructure is based on {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 30 April 2021
{: #hs-crypto-april2021}
{: release-note}

Added: Rotating your master key by using smart cards and the Management Utilities {: #add-master-key-rotation-smart-cards}
:   Besides rotating your master key [using key part files](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part) and [using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit), you can now also rotate the master key if you are using smart cards and the Management Utilities.

    For detailed instructions, see [Rotating master keys by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-smart-cards). For more information about how master key rotation works, see [Rotating master keys by using key part files](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro#how-master-key-rotation-works-use-key-part-files).

Updated: Restore key API and UI {: #update-restore-key-api-ui}
:   Now you can restore keys that were deleted within 30 days without providing any key materials. All root keys and standard keys, whether generated by {{site.data.keyword.hscrypto}} or imported by you, can be restored. For more information, see [Restoring keys](/docs/hs-crypto?topic=hs-crypto-restore-keys).

## 31 March 2021
{: #hs-crypto-march2021}
{: release-note}

Added: Grouping keys by using key rings {: #add-key-ring}
:   You can now group the keys in your {{site.data.keyword.hscrypto}} instance by creating a key ring. In this case, you can manage keys and control access at the key ring level. For how to use key rings, see [Managing key rings](/docs/hs-crypto?topic=hs-crypto-managing-key-rings).

Added: Initializing the service instance by using recovery crypto units {: #add-recovery-crypto-units}
:   Besides using smart cards and the Hyper Protect Crypto Services Management Utilities and using key part files, you can now also initialize your service instance by using recover crypto units in the Dallas (`us-south`) and Washington DC (`us-east`) regions.

    When you provision a service instance in either of the Dallas or Washington DC region, two recovery units are automatically assigned without extra costs. A random master key value is automatically generated in a recovery crypto unit and copied to the other crypto units for the service instance. The master key value never appears in the clear outside of the HSMs.

    For more information about the differences between the service instance initialization approaches, see [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit).

    For detailed instructions, see [Initializing service instances with recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit).

    To rotate your master key, see [Rotating master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit).

Added: Managing EP11 keystores and keys with the UI {: #add-ep11-keystores-keys-console}
:   Apart from using the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) to manage Enterprise PKCS #11 (EP11) keystores and keys, you can now use the UI to view, create, and delete EP11 keystores and keys. For more information, see [Managing EP11 keystores with the UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-keystores-ui) and [Managing EP11 keys with the UI](/docs/hs-crypto?topic=hs-crypto-manage-ep11-key-ui).

Added: Managing key aliases for a key {: #add-key-alias}
:   Key aliases are unique human-readable names that can be used to identify a key. You can now create up to five aliases for a key for easy recognition. For how to use key aliases, see [Managing key aliases](/docs/hs-crypto?topic=hs-crypto-manage-key-alias).

Added: Synchronizing protected resources associated with root keys {: #add-sync-resources}
:   When the state of a root key changes, the protected resources that are associated with the root key are notified of the key lifecycle event and are encouraged to respond accordingly. In the case where the resources do not respond to the key lifecycle notification, you can now manually initiate a renotification to those associated cloud services. For more information, see [Synchronizing associated resources](/docs/hs-crypto?topic=hs-crypto-sync-associated-resources).

Added: Using Virtual Private Endpoints for VPC {: #add-vpe-for-vpc}
:   You can now create virtual private endpoints (VPEs) for your {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance to access {{site.data.keyword.hscrypto}} within your VPC network. For more information, see [Using a virtual private endpoint for VPC](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc).

Updated: The cryptography algorithm that is used to generate signature keys {: #update-signature-key-algorithm}
:   The cryptography algorithm to generate signature keys is updated from Rivest-Shamir–Adleman 2048 (RSA 2048) to P521 Elliptic Curve (P521 EC). The cryptographic strength of P521 EC keys is equivalent to RSA 15360, which means the updated signature keys can provide the higher level of security comparing to the previous signature keys. The previous RSA 2048 signature keys are still valid and can be used.

## 28 February 2021
{: #hs-crypto-february2021}
{: release-note}

Added: Key verification by using the PKCS #11 API {: #add-key-verification}
:   To ensure that no tampering has occurred to the keys that are stored in the {{site.data.keyword.hscrypto}} instance by using the PKCS #11 API, a key verification mechanism is now provided for you to check the key objects that are stored in {{site.data.keyword.hscrypto}}. For instructions on how to verify key objects, see [Verifying that keys are protected by crypto units](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref#pkcs11-key-verify).

    For an example of how to retrieve checksum values for AES, DES2, and DES3 keys along with the verification of the key checksums, see [the code sample](https://github.com/IBM-Cloud/hpcs-pkcs11/blob/master/samples/pkcs11-checksum.c){: external}.

Added: Support for the Schnorr algorithm {: #add-schnorr}
:   {{site.data.keyword.hscrypto}} now supports the Schnorr algorithm, which can be used as a signing scheme to generate digital signatures. It is proposed as an alternative algorithm to the Elliptic Curve Digital Signature Algorithm (ECDSA) for cryptographic signatures in the Bitcoin system. Before you can use the Schnorr algorithm, make sure to enable this feature by following the instructions in [Enabling the Schnorr algorithm](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-schnorr).

## 31 January 2021
{: #hs-crypto-january2021}
{: release-note}

Added: Support for a single-tenant KMIP adapter {: #add-support-kmip-adapter}
:   {{site.data.keyword.hscrypto}} now provides a single tenant KMIP adapter to manage the key distribution in the vSphere or vSAN environment. For more information, see [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware).

## 31 December 2020
{: #hs-crypto-december2020}

Added: Managing the key create and import access policy {: #add-key-create-import-access}
:   After you set up your {{site.data.keyword.hscrypto}} instance, you can enable and update the key create and import access policy to control actions permissions for root keys and standard keys. For more information, see [Managing the key create and import access policy](/docs/hs-crypto?topic=hs-crypto-manage-keyCreateImportAccess).

Added: Provisioning and managing service instances with the private-only network {: #add-private-only-network}
:   To achieve increased security, you can now limit the network access to your service instance to the private-only network. You can either [choose the allowed network when you provision the service instance](/docs/hs-crypto?topic=hs-crypto-provision) or [update the network access policy after you set up the instance](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies).

    Before you [update the network access policy](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies), you need to initialize the service instance first. See [Initializing service instances with the IBM Cloud TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) for instructions.
    {: important}

Added: `ReencryptSingle` function in GREP11 API {: #add-reencryptsingle-function-grep11}
:   The GREP11 API now supports the `ReencryptSingle` function, which enables you to decrypt data with the original key and then encrypt the raw data with a different key in a single call within the cloud HSM. This single call is a viable option where a large amount of data needs to be reencrypted with different keys, and bypasses the need to perform a combination of `DecryptSingle` and `EncryptSingle` functions for each data item that needs to be reencrypted. For more information, see [GREP11 API reference - `ReencryptSingle` function](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref#grep11-ReencryptSingle).

Added: Support for accessing service instances through the Virtual Private Endpoint {: #add-vpe}
:   You can now connect your {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance to your {{site.data.keyword.hscrypto}} instance through a virtual private endpoint (VPE) gateway, so that you can manage your keys by using {{site.data.keyword.hscrypto}} through a private network. For more information, see [Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-virtual-private-endpoints-for-vpc).

Added: Support for the SLIP10 mechanism and Edwards-curve algorithm {: #add-slip10-eddsa}
:   {{site.data.keyword.hscrypto}} now supports the SLIP10 mechanism for hierarchical deterministic wallets to derive private and public key pairs. It now also supports the Edwards-curve (ED) 25519 algorithm for digital signatures. Before you can use the ED algorithm, make sure to enable this feature by following the instructions in [Enabling Edwards-curve Digital Signature Algorithm](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-EdDSA).

Added: Using Terraform to manage {{site.data.keyword.hscrypto}} instances and resources {: #add-terraform}
:   Terraform is an open source software to configure and automate cloud resource provisioning and management. Now you can provision and initialize {{site.data.keyword.hscrypto}} instances, as well as managing root keys and standard keys with the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in. For more information, see [Managing key management service resources with Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-manage_resources) and the [sample Terraform template for {{site.data.keyword.hscrypto}}](https://github.com/IBM-Cloud/terraform-provider-ibm/tree/master/examples/ibm-hpcs-crypto){: external}.

Updated: key management service API {: #update-kms-api-december}
:   The {{site.data.keyword.hscrypto}} key management service API is updated with the following changes:

    - Updated: The API methods for the following key actions are now transferred to individual request paths. The generic path format (except the action of restoring a key) is `/api/v2/keys/<key_ID>/actions/<action>` where `key_ID` is the UUID of the key and `action` is the action name that you want to execute.
        - [Wrap a key](/apidocs/hs-crypto#wrapkey).
        - [Unwrap a key](/apidocs/hs-crypto#unwrapkey).
        - [Rewrap a key](/apidocs/hs-crypto#rewrapkey).
        - [Rotate a key](/apidocs/hs-crypto#rotatekey).
        - [Authorize deletion for a key with a dual authorization policy](/apidocs/hs-crypto#setkeyfordeletion).
        - [Remove an authorization for a key with a dual authorization policy](/apidocs/hs-crypto#unsetkeyfordeletion).
        - [Enable operations for a key](/apidocs/hs-crypto#enablekey).
        - [Disable operations for a key](/apidocs/hs-crypto#disablekey).
        - [Restore a key](/apidocs/hs-crypto#restorekey).

    - Updated: You can now use the following two methods to manage the allowed network policy and the key create and import access policy:
        - [Set instance policies](/apidocs/hs-crypto#putinstancepolicy).
        - [List instance policies](/apidocs/hs-crypto#getinstancepolicy).

    - Deprecated: [Invoke an action on a key](/apidocs/hs-crypto#actiononkey).

        This method is originally used for performing actions on a key, such as wrap, unwrap, and rotate. It is now replaced with individual request path for each action.

    For more information about the API updates, see [{{site.data.keyword.hscrypto}} key management service API reference](/apidocs/hs-crypto){: external}.

## 30 November 2020
{: #hs-crypto-november2020}

Added: Support for the BIP32 mechanism {: #add-bip32-mechanism}
:   {{site.data.keyword.hscrypto}} now supports the Bitcoin Improvement Proposal 0032 (BIP32) standard for hierarchical deterministic wallets to define how to derive private and public keys of a digital wallet. To enable BIP 32, follow the instructions in [Enabling BIP32 deterministic wallets](/docs/hs-crypto?topic=hs-crypto-enable-mechanisms#enable-BIP32).

Added: TKE activity tracker events {: #add-tke-at-events}
:   {{site.data.keyword.hscrypto}} now supports the Trusted Key Entry (TKE) events auditing. You can now use {{site.data.keyword.at_full_notm}} to monitor TKE activities and analyze failed actions. For more information, see [Auditing events for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-at-events).

## 30 September 2020
{: #hs-crypto-september2020}

Added: Master key rotation {: #added-master-key-rotation}
:   You can now rotate your master key on demand by using the {{site.data.keyword.cloud}} Trusted Key Entry CLI plug-in so as to meet industry standards and cryptographic best practices. For more information about how it works, see [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).

    For the detailed instructions, see [Rotating master keys](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part).

Added: Support for performing cryptographic operations with the standard PKCS #11 API {: #added-pkcs11}
:   {{site.data.keyword.hscrypto}} now supports performing cryptographic operations with the standard Public-Key Cryptography Standards (PKCS) #11 API.

    With the support of PKCS #11 API, you don not need to change your existing applications that use PKCS #11 standard to make it run in the {{site.data.keyword.hscrypto}} cloud HSM environment. The PKCS #11 library accepts the PKCS #11 API requests from your applications and remotely accesses the cloud HSM to execute the corresponding cryptographic functions.

    For more information about the PKCS #11 API use cases, see [Using Hyper Protect Crypto Services as PKCS #11 HSMs](/docs/hs-crypto?topic=hs-crypto-use-cases#pkcs11_hsm).

    To learn more about the PKCS #11 API, see [Introducing PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro) and [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).

## 31 August 2020
{: #hs-crypto-august2020}

Added: Support for import tokens to securely upload encryption keys {: #added-import-tokens}
:   If you have *Writer* or *Manager* access permissions, you can now create import tokens to enable added security for encryption keys that you upload to {{site.data.keyword.hscrypto}}.

    To find out more about your options for importing keys, check out [Creating import tokens](/docs/hs-crypto?topic=hs-crypto-create-import-tokens). For a guided tutorial, see [Tutorial: Creating and importing encryption keys](/docs/hs-crypto?topic=hs-crypto-tutorial-import-keys).

## 31 July 2020
{: #hs-crypto-july2020}

Added: {{site.data.keyword.hscrypto}} aligns the key management functions with {{site.data.keyword.keymanagementserviceshort}} {: #added-key-protect-concurrency}
:   {{site.data.keyword.hscrypto}}, built on FIPS 140-2 Level 4-compliant HSM, now supports the same level of key management functions as {{site.data.keyword.keymanagementserviceshort}}. The added functions are as follows:

    * [Policy-based key rotation](/docs/hs-crypto?topic=hs-crypto-set-rotation-policy).
    * [Viewing root key versions](/docs/hs-crypto?topic=hs-crypto-view-key-versions).
    * [Disabling and enabling root keys](/docs/hs-crypto?topic=hs-crypto-disable-keys).
    * Dual authorization policies for {{site.data.keyword.hscrypto}} [instances](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) and [keys](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy).
    * [Viewing details about an encryption key](/docs/hs-crypto?topic=hs-crypto-view-key-details).
    * [Viewing associations between root keys and IBM Cloud resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources).
    * [Restoring a deleted key](/docs/hs-crypto?topic=hs-crypto-restore-keys).

Added: {{site.data.keyword.hscrypto}} expands into the Washington DC region {: #added-wdc-region}
:   You can now create {{site.data.keyword.hscrypto}} resources in the Washington DC (US East) region. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 30 June 2020
{: #hs-crypto-june2020}

Added: Support for quorum authentication {: #added-quorum-authentication-202006}
:   Both the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in and the {{site.data.keyword.hscrypto}} Management Utilities now support [quorum authentication](/docs/hs-crypto?topic=hs-crypto-understand-concepts#quorum-authenticaion-concept).

    Quorum authentication is the way to approve an operation by a set number of crypto unit administrators. Some sensitive operations require a sufficient number of crypto unit administrators to enter their credentials. Setting the [signature thresholds](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept) to a value greater than one enables quorum authentication.

    For more information about how to initialize a service instance by using the TKE CLI and enable quorum authentication, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

    For more information about how to initialize a service instance by using the Management Utilities and enable quorum authentication, see [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

## 30 April 2020
{: #hs-crypto-april2020}

Added: {{site.data.keyword.hscrypto}} adds support for EP11 private endpoints {: #added-private-endpoints-202004}
:   You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the Enterprise PKCS #11 service.

    To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using private endpoints](/docs/hs-crypto?topic=hs-crypto-secure-connection).

Added: {{site.data.keyword.hscrypto}} adds support for the Management Utilities {: #added-management-utilities-202004}
:   {{site.data.keyword.hscrypto}} now supports loading master key parts and signature keys from smart cards for service instance initialization. It ensures the highest level of protection for master key parts and signature keys.

    The Management Utilities are two applications that use smart cards to configure service instances. The Smart Card Utility Program sets up and manages the smart cards used. The Trusted Key Entry (TKE) application uses those smart cards to configure service instances. To use the Management Utilities, you need to order IBM-supported smart cards and smart card readers.

    For more information, see [Understanding the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#understand-management-utilities) and [Initializing service instances by using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

Updated: {{site.data.keyword.cloud_notm}} service integration {: #added-service-integration-202004}
:   {{site.data.keyword.hscrypto}} can now be integrated with more {{site.data.keyword.cloud_notm}} services:

    - {{site.data.keyword.ihsdbaas_mongodb_full}}
    - {{site.data.keyword.ihsdbaas_postgresql_full}}
    - HyTrust DataControl
    - {{site.data.keyword.containerlong_notm}}
    - {{site.data.keyword.openshiftlong_notm}}

    For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

## 31 August 2019
{: #hs-crypto-August2019}

Added: {{site.data.keyword.hscrypto}} adds support for private endpoints {: #added-private-endpoints}
:   You can now connect to {{site.data.keyword.hscrypto}} over the {{site.data.keyword.cloud_notm}} private network by targeting a private endpoint for the service.

    To get started, enable [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} for your infrastructure account. For more information, see [Using service endpoints to privately connect to {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-secure-connection).

Added: {{site.data.keyword.hscrypto}} Cloud HSM now supports EP11 cryptographic operations over gRPC {: #added-EP11}
:   The managed Cloud Hardware Security Module (HSM) supports Enterprise Public-Key Cryptography Standards (PKCS) #11, so your applications can integrate cryptographic operations like digital signing and validation through Enterprise PKCS #11 (EP11) API. The EP11 library provides an interface similar to the industry-standard PKCS #11 API.

    {{site.data.keyword.hscrypto}} provides a set of Enterprise PKCS #11 (EP11) over gRPC API calls (also referred to as *GREP11*), with which, all the Crypto functions are executed in HSM on cloud. GREP11 is a stateless interface for cloud programs.

    For more information about the GREP11 API, see [Introducing EP11 over gRPC](/docs/hs-crypto?topic=hs-crypto-grep11-intro) and [GREP11 API reference](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

Added: {{site.data.keyword.hscrypto}} expands into the Frankfurt region {: #added-frankfurt-region}
:   You can now create {{site.data.keyword.hscrypto}} resources in the Frankfurt region. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

Added: {{site.data.keyword.cloud_notm}} service integration {: #added-service-integration}
:   {{site.data.keyword.hscrypto}} can now be integrated with the following {{site.data.keyword.cloud_notm}} services:

    - {{site.data.keyword.cos_full_notm}}
    - {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud
    - {{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud
    - Key Management Interoperability Protocol (KMIP) for VMware&reg; on {{site.data.keyword.cloud_notm}}

    For more information, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

## 30 June 2019
{: #hs-crypto-June2019}

Added: {{site.data.keyword.hscrypto}} expands into Sydney region {: #added-sydney-region}
:   You can now create {{site.data.keyword.hscrypto}} resources in the Sydney region. For more information, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

## 31 March 2019
{: #hs-crypto-March2019}

{{site.data.keyword.hscrypto}} is generally available {: #ga-201903}
:   As of 29 March 2019, provisioning new Hyper Protect Crypto Services Beta instances will no longer be possible. Existing instances will have support until the End of Beta Support Date (30 April 2019).

    For more information about the {{site.data.keyword.hscrypto}} offering, see the [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} home page](https://www.ibm.com/cloud/hyper-protect-crypto){: external}.

High availability and disaster recovery {: #ha-dr-new}
:   {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, which now supports three availability zones in a selected region, is a highly available service with automatic features that help keep your applications secure and operational.

    You can create {{site.data.keyword.hscrypto}} resources in the supported [{{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions), which represent the geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. Each {{site.data.keyword.cloud_notm}} region contains [multiple availability zones](https://www.ibm.com/cloud/data-centers/) to meet local access, low latency, and security requirements for the region.

    For more information, see [High availability and disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr).

Scalability {: #scalability-new}
:   The service instance can be scaled out to a maximum of six crypto units to meet your performance requirement. In a production environment, it is suggested to select at least two crypto units to enable high availability. By selecting three or more crypto units, these crypto units are distributed among three availability zones in the selected region.

    Read [Provisioning the service](/docs/hs-crypto?topic=hs-crypto-provision) for more information.

## 28 February 2019
{: #hs-crypto-Feb2019}

{{site.data.keyword.hscrypto}} Beta is available {: #beta-201902}
:   {{site.data.keyword.hscrypto}} Beta version is released. You can now access the {{site.data.keyword.hscrypto}} service through **Catalog** > **Security** directly.

    As of 5 February 2019, provisioning new Hyper Protect Crypto Services Experimental instances will no longer be possible. Existing instances will have support until the End of Experimental Support Date (5 March 2019).

## 31 December 2018
{: #hs-crypto-Dec2018}

Added: Integration of {{site.data.keyword.keymanagementserviceshort}} API {: #kp-api}
:   {{site.data.keyword.keymanagementserviceshort}} API is now integrated with Hyper Protect Crypto Services to generate and protect your keys. You can call the {{site.data.keyword.keymanagementserviceshort}} API directly through {{site.data.keyword.hscrypto}}.

    For more information, see [Setting up the key management service API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api) and [{{site.data.keyword.hscrypto}} key management service API reference](/apidocs/hs-crypto){: external}.

Added: Support for HSM management with Keep Your own Key {: #hsm-kyok}
:   {{site.data.keyword.hscrypto}} now supports Keep Your Own Key (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. You can initialize and manage your service instance with {{site.data.keyword.cloud}} command-line interface (CLI).

    For more information, see [Initializing service instances to protect key storage](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

Deprecated: Function of accessing {{site.data.keyword.hscrypto}} through Advanced Cryptography Service Provider {: #deprecated-acsp}
:   At the current stage, accessing {{site.data.keyword.hscrypto}} through an Advanced Cryptography Service Provider (ACSP) client is being deprecated. If you are using a previous service instance, you can still use ACSP to explore {{site.data.keyword.hscrypto}}.
