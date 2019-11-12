---

copyright:
  years: 2018, 2019
lastupdated: "2019-10-24"

Keywords: delete, delete service instance, IBM Cloud console, IBM Cloud CLI

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}

# Deleting service instances
{: #delete-instance}

You can delete your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance with the {{site.data.keyword.cloud_notm}} console or the {{site.data.keyword.cloud_notm}} CLI. To do so, you need to first set all the crypto units of the service instance back to imprint mode by zeroizing the crypto units.
{: shortdesc}

## Step 1: Zeroize crypto units
{: #zeroize-crypto-unit}

If you have initialized your service instance and loaded the master key to the service instance, you need to set the crypto units back to imprint mode first. You can clear all crypto unit administrators and the master key registers with the following command.

```
ibmcloud tke cryptounit-zeroize
```
{: pre}

After you zeroize the crypto unit, the administrator signature keys and the master key are cleared from the crypto unit, which means you are not able to access any data that is protected by the master key, such as the root keys and standard keys.
{: important}

## Step 2: Delete your service instance
{: #delete-instance-step}

After you set the crypto units to imprint mode, you can choose to delete your service instance through the {{site.data.keyword.cloud_notm}} console resources page, the instance details page, or the CLI.

### Deleting instances from the {{site.data.keyword.cloud_notm}} console resources page
{: #delete-gui-resource}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console resources page by completing the following steps:

1. From the {{site.data.keyword.cloud_notm}} console, click **Resource List** on the left navigation menu.
2. Find the {{site.data.keyword.hscrypto}} service instance you want to delete under the **Services** section.
3. Click the overflow icon to open the actions menu.
4. Click **Delete**.

### Deleting instances from the {{site.data.keyword.cloud_notm}} console instance details page
{: #delete-gui-detail}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console instance details page by completing the following steps:

1. From the {{site.data.keyword.cloud_notm}} console, click **Resource List** on the left navigation menu.
2. Find the {{site.data.keyword.hscrypto}} service instance you want to delete under the **Services** section and click the instance name to open the instance details page.
3. Click the overflow icon to open the service instance actions menu.
4. Click **Delete service**.

### Deleting instances from the {{site.data.keyword.cloud_notm}} CLI
{: #delete-cli}

You can delete an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} CLI by running the following command:

```
ibmcloud resource service-instance-delete <instance_name|instance_ID>
```
{: pre}

Replace *instance_name* with your instance name and *instance_ID* with your instance ID. You can use either the instance name or the instance ID to run the command.
