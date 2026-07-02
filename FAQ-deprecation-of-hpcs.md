---

copyright:
  years: 2026, 2026
lastupdated: "2026-07-01"

keywords: security for Hyper Protect Crypto Services, compliance for Hyper Protect Crypto Services, FAQ for deprecation of Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services,

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# FAQs: Deprecation of IBM Cloud Hyper Protect Crypto Services 

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is deprecated. As of 28 March 2026, you can't create new instances, and access to free instances will be removed. Existing premium plan instances are supported until 28 March 2027. Any instances that still exist on that date will be deleted.
{: deprecated}


## 1. What is happening and why?
{: #what-is-happening-why}

IBM Cloud is withdrawing (service deprecation) IBM Cloud Hyper Protect Crypto Services (HPCS) across selected regions. This aligns with IBM’s strategy to deliver a more consistent experience across key management services and to unify BYOK/KYOK capabilities via IBM Cloud Key Protect Dedicated. This withdrawal affects all HPCS capabilities, including CloudKMS (KMIP), CloudHSM/GREP11, and Unified Key Orchestrator.

Impacted regions
:   - Dallas (us-south)
    - Washington D.C. (us-east)
    - Toronto (ca-tor)
    - Frankfurt (eu-de)
    - London (eu-gb)
    - Madrid (eu-es)
    - Tokyo (jp-tok)
    - São Paulo (br-sao) 

## 2. Which HPCS capabilities are affected?
{: #hpcs-capabilities}

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
{: # supported-mig-paths} 

1. CloudKMS (including KMIP for VMware):
   1. Migrate to IBM Cloud Key Protect Dedicated (where available).
   2. If Dedicated is not available in-region, migrate to IBM Cloud Key Protect (multi-tenant). 

2. CloudHSM / GREP11 (PKCS#11)
   1. Migrate to on-premises deployment to continue on IBM LinuxONE technology. 
   2. IBM Cloud Key Protect Dedicated PKCS#11 is planned for 2Q 2026 (where supported). 

3. Unified Key Orchestrator (UKO)
   1. Migrate to on-premises: UKO for Containers or UKO for z/OS. 

## 5. Migration tooling availability
{: #mig-tooling-availability}

IBM Cloud migration tooling for HPCS → Key Protect is planned to be available on March 20, 2026.  

## 6. How to prepare (in a phased approach)?
{: #how-prep-in-a-phased-approach}

1. Understand changes and target options going forward 
2. Assess affected assets/services and cryptographic dependencies 
3. Select and prepare the target environment (Key Protect or on-premises) 
4. Align cryptographic configuration and policies 
5. Select a key-migration approach and test 
6. Migrate applications and assets; update runbooks and procedures
7. Cut over and decommission legacy HPCS resources  

## 7. Migration Checklist for Customers for IBM Cloud Key Protect 
{: #mig-checklist-customers-KP} 

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
   {: note}

 
Please refer to our detailed Migration Guide for further details (Migration Guide for IBM Cloud HPCS KMS and KMIP for vmware). 

## 8. On‑premises migration (CloudHSM / UKO)
{: #on-prem-mig} 

1. Review the detailed migration guide for your use case (GREP11/PKCS#11 or UKO). 
2. Assess and validate datacenter requirements and capacity. 
3. Build a complete crypto asset/dependency inventory to manage interdependencies. 
4. Plan for operational model changes (people/process/monitoring). 
5. Provision target environment and conduct stability/performance testing.x 

On‑prem migration may require purchase of hardware, software, and services.
{: note} 

## 9. Roles, responsibilities, and financial planning 
{: #roles-resp-fin-plan}

Customers are responsible for planning and executing migration activities based on their current HPCS usage. Please work with your Customer Success Manager (CSM) on planning and risk identification. 

Some migration options shift from managed cloud service to customer‑managed deployments; budget and financial planning may be required. 


## 10. References
{: #References} 

1. HPCS → Key Protect Migration Guide (Refer to [KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st))
2. GREP11/PKCS#11 On‑prem Migration Guide (Refer to [GREP11/PKCS#11 Migration Guide](/docs/hs-crypto?topic=hs-crypto-migrate-hpcs-to-CCRT)) 
3. UKO Migration Guide (Refer to [UKO Migration Guide](/docs/hs-crypto?topic=hs-crypto-migration-guide)) 
4. ServiceNow request templates (Refer to the FAQ no **16. Support during the transition** in the same page)


## 11. What does this mean for customers?
{: #what-does-this-mean-for-customers}

Customers are responsible for planning and executing their migration based on how they currently use HPCS. Depending on the use case, this may include migrating to Key Protect Dedicated Migration tooling is planned to become available starting March 20, 2026 or moving to an onpremises deployment for CloudHSM or UKO scenarios.  
 

## 12. What happens if no action is taken?
{: #what-happens-if-no-action-is-taken} 

After March 20, 2027, any remaining HPCS instances will be terminated and cryptographic material will be deleted. Applications depending on HPCS will stop functioning. Customers will receive advance notifications. 

## 13. Which migration options are available by Use Case?
{: #which-migration-options-are-available-by-use-case}

CloudKMS and KMIP for VMware
:   - IBM Cloud Key Protect Dedicated (single‑tenant, supports Keep Your Own Key; available in selected regions)
    - IBM Cloud Key Protect Multi‑Tenant (all regions) 

Migration tooling will support key migration from HPCS to Key Protect. For more details, refer to [HPCS‑to‑KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st).


CloudHSM (GREP11 and PKCS#11)
:   - On‑premises deployment on IBM LinuxONE technology
    - IBM Cloud Key Protect Dedicated PKCS#11 (planned availability: Q2 2026) 

For HPCS to Confidential Computing Container Runtime (on-prem)(PID (5737-I09)) migration guide, follow [HPCS to CCRT migration guide](/docs/hs-crypto?topic=hs-crypto-migrate-hpcs-to-CCRT).
  

Unified Key Orchestrator
:   - Unified Key Orchestrator for Containers (on‑premises) 
    - Unified Key Orchestrator for z/OS (on‑premises) 

Follow [UKO to UKO on-prem migration guide](/docs/hs-crypto?topic=hs-crypto-migration-guide).

If the customer is using ISV applications that are affected by the migration, the migration needs to be planned and performed in shared responsibility / in coordination between the customer and the ISV.
{: important}

|Product / Capability |Alternative / Recommendation|
|---------------------|----------------------------|
|IBM Cloud Hyper Protect Crypto Services \n IBM CloudKMS including KMIP for vmware  | Migrate to \n - IBM Cloud Key Protect Dedicated (select regions). For more information, refer to [KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st) \n - IBM Cloud Key Protect Multi-Tenant (all regions). For more information, refer to [KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st) |
|IBM Cloud Hyper Protect Crypto Services \n CloudHSM / GREP11 | Migrate to \n - On-premises deployment (if you plan to continue IBM LinuxONE technology). For more information, refer to [GREP11/PKCS#11 Migration Guide](/docs/hs-crypto?topic=hs-crypto-migrate-hpcs-to-CCRT). \n - IBM Cloud Key Protect Dedicated PKCS#11 planed for 2Q 2026 (*requires migration to PKCS#11). For more information, refer to [KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st).| 
| IBM Cloud Hyper Protect Crypto Services \n CloudHSM PKCS#11 | Migrate to \n - On-premises deployment (if you plan to continue IBM LinuxONE technology). For more information, refer to [KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st). \n - IBM Cloud Key Protect Dedicated PKCS#11 planned for 2Q 2026. For more information, refer to [KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st).|
|IBM Cloud Hyper Protect Crypto Services \n Unified Key Orchestrator| Migrate to \n - on premises deployment \n - Unified Key Orchestrator for Containers \n - Unified Key Orchestrator for z/OS. \n For more information, refer to [UKO Migration Guide](/docs/hs-crypto?topic=hs-crypto-migration-guide)| 
{: caption="Product/Capability and their Alternative / Recommendation"}


## 14. How can I migrate my CloudKMS and KMIP for vmware keys to IBM Cloud Key Protect (Dedicated) – High level?
{: #how-to-mig-cloudkms-n-kmip-tocloud-kp}

**Migration Checklist for Customers for IBM Cloud Key Protect**
 1. Choose Your Target Key Protect Tier
    1. **Use Key Protect Dedicated** (single‑tenant, KYOK‑enabled with KMIP for VMware) in regions where it is available.
    2. **Use Key Protect Multi‑Tenant** in regions where the Dedicated tier is not available. 
 2. Prepare Your Environment 
    1. Review the HPCS to Key Protect Migration guide.  
    2. Create a **Key Protect instance** in your development or test environment. 
    3. For test purposes we recommend setting up a **Cloud Object Storage instance** encrypted with a key from Hyper Protect Crypto Services, to get familiar with the migration tool once it is available.
 3. Plan and Execute Migration
    1. Use the **IBM Cloud migration tools** to move keys from HPCS to Key Protect Dedicated or Multi‑Tenant tiers. You can test the tool with the COS instance setup in step.
   
   Migration tools will be available on **March 20, 2026**. 
    {: note}

For further details, please refer to [KP-Dedicated Migration Guide](/docs/key-protect?topic=key-protect-migrate-st).
## 15. How can I migrate to on‑premises environments?
{: #how-to-mig-to-onprem-env}

On‑premises migrations represent a significant transformation, including new operational responsibilities, hardware/software procurement, and updated security/compliance processes. Perform a full cryptographic asset inventory, review applicable migration guides, and plan a phased migration with testing and validation. 

**Important documents**
1. Unified Key Orchestrator to UKO on-prem migration guide. Refer [UKO on-prem migration guide](/docs/hs-crypto?topic=hs-crypto-migration-guide)
2. IBM Cloud Hyper Protect Crypto Services CloudHSM to on-prem migration guide. Refer [IBM Cloud Hyper Protect Crypto Services CloudHSM to on-prem migration guide](/docs/hs-crypto?topic=hs-crypto-migrate-hpcs-to-CCRT)


## 16. Support during the transition
{: #support-during-the-transition}

For assistance, please reach out via your defined support channels.

Consider Expert-Labs-Services to help, guide, and support this migration. 
{: tip}

If the appropriate point of contact is unknown, please send an email to ZaaS.Client.Acceleration@ibm.com 

- Work with your Customer Success Manager (CSM)


  
If applicable, please open an IBM Cloud Support ticket.   
**To do this**,
1. Go to https://cloud.ibm.com/unifiedsupport/supportcenter.
2. Create a case and provide title: 

```
Help with IBM Cloud Hyper Protect Crypto Services migration
```
 {: codeblock}
  
3. Provide description and your instance id, if available.


**For any additional matters**
- **IBM Cloud Hyper Protect Crypto Services**: Christopher Smith – chsmith@de.ibm.com 
- **KeyProtect**: Damneet Basak - damneet@us.ibm.com 

## 17. Recommended next steps for customers
{: #recommended-next-steps-customers}
 
1. Perform inventory of all applications and services using HPCS. If ISV applications are affected, coordinate migration (planning and implementation) with the ISV.
2. Select target platform per use case. 
3. Review the relevant migration guides and identify dependencies. 
4. Build a migration plan aligned with the migration window and test thoroughly. 
5. Engage IBM for planning and technical assistance; schedule regular checkpoints. 

 
