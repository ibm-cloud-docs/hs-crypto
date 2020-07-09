---

copyright:
  years: 2020
lastupdated: "2020-05-19"

keywords: crypto unit, add crypto units, remove crypto units, change crypto units number, adjust crypto units number, new crypto units, support center, support ticket, support case

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

# Adding or removing crypto units
{: #add-remove-crypto-units}

After you provision a {{site.data.keyword.hscrypto}} instance, you can request to add or remove crypto units by raising support tickets in the IBM Support Center.
{: shortdesc}

To adjust the number of crypto units, complete the following steps.

## Adding crypto units to an existing service instance
{: #add-crypto-units}

### Step 1: Request to add crypto units
{: #step1-support-ticket-change-number}

To add or remove crypto units, you need to first raise a support ticket.

1. In your {{site.data.keyword.cloud_notm}} dashboard, select **Support** to enter the Support Center. Click **View all** in the **Recent support cases** panel and click **Create new case**. Or, you can directly go to the [Manage cases page](https://cloud.ibm.com/unifiedsupport/cases){: external} and click **Create new case**.
2. On the **Create a case** page displayed, select the offering {{site.data.keyword.hscrypto}}, and then specify the following values:

  <table>
    <tr>
      <th>Field name</th>
      <th>Action</th>
    </tr>
    <tr>
      <td>Subject</td>
      <td>Enter <strong>Add crypto units</strong>.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>Enter your service instance ID, the region that your service instance resides in, and the number of crypto units you want to add. You can have no more than three crypto units for a service instance.</td>
    </tr>
    <tr>
      <td>Selected resources</td>
      <td>Select your {{site.data.keyword.hscrypto}} service instance.</td>
    </tr>
    <caption style="caption-side:bottom;">Table 1. Describes the fields required to add crypto units</caption>
  </table>

3. Check the **Email me updates about this issue** box, and click **Continue to review > Create case**.

  After the operation is completed successfully, you will get an email notification. You can also check the state in the Support Center by clicking **Support**.

4. To view the number of crypto units in the current service instance, run the `ibm tke cryptounits` command in the CLI or selecting the **Crypto units** tab in the Trusted Key Entry application, depending on how you store your master key parts.

To enhance availability and disaster-recovery capability, if you request to add crypto units, the new crypto units are automatically allocated in different availability zones within the same region where your service instance is located.
{: note}

Before you can use the new crypto units, complete the following two steps to initialize and activate them.

### Step 2: Initialize the new crypto units
{: #step2-initialize-new-crypto-units}

Depending on how you store your master key parts, you might initialize the new crypto units with the TKE CLI plug-in or the Management Utilities. Make sure to configure the new crypto units the same as the existing crypto units by referring to the following instructions:

- If you load the master key from your workstation, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)
- If you load the master key from smart cards, see [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

Additional monthly costs apply for each new crypto unit. You can check the detailed charges on the [billing and usage](https://cloud.ibm.com/billing/){: external} page under your account.
{: important}

### Step 3: Request to activate the new crypto units
{: #step3-activate-new-crypto-units}

After you initialize the new crypto units, you need to raise another support ticket to activate them.

1. In your {{site.data.keyword.cloud_notm}} dashboard, select **Support** to enter the Support Center. Click **View all** in the **Recent support cases** panel and click **Create new case**. Or, you can directly go to the [Manage cases page](https://cloud.ibm.com/unifiedsupport/cases){: external} and click **Create new case**.
2. On the **Create a case** page displayed, select the offering {{site.data.keyword.hscrypto}}, and then specify the following values:

  <table>
    <tr>
      <th>Field name</th>
      <th>Action</th>
    </tr>
    <tr>
      <td>Subject</td>
      <td>Enter <strong>Activate new crypto units</strong>.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>Enter your service instance ID, the region that your service instance resides in, the number of new crypto units, and the case number of the support ticket previously raised in [step 1](#step1-support-ticket-change-number).</td>
    </tr>
    <tr>
      <td>Selected resources</td>
      <td>Select your {{site.data.keyword.hscrypto}} service instance.</td>
    </tr>
    <caption style="caption-side:bottom;">Table 2. Describes the fields required to activate new crypto units</caption>
  </table>

3. Check the **Email me updates about this issue** box, and click **Continue to review > Create case**.

  After the activation is completed successfully, you will get an email notification. You can also check the state in the Support Center by clicking **Support**.

## Removing crypto units from an existing service instance
{: #remove-crypto-units}

To remove crypto units from an exsiting service instance, you need to only [raise a support ticket](#step1-support-ticket-change-number).

On the **Create a case** page, enter **Remove crypto units** as the subject, and include the number of crypto units that you want to remove in the case description.

## What's next
{: #add-remove-crypto-units-next}

Now you can use the new set of crypto units to manage encryption keys and perform cryptographic operations.

- Use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
- To learn more about using Enterprise PKCS #11 APIs to perform cryptographic operations for your applications, check out [Encrypt your data with Cloud HSM](/docs/hs-crypto?topic=hs-crypto-get-started#encrypt-data-hsm) and the [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
