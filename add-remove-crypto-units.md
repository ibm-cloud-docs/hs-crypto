---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-20"

keywords: crypto unit, add crypto units, remove crypto units, change crypto units number, adjust crypto units number, new crypto units, support center, support ticket, support case

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Adding or removing crypto units
{: #add-remove-crypto-units}

After you provision a {{site.data.keyword.hscrypto}} instance, you can request to add or remove crypto units by raising support tickets in the {{site.data.keyword.cloud}} Support Center.
{: shortdesc}

To adjust the number of crypto units, complete the following steps.

## Adding crypto units to an existing service instance
{: #add-crypto-units}

### Step 1: Request to add crypto units
{: #step1-support-ticket-change-number}

To add or remove crypto units, you need to first raise a support ticket.

1. In your {{site.data.keyword.cloud_notm}} dashboard, click the **Help** icon ![Help icon](../icons/help.svg "Help") > **Support center** from the UI menu bar to enter the Support Center. Click **View all** in the **Recent support cases** panel and click **Create new case**. Or, you can directly go to the [Manage cases page](https://cloud.ibm.com/unifiedsupport/cases){: external} and click **Create new case**.
2. On the **Create a case** page displayed, select the offering {{site.data.keyword.hscrypto}}, and then specify the following values:

    | Field name | Action |
    | --- | --- |
    | Subject | Enter **Add crypto units**. |
    | Description | Enter your [service instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID), the region that your service instance resides in, and the number of crypto units you want to add. You can have no more than three crypto units for a service instance. |
    | Selected resources | Select your {{site.data.keyword.hscrypto}} service instance. |
    {: caption="Table 1. Describes the fields that are required to add crypto units" caption-side="bottom"}

3. Check the **Email me updates about this issue** box, and click **Continue to review > Create case**.

    After the operation is completed successfully, you will get an email notification. You can also check the state in the Support Center by clicking the **Help** icon ![Help icon](../icons/help.svg "Help") > **Support center** from the UI menu bar.

4. To view the number of crypto units in the current service instance, run the `ibm tke cryptounits` command in the CLI. Or you can select the **Crypto units** tab in the Trusted Key Entry application, depending on how you store your master key parts.

For availability and disaster-recovery capability, if you request to add crypto units, the new crypto units are automatically allocated in different availability zones within the same region.
{: note}

Before you can use the new crypto units, complete the following two steps to initialize and activate them.

### Step 2: Initialize the new crypto units
{: #step2-initialize-new-crypto-units}

Depending on how you store your master key parts, you might initialize the new crypto units with the TKE CLI plug-in, or smart cards together with the Management Utilities. Make sure to configure the new crypto units the same as the existing crypto units by referring to the following instructions:

- If you load the master key from your workstation, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).
- If you load the master key from smart cards, see [Initializing service instances with smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

Extra monthly costs apply for each new crypto unit. You can check the detailed charges on the [billing and usage](https://cloud.ibm.com/billing/){: external} page under your account.
{: important}

### Step 3: Request to activate the new crypto units
{: #step3-activate-new-crypto-units}

After you initialize the new crypto units, you need to raise another support ticket to activate them.

1. In your {{site.data.keyword.cloud_notm}} dashboard, click the **Help** icon ![Help icon](../icons/help.svg "Help") > **Support center** from the UI menu bar to enter the Support Center. Click **View all** in the **Recent support cases** panel and click **Create new case**. Or, you can directly go to the [Manage cases page](https://cloud.ibm.com/unifiedsupport/cases){: external} and click **Create new case**.
2. On the **Create a case** page displayed, select the offering {{site.data.keyword.hscrypto}}, and then specify the following values:

    | Field name | Action |
    | --- | --- |
    | Subject | Enter **Activate new crypto units**. |
    | Description | Enter your [service instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID), the region that your service instance resides in, the number of new crypto units, and the case number of the support ticket that is previously raised in [step 1](#step1-support-ticket-change-number). |
    | Selected resources | Select your {{site.data.keyword.hscrypto}} service instance. |
    {: caption="Table 2. Describes the fields that are required to activate new crypto units" caption-side="bottom"}

3. Check the **Email me updates about this issue** box, and click **Continue to review > Create case**.

    After the activation is completed successfully, you will get an email notification. You can also check the state in the Support Center by clicking the **Help** icon ![Help icon](../icons/help.svg "Help") > **Support center** from the UI menu bar.

## Removing crypto units from an existing service instance
{: #remove-crypto-units}

To remove crypto units from an existing service instance, you need to [raise a support ticket](#step1-support-ticket-change-number).

On the **Create a case** page, enter **Remove crypto units** as the subject, and include the number of crypto units that you want to remove in the case description.

You need to keep at least two crypto units in a service instance for high availability.
{: note}

## What's next
{: #add-remove-crypto-units-next}

Now you can use the new set of crypto units to manage encryption keys and perform cryptographic operations.

- Use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- To learn more about performing cryptographic operations with the cloud HSM, see [Introducing cloud HSM](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm).
