---

copyright:
  years: 2018, 2022
lastupdated: "2022-02-28"

keywords: security and compliance, ibmcloud security compliance, compliant, data security, data encryption, data delete, common criteria, fips, iso, gdpr

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:term: .term}

# Security and compliance
{: #uko-security-and-compliance}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} has data security strategies in place to meet your security and compliance needs and ensure that your data remains protected in the cloud.
{: shortdesc}

## Security readiness
{: #uko-security-ready}

{{site.data.keyword.hscrypto}} ensures security readiness by adhering to {{site.data.keyword.IBM_notm}} best practices for systems, networking, and secure engineering.

To learn more about security controls across {{site.data.keyword.cloud_notm}}, see [How do I know that my data is safe](/docs/overview?topic=overview-security#security).
{: tip}

### Data encryption
{: #uko-data-encryption}

{{site.data.keyword.hscrypto}} offers a dedicated [hardware security module (HSM)](#x6704988){: term} to generate key material that you manage and perform [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) operations. {{site.data.keyword.hscrypto}} also supports the management of your own HSM [master keys](#x2908413){: term}. Built on FIPS 140-2 Level 4-certified HSMs, {{site.data.keyword.hscrypto}} offers the highest security level for cloud-based HSMs and stores cryptographic key material without exposing keys outside of a cryptographic boundary.

Access to the service takes place over HTTPS, and internal {{site.data.keyword.hscrypto}} communication uses the Transport Layer Security (TLS) 1.2 protocol to encrypt data in transit.

### Data deletion
{: #uko-data-deletion}

When you delete a key from {{site.data.keyword.hscrypto}}, the service marks the key as deleted, and the key moves to the _Destroyed_ state. Keys in this state can no longer decrypt data that is associated with the key. Therefore, before you delete a key, review the data that is associated with the key and ensure that you no longer require access to it. Do not delete a key that is actively protecting data in your production environments.

Within 30 days after you delete a key, you can restore the key to reverse the deletion. For more information, see [Restoring keys](/docs/hs-crypto?topic=hs-crypto-restore-keys).

Note that even if the key is not restored, your data remains in those services in the encrypted form. Metadata that is associated with a key, such as the key's transition history and name, is kept in the {{site.data.keyword.hscrypto}} database.

To help you determine what data is protected by a key, you can use the key management API to [view associations between a key and your cloud resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources).
{: note}

## Compliance readiness
{: #uko-compliance-ready}

{{site.data.keyword.hscrypto}} helps meet controls for global, industry, and regional compliance standards. The hardware security module (HSM) meets Common Criteria EAL 4 and is FIPS 140-Level 4 certified. The service is GDPR, HIPAA, and ISO certified.

For a complete listing of {{site.data.keyword.cloud_notm}} compliance certifications, see [Compliance on the {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/compliance){: external}.
{: tip}

### Common Criteria EAL4 certified
{: #uko-common-criteria-certified}

As the Hardware Security Module (HSM) used by {{site.data.keyword.hscrypto}}, the {{site.data.keyword.IBM_notm}} PCIe Cryptographic Coprocessor Version 3 (PCIeCC3), also referred to as the IBM 4768 crypto card or the Crypto Express6S (CEX6S), is Common Criteria EAL4 certified to meet the security requirements defined by the Common Criteria for Information Technology Security Evaluation.

Common Criteria is an international standard (ISO/IEC 15408) to assess the security of computer security products. Common Criteria provides assurance that the process of specification, implementation, and evaluation of a computer security product is complied with the standards and requirements defined.



### FIPS 140-2 Level 4
{: #uko-fips}

The Federal Information Processing Standard (FIPS) Publication 140-2 is a US government computer security standard that is used to approve cryptographic modules.

FIPS 140-2 defines four levels of security, including FIPS 140-2 Level 1, 2, 3, and 4. FIPS 140-2 Level 4 is the highest level of security. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a high probability of being detected, resulting in the immediate zeroization of all plaintext critical security parameters (CSPs).

{{site.data.keyword.hscrypto}} uses the IBM 4768 crypto card, which is certified at FIPS 140-2 Level 4, the highest level of certification achievable for commercial cryptographic devices. {{site.data.keyword.hscrypto}} is the only cloud HSM in the public cloud market that is built on an HSM designed to meet FIPS 140-2 Level 4 certification requirements.

The following certificate is for [IBM 4768 Cryptographic Coprocessor Security Module](https://csrc.nist.gov/projects/cryptographic-module-validation-program/Certificate/3410){: external}.

### General Data Protection Regulation
{: #uko-gdpr}

The General Data Protection Regulation (GDPR) seeks to create a harmonized data protection law framework across the European Union and aims to give citizens back the control of their personal data. GDPR also imposes strict rules on enterprises that are hosting and processing data, anywhere in the world.

{{site.data.keyword.IBM_notm}} is committed to providing you with innovative data privacy, security, and governance solutions to assist you in the journey to GDPR readiness.

To ensure GDPR compliance for your {{site.data.keyword.hscrypto}} resources, [enable the EU supported setting](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported) for your {{site.data.keyword.cloud_notm}} account. You can learn more about how {{site.data.keyword.hscrypto}} processes and protects personal data by reviewing the following addendums.

- [{{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Data Sheet Addendum (DSA)](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=46E9C81025D811E895B382FBC780E8BA){: external}
- [{{site.data.keyword.IBM_notm}} Data Processing Addendum (DPA)](https://www.ibm.com/support/customer/csol/terms/?id=DPA-DPL){: external}

### HIPAA support
{: #uko-hipaa-ready}

{{site.data.keyword.hscrypto}} meets controls for the US Health Insurance Portability and Accountability Act (HIPAA) to ensure safeguarding of protected health information (PHI).

If you or your company is a covered entity as defined by HIPAA, you can enable the HIPAA Supported setting for your {{site.data.keyword.cloud_notm}} account. To find out more, see [Enabling the HIPAA Supported setting](/docs/account?topic=account-eu-hipaa-supported#enabling-hipaa).

### IRAP support
{: #uko-IRAP-support}

{{site.data.keyword.hscrypto}} meets the requirements of the Information Security Registered Assessors Program (IRAP) to provide high-quality information and communications technology services to government in support of Australia’s security.

For more information, see [{{site.data.keyword.cloud_notm}} regional compliance programs](https://www.ibm.com/cloud/compliance/regional){: external}.

### ISO 27001, 27017, 27018
{: #uko-iso}

{{site.data.keyword.hscrypto}} is ISO 27001, 27017, 27018 certified. You can view compliance certifications by visiting [Compliance on the {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/compliance){: external}.

### SOC 2 Type 1
{: #uko-soc2-type1}

{{site.data.keyword.hscrypto}} is SOC 2 Type 1 certified. For information about requesting an {{site.data.keyword.cloud_notm}} SOC 2 report, see [Compliance on the {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/compliance){: external}.

