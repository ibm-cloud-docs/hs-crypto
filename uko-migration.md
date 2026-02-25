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

This document provides a structured guide for migrating from **IBM Cloud Hyper Protect Crypto Services (HPCS) with Unified Key Orchestrator (UKO)** to:

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

- Deploy Red Hat OpenShift on IBM LinuxONE  
- Configure secure networking and TLS  
- Integrate target HSMs  
- Validate container‑security posture  

### 5.2 Prepare z/OS Environment 
{: #prepare-zos}

Steps:

- Configure ICSF and cryptographic domains  
- Set up certificate and RACF controls  
- Validate the availability of hardware cryptography  

### 5.3 Deploy Unified Key Orchestrator 
{: #deploy-uko}

- Install UKO components on LinuxONE or z/OS  
- Configure identity management (LDAP or RACF)  
- Enable high availability, as required  

## 6. Phase 3 – Policy and Configuration Migration 
{: #phase-3-policy-migration}

### 6.1 UKO Configuration Alignment 
{: #uko-configuration-alignment}

Recreate or migrate:

- Key naming conventions  
- Grouping and labels  
- Rotation schedules  
- Notification and approval workflows  

> **Recommendation:** Review and rationalize policies rather than replicate them directly.

### 6.2 Identity and Access Mapping 
{: #identity-access-mapping}

Map:

- IBM Cloud IAM roles → on‑premises identity providers  
- Cloud‑based UKO users → LinuxONE or z/OS identities  
- API credentials → certificate‑based or token‑based authentication  

## 7. Phase 4 – Key Migration or Regeneration 
{: #phase-4-key-migration}

### 7.1 Wrapped Key Migration (When Permitted) 
{: #wrapped-key-migration}

Steps:

- Establish trusted wrapping keys on both platforms  
- Export keys from cloud UKO in wrapped format  
- Import keys into on‑premises UKO keystores  
- Validate attributes and key usability  

### 7.2 Regeneration and Re‑Encryption (Preferred Model)
{: #regeneration-reencryption}

Steps:

- Generate new keys under on‑premises governance  
- Enable dual‑key operation in applications  
- Re‑encrypt data progressively  
- Revoke and archive cloud‑managed keys  

## 8. Phase 5 – Application Migration and Validation 
{: #phase-5-app-migration}

### 8.1 Application Reconfiguration 
{: #application-reconfiguration}

- Update UKO endpoints  
- Adjust authentication mechanisms  
- Validate z/OS or container‑based SDKs  

### 8.2 Functional and Compliance Testing 
{: #functional-compliance-testing}

Validate:

- Cryptographic correctness  
- Policy‑enforcement behavior  
- Completeness of audit trails  
- Error and exception handling  

### 8.3 Performance Validation 
{: #performance-validation}

- Benchmark latency and throughput  
- Validate scale‑out behavior on LinuxONE  
- Confirm workload impact on z/OS  

## 9. Phase 6 – Cutover and Decommissioning 
{: #phase-6-cutover}

### 9.1 Production Cutover 
{: #production-cutover}

- Freeze changes to cloud‑hosted UKO  
- Redirect applications to on‑premises UKO  
- Monitor keys, policies, and audit logs  

### 9.2 Decommission IBM Cloud Resources 
{: #cloud-decommissioning}

- Remove application access to cloud UKO  
- Destroy or archive cloud keys according to compliance rules  
- Retain audit records as required  

## 10. Operational, Security, and Compliance Considerations 
{: #operational-considerations}

- Enforce separation of duties  
- Maintain key backups and test recovery procedures  
- Update operational runbooks  
- Align with regulatory and audit requirements  

## 11. Risks and Mitigations 
{: #risks-mitigations}

| Risk | Mitigation |
|------|------------|
| Policy mismatches | Early governance review |
| Key‑migration constraints | Prefer key regeneration strategy |
| Application incompatibility | Staged migration and thorough testing |
| Operational complexity | Automation and documentation |

## 12. Summary 
{: #summary}

Migrating from **IBM Cloud HPCS with Unified Key Orchestrator** to **UKO on IBM LinuxONE or z/OS** provides greater control, integration depth, and regulatory alignment.  
A phased and policy‑driven approach helps ensure a secure, compliant, and predictable migration while maintaining business continuity.
