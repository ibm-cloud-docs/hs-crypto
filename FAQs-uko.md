---

copyright:
  years: 2022
lastupdated: "2022-02-10"

keywords: frequently asked questions, cryptographic algorithm, regions, pricing, security compliance, key ceremony, critical security parameters, cryptographic module, security Level, fips, performance, capacity

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:faq: data-hd-content-type='faq'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}

# FAQs: {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}
{: #faq-uko}

Read to get answers for questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}.
{: shortdesc}

## What is Unified Key Orchestrator?
{: #faq-what-is-uko}
{: faq}

Unified Key Orchestrator (UKO) is a new feature of Hyper Protect Crypto Services (HPCS) which provides the only cloud native single-point-of-control of encryption keys across an enterprise's hybrid multicloud. 

* KYOK and BYOK from across hybrid multicloud environments, including on-premises...  
* ... and control all of them with UKO on IBM Cloud.

## What is the difference between key management, key orchestration, and key governance?
{: #faq-uko-differences}
{: faq}

In short: key management is "what and by whom," key governance is "to which degree and how well," and key orchestration is "where and how." 


Key orchestration brings both key management and key governance into operations within an enterprise: 
* key management is the people, processes, and technology which define how encryption keys exist and operate within an enterprise, including key lifecycle stages and roles / duties definitions; 
* key governance is the business controls and oversight defined by an enterprise's security and risk management practices to ensure encryption key risks are identified, assessed, and addressed by risk mitigation policies and controls, including applicable regulations and/or compliance requirements; and 
* key orchestration is the activities and means which initiate and manage encryption keys through their lifecycle within an enterprise, including automation and integration into reporting and monitoring. 


For more information about key management, see NIST SP 800-57 Part 2 Rev 1 "Recommendation for Key Management: Part 2 – Best Practices for Key Management Organizations" https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt2r1.pdf


## Does HPCS + UKO provide all three [key management, governance, and orchestration]?
{: #faq-uko-functions}
{: faq}

Yes; UKO provides a simplified means of key management, governance, and orchestration: one place to define, operate, and oversee encryption keys across hybrid multicloud environments.  


## Is UKO a separate offering?
{: #faq-uko-offering}
{: faq}

No, from a technology point of view -- UKO is a feature of HPCS; HPCS must be deployed / provisioned to implement and use UKO.  The HPCS differentiator of keys being backed by the highest security HSM available applies to UKO as well; IBM's EP11 HSM -- the only FIPS 140-2 Level 4-certified HSM available on the market.


## How is UKO different from HPCS?
{: #faq-uko-hpcs}
{: faq}

UKO extends "base" HPCS and introduces another market differentiation for IBM Cloud: IBM Cloud is the only cloud service provider offering native cloud encryption key orchestration (lifecycle management) across hybrid multicloud environments: IBM Cloud, IBM Satellite, other cloud service providers, and on-premises.  


## Can we claim FIPS differentiation for UKO?
{: #faq-uko-fips}
{: faq}

Yes; UKO is built on / extends HPCS, which includes IBM's EP11 HSM -- the only HSM certified to the highest available level (FIPS 140-2 Level 4 certification).


## What is the UKO pricing?
{: #faq-pricing-uko}
{: faq}

PLEASE CONFIRM PRICING FOR GA -- monthly vs hourly etc

## Which on-cloud vendors / providers are supported by UKO?
{: #faq-uko-vendor-cloud}
{: faq}

IBM Cloud Hyper Protect Crypto Services
IBM Cloud Key Protect
Microsoft Azure Key Vault
Google Cloud Key Management (RP-3 not in MDE)
AWS Key Management System


## Which on-premises vendors / providers are supported by UKO?
{: #faq-uko-vendor-onprem}
{: faq}

IBM Enterprise Key Management Foundation - Web Edition (EKMF Web)
Pervasive Encryption on LinuxONE
Pervasive Encryption on Linux on Z (zKey)
IBM® Security Guardium® Key Lifecycle Manager
{Need more info here}


## How is UKO different from EKMF Web?
{: #faq-uko-ekmf}
{: faq}

EKMF Web and Unified Key Orchestrator share the same base. Both are developed in parallel with EKMF Web being an on-premises product for IBM Z14 or Z15 environments, running z/OS V2.3 or z/OS V2.4 and DB2.


| Product | Attribute | Details |
| ------- | ----------- | ----------------------- |
|IBM EKMF Web|on-premises|requires IBM Z14 or IBM Z15; running z/OS v2.3, 2.4 or 2.5, Db2 12.1+ and Websphere Application Server Liberty 21.0.0.3+; TKE is required to create the EKMF Web; Disaster Recovery Key in a form that enables an organization to restore the key in the CKDS; CAPEX; Operated by client|
|IBM Cloud UKO|on-cloud|"as a Service", cloud native in IBM Cloud; based on customer setup/ security posture; SmartCard based setup requires purchase of Smart Cards, card reader(s); OPEX for service; CAPEX for SCs, readers, etc. ; service operated by client; IaaS / PaaS by IBM Cloud|
{: caption="Table 1. Differences between EKMF Web and {{site.data.keyword.uko_full_notm}}" caption-side="bottom"}

## What multizone regions (MZRs) is UKO available in? 
{: #faq-uko-mzr}
{: faq}

UKO is available in all the regions where IBM Cloud Hyper Protect Crypto Services is available, which are Dallas, Washington DC, Frankfurt, Sydney, London and Tokyo. Coming soon to São Paulo and Toronto.


## I don't see HPCS available in <x> region and my customer has data residency requirements. Can they still use UKO? 
{: #faq-uko-region}
{: faq}

Yes, if the client is comfortable with their encryption keys residing in region(s) where HPCS is available.  Client can choose data center within their required data residency region and use IBM Cloud Hyper Protect Crypto Services and UKO where it is available. 