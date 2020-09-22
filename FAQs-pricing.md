---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: frequently asked questions, cryptographic algorithm, regions, pricing, security compliance, key ceremony, critical security parameters, cryptographic module, security Level, fips, provisioning and operations

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

# FAQs: Pricing
{: #faq-pricing}

This topic can help you with questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} pricing.
{: shortdesc}

## How am I charged for my use of {{site.data.keyword.hscrypto}}?
{: #faq-how-charge-hpcs}
{: faq}
{: support}

A monthly charge for each provisioned crypto unit and API calls is billed at a rate of $0.01 USD per 10,000 API calls over 1 million API calls. The detailed [pricing plan](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external} is available for your reference.

For example, if you want to crypto-process 5000 keys by using {{site.data.keyword.hscrypto}}, for high availability, you need to set up two crypto units. The amount is $3120 ($1560 per crypto unit) per month. The first 1,000,000 API calls per crypto unit are free of charge. However, if you perform 2,000,000 API calls per month per crypto unit, you are charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls) per crypto unit. In total, there is a monthly charge of $3142 ($3140 for the crypto units and $2 for the additional API calls on both crypto units) for your service instance. The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1560 |
| Crypto unit 2 | $1560 |
| First 1,000,000 API calls for Crypto unit 1 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 1 | $1 ($0.01 x 100) |
| First 1,000,000 API calls for Crypto unit 2 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 2 | $1 ($0.01 x 100) |
| End of month charge | $3122  |
{: caption="Table 1. A billing example of two crypto units with monthly API calls of 2,000,000 per crypto unit" caption-side="bottom"}

## Is there a free trial for {{site.data.keyword.hscrypto}}?
{: #faq-free-trial}
{: faq}

Yes, a free trial period of 30 days is available for {{site.data.keyword.hscrypto}}. 
