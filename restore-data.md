---

copyright:
  years: 2019
lastupdated: "2019-12-09"

keywords: disaster recovery, restore, support

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
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
{: help}
{: support}

If a regional disaster that affects all available zones occurs, you're notified through the [IBM Cloud status](https://cloud.ibm.com/status?selected=status){: external} web page and an email. In this case, you need to open an IBM Support ticket. IBM can then provision a new service instance for you in another region by using the same instance ID, and restore all the key resources from the backup. And then, you need to load your [master key](#x2908413){: term} to the new service instance in the new region.
{: shortdesc}

In the process, you're the only person who owns the master key. IBM administrators or any third-party users cannot access your data or keys in the backup or the restored service instance.
{: note}

To restore a backup to an existing service instance, follow these steps:
1. In your {{site.data.keyword.cloud_notm}} dashboard, select **Support > Manage cases > Create new case**. Or, you can go to the [support page](https://cloud.ibm.com/unifiedsupport/cases/manage){: external} and click **Create new case**.
2. On the **New support case** web page displayed, select the type of support you need: **Technical**, and then specify the following values:

  <table>
    <tr>
      <th>Field name</th>
      <th>Action</th>
    </tr>
    <tr>
      <td>Offering</td>
      <td>Select <strong>Security and Identity: Hyper Protect Crypto Services</strong>.</td>
    </tr>
    <tr>
      <td>Search Offering resources</td>
      <td>Select your {{site.data.keyword.hscrypto}} service instance.</td>
    </tr>
    <tr>
      <td>Subject</td>
      <td>Enter <strong>Disaster recovery</strong>.</td>
    </tr>
    <tr>
      <td>Description</td>
      <td>Enter your service instance ID and the region that your service instance resides in.</td>
    </tr>
    <caption style="caption-side:bottom;">Table 1. Describes the fields that are displayed on the <strong>New support case</strong> page</caption>
  </table>

3. Check the **Email me updates** box, and click **Submit**.

  When the restore completes successfully, you will get an email notification, which includes the new region information that your service instance resides in. Alternatively, you can check the state by clicking **Support > Manage Cases**. For more information about {{site.data.keyword.IBM_notm}} Support, see [Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

4. After the restore is done, load your master key to the service instance in the new region. Depending on how you store your master key parts, you can follow the instructions in [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).

  Make sure to load the same master key to the service instance in the new region so that your key resources can still be accessed.
  {: important}

## What's next
{: #restore-data-next}

- Go to the **Manage** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To learn more about using Enterprise PKCS #11 APIs to perform cryptographic operations for your applications, check out [Encrypt your data using Cloud HSM](/docs/hs-crypto?topic=hs-crypto-get-started#encrypt-data-hsm) and the [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
- Use {{site.data.keyword.hscrypto}} as the root key provider for other {{site.data.keyword.cloud_notm}} services. For more information about integrating {{site.data.keyword.hscrypto}}, check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services).
