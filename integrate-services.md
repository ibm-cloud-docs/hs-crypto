---

copyright:
  years: 2018, 2020
lastupdated: "2020-09-18"

keywords: integration, encryption at rest, cloud object storage, object storage, kmip, containers, vmware, database, compute

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
{:table: .aria-labeledby="caption"}
{:term: .term}

# Integrating {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.hscrypto}}
{: #integrate-services}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} integrates with data and storage solutions to help you bring and manage your own encryption in the cloud.
{: shortdesc}

After you [create an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision) and [initialize the service instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm), you can integrate {{site.data.keyword.hscrypto}} with the following supported services.

## Integrating with storage services
{: #storage-integration}

Add [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to your storage by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.cos_full_notm}}](https://cloud.ibm.com/catalog/services/cloud-object-storage){: external}|For detailed steps of how to integrate {{site.data.keyword.cos_full_notm}}, check out the following references: <ul><li>Demo video: [Integrating {{site.data.keyword.cos_full_notm}} with {{site.data.keyword.hscrypto}}](https://www.youtube.com/watch?v=e_4RO7r_t8M){: external}</li><li>Instructions: [Server-side encryption with {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}}](/docs/cloud-object-storage?topic=cloud-object-storage-encryption)</li></ul>|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud (Gen 1 compute)](https://cloud.ibm.com/vpc/storage/storageVolumes){: external}|For detailed steps of how to integrate {{site.data.keyword.block_storage_is_short}} (Gen 1 compute), check out [Creating block storage volumes with customer-managed encryption](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-encryption).|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud (Gen 2 compute)](https://cloud.ibm.com/vpc-ext/storage/storageVolumes){: external}  | For detailed steps of how to integrate {{site.data.keyword.block_storage_is_short}} (Gen 2 compute), check out [Creating block storage volumes with customer-managed encryption](/docs/vpc?topic=vpc-block-storage-vpc-encryption).  |
{: caption="Table 1. Supported storage services" caption-side="bottom"}

## Integrating with database services
{: #database-integration}

Associate the encryption keys that you manage in {{site.data.keyword.hscrypto}} with your database service instances and leverage [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to add another layer of protection to your data. With full control over your keys, no one else including {{site.data.keyword.cloud_notm}} administrators can access your data.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.ihsdbaas_postgresql_full}}](https://cloud.ibm.com/catalog/services/hyper-protect-dbaas-for-postgresql){: external}|For detailed steps of how to integrate {{site.data.keyword.ihsdbaas_postgresql_full}}, check out [{{site.data.keyword.hscrypto}} integration](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-hpcs-byok).|
|[{{site.data.keyword.ihsdbaas_mongodb_full}}](https://cloud.ibm.com/catalog/services/hyper-protect-dbaas-for-mongodb){: external}|For detailed steps of how to integrate {{site.data.keyword.ihsdbaas_mongodb_full}}, check out [{{site.data.keyword.hscrypto}} integration](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-hpcs-byok).|
{: caption="Table 2. Supported database services" caption-side="bottom"}


## Integrating with compute services
{: #compute-integration}

Use {{site.data.keyword.hscrypto}} to provide secure key management capability for compute services.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud](https://cloud.ibm.com/vpc/compute/vs){: external}|Create an encrypted block storage volume when you create a virtual server instance by using {{site.data.keyword.hscrypto}}. Use your own root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest. </br></br> To learn detailed steps of integrating {{site.data.keyword.vsi_is_short}}, check out [Creating virtual server instances with customer-managed encryption](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-creating-instances-byok).|
|[Key Management Interoperability Protocol (KMIP) for VMware on {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/infrastructure/vmware-solutions/console/gettingstarted/KMIPAdapter){: external}|Use {{site.data.keyword.hscrypto}} to manage encryption keys that are used by VMware solutions on {{site.data.keyword.cloud_notm}}. </br></br> To learn more about integrating VMware Solutions, check out the following references: <ul><li>Overview: [KMIP for VMware on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations)</li><li>Overview video: [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} and VMware on {{site.data.keyword.cloud_notm}} solutions](https://www.youtube.com/watch?v=9n8-hQBMYWQ){: external}</li><li>Tutorial: [Use {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} to encrypt VMware disks](https://developer.ibm.com/tutorials/use-hyper-protect-crypto-services-to-encrypt-vmware-disks/)</li><li>Demo video: [Integrating {{site.data.keyword.hscrypto}} with VMware on {{site.data.keyword.cloud_notm}} solutions](https://www.youtube.com/watch?v=huQ5wUfrW4c){: external}</li></ul>|
|[HyTrust DataControl for {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/infrastructure/vmware-solutions/console/gettingstarted/HyTrustDC){: external}|The HyTrust DataControl service integrates with {{site.data.keyword.hscrypto}} to protect your data with strong encryption and scalable key management. The service provides encryption at both the operating system level and at the data level to secure your workloads throughout their lifecycles. </br></br> To learn more about HyTrust DataControl, check out the following references:<ul><li>Overview: [HyTrust DataControl overview](/docs/vmwaresolutions?topic=vmwaresolutions-htdc_considerations)</li><li>Website: [HyTrust DataControl for {{site.data.keyword.cloud_notm}}](https://www.hytrust.com/datacontrol-ibm-cloud/){: external}</li></ul>|
{: caption="Table 3. Supported compute services" caption-side="bottom"}

## Integrating with container services
{: #container-integration}

Use your own root keys managed by {{site.data.keyword.hscrypto}} to protect container secrets and enable more granular control over user access.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.containerlong_notm}}](https://cloud.ibm.com/kubernetes/catalog/cluster){: external}|For detailed steps of how to integrate {{site.data.keyword.containerlong_notm}}, check out [Encrypting the Kubernetes master's local disk and secrets by using a KMS provider](/docs/containers?topic=containers-encryption#keyprotect).|
|[{{site.data.keyword.openshiftlong_notm}}](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster){: external}|For detailed steps of how to integrate {{site.data.keyword.openshiftshort}}, check out [Encrypting the {{site.data.keyword.openshiftshort}} master's local disk and secrets by using a KMS provider](/docs/openshift?topic=openshift-encryption#keyprotect).|
{: caption="Table 4. Supported container services" caption-side="bottom"}


## Understanding your integration
{: #understand-integration}

When you integrate a supported service with {{site.data.keyword.hscrypto}}, you enable [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) for that service. This integration allows you to use a root key that you store in {{site.data.keyword.hscrypto}} to wrap the data encryption keys that encrypt your data at rest.

For example, you can create a root key, manage the key in {{site.data.keyword.hscrypto}}, and use the root key to protect the data that is stored across different cloud services.

The following diagram illustrates the scene of integrating {{site.data.keyword.hscrypto}} with two services.

![The diagram shows a contextual view of your {{site.data.keyword.hscrypto}} integration.](/image/hpcs-integrations.svg "Cloud services integrates with Hyper Protect Crypto Services"){: caption="Figure 1. Integrating {{site.data.keyword.hscrypto}}" caption-side="bottom"}

Behind the scenes, the {{site.data.keyword.hscrypto}} key management API drives the envelope encryption process.

The following table lists the API methods that add or remove envelope encryption on a resource.

<table>
  <tr>
    <th>Method</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>POST /keys/{root_key_ID}?action=wrap</code></td>
    <td><a href="/docs/hs-crypto?topic=hs-crypto-wrap-keys">Wrap (encrypt) a data encryption key</a></td>
  </tr>
  <tr>
    <td><code>POST /keys/{root_key_ID}?action=unwrap</code></td>
    <td><a href="/docs/hs-crypto?topic=hs-crypto-unwrap-keys">Unwrap (decrypt) a data encryption key</a></td>
  </tr>
  <caption style="caption-side:bottom;">Table 5. Describes the {{site.data.keyword.hscrypto}} key management API methods</caption>
</table>

To find out more about programmatically managing your keys in {{site.data.keyword.hscrypto}}, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
{: tip}

<!--
## Integrating a supported service
{: #grant-access}

To add an integration, create an authorization between services by using the {{site.data.keyword.iamlong}} dashboard. Authorizations enable service to service access policies, so you can associate a resource in your cloud data service with a root key that you manage in {{site.data.keyword.hscrypto}}.

Be sure to provision both services in the same region before you create an authorization. To learn more about service authorizations, see [Granting access between services](/docs/account?topic=account-serviceauth){: external}.
{: note}

When you're ready to integrate a service, use the following steps to create an authorization:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source and target service for the authorization.

  For **Source service**, select the cloud data service that you want to integrate with {{site.data.keyword.hscrypto}}. For **Target service**, select **{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}**.

5. Enable the **Reader** role.

    With *Reader* permissions, your source service can browse the root keys that are provisioned in the specified instance of {{site.data.keyword.hscrypto}}.

6. Click **Authorize**.
-->

## What's next
{: #integration-next-steps}

Add advanced encryption to your cloud resources by creating a root key in {{site.data.keyword.hscrypto}}. Add a new resource to a supported cloud data service, and then select the root key that you want to use for advanced encryption.

- To find out more about creating root keys with the {{site.data.keyword.hscrypto}} service, see [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
- To find out more about bringing your own root keys to the {{site.data.keyword.hscrypto}} service, see [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys).
