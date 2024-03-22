---

copyright:
  years: 2020, 2024
lastupdated: "2024-03-22"

keywords: frequently asked questions, cryptographic algorithm, regions, pricing, security compliance, key ceremony, critical security parameters, cryptographic module, security Level, fips, maintenance

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# FAQs: Support and maintenance
{: #faq-support-maintenance}

Read to get answers for support and maintenance related questions about {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## How is routine maintenance performed on {{site.data.keyword.hscrypto}}?
{: #faq-routine-maintenance}
{: faq}

If one available zone that contains your provisioned service instance goes down, {{site.data.keyword.hscrypto}} has automatic in-region data failover in place if you have 2 or 3 crypto units provisioned. IBM also performs cross-region backup for your key resources. Your data is automatically backed up in another supported region daily. If a regional disaster that affects all available zones occurs, you need to open a support ticket so that IBM can restore your data in another supported [{{site.data.keyword.cloud_notm}} regions](/docs/hs-crypto?topic=hs-crypto-regions) from the backup. And then, you need to manually load your master key to your new service instance. For more information, see [Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data).

## How do I get support for {{site.data.keyword.hscrypto}}?
{: #faq-hpcs-support}
{: faq}

If you have technical questions about {{site.data.keyword.hscrypto}}, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/hyper-protect-crypto){: external} and tag your question with `ibm-cloud` and `hyper-protect-crypto`.

For more information about opening an IBM support ticket, or about support levels and ticket severities, see [Using the Support Center](/docs/get-support?topic=get-support-using-avatar).

## After the service initialization is done, is there any best practices for managing smart cards or key part files?
{: #faq-manage-smartcards}
{: faq}

It is your responsibility to secure assets used to initialize the {{site.data.keyword.hscrypto}} instance:

* Store smart cards, the associated PINs, and the smart card readers in secure vaults to prevent unauthorized access.
* Secure key part files in the directory associated with CLOUDTKEFILES in an approved file storage vault.

Make sure you follow these best practice to maintain your secure assets:

* Store the PINS in an approved password vault in the customer environment.
* Prepare a transition plan for administrators to hand over all crypto assets as they move over to different roles.
* Update the Disaster Recovery plans to verify crypto assets such as smart cards, PINs, smart card readers.

You can find more detailed instructions by following these links:

* [Key ceremony through cloud TKE CLI and key part files](https://cloud.ibm.com/media/docs/downloads/hs-crypto/HPCS-Key-Ceremony-using-Key-Part-files.pdf){: external}
* [Key ceremony through cloud TKE and smart cards](https://cloud.ibm.com/media/docs/downloads/hs-crypto/IBM_Cloud_HyperProtectCryptoSevices_TKE_Procedures.pdf){: external}
