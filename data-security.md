---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-23"

keywords: Hyper Protect Crypto Services, data security, Hyper Protect Crypto Services compliance, encryption key deletion

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

# Security and compliance
{: #security-and-compliance}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} has data security strategies in place to meet your compliance needs and ensure your data remains secure and protected in the cloud.
{: shortdesc}

## Security readiness
{: #security-ready}

{{site.data.keyword.hscrypto}} ensures security readiness by adhering to {{site.data.keyword.IBM_notm}} best practices for systems, networking, and secure engineering.

To learn more about security controls across {{site.data.keyword.cloud_notm}}, see [How do I know that my data is safe?](/docs/overview?topic=overview-security#security).
{: tip}

### Data encryption
{: #data-encryption}

{{site.data.keyword.hscrypto}} offers a dedicated hardware security module (HSM) to generate key material that you manage and perform [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) operations. {{site.data.keyword.hscrypto}} also supports the management of your own HSM master keys. Built on FIPS 140-2 Level 4-certified HSMs, {{site.data.keyword.hscrypto}} offers the highest security level for cloud-based HSMs and stores cryptographic key material without exposing keys outside of a cryptographic boundary.

Access to the service takes place over HTTPS, and internal {{site.data.keyword.hscrypto}} communication uses the Transport Layer Security (TLS) 1.2 protocol to encrypt data in transit.

### Data deletion
{: #data-deletion}

When you delete a key, the service marks the key as deleted, and the key transitions to the _Destroyed_ state. Keys in this state are no longer recoverable, and the cloud services that use the key can no longer decrypt data that is associated with the key. Your data remains in those services in its encrypted form. Metadata that is associated with a key, such as the key's transition history and name, is kept in the {{site.data.keyword.hscrypto}} database.

Deleting a key in {{site.data.keyword.hscrypto}} is a destructive operation. Keep in mind that after you delete a key, the action cannot be reversed, and any data that is associated with the key is immediately lost at the moment the key is deleted. Before you delete a key, review the data that is associated with the key and ensure that you no longer require access to it. Do not delete a key that is actively protecting data in your production environments.

To help you determine what data is protected by a key, you can view how your {{site.data.keyword.hscrypto}} service instance maps to your existing cloud services by running `ibmcloud iam authorization-policies`. To learn more about viewing service authorizations from the console, see [Granting access between services](/docs/iam?topic=iam-serviceauth).
{: note}

## Compliance readiness
{: #compliance-ready}

{{site.data.keyword.hscrypto}} meets controls for global, industry, and regional compliance standards, including FIPS 140-2 Level 4, GDPR, <!--HIPAA, -->ISO 27001, 27017, 27018, and others.

For a complete listing of {{site.data.keyword.cloud_notm}} compliance certifications, see [Compliance on the {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/compliance){: external}.
{: tip}

<!-- ### EU support
{: #eu-support}

{{site.data.keyword.hscrypto}} has extra controls in place to protect your {{site.data.keyword.hscrypto}} resources in the European Union (EU).

If you use {{site.data.keyword.hscrypto}} resources in the Frankfurt, Germany region to process personal data for European citizens, you can enable the EU Supported setting for your {{site.data.keyword.cloud_notm}} account. To find out more, see [Enabling the EU Supported setting](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported) and [Requesting support for resources in the European Union](/docs/get-support?topic=get-support-getting-customer-support#eusupported). -->

### FIPS 140-2 Level 4
{: #fips}

The Federal Information Processing Standard (FIPS) Publication 140-2 is a U.S. government computer security standard that is used to approve cryptographic modules.

FIPS 140-2 defines four levels of security, including FIPS 140-2 Level 1, 2, 3, and 4. FIPS 140-2 Level 4 is the highest level of security. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access. Penetration of the cryptographic module enclosure from any direction has a very high probability of being detected of all plaintext critical security parameters (CSPs).

{{site.data.keyword.hscrypto}} is the only cloud HSM in the public cloud market built on an HSM designed to meet FIPS 140-2 Level 4 certification requirements. The certification was achieved on 3/20/2019 and is listed on the [Cryptographic Module Validation Program (CVMP) Validated Modules List](https://csrc.nist.gov/Projects/cryptographic-module-validation-program/Validated-Modules){: external}.

### General Data Protection Regulation (GDPR)
{: #gdpr}

The GDPR seeks to create a harmonized data protection law framework across the EU and aims to give citizens back the control of their personal data, while imposing strict rules on those hosting and processing this data, anywhere in the world.

{{site.data.keyword.IBM_notm}} is committed to providing you with innovative data privacy, security, and governance solutions to assist them in their journey to GDPR readiness.

To ensure GDPR compliance for your {{site.data.keyword.hscrypto}} resources, [enable the EU supported setting](/docs/account?topic=account-eu-hipaa-supported#bill_eusupported) for your {{site.data.keyword.cloud_notm}} account. You can learn more about how {{site.data.keyword.hscrypto}} processes and protects personal data by reviewing the following addendums.

- [{{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Data Sheet Addendum (DSA)](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=46E9C81025D811E895B382FBC780E8BA){: external}
- [{{site.data.keyword.IBM_notm}} Data Processing Addendum (DPA)](https://www.ibm.com/support/customer/csol/terms/?cat=dpa){: external}

<!-- ### HIPAA support
{: #hipaa-ready}

{{site.data.keyword.keymanagementserviceshort}} meets controls for the US Health Insurance Portability and Accountability Act (HIPAA) to ensure safeguarding of protected health information (PHI).

If you or your company is a covered entity as defined by HIPAA, you can enable the HIPPA Supported setting for your {{site.data.keyword.cloud_notm}} account. To find out more, see [Enabling the HIPAA Supported setting](/docs/account?topic=account-eu-hipaa-supported#enabling-hipaa). -->

### ISO 27001, 27017, 27018
{: #iso}

{{site.data.keyword.hscrypto}} is ISO 27001, 27017, 27018 certified. You can view compliance certifications by visiting [Compliance on the {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/compliance){: external}.

<!-- ### SOC 2 Type 1
{: #soc2-type1}

{{site.data.keyword.hscrypto}} is SOC 2 Type 1 certified. For information about requesting an {{site.data.keyword.cloud_notm}} SOC 2 report, see [Compliance on the {{site.data.keyword.cloud_notm}}](https://www.ibm.com/cloud/compliance){: external}.-->
