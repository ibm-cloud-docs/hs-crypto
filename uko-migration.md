---

copyright:
  years: 2018, 2026
lastupdated: "2026-02-25"

keywords: migration, migration guide, migration to on-prem

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

# Migration Guide for IBM Cloud Hyper Protect Crypto Services with Unified Key Orchestrator 
{: #migration-guide}

## 1. Purpose and Scope 
{: #purpose-and-scope}

This topic provides structured guidance for migrating from **IBM Cloud Hyper Protect Crypto Services (HPCS) with Unified Key Orchestrator (UKO)** to:

- **Unified Key Orchestrator for Containers on IBM LinuxONE**, or  
- **Unified Key Orchestrator for z/OS**.

The guide focuses on:

- Cryptographic key‑management governance  
- Policy and configuration migration  
- Application integration  
- Operational continuity across hybrid‑cloud and on‑premises environments  

The intended audience includes security architects, cryptographic officers, platform engineers, and compliance stakeholders.

## 2. Source and Target Architecture Overview 
{: #architecture-overview}

### 2.1 Source Environment: IBM Cloud HPCS with Unified Key Orchestrator 
{: #source-environment}

**Characteristics**

- Managed service running on IBM Cloud  
- Backed by a **FIPS 140‑2 Level 4** Hardware Security Module (HSM)  
- Unified Key Orchestrator providing:  
  - Centralized, policy‑based key‑lifecycle management  
  - Multi‑HSM and multi‑service orchestration  
  - REST API and CLI interfaces  
- Integrates with:  
  - IBM Cloud HPCS  
  - External keystores  
  - Cloud‑native applications  
- Shared responsibility model between IBM and the customer  

### 2.2 Target Environment: On‑Premises Unified Key Orchestrator 
{: #target-environment}

#### 2.2.1 UKO for Containers on IBM LinuxONE 
{: #uko-linuxone}

**Characteristics**

- Customer‑managed UKO deployed as containerized services  
- Runs on Red Hat OpenShift on IBM LinuxONE  
- Uses on‑premises HSMs (Crypto Express, Crypto appliances, and so on)  
- Provides high availability and horizontal scalability  

#### 2.2.2 UKO for z/OS 
{: #uko-zos}

**Characteristics**

- Native UKO deployment integrated with z/OS  
- Tight integration with ICSF and z/OS cryptographic services  
- Supports workloads requiring:  
  - Low latency  
  - High throughput  
  - z/OS‑native security controls  

In both deployment models, customers assume full responsibility for infrastructure, security, and operations.

## 3. Migration Strategy 
{: #migration-strategy}

The migration adopts a **governance‑first, phased approach**:

1. Discovery and assessment  
2. Target‑platform preparation  
3. Policy and configuration migration  
4. Key migration or regeneration  
5. Application integration and validation  
6. Production cutover and decommissioning  

This structured approach minimizes disruption while maintaining compliance and audit readiness.

## 4. Phase 1 – Discovery and Assessment 
{: #phase-1-discovery}

### 4.1 Inventory of Managed Keys
{: #inventory-of-keys}

Collect the following from IBM Cloud UKO:

- Key types (symmetric, asymmetric, wrapping keys)  
- Key aliases and groups  
- Lifecycle state and rotation policies  
- Associated keystores and HSM backends  
- Allowed cryptographic operations  

### 4.2 Policy and Governance Analysis 
{: #policy-governance-analysis}

Capture existing governance constructs:

- Key‑access policies  
- Approval workflows (multi‑party control)  
- Separation‑of‑duties models  
- Audit and data‑retention configurations  

### 4.3 Application Dependency Mapping 
{: #application-dependency-mapping}

For each application:

- UKO APIs consumed  
- HSM dependency (HPCS, GREP11, PKCS#11)  
- SLA and latency requirements  
- Platform dependency (cloud, Linux, z/OS)  

## 5. Phase 2 – Target Platform Preparation 
{: #phase-2-preparation}

### 5.1 Prepare LinuxONE Container Platform 
{: #prepare-linuxone}

Steps:

1. Deploy Red Hat OpenShift on IBM LinuxONE  
1. Configure secure networking and TLS  
1. Integrate target HSMs  
1. Validate container‑security posture  

### 5.2 Prepare z/OS Environment 
{: #prepare-zos}

Steps:

1. Configure ICSF and cryptographic domains  
1. Set up certificate and RACF controls  
1. Validate the availability of hardware cryptography  

### 5.3 Deploy Unified Key Orchestrator 
{: #deploy-uko}

1. Install UKO components on LinuxONE or z/OS  
1. Configure identity management (LDAP or RACF)  
1. Enable high availability, as required  

## 6. Phase 3 – Policy and Configuration Migration 
{: #phase-3-policy-migration}

### 6.1 UKO Configuration Alignment 
{: #uko-configuration-alignment}

Recreate or migrate:

1. Key naming conventions  
1. Grouping and labels  
1. Rotation schedules  
1. Notification and approval workflows  

> **Recommendation:** Review and rationalize policies rather than replicate them directly.

### 6.2 Identity and Access Mapping 
{: #identity-access-mapping}

Map:

1. IBM Cloud IAM roles → on‑premises identity providers  
1. Cloud‑based UKO users → LinuxONE or z/OS identities  
1. API credentials → certificate‑based or token‑based authentication  

## 7. Phase 4 – Key Migration or Regeneration 
{: #phase-4-key-migration}

### 7.1 Wrapped Key Migration (When Permitted) 
{: #wrapped-key-migration}

Steps:

1. Establish trusted wrapping keys on both platforms  
1. Export keys from cloud UKO in wrapped format  
1. Import keys into on‑premises UKO keystores  
1. Validate attributes and key usability  

### 7.2 Regeneration and Re‑Encryption (Preferred Model)
{: #regeneration-reencryption}

Steps:

1. Generate new keys under on‑premises governance  
1. Enable dual‑key operation in applications  
1. Re‑encrypt data progressively  
1. Revoke and archive cloud‑managed keys  

## 8. Phase 5 – Application Migration and Validation 
{: #phase-5-app-migration}

### 8.1 Application Reconfiguration 
{: #application-reconfiguration}

1. Update UKO endpoints  
1. Adjust authentication mechanisms  
1. Validate z/OS or container‑based SDKs  

### 8.2 Functional and Compliance Testing 
{: #functional-compliance-testing}

Validate:

1. Cryptographic correctness  
1. Policy‑enforcement behavior  
1. Completeness of audit trails  
1. Error and exception handling  

### 8.3 Performance Validation 
{: #performance-validation}

1. Benchmark latency and throughput  
1. Validate scale‑out behavior on LinuxONE  
1. Confirm workload impact on z/OS  

## 9. Phase 6 – Cutover and Decommissioning 
{: #phase-6-cutover}

### 9.1 Production Cutover 
{: #production-cutover}

1. Freeze changes to cloud‑hosted UKO  
1. Redirect applications to on‑premises UKO  
1. Monitor keys, policies, and audit logs  

### 9.2 Decommission IBM Cloud Resources 
{: #cloud-decommissioning}

1. Remove application access to cloud UKO  
1. Destroy or archive cloud keys according to compliance rules  
1. Retain audit records as required  

## 10. Operational, Security, and Compliance Considerations 
{: #operational-considerations}

1. Enforce separation of duties  
1. Maintain key backups and test recovery procedures  
1. Update operational runbooks  
1. Align with regulatory and audit requirements  

## 11. Risks and Mitigations 
{: #risks-mitigations}

| Risk | Mitigation |
|------|------------|
| Policy mismatches | Early governance review |
| Key‑migration constraints | Prefer key regeneration strategy |
| Application incompatibility | Staged migration and thorough testing |
| Operational complexity | Automation and documentation |
{: caption="Risks and Mitigations" caption-side="bottom"}

## 12. Summary 
{: #summary}

Migrating from **IBM Cloud HPCS with Unified Key Orchestrator** to **UKO on IBM LinuxONE or z/OS** provides greater control, integration depth, and regulatory alignment.  
A phased and policy‑driven approach helps ensure a secure, compliant, and predictable migration while maintaining business continuity.
