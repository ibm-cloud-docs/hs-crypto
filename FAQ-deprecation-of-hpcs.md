---

copyright:
  years: 2026, 2026
lastupdated: "2026-02-25"

keywords: security for Hyper Protect Crypto Services, compliance for Hyper Protect Crypto Services, FAQ for deprecation of Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services,

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# FAQs: Deprecation of IBM Cloud Hyper Protect Crypto Services 


## What is happening?
{: #what-is-happening}

IBM Cloud will withdraw IBM Cloud Hyper Protect Crypto Services in the following regions: Dallas, Washington D.C., Toronto, Frankfurt, London, Madrid, Tokyo, and São Paulo. This withdrawal affects all HPCS capabilities, including CloudKMS (KMIP), CloudHSM/GREP11, and Unified Key Orchestrator. 

## Key dates
{: #key-dates}

    - External announcement: Delayed
    - End of marketing: To be updated
    - Customer migration window:  To be updated
    - End of support / service shutdown:  To be updated

## What does this mean for customers?
{: #what-does-this-mean-for-customers}

Customers are responsible for planning and executing their migration based on how they currently use HPCS. Depending on the use case, this may include migrating to Key Protect (Dedicated or multitenant) or moving to an onpremises deployment for CloudHSM or UKO scenarios. Migration tooling is planned to become available starting March 20, 2026. 
 

## Why is IBM Cloud retiring Hyper Protect Crypto Services?
{: #why-is-ibm-cloud-retiring-hyper-protect-crypto-services} 

IBM Cloud is evolving its key management portfolio to deliver a more consistent customer experience and clearer choices between multi‑tenant BYOK and single‑tenant KYOK.  

IBM is offering a set of Migration Options depending on use case, and customer operational requirements. 

## What is expected from you?
{: #what-is-expected-from-you}

  - Identify all customer accounts using affected HPCS services 
  - Review supported migration paths and timelines 
  - Proactively engage customers after the external announcement 
  - Track migration progress and escalate risks as needed 

## What happens if no action is taken?
{: #what-happens-if-no-action-is-taken} 

After February 13, 2027, any remaining HPCS instances will be terminated and cryptographic material deleted. Applications depending on HPCS will stop functioning. Customers will receive advance notifications. 

## Which migration options are available by Use Case?
{: which-migration-options-are-available-by-use-case}

**CloudKMS and KMIP for VMware**
: - IBM Cloud Key Protect Dedicated (single‑tenant, KYOK; selected regions) 
  - IBM Cloud Key Protect Multi‑Tenant (all regions) 
Migration tooling will support key migration from HPCS to Key Protect. Follow [HPCS to Key Protect Migration guide](/docs/hs-crypto?topic=migrating-hpcs-cloud(grep11)).


**CloudHSM (GREP11 and PKCS#11)**
:
  - On‑premises deployment on IBM LinuxONE technology 
  - IBM Cloud Key Protect Dedicated PKCS#11 (planned availability: Q2 2026) 
Follow [HPCS to HPVS on-prem migration guide]().

**Unified Key Orchestrator**
:
  - Unified Key Orchestrator for Containers (on‑premises) 
  - Unified Key Orchestrator for z/OS (on‑premises) 

Follow [UKO to UKO on-prem migration guide]().

|Product / Capability |Alternative / Recommendation|
|---------------------|----------------------------|
|IBM Cloud Hyper Protect Crypto Services \n IBM CloudKMS including KMIP for vmware  | Migrate to \n - IBM Cloud Key Protect Dedicated (select regions) \n - IBM Cloud Key Protect Multi-Tenant (all regions). For more information, refer to KP-Dedicated Migration Guide.|
|IBM Cloud Hyper Protect Crypto Services \n CloudHSM / GREP11 | Migrate to \n - On-premises deployment (if you plan to continue IBM LinuxONE technology). For more information, refer to [GREP11/PKCS#11 Migration Guide](./migrating-hpcs-cloudHSM(grep11).md). \n - IBM Cloud Key Protect Dedicated PKCS#11 planed for 2Q 2026 (*requires migration to PKCS#11). For more information, refer to KP-Dedicated Migration Guide.| 
| IBM Cloud Hyper Protect Crypto Services \n CloudHSM PKCS#11 | Migrate to \n - On-premises deployment (if you plan to continue IBM LinuxONE technology). For more information, refer to [GREP11/PKCS#11 Migration Guide](./migrating-hpcs-cloudHSM(grep11).md). \n - IBM Cloud Key Protect Dedicated PKCS#11 planned for 2Q 2026. For more information, refer to KP-Dedicated Migration Guide|
|IBM Cloud Hyper Protect Crypto Services \n Unified Key Orchestrator| Migrate to \n - on premises deployment \n - Unified Key Orchestrator for Containers \n - Unified Key Orchestrator for z/OS. For more information, refer to UKO Migration Guide| 

{: caption="Product/Capability and their Alternative / Recommendation"}


## How can I migrate my CloudKMS and KMIP for vmware keys to IBM Cloud Key Protect (Dedicated) – High level? 
**Migration Checklist for Customers for IBM Cloud Key Protect**
:
   1. Choose Your Target Key Protect Tier 
      a. Use Key Protect Dedicated (single‑tenant, KYOK‑enabled with KMIP for VMware) in regions where it is available. 
      b.Use Key Protect Multi‑Tenant in regions where the Dedicated tier is not available. 
   2. Prepare Your Environment 
      a. Review the HPCS to Key Protect Migration guide  
      b. Create a Key Protect instance in your development or test environment. 
      c. For test purposes we recommend to set up a Cloud Object Storage instance encrypted with a key from Hyper Protect Crypto Services, to get familiar with the migration tool once it is available 
   3. Plan and Execute Migration
      a. Use the IBM Cloud migration tools to move keys from HPCS to Key Protect Dedicated or Multi‑Tenant tiers. You can test the tool with the COS instance setup in step 2. 
      
      Migration tools will be available on March 20, 2026. 
        {: Note}

## How can I Migrate to On‑Premises Environments 

On‑premises migrations represent a significant transformation, including new operational responsibilities, hardware/software procurement, and updated security/compliance processes. Perform a full cryptographic asset inventory, review applicable migration guides, and plan a phased migration with testing and validation. 

**Important documents**
:   - Unified Key Orchestrator to UKO on-prem migration guide. Refer [UKO on-prem migration guide](https://cloud.ibm.com/docs/vpc?topic=vpc-migration_guide)
    - IBM Cloud Hyper Protect Crypto Services CloudHSM to on-prem migration guide. Refer [IBM Cloud Hyper Protect Crypto Services CloudHSM to on-prem migration guide](./migrating-hpcs-cloudHSM(grep11).md)


## Support During the Transition

IBM provides documentation and expert assistance throughout the migration period. Engage your IBM account team or Customer Success Manager, and raise technical requests via ServiceNow. 

**For additional assistance**
:  
- **HPCS contact**: Christopher Smith – chsmith@de.ibm.com 
- **KeyProtect contact**: Damneet Basak - damneet@us.ibm.com 

## Recommended Next Steps for Customers 
1. Inventory all applications and services using HPCS. 
2. Select target platform per use case. 
3. Review the relevant migration guides and identify dependencies. 
4. Build a migration plan aligned with the migration window and test thoroughly. 
5. Engage IBM for planning and technical assistance; schedule regular checkpoints. 

 
