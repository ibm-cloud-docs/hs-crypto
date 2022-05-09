---

copyright:
  years: 2022
lastupdated: "2022-04-21"

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}
{:note: .note}

# FAQs: {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}
{: #faq-uko}

Read to get answers for questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}.
{: shortdesc}

## What is the difference between key management, key orchestration, and key governance?
{: #faq-uko-differences}
{: faq}

Key orchestration brings both key management and key governance capabilities into operations within an enterprise: 

* *Key management* is the people, processes, and technology that define how encryption keys exist and operate within an enterprise, including key lifecycle stages, and roles and duties definitions. 
* *Key governance* is the business control that is defined by the security and risk management practices of an enterprise. Key governance ensures encryption key risks are identified, assessed, and addressed by risk mitigation policies and controls, including applicable regulations and compliance requirements.
* *Key orchestration* is the activities and means that initiate and manage encryption keys through their lifecycle within an enterprise, including automation and integration into reporting and monitoring. 

For more information about key management, see [NIST SP 800-57 Part 2 Rev 1 "Recommendation for Key Management: Part 2 – Best Practices for Key Management Organizations"](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt2r1.pdf){: external}.


## Does {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} provide key management, governance, and orchestration at the same time?
{: #faq-uko-functions}
{: faq}

Yes. {{site.data.keyword.uko_full_notm}} provides a simplified means of key management, governance, and orchestration: one place to define, operate, and oversee encryption keys across hybrid multicloud environments.  


## Is {{site.data.keyword.uko_full_notm}} a separate offering?
{: #faq-uko-offering}
{: faq}

No. From a technology point of view, {{site.data.keyword.uko_full_notm}} is a feature of {{site.data.keyword.hscrypto}}. You need to provision and deploy a {{site.data.keyword.hscrypto}} instance to implement and use {{site.data.keyword.uko_full_notm}}. 

## How is {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} different from the {{site.data.keyword.hscrypto}} Standard Plan?
{: #faq-uko-hpcs}
{: faq}

{{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} extends the Standard Plan. {{site.data.keyword.cloud_notm}} is the only cloud service provider that offers native cloud encryption key orchestration and lifecycle management across hybrid multicloud environments, including {{site.data.keyword.cloud_notm}}, IBM Satellite, other cloud service providers, and on-premises environments.  


## What type of HSM is used for {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}?
{: #faq-uko-fips}
{: faq}

{{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} is built on the FIPS 140-2 Level 4 certified HSM as the  {{site.data.keyword.hscrypto}} Standard Plan.

## Which cloud vendors or providers are supported by {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} as connected external keystores?
{: #faq-uko-vendor-cloud}
{: faq}

The following list contains a few cloud providers:

- Keystores of another {{site.data.keyword.hscrypto}} instance
- Keystores of {{site.data.keyword.keymanagementservicefull}}
- Microsoft Azure Key Vault
- AWS Key Management Service





## How is {{site.data.keyword.uko_full_notm}} different from EKMF Web?
{: #faq-uko-ekmf}
{: faq}

IBM&reg; Enterprise Key Management Foundation - Web Edition (EKMF Web) and {{site.data.keyword.uko_full_notm}} share the same code base. 

EKMF Web is an on-premises product for IBM Z14 or Z15 environments, running z/OS V2.3 or z/OS V2.4 and IBM Db2. {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} is a cloud native service in IBM Cloud, which offers key management and orchestration in a hybrid multicloud environment.


## What multizone regions is {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} available in? 
{: #faq-uko-mzr}
{: faq}

{{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} is available in all regions where {{site.data.keyword.hscrypto}} is available. Refer to [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions) for a list of available regions of {{site.data.keyword.hscrypto}}.


## Can I still use {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}} for key management even if {{site.data.keyword.hscrypto}} is not available in the {{site.data.keyword.cloud_notm}} region that my service resides in?
{: #faq-uko-region}
{: faq}

Yes. You can choose a data center within your required data residency region and use {{site.data.keyword.uko_full_notm}} in any regions where {{site.data.keyword.hscrypto}} is available. Note that your encryption keys is managed in the regions where your {{site.data.keyword.hscrypto}} instances are available.

## How many keystores can be created for an instance of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}?
{: #faq-uko-keystore-number}
{: faq}

There is an internal KMS keystore limit of 50, but there is no external keystore limit. The first five internal keystores and the very first external keystore are free of charge. Each additional internal or external keystore is charged with a tiered pricing starting at $225 USD per month. For keystores that are created or connected less than a month, the cost is prorated based on actual days within the month. For more information about pricing, see [the pricing sample](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-how-charge-hpcs-uko).
