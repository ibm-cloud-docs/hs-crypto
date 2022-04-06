---

copyright:
  years: 2020, 2022
lastupdated: "2022-04-06"

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

# FAQs: {{site.data.keyword.hscrypto}} Standard Plan
{: #faq-performance-capacity}

Read to get answers for questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} Standard Plan.
{: shortdesc}

## How many keys can be stored in a {{site.data.keyword.hscrypto}} service instance?
{: #faq-keys-number}
{: faq}

A {{site.data.keyword.hscrypto}} service instance can hold a maximum of 5000 keys.


## How many key rings can be created for a {{site.data.keyword.hscrypto}} service instance?
{: #faq-keyrings-number}
{: faq}

There is a KMS key ring limit of 50, but there is no GREP11 keystore limit. However, you can create as many as five keystores, including KMS key rings and EP11 keystores, free of charge. Each additional key ring or EP11 keystore is charged with a tiered pricing starting at $225 USD per month. For more information about pricing, see [the pricing sample](/docs/hs-crypto?topic=hs-crypto-faq-pricing#faq-how-charge-hpcs).

## Can I add or remove crypto units after I provision a service instance?
{: #faq-add-remove-crypto-unit}
{: faq}

Yes, you can request to add or remove crypto units by raising support tickets in the IBM Support Center. For detailed instructions, see [Adding or removing crypto units](/docs/hs-crypto?topic=hs-crypto-add-remove-crypto-units).

## Is there a Service Level Agreement (SLA) specifically for {{site.data.keyword.hscrypto}}?
{: #faq-hpcs-sla}
{: faq}

Yes, you can find the [SLA](https://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-8506-01){: external} for detailed terms.
