---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-18"

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

## How am I charged for my use of {{site.data.keyword.hscrypto}} standard plan?
{: #faq-how-charge-hpcs}
{: faq}
{: support}

Each provisioned operational crypto unit is charged $2.13 USD per hour. If you also enable [failover crypto units](/docs/hs-crypto?topic=hs-crypto-understand-concepts#crypto-unit-concept), each failover crypto unit is also charged the same as the operational crypto unit. 

The first five keystores, including KMS key rings and EP11 keystores, are free of charge. Each additional key ring or EP11 keystore is charged with a tiered pricing starting at $225 USD per month. For keystores that are created or connected less than a month, the cost is prorated based on actual days within the month.

The detailed [pricing plan](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external} is available for your reference.

The following example shows a total charge of 30 days (720 hours). The user enables two operational crypto units and two failover crypto units for cross-region high availability. The user also creates 10 KMS keystores and 12 GREP11 keystores. The first five keystores, including both KMS keystores and GREP11 keystores, are free of charge.

| Pricing components | Cost for 30 days (720 hours) |
|-----|----------------|
| Operational crypto unit 1 | $1533.6 (30x24x2.13) |
| Operational crypto unit 2 | $1533.6 (30x24x2.13) |
| Failover crypto unit 1 | $1533.6 (30x24x2.13) |
| Failover crypto unit 2 | $1533.6 (30x24x2.13) |
| 10 KMS keystores and 12 GREP11 keystores | $3795 (5x0+15x225+2x210) |
| Total charge| $9929.4  |
{: caption="Table 1. A standard plan billing example of 30 days" caption-side="bottom"}


## How am I charged for my use of {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}?
{: #faq-how-charge-hpcs-uko}
{: faq}
{: support}

Each provisioned operational crypto unit is charged $2.13 USD per hour. After you connect to an external keystore of any type, the {{site.data.keyword.uko_full_notm}} base price of $6.25 USD/hour is charged. 

The first five internal keystores and the very first external keystore are free of charge. Each additional internal or external keystore is charged with a tiered pricing starting at $225 USD per month. For keystores that are created or connected less than a month, the cost is prorated based on actual days within the month.

The detailed [pricing plan](/catalog/services/hyper-protect-crypto-services){: external} is available for your reference.

The following example shows a total charge of 30 days (720 hours). The user enables two operational crypto units in the service instance, and creates 22 internal keystores and 15 external keystores. The first five internal keystores and the first external keystore are free of charge.

| Pricing components | Cost for 30 days (720 hours) |
|-----|----------------|
| Operational crypto unit 1 | $1533.6 (30x24x2.13) |
| Operational crypto unit 2 | $1533.6 (30x24x2.13) |
| 22 internal keystores | $3795 (5x0+15x225+2x210) |
| 15 external keystores | $3150 (1x0+14x225) |
| {{site.data.keyword.uko_full_notm}} connection | $4500 (30x24x6.25) |
| Total charge| $14512.2  |
{: caption="Table 2. A {{site.data.keyword.uko_full_notm}} billing example of 30 days" caption-side="bottom"}


## Is there a free trial for {{site.data.keyword.hscrypto}}?
{: #faq-free-trial}
{: faq}

If you have a [promo code](https://www.ibm.com/cloud/hyper-protect-crypto){: external}, you can [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) and get two crypto units at no charge for 30 days.
