---

copyright:
  years: 2024
lastupdated: "2024-05-20"

keywords: bring your own hsm, byohsm, hybrid hpcs, provision byohsm

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Provisioning a {{site.data.keyword.hscrypto}} instance with BYOHSM
{: #provision-instance-with-byohsm}

After you deploy your on-premises hardware security modules (HSMs), you can now start to provision a {{site.data.keyword.hscrypto}} instance with the Bring Your Own HSM (BYOHSM) function enabled.
{: shortdesc}

The Bring Your Own HSM (BYOHSM) function is available only in the Standard Plan service instances in the VPC-based regions. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).
{: note}

## Before you begin
{: #provision-instance-with-byohsm-prerequisites}

Before you can provision a {{site.data.keyword.hscrypto}} instance with BYOHSM, make sure that you meet the following prerequisites:

1. [Deploy your on-premises HSMs to work with {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm).
1. Contact IBM by [creating a support case](/docs/get-support?topic=get-support-open-case) to get the required information. [Provide the information needed](/docs/hs-crypto?topic=hs-crypto-deploy-hsm-for-byohsm#deploy-byohsm-prepare-info) to establish a secure HSM connection. 
1. IBM will then provide you with the following information that is needed for provisioning an instance:

    - **HSM connector ID**: The unique identifier for your HSM connection. {{site.data.keyword.hscrypto}} uses this ID to refer to the backend infrastructure for BYOHSM on {{site.data.keyword.cloud_notm}}.
    - **VPC CRN**: In your Transit Gateway configuration, you need to [request a connection to the VPC CRN](/docs/transit-gateway?topic=transit-gateway-adding-cross-account-connections&interface=ui).
    - **HSM client certificate**: The client certificate for establishing NTLS communications between HSMs and your instance. You need to install this certificate on your HSMs to ensure that the communications from {{site.data.keyword.hscrypto}} can be verified.

## Provisioning {{site.data.keyword.hscrypto}} with the UI
{: #provision-instance-byohsm-ui}

To provision a {{site.data.keyword.hscrypto}} instance with BYOHSM, complete the following steps:

You cannot enable or disable the BYOHSM function after you provision an instance.
{: note}

1. [Log in to your {{site.data.keyword.cloud_notm}} account](https://cloud.ibm.com/login){: external}.
1. Click **Create resource** to view the list of services that are available on {{site.data.keyword.cloud_notm}}.
1. Under **Category**, select **Security**.
1. From the list of services displayed, click the **{{site.data.keyword.hscrypto}}** tile.
1. On the service page, under **Select a location**, select a VPC-based region. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).
1. Under **Select a pricing plan**, select **Standard**.
1. Under **Configure your resource**, complete the form with the following details:

    - Under **Service name**, enter a name for your service instance.
    - Under **Select a resource group**, select the resource group where you want to organize and manage your service instance. You can select the initial resource group that is named `Default` or other groups that you create. For more information, see [Creating and managing resource groups](/docs/account?topic=account-rgs).
    - (Optional) Under **Tags**, add tags to organize your resources. If your tags are billing related, consider writing tags as `key:value` pairs to help with grouping, such as `costctr:124`. For more information, see [Working with tags](/docs/account?topic=account-tag).
    - Under **Allowed network**, choose the network access to your service instance:

        - **Public and private (default)**: Manage your instance through both public and private network by using the UI, CLI, or API. This is the default option.
        - **Private only**: Access your service instance only through private network by using CLI or API. The UI is not available for the private-only network access.

            A private instance accepts API requests through the private endpoints only. The private endpoints are only accessible when your {{site.data.keyword.cloud_notm}} account, along with all associated resources, is enabled with [virtual routing and forwarding (VRF) and service endpoints](/docs/account?topic=account-vrf-service-endpoint). You cannot access your private-only instance through the CLI or API if your server or machine is outside the {{site.data.keyword.cloud_notm}} network.
            {: important}

        You can still [update the network access policy](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies) after you provision the service instance.

    - Under **HSM connection**, select **Bring Your Own HSM**.
    - Under **HSM connector ID**, enter the HSM connector ID that you get from IBM. This field is displayed only after you select **Bring Your Own HSM** for the **HSM connection** field.

1. Click **Create** to provision an instance of {{site.data.keyword.hscrypto}} with BYOHSM in the account, region, and resource group where you are logged in.

## What's next
{: #provision-instance-byohsm-next}

After you create an instance with the BYOHSM feature enabled, you can use your own HSMs for key generation and management. For more information about using BYOHSM, see the following links:

- [Creating key management service (KMS) keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys)
- [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware){: external}
- [Managing user access and enhancing security](/docs/hs-crypto?topic=hs-crypto-manage-access)
- [KMS API reference](/apidocs/hs-crypto){: external}
- [KMS CLI reference](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#kp-cli-plugin){: external}
