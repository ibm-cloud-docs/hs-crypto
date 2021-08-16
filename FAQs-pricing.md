---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-16"

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
{:note: .note}

# FAQs: Pricing
{: #faq-pricing}

Read to get answers for questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} pricing.
{: shortdesc}

## How am I charged for my use of {{site.data.keyword.hscrypto}}?
{: #faq-how-charge-hpcs}
{: faq}
{: support}

Each provisioned operational crypto unit is charged $1560 USD per calendar month. If you also enable [failover crypto units](/docs/hs-crypto?topic=hs-crypto-understand-concepts#crypto-unit-concept), each failover crypto unit is also charged the same as the operational crypto unit. The first 1,000,000 API calls per service instance are free of charge. After that, each 10,000 API calls are billed at a rate of $0.01 USD. The detailed [pricing plan](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external} is available for your reference.

{{site.data.keyword.cloud_notm}} account billing cycles are based on Universal Time Coordinated (UTC). The billing cycle begins at 00:00:00 UTC on the first day of the month and ends at 23:59:59 UTC on the last calendar day of the month. For example, if you create a service instance on 15 August and delete it on 15 September, it is counted as two calendar months and you are charged $3120 per crypto unit.
{: note}

The following example is for your reference. If you want to crypto-process 5000 keys by using two operational crypto units and two failover crypto units for cross-region high availability, the amount is $6240 ($1560 per crypto unit) per calendar month. The first 1,000,000 API calls per service instance are free of charge. However, if you perform 3,000,000 API calls per month, you are charged extra $2 ($0.01 per 10,000 API calls over 1,000,000 API calls). In total, there is a monthly charge of $6242 ($3120 for the two operational crypto units, $3120 for the two failover crypto units, and $2 for the extra 2,000,000 API calls) for your service instance. The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Operational crypto unit 1 | $1560 |
| Operational crypto unit 2 | $1560 |
| Failover crypto unit 1 | $1560 |
| Failover crypto unit 2 | $1560 |
| First 1,000,000 API calls | $0 |
| 2,000,000 extra API calls| $2 ($0.01 x 200) |
| End of month charge | $6242  |
{: caption="Table 1. A billing example of two operational and two failover crypto units with monthly API calls of 3,000,000 in total" caption-side="bottom"}

## Is there a free trial for {{site.data.keyword.hscrypto}}?
{: #faq-free-trial}
{: faq}

If you have a [promo code](https://www.ibm.com/cloud/hyper-protect-crypto){: external}, you can [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) and get two crypto units at no charge for 30 days.
