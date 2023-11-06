---

copyright:
  years: 2023
lastupdated: "2023-11-06"

keywords: bring your own hsm, byohsm, hybrid hpcs, hybrid hsm, hybrid KMS, hybrid hpcs overview, hybrid KMS

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}

# Introducing Bring Your Own HSM
{: #introduce-bring-your-own-hsm}

By enabling the Bring Your Own Hardware Security Module (BYOHSM) function in {{site.data.keyword.hscrypto}}, you can use your own on-premises HSMs for generating encryption keys while still leveraging the key management service in the cloud.
{: shortdesc}

The Bring Your Own HSM (BYOHSM) function is available only in the Standard Plan service instances in the VPC-based regions. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).
{:note}

## What is Bring Your Own HSM?
{: #what-is-byohsm}

Instead of using IBM-provided cloud HSMs for key generation and management, you can use your own on-premises HSMs for your {{site.data.keyword.hscrypto}} instance. Bring Your Own HSM extends your local key management capability to the cloud and creates a scalable, unified, and secure hybrid cloud eco-system for your regulated workloads. The following architecture diagram shows the difference between {{site.data.keyword.hscrypto}} instances with and without this function enabled.

![BYOHSM architecture](/images/byohsm-archi.svg "BYOHSM architecture"){: caption="Figure 1. Architecture comparison between {{site.data.keyword.hscrypto}} with and without BYOHSM" caption-side="bottom"}

With the Bring Your Own HSM function, you can benefit from the following aspects:

- **Data sovereignty**: You have physical control over your HSMs and encryption keys, which helps you comply with the data sovereignty regulations.
- **Simplified HSM management**: If you have already provisioned HSMs in your enterprise, you can continue using it for {{site.data.keyword.hscrypto}}. In this way, you can have a unified control of HSM management and a consistent key management infrastructure.

However, compared to cloud HSMs, on-premises HSMs also have the following disadvantages:

- **High cost**: If you don't have an on-premises HSM, you need to purchase at least one for {{site.data.keyword.hscrypto}} to use.
- **Full responsibility for hardware setup and maintenance**: You need to complete the initial setup of HSMs based on the provider's guideline, configure and deploy your HSMs to work with {{site.data.keyword.hscrypto}}, and keep your HSMs in a secure place and in a good status.
- **No access to the PKCS #11 and GREP11 APIs of the cloud HSM**: With BYOHSM, your {{site.data.keyword.hscrypto}} instance no longer uses the cloud HSM for key generation and management. Therefore, you are not able to use the PKCS #11 and GREP11 APIs.

## How to enable Bring Your Own HSM?
{: #how-to-enable-byohsm}

To enable the Bring Your Own HSM function, you need to complete the following steps:

1. Purchase and set up your on-premises HSMs.

    You are responsible for the initial setup of HSMs that you want to use for your service instance within your own infrastructure. Make sure to follow the relevant product guidelines from your HSM provider. Currently, {{site.data.keyword.hscrypto}} supports Thales HSM A7xx models only. For more information, see [Limitations and scope](#byohsm-limitation-scope).

2. Configure and deploy HSMs to connect to your instance.

    You need to configure networks, create partitions and specific keys, and prepare information needed for connection. To achieve high availability, it is suggested to deploy at least two HSMs. For more information, see [Deploying an HSM to use with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm).

3. Provision a {{site.data.keyword.hscrypto}} instance with BYOHSM enabled.

    After you collect all the information needed, you can contact IBM and create a {{site.data.keyword.hscrypto}} instance with the Bring Your Own HSM function enabled. For more information, see [Provisioning instances with Bring Your Own HSM](/docs/hs-crypto?topic=hs-crypto-provision-instance-with-byohsm).

    You cannot enable or disable the BYOHSM function after you provision an instance.
    {: note}

## Limitations and scope
{: #byohsm-limitation-scope}

When you decide whether to enable this function, you might need to consider the following limitations:

- Supported HSM types

    Currently, {{site.data.keyword.hscrypto}} supports the following HSM types with the specific firmware and software versions:

    - [Thales SafeNet Luna Network A730 and A750 model HSMs](https://thalesdocs.com/gphsm/luna/7/docs/network/Content/Home_Luna.htm){: external}
    - Application/OS version: 7.4.2 or later
    - Firmware version: 7.3.3 or later

    If you use older versions, make sure to upgrade your firmware and software versions to the latest version. For more information, see [HSM Updates and Upgrades](https://thalesdocs.com/gphsm/luna/7/docs/network/Content/admin_hsm/updates/upgrade.htm){: external}. 
    
    For security best practice, it is suggested to run your HSMs in FIPS mode, which allows your HSM to create FIPS-compliant keys. To check out the current mode, use the LunaSH command [`hsm showpolicies`](https://thalesdocs.com/gphsm/luna/7/docs/network/Content/lunash/commands/hsm/hsm_showpolicies.htm){: external}. The value of `Enable non-FIPS algorithms` should be `Disallowed`.
    {: tip}

- Limited region availability

    The Bring Your Own HSM (BYOHSM) function is available only in the VPC-based regions. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions). However, you can set up your own HSMs in another location as long as the network connectivity works between your {{site.data.keyword.hscrypto}} instance and your HSMs. It is suggested that you ensure a close physical proximity between HSMs and your instance, and connect them by using a private network.

## Responsibilities
{: #byohsm-responsibility}

With the Bring Your Own HSM function enabled, your {{site.data.keyword.hscrypto}} instance is extended to your own infrastructure. IBM no longer fully manages your service instance and you need to understand your responsibilities.

- User responsibilities

    - Make sure that your HSMs are properly configured to work with {{site.data.keyword.hscrypto}}. You are responsible to purchase and set up the HSMs within your own infrastructure. For more information about the type of HSMs that are supported, see [Limitations and scope](#byohsm-limitation-scope). Make sure to follow the relevant product documentation from your HSM provider about its setup, maintenance, and troubleshooting. IBM is only responsible for errors that result from issues with the {{site.data.keyword.hscrypto}} instance, not from any issues with your HSM.
    - Ensure network connectivity between HSMs and your {{site.data.keyword.hscrypto}} instance. For more information about how to establish the network, see [Network connectivity best practice](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-network-connection).
    - Contact IBM before you provision an instance with the Bring Your Own HSM function enabled. You must provide [the information needed](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-prepare-info) to connect to your HSMs, so that IBM can configure and deploy the backend environment for your instance first.

- IBM responsibilities

    - Ensure the normal operations and maintenance of {{site.data.keyword.hscrypto}} instances.
    - Ensure the security of key operations and key-related processes.
    - Support for issues that are related to the {{site.data.keyword.hscrypto}} instance, not for issues with your HSM.
