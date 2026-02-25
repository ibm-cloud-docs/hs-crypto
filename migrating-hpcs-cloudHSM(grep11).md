--- 

copyright:
  years: 2026, 2026
lastupdated: "2026-02-25"

keywords: migration guide for Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services

subcollection: hs-crypto

content-type: migration-guide
---


{{site.data.keyword.attribute-definition-list}}



# Migrating {{site.data.keyword.hscrypto}} to Onpremises IBM Hyper Protect Virtual Server (HPVS) 


This topic describes a structured approach for migrating cryptographic workloads, keys, and applications from  **IBM Cloud Hyper Protect Crypto Services (HPCS)** using CloudHSM to **Onpremises IBM Hyper Protect Virtual Server (HPVS)** with IBM Crypto Appliances and GREP11. 

This migration topics is intended for security architects, infrastructure engineers, and application owners responsible for HSM-backed key management and cryptographic operations. 
{: note}

## Source and Target Architecture Overview
{: #source-target-arch-overview}
### Source: IBM Cloud HPCS (CloudHSM)
{: #source-cloudhsm}

Key characteristics
:   - Fully managed IBM Cloud service 
    - FIPS 1402 Level 4 certified hardware 
    - Multitenant service with customer-controlled master key concept (KYOK) 
    - Access via:  
        - PKCS#11 
        - GREP11 
        - Enterprise Key Management APIs 

### Target: OnPremises HPVS + Crypto Express Network API 
{: #Target-onprem-hpvs+crpto-api}

Key characteristics
:   - Customer-controlled onpremises environment 
    - IBM Crypto Appliances (For example, CEX or dedicated Crypto Express hardware) 
    - GREP11 server exposes GREP11 interface to workloads 
    - HPVS provides secure, isolated virtual servers with:  
      - Secure boot 
      - Memory encryption 
      - Confidential computing guarantees 


## Migration Strategy 
{: #migration-technology}

The migration follows a phased approach
:   
    1. Assessment and readiness
    2. Target environment preparation 
    3. Cryptographic configuration alignment 
    4. Key migration or re-keying 
    5. Application migration and validation 
    6. Cutover and decommissioning 


## Phase 1 – Assessment and Readiness
{: #phasse1-assessment-readiness}

### Inventory Cryptographic Assets 
{: #inventory-cryptographic-assets}

Identify and document
:   
    - Key types (AES, RSA, EC, HMAC, wrapping keys) 
    - Key sizes and attributes 
    - Key usage (encrypt/decrypt, sign/verify, wrap/unwrap) 
    - Key lifecycle state (active, suspended, rotation schedule) 
    - HPCS access patterns (PKCS#11 vs GREP11) 

### Application Dependency Analysis 
{: #application-dependency-analysis}

For each application 
:   
    - HSM interface used (For example, GREP11, PKCS11)
    - Sessions per second and performance requirements
    - Latency sensitivity 
    - Compliance requirements (For example, PCI DSS, GDPR, financial regulations)

### Migration Model Decision 
{: #migration-model-decision}

Decide per application and key set 
:
    - Key migration (export/import where allowed) 
    - Logical migration (re-key and re-encrypt data) 

Many HSM deployments or key attributes prohibit raw key export. Hence, wrapping-based migration or re-keying is typically preferred.
{: note}

## Phase 2 – Target Environment Preparation
{: #phase2-target-environment-preparation}
### Deploy IBM Crypto Appliance
{: #deploy-ibm-crypto-appliance}

Steps 
:   1. Install and rack the crypto appliance 
    2. Perform initial trusted initialization (TKE or equivalent) 
    3. Configure:
       1. Administrative roles 
       2. Backup and recovery cards 
       3. Audit logging 

   
### Deploy HPVS OnPremises
{: #deploy-hpvs-onpremises}

Steps 
:   1. Install HPVS infrastructure
    2. Configure secure networking between HPVS and crypto appliance 
    3. Enable confidential workload support 


### Enable GREP11 Service
{: #enable-grep11-service}

To enable GREP11 service, perform the following steps
:   1. Configure GREP11 endpoint on the crypto appliance 
    2. Define GREP11 domains and roles 
    3. Validate connectivity from HPVS workloads 


## Phase 3 – Cryptographic Configuration Alignment
{: #phase3-cryptographic-configuration-alignment}
### Policy Alignment
{: #policy-alignment}

Ensure consistency between cloud and onprem environments 
:   - Key usage policies 
    - Rotation requirements 
    - Audit and logging rules 
    - Access control models 

  
### Namespace and Object Mapping
{: #namespace-and-object-mapping} 

Map
:   - HPCS key IDs → GREP11 object labels 
    - HPCS IAM roles → GREP11 roles and certificates 
    - Tenants / resource groups → GREP11 domains 
  
    
## Phase 4 – Key Migration or ReKeying
{: #phase4-key-migration-or-rekeying}
### Option A: Wrapped Key Migration
{: #optiona-wrapped-key-migration}

If allowed by policy 
:
    1. Create a symmetric or asymmetric wrapping key in both environments 
    2. Export keys from HPCS in wrapped form 
    3. Import wrapped keys into GREP11 
    4. Verify attributes and usage flags 

### Option B: ReKey and Data ReEncryption (Recommended)
{: #optionb-rekey-and-data-reencryption}

Steps 
:
    1. Generate new keys in onprem GREP11
    2. Update applications to support dual-key operation 
    3. Gradually re-encrypt data with new keys 
    4. Retire old HPCS-backed keys 

## Phase 5 – Application Migration and Validation
{: #phase5-application-migration-and-validation}
### Application Configuration Changes
{: #application-configuration-changes}
    - Update HSM endpoints 
    - Update certificates and trust stores 
    - Adjust session pooling and retry logic 

### Functional Validation
{: #functional-validation}

Validate
:   - Cryptographic operations 
    - Error handling 
    - Failover behavior 
    - Audit event generation 

  
### Performance and Load Testing
{: #performance-and-load-testing}

    - Measure latency and throughput 
    - Tune GREP11 connection settings 
    - Validate appliance capacity planning

## Phase 6 – Cutover and Decommissioning
{: #phase6-cutover-and-decommissioning}
### Cutover Execution
{: #cutover-execution}
    - Freeze key changes in HPCS 
    - Switch production traffic to onprem HPVS 
    - Monitor logs and metrics closely

### Decommission Cloud Resources
{: #decommission-cloud-resources} 
    - Disable applications’ access to HPCS 
    - Destroy or archive cloud keys per compliance policy 
    - Retain audit logs for regulatory retention periods 

## Security, Compliance, and Operational Considerations
{: #security-compliance-and-operational-considerations}
    - Maintain separation of duties (admins vs crypto officers) 
    - Regularly back up GREP11 keys using secure mechanisms 
    - Test disaster recovery procedures 
    - Update SOPs and operational runbooks 

## Risks and Mitigations
{: #risks-and-mitigations}

| Risk | Mitigation  |
|------|-------------|
| Non-exportable keys | Use re-keying strategy  |
| Performance regression  | Pre-cutover load testing |
| Operational errors | Dual-control and change management |
| Compliance gaps |Early audit and policy review | 
{: caption="Risks and Mitigations"}


## Summary
{: #summary}

Migrating from IBM Cloud HPCS to an onpremises HPVS solution with Crypto Appliance and GREP11 provides greater control, data residency assurance, and isolation. A phased migration approach focusing on policy alignment, secure key handling, and thorough validation minimizes risk and ensures continuity of cryptographic operations. 
