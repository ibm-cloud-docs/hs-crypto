---

copyright:
  years: 2018, 2019
lastupdated: "2019-33-22"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# FAQs
{: #faqs}

You can use the following FAQs to help you with {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.

## HSM certifications
{: #HSM-certifications}

### How can I validate that an IBM Crypto Card (HSM) has been validated to meet FIPS 140-2 Level 4?
{: #FIPS-L4}

FIPS 140-2 Level 4 is a very high protection level not widely available in the marketplace. IBM is the leading vendor for highest level certified HSMs, and has invested heavily to maintain this validation for every new generation of cards. The requirement for the high level of assurance has been collected from Government requirements. For validation of the certification, you are pointed to the NIST home page because the certification has been published there. 

### What is the difference between FIPS 140-2 Level 2, 3, and Level 4?
{: #FIPS-levels}

* FIPS 140-2 Level 2: Requirements for tamper evidence done by seals, pick-resistant locks at removeable covers and doors. Tamper-evident coatings or seals are placed on a cryptographic module so that the coating or seal must be broken to attain physical access to the plaintext cryptographic keys and critical security parameters (CSPs) within the module. Security Level 2 requires, at a minimum, role-based authentication in which a cryptographic module authenticates the authorization of an operator to assume a specific role and perform a corresponding set of services.
 
* FIPS 140-2 Level 3: Physical security mechanisms required at Security Level 3 are intended to have a high probability of detecting and responding to attempts at physical access, use or modification of the cryptographic module. Security Level 3 requires identity-based authentication mechanisms, enhancing the security provided by the role-based authentication   mechanisms specified for Security Level 2.  

* FIPS 140-2 Level 4: At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a very high probability of being detected, resulting in the immediate zeroization of all plaintext CSPs (Critical Security Parameters). Security Level 4 cryptographic modules are useful for operation in physically unprotected environments. Security Level 4 also protects a cryptographic module against a security compromise because of environmental conditions or fluctuations outside of the module's normal operating ranges for voltage and temperature. Intentional excursions beyond the normal operating ranges may be used by an attacker to thwart a cryptographic module's defenses.   

## Key management
{: #key-management}

### Can {{site.data.keyword.hscrypto}} be used in combination with {{site.data.keyword.keymanagementserviceshort}} service?

 {{site.data.keyword.hscrypto}} is a managed Crypto Service that comes with a fully compatible {{site.data.keyword.keymanagementserviceshort}} API, that has an identical user experience as Key Protect. The major difference is, that {{site.data.keyword.hscrypto}} relies on an HSM that has been FIPS 140-2 lvl 4 certified. And it provides full control with the HSM master key being managed by the customer (KYOK). The service is dedicated per instance compared to the multi-tenant setup for {{site.data.keyword.keymanagementserviceshort}}. {{site.data.keyword.hscrypto}} also offers HSM capabilities for cryptographic operations like sign/verify, key generate, cryptographic hashing, encrypt/decrypt, and wrap/unwrap. 

### How long can a key name be?
{: #key_names}

You can use a key name that is up to 50 characters in length.

### Can I use language characters as part of the key name?
{: #key_chars}

Language characters, such as Chinese characters, cannot be used as part of the key name.

### What happens when I delete a key?
{: #key_destruction}

When you delete a key, you permanently shred its contents and associated data. The data that was encrypted with the key will no longer be accessible.

Before you delete a key, ensure that you no longer require access to any data that is associated with the key.

## Pricing
{: #pricing}

### Where can I find the detailed pricing information?
{: #pricing_info}

You can refer to the **Pricing** tab on the [{{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){: new_window} for details.

### Is there a pricing example I can refer to?
{: #pricing_example}

Here is one. If you have a requirement of 5000 keys to be crypto-processed, for high availability, you need to set up two crypto units. The amount is $3140 ($1570 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month per crypto unit, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls) per crypto unit. In total, there will be a monthly charge of $3142 ($3140 for the crypto units and $2 for the additional API calls on both crypto units) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1570 |
| Crypto unit 2 | $1570 |
| First 1,000,000 API calls for Crypto unit 1 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 1 | $1 ($0.01 x 100) |
| First 1,000,000 API calls for Crypto unit 2 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 2 | $1 ($0.01 x 100) |
| End of month charge | $3142  |

*Table 1. Charge of two crypto units with monthly API calls of 2,000,000 per crypto unit*
