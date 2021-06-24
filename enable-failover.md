---

copyright:
  years: 2021
lastupdated: "2021-06-24"

keywords: failover crypto unit, add failover crypto units, enable failover, enable cross-region recovery

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:hide-in-docs: .hide-in-docs}
{:hide-dashboard: .hide-dashboard}
{:external: target="_blank" .external}
{:term: .term}

# Enabling or adding failover crypto units
{: #enable-add-failover}

Failover crypto units back up the operational crypto units and keystores in another region. When a regional disaster occurs, you can use failover crypto units to automatically restore your data, thus reducing the downtime and data loss. This topic guides you through how to enable or add failover crypto units after you create a {{site.data.keyword.hscrypto}} instance.
{: shortdesc}

## Enabling or adding failover crypto units with the {{site.data.keyword.cloud_notm}} CLI
{: #enable-add-failover-cli}

If you have a service instance in the `us-south` or `us-east` region, you can enable or add failover crypto units with the {{site.data.keyword.cloud_notm}} Trused Key Entry (TKE) CLI plug-in.

1. Make sure that you install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-install-ibmcloud-cli) and the latest TKE CLI plug-in with the following command:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  If you have installed the TKE CLI plug-in, make sure to update your plug-in to the latest version with the following command:

  ```
  ibmcloud plugin update tke
  ```
  {: pre}

2. Run the following command:

  ```
  ibmcloud tke failover-enable
  ```
  {: pre}

  This command walks you through the procedure to enable or add failover crypto units. Follow the prompts to complete the following steps:

  1. Enter the total number of failover crypto units that you want to assign to your service instance.

    You can specify the total number of failover crypto units that is equal to or less than the number of operational crypto units. However, to meet high availability, at least two failover crypto units need to be assigned. Failover crypto units are also charged. For the detailed pricing information, see [FAQs: Pricing](/docs/hs-crypto?topic=hs-crypto-faq-pricing).

    The following output is an example that is displayed:

    ```
    You currently have 0 failover crypto unit(s) for the selected instance 00000a09-0563-4e00-b259-06a4edfc4cba
    Since you have 2 operational crypto units for this instance, you can have up to 2 failover crypto units
    Enter the total number of failover crypto units you would like (max 2):
    > 2

    You will now have 2 failover crypto units. This will affect your billing. For more information, see https://cloud.ibm.com/docs/hs-crypto?topic=hs-crypto-faq-pricing

    Would you like to continue? [y/n]:
    > y
    ```
    {: sreen}

    If your instance already has a certain number of failover crypto units assigned, you can also use this command and follow the same procedure to add more failover crypto units.
    {: tip}

  2. Type `y` to confirm the action. The failover crypto units are assigned in the target failover region.

    Failover crypto units are now available in `us-south` and `us-east`. The two regions are each other's target failover region. For example, if your instance is located in `us-south`, the failover region for your instance is `us-east`.

    The following output is an example that is displayed:

    ```
    Instance 00000a09-0563-4e00-b259-06a4edfc4cba targetting backup region us-south
    2 failover crypto units have been assigned.
    Getting cryptounit info... this may take a moment

    API endpoint:    https://cloud.ibm.com
    Region:          us-south
    User:            user@ibm.com
    Account:         user-account (8230.....a255)
    Resource group:  Default

    SERVICE INSTANCE: 00000a09-0563-4e00-b259-06a4edfc4cba
    CRYPTO UNIT NUM   SELECTED   TYPE           LOCATION
    1                 true       OPERATIONAL    [us-east].[AZ3-CS3].[02].[03]
    2                 true       OPERATIONAL    [us-east].[AZ2-CS2].[02].[03]
    3                 true       RECOVERY       [us-east].[AZ2-CS4].[03].[06]
    4                 true       RECOVERY       [us-south].[AZ3-CS2].[03].[20]
    5                 false      FAILOVER       [us-south].[AZ2-CS2].[03].[04]
    6                 false      FAILOVER       [us-south].[AZ3-CS3].[01].[07]

    Note: all operational crypto units in a service instance must be configured the same.
    Use 'ibmcloud tke cryptounit-compare' to check how crypto units are configured.
    You should initialize your failover crypto units now to be prepared for a failover event.
    ```
    {: screen}

3. Initialize failover crypto units by using the same master key as the operational crypto units initialization.

  You need to initialize failover crypto units before you can use them for a regional disaster recovery. Select one of the following ways to initialize failover crypto units and make sure to use the same master key that is for the operational crypto units initialization:

  - [Initializing service instances with smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)
  - [Initializing service instances by using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)
  - [Initializing service instances by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)

## What's next
{: #enable-add-failover-next}

If a regional disaster occurs, you can use failover crypto units for automatic data restoration. For more information, see [Cross-region disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr#cross-region-disaster-recovery) and [Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data).
