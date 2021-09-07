---

copyright:
  years: 2020, 2021
lastupdated: "2021-09-07"

keywords: frequently asked questions, cryptographic algorithm, regions, pricing, security compliance, key ceremony, critical security parameters, cryptographic module, security Level, fips, provisioning, operations

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

# FAQs: Provisioning and operations
{: #faq-provisioning-operations}

Read to get answers for questions about provisioning an {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance and related operations.
{: shortdesc}

## Are there any prerequisites for using {{site.data.keyword.hscrypto}}?
{: #faq-hpcs-prerequisites}
{: faq}

To use {{site.data.keyword.hscrypto}}, you need to have a Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account.

If you don't have an {{site.data.keyword.cloud_notm}} account, create an account first by going to [{{site.data.keyword.Bluemix_notm}} registration](https://cloud.ibm.com/registration){: external}. To check your account type, go to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/login){: external} and click **Management** > **Account** > **Account settings**. You can also [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) if you have one. For more information about {{site.data.keyword.cloud_notm}} accounts, see [FAQs for accounts](/docs/account?topic=account-accountfaqs).

The service can be provisioned quickly by following instructions in [Provisioning service instances](/docs/hs-crypto?topic=hs-crypto-provision). However, in order to perform key management and cryptographic operations, you need to [initialize service instances](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode) first by using {{site.data.keyword.cloud_notm}} TKE CLI plug-in or the Management Utilities.

## How to initialize {{site.data.keyword.hscrypto}} service instances?
{: #faq-how-to-initialize}
{: faq}
{: support}

To initialize the service instance, you need to create administrator signature keys, exit the imprint mode, and load the master key to the instance. To meet various security requirements of your enterprises, IBM offers you the following options to load the master key: 

- [Using the IBM {{site.data.keyword.hscrypto}} Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) for the highest level of security. This solution uses smart cards to store signature keys and master key parts. Signature keys and master key parts never appear in the clear outside the smart card.

- Using the {{site.data.keyword.cloud_notm}} TKE CLI plug-in for a solution that does not require the procurement of smart card readers and smart cards. This solution supports two approaches to initializing service instances: [by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit) and [by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm). When you use recovery crypto units, the master key is automatically generated within crypto units and you don't need to create multiple master key parts. When you use key part files, file contents are decrypted and appear temporarily in the clear in workstation memory.

For more information, see [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode).

## Are there any recommendations on how to set up smart cards?
{: #faq-smart-card-setup}
{: faq}
{: support}

It is suggested that each master key part is created on a separate EP11 smart card and is assigned to a different person. Backup copies of all smart cards need to be created and stored in a safe place. It is suggested that you order 8 or 10 smart cards and initialize them this way:

- Create a certificate authority smart card and a backup certificate authority smart card.
- Create two EP11 smart cards to hold an administrator signature key. Generate the administrator signature key on one EP11 smart card and copy it to the other.
- Create four or six EP11 smart cards to hold master key parts. Generate an EP11 master key part on 2 or 3 of the smart cards, depending on whether you want to use 2 or 3 key parts when you load your master key. Copy each key part value to a backup EP11 smart card.

A backup certificate authority smart card can be created by using the Smart Card Utility Program. Select **CA Smart Card** > **Backup CA smart card** from the menu, and follow the prompts.

The contents of an EP11 smart card can be copied to another EP11 smart card that was created in the same smart card zone by using the Trusted Key Entry application. On the **Smart card** tab, click **Copy smart card**, and follow the prompts.

For greater security, you can generate administrator signature keys on more EP11 smart cards and set the signature thresholds in your crypto units to a value greater than one. You can install up to eight administrators in your crypto units and specify that up to eight signatures are required for some administrative commands.

To find out details on how to procure and set up smart cards and other Management Utilities components, see [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities).

## How can I procure smart cards and smart card readers?
{: #faq-procure-smart-card}
{: faq}

If you are in the United States, you can order smart cards and smart card readers online. For more information, see [Order smart cards and smart card readers](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#order-smart-card-and-reader).

For procurement from other countries, contact IBM Part Sales through the following email addresses. For countries that are not listed, contact `ppricing@de.ibm.com`. In the email, provide the Field Replaceable Unit (FRU) number, 00RY790, for the smart card.

|Country| Email address |
|--------------|-----------------------|
|Belgium  | parts@be.ibm.com|
|Denmark  | reservedele@dk.ibm.com|
|Germany | partsale@de.ibm.com|
|France | vtepce@fr.ibm.com|
|Ireland | emeapart@ie.ibm.com|
|Israel | psale@il.ibm.com|
|Poland | parts@pl.ibm.com|
|Portugal | ptsales@pt.ibm.com|
|South Africa    |autoship@za.ibm.com |
|Spain    | ventadepiezas@es.ibm.com|
|Switzerland | pasa@ch.ibm.com|
|UK | parts_sales@uk.ibm.com|
{: caption="Table 2. IBM Part Sales contacts" caption-side="bottom"}

## How many crypto units shall I set up in my service instance?
{: #faq-crypto-units-number}
{: faq}

You need to set up at least two crypto units for high availability. {{site.data.keyword.hscrypto}} sets the upper limit of crypto unit to 3.

## Can I use {{site.data.keyword.hscrypto}} along with other {{site.data.keyword.cloud_notm}} services?
{: #faq-hpcs-with-cloud-services}
{: faq}

Yes. {{site.data.keyword.hscrypto}} can be integrated with many {{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.cos_full_notm}}, {{site.data.keyword.vmwaresolutions_short}}, {{site.data.keyword.containerlong_notm}}, and {{site.data.keyword.openshiftlong_notm}}. For a complete list of services and instructions on integrations, see [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services). 

## How does my application connect to a {{site.data.keyword.hscrypto}} service instance?
{: #faq-application-connection}
{: faq}

{{site.data.keyword.hscrypto}} provides the standard APIs for users to access. Your applications can connect to a {{site.data.keyword.hscrypto}} service instance by using the APIs directly over the public internet. If a more secured and isolated connection is needed, you can also use [private endpoints](/docs/hs-crypto?topic=hs-crypto-secure-connection). You can connect your service instance through {{site.data.keyword.cloud_notm}} service endpoints over the {{site.data.keyword.cloud_notm}} private network.



## Can I generate master key on-premises and store the master key parts in the smart cards?
{: #faq-generate-master-key-on-premises}

Generating master key on-premises is not supported.

## Can I import root keys from an on-premises HSM?
{: #faq-import-key-on-premises}
{: faq}

Importing root keys from an on-premises HSM is not supported.

## Can I use {{site.data.keyword.hscrypto}} only for cryptographic operations, but use other {{site.data.keyword.cloud_notm}} services such as {{site.data.keyword.keymanagementserviceshort}} for key management?
{: #faq-hpcs-with-key-protect}
{: faq}

Yes. {{site.data.keyword.hscrypto}} can be used with {{site.data.keyword.keymanagementserviceshort}} for key management. In this way, {{site.data.keyword.hscrypto}} is responsible for only cryptographic operations, while {{site.data.keyword.keymanagementserviceshort}} provides key management service secured by multi-tenant FIPS 140-2 Level 3 certified cloud-based HSM.



## Can I use {{site.data.keyword.hscrypto}} along with other cloud provider services such as AWS and Azure?
{: #faq-hpcs-other-cloud-vendor}
{: faq}

Yes. Any application can connect to {{site.data.keyword.hscrypto}} and use our APIs from anywhere on the internet.
