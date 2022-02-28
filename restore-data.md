---

copyright:
  years: 2019, 2022
lastupdated: "2022-02-28"

keywords: disaster recovery, restore, recovery, cross region restore, support ticket, support center

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}


# Restoring your data from another region
{: #restore-data}

If a regional disaster that affects all available zones occurs, you're notified through the [IBM Cloud status](https://cloud.ibm.com/status?selected=status){: external} web page and an email. In this case, depending on your [pricing plan](/docs/hs-crypto?topic=hs-crypto-provision)and whether you enable failover crypto units, you can restore your data by using failover crypto units or opening an IBM support ticket.
{: shortdesc}

## Restoring your data by using failover crypto units
{: #restore-data-failover-crypto-units}

If you are using the Standard plan, and create your instance in Dallas (`us-south`) or Washington DC (`us-east`) and you enable failover crypto units, your data is restored automatically to reduce the downtime and data loss. In this case, you switch to use the failover crypto units in another region to manage your keys and perform cryptographic operations. The failover crypto units contains a backup of all the encryption keys and other resources in the operational crypto units.

At the same time, IBM repairs your service instance in the original region. If new operational crypto units are required to complete the repair, you will be notified by IBM and you need to load the master key to the new operational crypto units by [using recovery crypto units or master key parts](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode). After your original service instance is recovered, IBM automatically redirects traffic back to the original region.

To use failover crypto units to restore data in a regional disaster, make sure that you initialize and configure all the failover crypto units the same as the operational crypto units before the disaster happens. For more information about initialization approaches, see [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode).
{: important}

## Restoring your data by opening an IBM support ticket
{: #restore-data-open-support-ticket}

If you don't enable failover crypto units or you are using {{site.data.keyword.hscrypto}} with {{site.data.keyword.uko_full_notm}}, you need to open an IBM support ticket to restore your data. IBM can then provision a new service instance for you in another region by using the same instance ID, and restore all the key resources from the backup. And then, you need to load your [master key](#x2908413){: term} to the new service instance in the new region.

In the process, you're the only person who owns the master key. IBM administrators or any third-party users cannot access your data or keys in the backup or the restored service instance.
{: note}

To restore a backup to an existing service instance, follow these steps:

1. In the {{site.data.keyword.cloud_notm}} console, select **Support** to enter the Support Center. Click **View all** in the **Recent support cases** panel and click **Create new case**. Or, you can directly go to the [Manage cases page](https://cloud.ibm.com/unifiedsupport/cases){: external} and click **Create new case**.
2. On the **Create a case** page displayed, select the offering {{site.data.keyword.hscrypto}}, and then specify the following values:

    <table>
    <tr>
      <th>Field name</th>
      <th>Action</th>
    </tr>
    <tr>
      <td>Subject</td>
      <td>Enter <strong>Disaster recovery</strong>.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>Enter your <a href="/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID">service instance ID</a> and the region that your service instance resides in.</td>
    </tr>
    <tr>
      <td>Selected resources (optional)</td>
      <td>Select your {{site.data.keyword.hscrypto}} service instance.</td>
    </tr>
    <caption>Table 1. Describes the fields that are displayed on the <strong>Create a case</strong> page</caption>
    </table>

3. Check the **Email me updates about this issue** box, and click **Continue to review > Create case**.

    When the restore completes successfully, you will get an email notification, which includes the new region information that your service instance resides in. Alternatively, you can check the state by clicking **Support**. For more information about {{site.data.keyword.IBM_notm}} Support, see [Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

4. After you open the ticket, IBM provisions new crypto units for you in another region by using the same instance ID, and restores all the key resources from the backup. And then, you need to load your master key to the new service instance in the new region. Depending on how you store your master key parts, you can follow the instructions in [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

    Make sure to load the same master key to the service instance in the new region so that your key resources can still be accessed.
    {: important}

## What's next
{: #restore-data-next}

- Go to the **Manage** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management API reference doc](/apidocs/hs-crypto){: external}.
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
- Use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
