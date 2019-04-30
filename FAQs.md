---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-29"

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

## What's {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #what-is-hpcs}

{{site.data.keyword.cloud_notm}}  {{site.data.keyword.hscrypto}} is a dedicated key management and cloud HSM service that provides:

* A dedicated key management service with Bring Your Own Key data-at-rest encryption with customer-managed keys in IBM Cloud’s data and storage services.
* A cloud HSM for cryptographic operations utilizing FIPS 140-2 Level 4 certified HSM Hardware.

## How do I know if {{site.data.keyword.hscrypto}} is right for my company?
{: #choose-hs-crypto}

With {{site.data.keyword.hscrypto}} you can ensure regulatory compliance and strengthen data security by protecting data with encryption keys in IBM’s fully managed, dedicated key management system and cloud HSM service that supports Keep Your Own Key. Keep your own  keys for cloud data encryption protected by a dedicated cloud HSM.

If you are concerned on data security and compliance in the cloud, you are able to maintain complete control over data encryption and signature keys in a cloud consumable HSM with industry-leading security for cloud data and digital assets, regulatory compliance support through data encryption and controls on privileged access. {{site.data.keyword.cloud_notm}} administrators have no access to the keys.

Key features are:

* Full control of the entire key hierarchy including the HSM master keys
* Industry-leading security for cloud data and digital  assets
* Reduced data compromise risk because of in-built protection against privileged access threats
* Regulatory compliance through data encryption and controls on privileged  access

## Why is {{site.data.keyword.hscrypto}} better than other cloud HSMs or key management services?
{: #hs-crypto-advantages}

This is the only cloud HSM in the public cloud market to be built on FIPS 140-2 Level 4 certified hardware. Additionally, IBM offers a unique initialization scheme  through a key ceremony to take ownership of the HSM (bring your own administrator), supporting multiple distinct roles with administration and HSM master key management responsibilities. This provides you with complete control of the key hierarchy including the HSMs that protect your keys.

## What is a 140-2 FIPS Level 4 Certification and how can I validate it?
{: #FIPS-level4-meaning}

The Federal Information Processing Standard (FIPS) Publication 140-2 is a U.S. government computer security standard that is used to approve cryptographic modules.

* [Security Requirements for Cryptographic Modules ![External link icon](image/external_link.svg "External link icon")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}.
* [Cryptographic Module Validation Program ![External link icon](image/external_link.svg "External link icon")](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Standards){:new_window}.
* FIPS 140-2 defines four levels of security, including FIPS 140-2 Level 1, 2, 3, and Level 4.

## What is the difference between FIPS 140-2 Level 1, 2, 3, and Level 4?
{: #FIPS-levels}

* **Level 1**: The lowest level of security. No specific physical security mechanisms are required in a Security Level 1 cryptographic module beyond the basic requirement for production-grade components.
* **Level 2**: Improves the physical security mechanisms of a Level 1 cryptographic module by requiring features that show evidence of tampering, including tamper-evident coatings or seals that must be broken to attain physical access to the plaintext cryptographic keys and critical security parameters (CSPs) within the module, or pick-resistant locks on covers or doors to protect against unauthorized physical access. Security Level 2 requires, at minimum, role-based authentication in which a cryptographic module authenticates the authorization of an operator to assume a specific role and perform a corresponding set of services.
* **Level 3**: Provides a high probability of detecting and responding to attempts at physical access, use or modification of the cryptographic module. The physical security mechanisms can include the use of strong enclosures and tamper-detection/response circuitry that zeroizes all plaintext CSPs when the removable covers/doors of the cryptographic module are opened. Security Level 3 requires identity-based authentication mechanisms, enhancing the security provided by the role-based authentication mechanisms specified for Security Level 2.
* **Level 4**: The highest level of security. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a very high probability of being detected of all plaintext CSPs.

  Security Level 4 cryptographic modules are useful for operation in physically unprotected environments. Security Level 4 also protects a cryptographic module against a security compromise because of environmental conditions or fluctuations outside of the module's normal operating ranges for voltage and temperature. Intentional excursions beyond the normal operating ranges can be used by an attacker to prevent a cryptographic module's defenses.

  A cryptographic module is required to either include special environmental protection features designed to detect fluctuations and delete CSPs, or to undergo environmental failure testing to ensure that the module will not be affected by fluctuations outside of the normal operating range in a manner that can compromise the security of the module. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a very high probability of being detected, resulting in the immediate zeroization of all plaintext CSPs.

  {{site.data.keyword.hscrypto}} is the only cloud HSM in the public cloud market built on an HSM designed to meet FIPS 140-2 Level 4 certification requirements. The certification was achieved on 3/20/19 and is listed on the Cryptographic Module Validation Pgram (CVMP) Validated Modules List ![External link icon](image/external_link.svg "External link icon")]](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules){:new_window}.

## What crypto card does {{site.data.keyword.hscrypto}} use?
{: #crypto-card}

{{site.data.keyword.hscrypto}} use the IBM 4768 crypto card, also referred to as Crypto Express 6S (CEX6S). IBM CEX6S is designed to be certified at FIPS 140-2 Level 4, the highest level of certification achievable for commercial cryptographic devices. The certification was achieved on 3/20/19 and is listed on the Cryptographic Module Validation Pgram (CVMP) Validated Modules List ![External link icon](image/external_link.svg "External link icon")](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules){:new_window}.

For  more information, see the [IBM CryptoCards page ![External link icon](image/external_link.svg "External link icon")](https://www.ibm.com/security/cryptocards/cryptonews){:new_window} and [IBM CryptoCards Overview ![External link icon](image/external_link.svg "External link icon")](https://www.ibm.com/security/cryptocards/pciecc3/overview){:new_window}.

## What is Hardware Security Module?
{: #what-is-hsm}

A Hardware Security Module (HSM) provides secure key storage and cryptographic operations within a tamper-resistant hardware device for sensitive data. HSMs are used to provision cryptographic keys and are designed to securely store cryptographic key material and use the key material without exposing it outside the cryptographic boundary of the hardware.

## How is this service different from {{site.data.keyword.cloud_notm}} HSM?
{: #differentiators-cloud-hsm}

IBM has an IaaS [{{site.data.keyword.cloud_notm}} HSM service, which is different from the {{site.data.keyword.hscrypto}}. {{site.data.keyword.cloud_notm}} HSM is FIPS 140-2 Level 3 compliant.
{{site.data.keyword.hscrypto}} is a managed HSM service where no special skills are needed to manage the HSM other than loading of the keys. High availability, backup (currently is backed up daily by the service and is not triggered by users), and scaling can all be done using cloud APIs. This is also the only cloud HSM built on FIPS 140-2 Level 4 certified hardware.

## I have workloads running in a data center where {{site.data.keyword.hscrypto}} is not available. Can I still subscribe to this service?
{: #data-center-question}

Yes. {{site.data.keyword.hscrypto}} can be accessed remotely worldwide for key management and cloud HSM capabilities.

## What is key management?
{: #what-key-management}

{{site.data.keyword.hscrypto}} integrates with [{{site.data.keyword.keymanagementservicefull}} ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/catalog/services/key-protect){:new_window} for {{site.data.keyword.cloud_notm}} APIs to generate and encrypt keys. The Keep Your Own Keys function is also enabled by {{site.data.keyword.hscrypto}} to provide access to cryptographic hardware that is FIPS 140-2 Level 4 certified technology, the highest level attainable certification level. {{site.data.keyword.hscrypto}} offers network addressable HSMs.

## Can {{site.data.keyword.hscrypto}} be used in combination with {{site.data.keyword.keymanagementserviceshort}} service?
{: #combine-with-Key-Protect}

IBM offers multiple options for you to look to protect your data in the cloud, based on the level of control you need.

It’s ultimately based upon the level of control and security your business requires.

<table><tr><th>Capabilities</th>
<th>{{site.data.keyword.keymanagementserviceshort}}</th>
<th>{{site.data.keyword.hscrypto}}</th>
</tr>
</thead>
<tbody><tr><td rowspan="2">Key management</td>
<td><p>Multi-tenant key management service with key vaulting provided by IBM controlled, FIPS 140-2 Level 3 compliant HSMs.</p>

<p>Provides Bring-Your-Own-Key (BYOK) support for you to use your own keys for data protection.</p>
</td>
<td><p>Single-tenant key management service with key vaulting provided by dedicated and customer-controlled FIPS 140-2 Level 4 compliant HSMs.</p>

<p>Provides Keep-Your-Own-Key (KYOK) (that is, BYOK with more customer control) support for you to completely own your data encryption keys and HSMs.</p>
</td>
</tr>
<tr><td colspan="2">Common key provider API, providing a consistent approach for integration to adopting services.</td>
</tr>
<tr><td>Cloud HSM</td>
<td>N/A</td>
<td>Managed FIPS 140-2 Level 4 certified HSMs that supports industry standards to provide industry-leading security for cloud data and digital assets.</td>
</tr>
</tbody>
 <caption style="caption-side:bottom;">Table 1. Comparing {{site.data.keyword.keymanagementserviceshort}} with {{site.data.keyword.hscrypto}}</caption>
</table>

## How is {{site.data.keyword.hscrypto}} different from {{site.data.keyword.keymanagementserviceshort}}?
{: #differentiators}

{{site.data.keyword.keymanagementservicefull}} is a multi-tenant key management service with key vaulting provided by FIPS 140-2 Level 3 IBM-managed HSMs.

{{site.data.keyword.hscrypto}} is a single-tenant service designed for you to look for complete control of your data encryption keys and cloud HSMs that protect these keys. Additionally, this service also supports industry standards such as Public-Key Cryptography Standards #11 (PKCS #11) for cryptographic services like digital signing and Secure Sockets Layer (SSL) offloading.

## How long can a key name be?
{: #key-name-length}

You can use a key name that is up to 50 characters in length.

## Can I use language characters as part of the key name?
{: #key-name-rules}

Language characters, such as Chinese characters, cannot be used as part of the key name.

## What happens when I delete a key?
{: #delete-a-key}

When you delete a key, you permanently shred its contents and associated data. The data that was encrypted with the key will no longer be accessible.

Before you delete a key, ensure that you no longer require access to any data that is associated with the key.

## Where can I find the detailed pricing information?
{: #pricing_info}

Pricing can be found on the [{{site.data.keyword.hscrypto}} catalog page ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services?cm_mc_uid=31713117745615537421882&cm_mc_sid_50200000=37117111555483426683&cm_mc_sid_52640000=50865531555483426686){:new_window}, or on the **Pricing** tab of the [{{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){: new_window}.

## Is there a pricing example I can refer to?
{: #pricing_example}

Here is one. If you want to crypto-process 5000 keys using {{site.data.keyword.hscrypto}}, for high availability, you need to set up two crypto units. The amount is $3120 ($1560 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month per crypto unit, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls) per crypto unit. In total, there will be a monthly charge of $3142 ($3140 for the crypto units and $2 for the additional API calls on both crypto units) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1560 |
| Crypto unit 2 | $1560 |
| First 1,000,000 API calls for Crypto unit 1 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 1 | $1 ($0.01 x 100) |
| First 1,000,000 API calls for Crypto unit 2 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 2 | $1 ($0.01 x 100) |
| End of month charge | $3122  |

*Table 1. Charge of two crypto units with monthly API calls of 2,000,000 per crypto unit*

<!--
## HSM certifications
{: #HSM-certifications}

### How can I validate that an IBM Crypto Card (HSM) has been validated to meet FIPS 140-2 Level 4?
{: #FIPS-L4}

FIPS 140-2 Level 4 is a very high protection level not widely available in the marketplace. IBM is the leading vendor for highest level certified HSMs, and has invested heavily to maintain this validation for every new generation of cards. The requirement for the high level of assurance has been collected from Government requirements. For validation of the certification, you are pointed to the NIST home page because the certification has been published there. 

### What is the difference between FIPS 140-2 Level 2, 3, and Level 4?
{: #FIPS-levels}

* FIPS 140-2 Level 2: Requirements for tamper evidence done by seals, pick-resistant locks at removeable covers and doors. Tamper-evident coatings or seals are placed on a cryptographic module so that the coating or seal must be broken to attain physical access to the plaintext cryptographic keys and critical security parameters (CSPs) within the module. Security Level 2 requires, at minimum, role-based authentication in which a cryptographic module authenticates the authorization of an operator to assume a specific role and perform a corresponding set of services.
 
* FIPS 140-2 Level 3: Physical security mechanisms required at Security Level 3 are intended to have a high probability of detecting and responding to attempts at physical access, use or modification of the cryptographic module. Security Level 3 requires identity-based authentication mechanisms, enhancing the security provided by the role-based authentication mechanisms specified for Security Level 2.  

* FIPS 140-2 Level 4: At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a very high probability of being detected, resulting in the immediate zeroization of all plaintext CSPs. Security Level 4 cryptographic modules are useful for operation in physically unprotected environments. Security Level 4 also protects a cryptographic module against a security compromise because of environmental conditions or fluctuations outside of the module's normal operating ranges for voltage and temperature. Intentional excursions beyond the normal operating ranges may be used by an attacker to thwart a cryptographic module's defenses.   

## Key management
{: #key-management}

### Can {{site.data.keyword.hscrypto}} be used in combination with {{site.data.keyword.keymanagementserviceshort}} service?

 {{site.data.keyword.hscrypto}} is a managed Crypto Service that comes with a fully compatible {{site.data.keyword.keymanagementserviceshort}} API, that has an identical user experience as {{site.data.keyword.keymanagementserviceshort}}. The major difference is, that {{site.data.keyword.hscrypto}} relies on an HSM that has been FIPS 140-2 Level 4 certified. And it provides full control with the HSM master key being managed by the user (KYOK). The service is dedicated per instance compared to the multi-tenant setup for {{site.data.keyword.keymanagementserviceshort}}. {{site.data.keyword.hscrypto}} also offers HSM capabilities for cryptographic operations like sign/verify, key generate, cryptographic hashing, encrypt/decrypt, and wrap/unwrap. 

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

Here is one. If you want to crypto-process 5000 keys using {{site.data.keyword.hscrypto}}, for high availability, you need to set up two crypto units. The amount is $3120 ($1560 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month per crypto unit, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls) per crypto unit. In total, there will be a monthly charge of $3142 ($3140 for the crypto units and $2 for the additional API calls on both crypto units) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1560 |
| Crypto unit 2 | $1560 |
| First 1,000,000 API calls for Crypto unit 1 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 1 | $1 ($0.01 x 100) |
| First 1,000,000 API calls for Crypto unit 2 | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) for Crypto unit 2 | $1 ($0.01 x 100) |
| End of month charge | $3122  |

*Table 1. Charge of two crypto units with monthly API calls of 2,000,000 per crypto unit*

-->
