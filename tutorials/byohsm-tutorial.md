---

copyright:
  years: 2024
lastupdated: "2024-03-07"

keywords: bring your own hsm, byohsm, hybrid hpcs, deploy hsm, hybrid KMS, byohsm get started

subcollection: hs-crypto

content-type: tutorial
services: hs-crypto
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}

# Managing your keys with BYOHSM in {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} 
{: #tutorial-byohsm}
{: toc-content-type="tutorial"}
{: toc-services="hs-crypto"}
{: toc-completion-time="2h"}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is a dedicated key management service based on {{site.data.keyword.cloud_notm}}. With the Bring Your Own HSM (BYOHSM) function in {{site.data.keyword.hscrypto}}, you can use your own on-premises HSMs to generate encryption keys instead of using IBM-provided cloud HSMs, while still leveraging the single-tenant cloud key management service provided by {{site.data.keyword.hscrypto}}.
{: shortdesc}

The Bring Your Own HSM (BYOHSM) function is available only in the Standard Plan service instances in the VPC-based regions. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).
{: note}

BYOHSM extends your local key management capability to the cloud and creates a scalable, unified, and secure hybrid cloud ecosystem for your regulated workloads. By connecting your own HSMs to {{site.data.keyword.hscrypto}}, you have complete physical control over your keys to meet the data sovereignty regulations.

## Objectives
{: #tutorial-byohsm-objectives}

This tutorial shows how you basic steps to manage keys with BYOHSM in {{site.data.keyword.hscrypto}}.


## Before you begin
{: #tutorial-byohsm-prerequisites}

To use the BYOHSM function of {{site.data.keyword.hscrypto}}, make sure that you have a Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account. For details about the {{site.data.keyword.cloud_notm}} account types, see [Account types](/docs/account?topic=account-accounts){: external}.

- To check your account type, log in to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/login){: external} and click **Management** &gt; **Account** &gt; **Account settings**.
- If you have a Lite account, make sure to [upgrade your account](/docs/account?topic=account-upgrading-account){: external} to a Pay-As-You-Go or Subscription account.

## Task flow
{: #tutorial-byohsm-steps}

Get started with BYOHSM by completing the following steps:

- [Before you begin](#tutorial-byohsm-prerequisites)
- [Step 1: Purchase and set up your on-premises HSMs](#tutorial-byohsm-step1)
- [Step 2: Configure and deploy your HSMs to work with {{site.data.keyword.hscrypto}}](#tutorial-byohsm-step2)
- [Step 3: Contact IBM to get the required information](#tutorial-byohsm-step3)
- [Step 4: Provision a {{site.data.keyword.hscrypto}} instance with BYOHSM](#tutorial-byohsm-step4)
- [Step 5: Use your {{site.data.keyword.hscrypto}} instance with BYOHSM](#tutorial-byohsm-step5)

## Purchase and set up your on-premises HSMs
{: #tutorial-byohsm-step1}
{: step}

If you don't have an HSM for your enterprise, purchase one to connect to your {{site.data.keyword.hscrypto}} instance and enable the BYOHSM function. Currently, only Thales SafeNet Luna Network A730 and A750 model HSMs are supported. For more information, see [supported types of HSMs](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm#byohsm-limitation-scope). Make sure that you complete the initial setup based on your providers guidelines.

To achieve high availability, it is suggested to prepare and use at least two HSMs.
{: tip}

## Configure and deploy your HSMs to work with {{site.data.keyword.hscrypto}}
{: #tutorial-byohsm-step2}
{: step}

1. Create an application partition in each HSM to store cryptographic objects and perform operations. For more information, see [Creating partitions](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-partition).
1. Create the following keys that are needed to establish a secure HSM connection. For more information, see [Creating keys](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-key).

    | Key type | Description |
    | --------  | ----------- |
    | Master Key Encryption Key (MKEK) |	(256-bit AES key) A root level encryption key for wrapping and unwrapping instance keys in {{site.data.keyword.hscrypto}}. |
    | Signing key (SKEY) |	(256-bit AES key) Used for signing and verification of instance keys and user keys in {{site.data.keyword.hscrypto}}. |
    | Import Key (IKEY)	| (192-bit DES3 key) Used to encrypt and decrypt the key materials to be imported into {{site.data.keyword.hscrypto}}. |
    | Transit Key Encryption Keys (TKEKs)	| (10 pairs of RSA asymmetric keys) Used to securely import your own keys into {{site.data.keyword.hscrypto}}. |
    {: caption="Table 1. Keys needed for Bring Your Own HSM" caption-side="bottom"}

1. Prepare the network to connect the on-premises HSMs to your {{site.data.keyword.hscrypto}} instance. For more information about how to achieve better network performance, see [Network connectivity best practice](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-network-connection).
1. Collect the following information that you need to provide when you contact IBM in [Step 3](#tutorial-byohsm-step3).

    | Attribute | Description |
    | --------- | ----------- |
    | HSM IP address | The IP address of your HSM. |
    | HSM server certificate | The NTLS communications that are used by the Thales HSM require certificate exchanges between the HSM and {{site.data.keyword.hscrypto}}. You need to create a TLS certificate on your HSM and provide the certificate for {{site.data.keyword.hscrypto}} to verify communications from the HSM. |
    | Partition label | The name of the application partition that you create for {{site.data.keyword.hscrypto}} to use. |
    | Partition crypto officer password | The credential for {{site.data.keyword.hscrypto}} to log in to the corresponding application partition to perform key operations. |
    | Master key label | The label or name of the Master Key Encryption Key (MKEK). The label is used by {{site.data.keyword.hscrypto}} to refer to the master key in PKCS #11 API calls. |
    | Signing key label | The label or name of the Signing key (SKEY). It is used for data authentication such as data signing and verification. |
    | Import key label | The label or name of the Import key (IKEY). {{site.data.keyword.hscrypto}} uses this key to encrypt or decrypt key materials to be imported. |
    | Transit Key Encryption Key label prefix | The label prefix of the Transit Key Encryption Key that is used for securely importing your own keys. |
    {: caption="Table 2. Information needed for Bring Your Own HSM" caption-side="bottom"}

## Contact IBM to get the required information
{: #tutorial-byohsm-step3}
{: step}

Contact IBM by [creating a support case](/docs/get-support?topic=get-support-open-case) to get the required information. Provide the information that you collect in [Step 2](#tutorial-byohsm-step2) including the subnets where your HSMs can be reached. Each subnet corresponds to one Availability Zone (AZ).

IBM will then provide you with the following information:

- Your unique **HSM connector ID**. You need to provide the ID when you provision an instance in [step 4](#tutorial-byohsm-step4).
- The **VPC CRN**. In your Transit Gateway configuration, you need to [request a connection to the VPC CRN](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections&interface=ui).
- The **HSM client certificate**. You need to install this certificate on your HSMs to ensure that the communications from {{site.data.keyword.hscrypto}} can be verified.

## Provision a {{site.data.keyword.hscrypto}} instance with BYOHSM
{: #tutorial-byohsm-step4}
{: step}

Provision a {{site.data.keyword.hscrypto}} instance on the [service catalog page](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services){: external} with the following field values:

- Under **Select a pricing plan**, select **Standard**.
- Under **Select a location**, select a VPC-based region. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).
- Under **HSM connection**, select **Bring Your Own HSM**.
- Under **HSM connector ID**, enter the HSM connector ID that you get from IBM. This field is displayed only after you select **Bring Your Own HSM** for the **HSM connection** field.

For more information, see [Provisioning a {{site.data.keyword.hscrypto}} instance with BYOHSM](/docs/hs-crypto?topic=hs-crypto-provision&interface=ui).

## Use your {{site.data.keyword.hscrypto}} instance with BYOHSM
{: #tutorial-byohsm-step5}
{: step}

After you create an instance with the BYOHSM function enabled, you can use your own HSMs for key generation and management. For more information, see the following links:

- [Creating key management service (KMS) keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys)
- [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware){: external}
- [KMS API reference](/apidocs/hs-crypto){: external}
- [KMS CLI reference](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#kp-cli-plugin){: external}

## What's next
{: #tutorial-byohsm-next}

To learn more about BYOHSM, see [Introducing Bring Your Own HSM](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm).
