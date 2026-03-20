---

copyright:
  years: 2026, 2026
lastupdated: "2026-03-20"

keywords: security for Hyper Protect Crypto Services, compliance for Hyper Protect Crypto Services, FAQ for deprecation of Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services,

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# FAQs: Deprecation of IBM Cloud Hyper Protect Crypto Services 


## 1. What is happening and why?
{: #what-is-happening-why}

IBM Cloud is withdrawing (service deprecation) IBM Cloud Hyper Protect Crypto Services (HPCS) across selected regions. This aligns with IBM’s strategy to deliver a more consistent experience across key management services and to unify BYOK/KYOK capabilities via IBM Cloud Key Protect Dedicated. This withdrawal affects all HPCS capabilities, including CloudKMS (KMIP), CloudHSM/GREP11, and Unified Key Orchestrator.

Impacted regions
:   - Dallas (us-east)
    - Washington D.C. (us-south)
    - Toronto (ca-tor)
    - Frankfurt (eu-de)
    - London (eu-gb)
    - Madrid (eu-es)
    - Tokyo (jp-tok)
    - São Paulo (br-sao) 

## 2. Which HPCS capabilities are affected?

- CloudKMS (including KMIP for VMware)
- CloudHSM / GREP11 (PKCS#11)
- Unified Key Orchestrator (UKO) 

## 3. Key dates and milestones
{: #key-dates}

| Milestone | Date |
|-----------|------|
|**External announcement** | March 20, 2026 |
|**End of marketing**| March 28, 2026 |
|**End of support / service shutdown**: | March 20, 2027 |
{: caption="Key dates and milestones"}


## 4. Supported migration paths (by use case) 

1. CloudKMS (including KMIP for VMware):
   1. Migrate to IBM Cloud Key Protect Dedicated (where available).
   2. If Dedicated is not available in-region, migrate to IBM Cloud Key Protect (multi-tenant). 

2. CloudHSM / GREP11 (PKCS#11)
   1. Migrate to on-premises deployment to continue on IBM LinuxONE technology. 
   2. IBM Cloud Key Protect Dedicated PKCS#11 is planned for 2Q 2026 (where supported). 

3. Unified Key Orchestrator (UKO)
   1. Migrate to on-premises: UKO for Containers or UKO for z/OS. 

## 5. Migration tooling availability
IBM Cloud migration tooling for HPCS → Key Protect is planned to be available on March 20, 2026. CSMs should factor this date into migration planning and avoid committing to earlier tooling availability. 

## 6. How to prepare(in a phased approach)?

1. Understand changes and target options going forward 
2. Assess affected assets/services and cryptographic dependencies 
3. Select and prepare the target environment (Key Protect or on-premises) 
4. Align cryptographic configuration and policies 
5. Select a key-migration approach and test 
6. Migrate applications and assets; update runbooks and procedures
7. Cut over and decommission legacy HPCS resources  

## 7. Migration Checklist for Customers for IBM Cloud Key Protect  

1. Choose Your Target Key Protect Tier
   1. Use Key Protect Dedicated (single‑tenant, KYOK‑enabled with KMIP for VMware) in regions where it is available. 
   2. Use Key Protect Multi‑Tenant in regions where the Dedicated tier is not available. 
2. Prepare Your Environment 
   1. Review the HPCS to Key Protecet Migration guide
   2. Create a Key Protect instance in your development or test environment. 
   For test purposes we recommend to set up a Cloud Object Storage instance encrypted with a key from Hyper Protect Crypto Services, to get familiar with the migration tool once it is available 
3. Plan and Execute Migration 
   1. Use the IBM Cloud migration tools to move keys from HPCS to Key Protect Dedicated or Multi‑Tenant tiers. You can test the tool with the COS instance setup in step 2. 
   
   Migration tools will be available on March 20, 2026.
   {: Note}

 
Please refer to our detailed Migration Guide for further details (Migration Guide for IBM Cloud HPCS KMS and KMIP for vmware). 

## 8. On‑premises migration (CloudHSM / UKO) 

- Review the detailed migration guide for your use case (GREP11/PKCS#11 or UKO). 
- Assess and validate datacenter requirements and capacity. 
- Build a complete crypto asset/dependency inventory to manage interdependencies. 
- Plan for operational model changes (people/process/monitoring). 
- Provision target environment and conduct stability/performance testing.x 

On‑prem migration may require purchase of hardware, software, and services.
{: Note} 

## 9. Roles, responsibilities, and financial planning 

Customers are responsible for planning and executing migration activities based on their current HPCS usage. CSMs should proactively engage to support planning and risk identification. 

Some migration options shift from managed cloud service to customer‑managed deployments; budget and financial planning may be required. 

## 10. IBM support during the transition 

Primary path
: raise development/support requests via ServiceNow using prepared templates. 

Internal Slack channel
: #ask-hyper-protect. 

Contacts
: Christopher Smith (HPCS) and Damneet Basak (Key Protect Dedicated / tooling). 

## 11. CSM actions (CTA) 

- Review all client deployments using affected HPCS services. 
- Map each workload to a supported target (Key Protect tier or on‑prem) and a proposed timeline. 
- After the external announcement, contact customers to inform them and align on next steps. 
- Track migration progress, risks, and issues; escalate via internal paths as needed. 

## 12. References (internal) 

- HPCS → Key Protect Migration Guide (internal link) 
- GREP11/PKCS#11 On‑prem Migration Guide (internal link) 
- UKO Migration Guide (internal link) 
- ServiceNow request templates (internal link) 

## 13. What does this mean for customers?
{: #what-does-this-mean-for-customers}

Customers are responsible for planning and executing their migration based on how they currently use HPCS. Depending on the use case, this may include migrating to Key Protect (Dedicated or multitenant) or moving to an onpremises deployment for CloudHSM or UKO scenarios. Migration tooling is planned to become available starting March 20, 2026. 
 

## 14. Why is IBM Cloud retiring Hyper Protect Crypto Services?
{: #why-is-ibm-cloud-retiring-hyper-protect-crypto-services} 

IBM Cloud is evolving its key management portfolio to deliver a more consistent customer experience and clearer choices between multi‑tenant BYOK and single‑tenant KYOK.  

IBM is offering a set of Migration Options depending on use case, and customer operational requirements. 

## 15. What is expected from you?
{: #what-is-expected-from-you}

  1. Identify all customer accounts using affected HPCS services 
  2. Review supported migration paths and timelines 
  3. Proactively engage customers after the external announcement 
  4. Track migration progress and escalate risks as needed 

## 16. What happens if no action is taken?
{: #what-happens-if-no-action-is-taken} 

After February 13, 2027, any remaining HPCS instances will be terminated and cryptographic material will be deleted. Applications depending on HPCS will stop functioning. Customers will receive advance notifications. 

## 17. Which migration options are available by Use Case?
{: which-migration-options-are-available-by-use-case}

CloudKMS and KMIP for VMware
:   - IBM Cloud Key Protect Dedicated (single‑tenant, KYOK; selected regions)
    - IBM Cloud Key Protect Multi‑Tenant (all regions) 


Migration tooling will support key migration from HPCS to Key Protect. Follow [HPCS to Key Protect Migration guide]().


CloudHSM (GREP11 and PKCS#11)
:   - On‑premises deployment on IBM LinuxONE technology
    - IBM Cloud Key Protect Dedicated PKCS#11 (planned availability: Q2 2026) 

Follow [HPCS to CCRT migration guide](/docs/hs-crypto?topic=hs-crypto-migrate-hpcs-to-hpvs).
  

Unified Key Orchestrator
:   - Unified Key Orchestrator for Containers (on‑premises) 
    - Unified Key Orchestrator for z/OS (on‑premises) 

Follow [UKO to UKO on-prem migration guide](/docs/hs-crypto?topic=hs-crypto-migration-guide).

|Product / Capability |Alternative / Recommendation|
|---------------------|----------------------------|
|IBM Cloud Hyper Protect Crypto Services \n IBM CloudKMS including KMIP for vmware  | Migrate to \n - IBM Cloud Key Protect Dedicated (select regions) \n - IBM Cloud Key Protect Multi-Tenant (all regions). For more information, refer to KP-Dedicated Migration Guide.|
|IBM Cloud Hyper Protect Crypto Services \n CloudHSM / GREP11 | Migrate to \n - On-premises deployment (if you plan to continue IBM LinuxONE technology). For more information, refer to [GREP11/PKCS#11 Migration Guide](/docs/hs-crypto?topic=hs-crypto-migrate-hpcs-to-hpvs). \n - IBM Cloud Key Protect Dedicated PKCS#11 planed for 2Q 2026 (*requires migration to PKCS#11). For more information, refer to KP-Dedicated Migration Guide.| 
| IBM Cloud Hyper Protect Crypto Services \n CloudHSM PKCS#11 | Migrate to \n - On-premises deployment (if you plan to continue IBM LinuxONE technology). For more information, refer to KP-Dedicated Migration Guide. \n - IBM Cloud Key Protect Dedicated PKCS#11 planned for 2Q 2026. For more information, refer to KP-Dedicated Migration Guide|
|IBM Cloud Hyper Protect Crypto Services \n Unified Key Orchestrator| Migrate to \n - on premises deployment \n - Unified Key Orchestrator for Containers \n - Unified Key Orchestrator for z/OS. For more information, refer to [UKO Migration Guide](/docs/hs-crypto?topic=hs-crypto-migration-guide)| 
{: caption="Product/Capability and their Alternative / Recommendation"}


## 18. How can I migrate my CloudKMS and KMIP for vmware keys to IBM Cloud Key Protect (Dedicated) – High level? 
**Migration Checklist for Customers for IBM Cloud Key Protect**
 1. Choose Your Target Key Protect Tier
    1. Use Key Protect Dedicated (single‑tenant, KYOK‑enabled with KMIP for VMware) in regions where it is available.
    2. Use Key Protect Multi‑Tenant in regions where the Dedicated tier is not available. 
 2. Prepare Your Environment 
    1. Review the HPCS to Key Protect Migration guide  
    2. Create a Key Protect instance in your development or test environment. 
    3. For test purposes we recommend to set up a Cloud Object Storage instance encrypted with a key from Hyper Protect Crypto Services, to get familiar with the migration tool once it is available 
 3. Plan and Execute MigrationUse the IBM Cloud migration tools to move keys from HPCS to Key Protect Dedicated or Multi‑Tenant tiers. You can test the tool with the COS instance setup in step 2. 
    
    Migration tools will be available on March 20, 2026. 
    {: Note}

## 19. How can I migrate to on‑premises environments?

On‑premises migrations represent a significant transformation, including new operational responsibilities, hardware/software procurement, and updated security/compliance processes. Perform a full cryptographic asset inventory, review applicable migration guides, and plan a phased migration with testing and validation. 

**Important documents**
1. Unified Key Orchestrator to UKO on-prem migration guide. Refer [UKO on-prem migration guide](/docs/hs-crypto?topic=hs-crypto-migration-guide)
2. IBM Cloud Hyper Protect Crypto Services CloudHSM to on-prem migration guide. Refer [IBM Cloud Hyper Protect Crypto Services CloudHSM to on-prem migration guide](/docs/hs-crypto?topic=hs-crypto-migrate-hpcs-to-hpvs)


## 20. Support during the transition

IBM provides documentation and expert assistance throughout the migration period. Engage your IBM account team or Customer Success Manager, and raise technical requests via ServiceNow. 

**For additional assistance**
- **HPCS contact**: Christopher Smith – chsmith@de.ibm.com 
- **KeyProtect contact**: Damneet Basak - damneet@us.ibm.com 

## 21. Recommended next steps for customers
 
1. Perform inventory of all applications and services using HPCS. 
2. Select target platform per use case. 
3. Review the relevant migration guides and identify dependencies. 
4. Build a migration plan aligned with the migration window and test thoroughly. 
5. Engage IBM for planning and technical assistance; schedule regular checkpoints. 

 
