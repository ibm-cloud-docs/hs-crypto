---

copyright:
  years: 2020, 2022
lastupdated: "2022-07-19"

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

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

## Can I initialize my service instance through the TKE CLI plug-in by using a proxy?
{: #faq-tke-proxy}
{: faq}

Yes, if the proxy is configured for HTTPS port 443. You can add an entry to the local hostname mapping of your workstation with the TKE CLI, for example, in `/etc/hosts`. In this host mapping entry, map the TKE API endpoint `tke.<region>.hs-crypto.cloud.ibm.com` to your proxy. For example, for an instance in Frankfurt the URL is `tke.eu-de.hs-crypto.cloud.ibm.com`.

## Are there any recommendations on how to set up smart cards?
{: #faq-smart-card-setup}
{: faq}
{: support}

It is suggested that each master key part is created on a separate EP11 smart card and is assigned to a different person. Backup copies of all smart cards need to be created and stored in a safe place. It is suggested that you order 10 or 12 smart cards and initialize them this way:

- Create a certificate authority (CA) smart card and a backup certificate authority smart card.
- Create two EP11 smart cards and two backup EP11 smart cards to store two administrator signature keys. Generate administrator signature keys separately on two EP11 smart cards and copy them to other two backup smart cards.
- Create two EP11 smart cards and two backup EP11 smart cards to store two master key parts, or create three EP11 smart cards and three backup EP11 smart cards to store three master key parts. Generate EP11 master key parts separately on two or three smart cards, depending on the number of key parts when you load your master key. Copy each key part value to a backup EP11 smart card.

For calculating the number of smart cards needed, you can refer to the following formulas:

| Assumptions | Formula       |
| ----------- | ------------- |
| - The number of backups per smart card: x \n - The number of administrators (1 to 8): y \n - The number of master key parts (2 or 3): z \n - Store administrator signature keys separately from master key parts | 1 (CA card) + x (CA card backups) + y (administrator signature key EP11 cards)+ y * x (administrator signature key EP11 card backups) + z (master key part EP11 cards)+ z * x (master key part EP11 card backups) = (1+x) * (1+y+z) |
| - The number of backups per smart card: x \n - The number of administrators (1 to 8): y \n - The number of master key parts (2 or 3): z \n - Store administrator signature keys together with master key parts \n - The number of master key parts equals to the number of administrators (y = z)  | 1 (CA card) + x (CA card backups) + z (administrator signature key and master key part EP11 cards)+ z * x (administrator signature key and master key part EP11 card backups) = (1+x) * (1+z) |
{: caption="Table 1. Formulas for calculating smart cards number" caption-side="bottom"}

A backup certificate authority smart card can be created by using the Smart Card Utility Program. Select **CA Smart Card** > **Backup CA smart card** from the menu, and follow the prompts.

The contents of an EP11 smart card can be copied to another EP11 smart card that was created in the same smart card zone by using the Trusted Key Entry application. On the **Smart card** tab, click **Copy smart card**, and follow the prompts.

For greater security, you can generate administrator signature keys on more EP11 smart cards and set the signature thresholds in your crypto units to a value greater than one. You can install up to eight administrators in your crypto units and specify that up to eight signatures are required for some administrative commands.

To find out details on how to procure and set up smart cards and other Management Utilities components, see [Setting up smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities).

## How can I procure smart cards and smart card readers?
{: #faq-procure-smart-card}
{: faq}

To procure smart cards and smart card readers, follow the procedure in [Order smart cards and smart card readers](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#order-smart-card-and-reader).

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



## Can I use {{site.data.keyword.hscrypto}} for applications hosted in other cloud service providers such as AWS, Azure, and GCP?
{: #faq-hpcs-other-cloud-vendor}
{: faq}

Yes. An application hosted in other cloud service providers can call the public APIs for Keep You Own Key (KYOK) or PKCS #11 with an appropriate network connection.
