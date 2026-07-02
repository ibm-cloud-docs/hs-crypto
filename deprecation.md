---

copyright:
  years: 2026, 2026
lastupdated: "2026-07-01"

keywords: security for Hyper Protect Crypto Services, compliance for Hyper Protect Crypto Services, FAQ for deprecation of Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services,

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

# Deprecation
{: #deprecation}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is deprecated. As of 28 March 2026, you can't create new instances, and access to free instances will be removed. Existing premium plan instances are supported until 28 March 2027. Any instances that still exist on that date will be deleted.
{: deprecated}

## Important dates
{: #important-dates}

The service will no longer be supported by {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} as of **28 March 2027**. At the end-of-support date, any instances of service-name that are still running will be permanently disabled and deprovisioned. 
{: shortdesc}

| Milestone | Date |
|-----------|------|
|**External announcement** | March 20, 2026 |
|**End of marketing**| March 28, 2026 |
|**End of support / service shutdown**: | March 20, 2027 |
{: caption="Key dates and milestones"}

## Deprecation details
For the detailed information about deprecation of these services, refer to [FAQs: Deprecation of IBM Cloud Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-faqs-deprecation-of-ibm-cloud-hyper-protect-crypto-services). 

## Recommended next steps for customers
{: #recommended-next-steps-customers}
 
1. Perform inventory of all applications and services using HPCS. If ISV applications are affected, coordinate migration (planning and implementation) with the ISV.
2. Select target platform per use case. 
3. Review the relevant migration guides and identify dependencies. 
4. Build a migration plan aligned with the migration window and test thoroughly. 
5. Engage IBM for planning and technical assistance; schedule regular checkpoints. 

 
## Deleting service-name instances and data
{: #service-delete} 

After **20 March 2027**, any remaining HPCS instances will be terminated and cryptographic material will be deleted. Applications depending on HPCS will stop functioning. Customers will receive advance notifications. 

## Migrating to equivalent-offering
{: #migration-options-are-available-by-use-case}

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


 
