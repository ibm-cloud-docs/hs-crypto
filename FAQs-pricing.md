---

copyright:
  years: 2020, 2022
lastupdated: "2022-01-30"

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

Each provisioned operational crypto unit is charged $1560 USD per calendar month. If you also enable [failover crypto units](/docs/hs-crypto?topic=hs-crypto-understand-concepts#crypto-unit-concept), each failover crypto unit is also charged the same as the operational crypto unit. The detailed [pricing plan](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external} is available for your reference.

{{site.data.keyword.cloud_notm}} account billing cycles are based on Universal Time Coordinated (UTC). The billing cycle begins at 00:00:00 UTC on the first day of the month and ends at 23:59:59 UTC on the last calendar day of the month. For example, if you create a service instance on 15 August and delete it on 15 September, it is counted as two calendar months and you are charged $3120 per crypto unit.
{: note}

The following example is for your reference. If you want to crypto-process 5000 keys by using two operational crypto units and two failover crypto units for cross-region high availability, this would result in a total charge of $6240 ($1560 per crypto unit) per calendar month.

| Pricing components | Cost per month |
|-----|----------------|
| Operational crypto unit 1 | $1560 |
| Operational crypto unit 2 | $1560 |
| Failover crypto unit 1 | $1560 |
| Failover crypto unit 2 | $1560 |
| End of month charge | $6240  |
{: caption="Table 1. A billing example of two operational and two failover crypto units" caption-side="bottom"}

## Is there a free trial for {{site.data.keyword.hscrypto}}?
{: #faq-free-trial}
{: faq}

If you have a [promo code](https://www.ibm.com/cloud/hyper-protect-crypto){: external}, you can [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) and get two crypto units at no charge for 30 days.
