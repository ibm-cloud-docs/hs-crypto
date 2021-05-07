---

copyright:
  years: 2018, 2021
lastupdated: "2021-05-07"

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

You can integrate {{site.data.keyword.cloud_notm}} services with {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to build solutions for you to bring and manage your own encryption in the cloud.
{: shortdesc}

After you [create an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision) and [initialize the service instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm), you can integrate {{site.data.keyword.hscrypto}} with the following supported services.

## Storage service integrations
{: #storage-integration}

Add [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to your storage by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.cos_full_notm}}](https://cloud.ibm.com/catalog/services/cloud-object-storage){: external}|For detailed steps of how to integrate {{site.data.keyword.cos_full_notm}}, check out the following references: <ul><li>Demo video: [Integrating {{site.data.keyword.cos_full_notm}} with {{site.data.keyword.hscrypto}}](https://mediacenter.ibm.com/media/0_mgxwp16v){: external}</li><li>Instructions: [Server-side encryption with {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}}](/docs/cloud-object-storage?topic=cloud-object-storage-encryption)</li></ul>|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud (Gen 1 compute)](https://cloud.ibm.com/vpc/storage/storageVolumes){: external}|For detailed steps of how to integrate {{site.data.keyword.block_storage_is_short}} (Gen 1 compute), check out [Creating block storage volumes with customer-managed encryption](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-encryption).|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud (Gen 2 compute)](https://cloud.ibm.com/vpc-ext/storage/storageVolumes){: external}  | For detailed steps of how to integrate {{site.data.keyword.block_storage_is_short}} (Gen 2 compute), check out [Creating block storage volumes with customer-managed encryption](/docs/vpc?topic=vpc-block-storage-vpc-encryption).  |
{: caption="Table 1. Supported storage services" caption-side="bottom"}

## Database service integrations
{: #database-integration}

Associate the encryption keys that you manage in {{site.data.keyword.hscrypto}} with your database service instances and leverage [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to add another layer of protection to your data. With full control over your keys, no one else including {{site.data.keyword.cloud_notm}} administrators can access your data.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.ihsdbaas_postgresql_full}}](https://cloud.ibm.com/catalog/services/hyper-protect-dbaas-for-postgresql){: external}|For detailed steps of how to integrate {{site.data.keyword.ihsdbaas_postgresql_full}}, check out [{{site.data.keyword.hscrypto}} integration](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-hpcs-byok).|
|[{{site.data.keyword.ihsdbaas_mongodb_full}}](https://cloud.ibm.com/catalog/services/hyper-protect-dbaas-for-mongodb){: external}|For detailed steps of how to integrate {{site.data.keyword.ihsdbaas_mongodb_full}}, check out [{{site.data.keyword.hscrypto}} integration](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-hpcs-byok).|
|[{{site.data.keyword.cloud_notm}} Databases for DataStax](https://cloud.ibm.com/catalog/services/databases-for-cassandra){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Databases for Elasticsearch](https://cloud.ibm.com/catalog/services/databases-for-elasticsearch){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Databases for EnterpriseDB](https://cloud.ibm.com/catalog/services/databases-for-enterprisedb){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Databases for etcd](https://cloud.ibm.com/catalog/services/databases-for-etcd){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Databases for Enterprise DB (EDB)](https://cloud.ibm.com/catalog/services/databases-for-enterprisedb){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Databases for MongoDB](https://cloud.ibm.com/catalog/services/databases-for-mongodb){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Databases for PostgreSQL](https://cloud.ibm.com/catalog/services/databases-for-postgresql){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Databases for Redis](https://cloud.ibm.com/catalog/services/databases-for-redis){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Databases, check out [the integration tutorial](/docs/cloud-databases?topic=cloud-databases-hpcs).|
|[{{site.data.keyword.cloud_notm}} Messages for RabbitMQ](https://cloud.ibm.com/catalog/services/messages-for-rabbitmq){: external}|For detailed steps of how to integrate {{site.data.keyword.cloud_notm}} Messages for RabbitMQ, check out [the integration tutorial](/docs/messages-for-rabbitmq?topic=cloud-databases-hpcs).|
{: caption="Table 2. Supported database services" caption-side="bottom"}


## Compute service integrations
{: #compute-integration}

Use {{site.data.keyword.hscrypto}} to provide secure key management capability for compute services.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud](https://cloud.ibm.com/vpc/compute/vs){: external}|Create an encrypted block storage volume when you create a virtual server instance by using {{site.data.keyword.hscrypto}}. Use your own root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest. </br></br> To learn detailed steps of integrating {{site.data.keyword.vsi_is_short}}, check out [Creating virtual server instances with customer-managed encryption](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-creating-instances-byok).|
|[Key Management Interoperability Protocol (KMIP) for VMware on {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/infrastructure/vmware-solutions/console/gettingstarted/KMIPAdapter){: external}|Use {{site.data.keyword.hscrypto}} to manage encryption keys that are used by VMware solutions on {{site.data.keyword.cloud_notm}}. </br></br> To learn more about integrating VMware Solutions, check out the following references: <ul><li>Overview: [KMIP for VMware on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations)</li><li>Overview video: [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} and VMware on {{site.data.keyword.cloud_notm}} solutions](https://mediacenter.ibm.com/media/0_4wm4bq4s){: external}.</li><li>Tutorial: [Use {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} to encrypt VMware disks](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware).</li><li>Demo video: [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](https://mediacenter.ibm.com/media/1_e5gk6ktn){: external}.</li></ul>|
|[HyTrust DataControl for {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/infrastructure/vmware-solutions/console/gettingstarted/HyTrustDC){: external}|The HyTrust DataControl service integrates with {{site.data.keyword.hscrypto}} to protect your data with strong encryption and scalable key management. The service provides encryption at both the operating system level and at the data level to secure your workloads throughout their lifecycles. </br></br> To learn more about HyTrust DataControl, check out the following references:<ul><li>Overview: [HyTrust DataControl overview](/docs/vmwaresolutions?topic=vmwaresolutions-htdc_considerations)</li><li>Website: [HyTrust DataControl for {{site.data.keyword.cloud_notm}}](https://www.hytrust.com/datacontrol-ibm-cloud/){: external}</li></ul>|
{: caption="Table 3. Supported compute services" caption-side="bottom"}

## Container service integrations
{: #container-integration}

Use your own root keys managed by {{site.data.keyword.hscrypto}} to protect container secrets and enable more granular control over user access.

|Service|Integration instructions|
|-------|-----------|
|[{{site.data.keyword.containerlong_notm}}](https://cloud.ibm.com/kubernetes/catalog/cluster){: external}|For detailed steps of how to integrate {{site.data.keyword.containerlong_notm}}, check out [Encrypting the Kubernetes master's local disk and secrets by using a KMS provider](/docs/containers?topic=containers-encryption#keyprotect).|
|[{{site.data.keyword.openshiftlong_notm}}](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster){: external}|<ul><li> You can integrate {{site.data.keyword.openshiftshort}} with the {{site.data.keyword.hscrypto}} key management service to protect sensitive information in your cluster, check out [Encrypting the {{site.data.keyword.openshiftshort}} master's local disk and secrets by using a KMS provider](/docs/openshift?topic=openshift-encryption#keyprotect).</li><li>You can also deploy the {{site.data.keyword.hscrypto}} Router to encrypt routes with a private key that is stored in the EP11 keystore of the {{site.data.keyword.hscrypto}} instance. For detailed steps, check out [Encrypting routes with keys that are stored in {{site.data.keyword.hscrypto}}](/docs/openshift?topic=openshift-hpcs-router). </li></ul>|
{: caption="Table 4. Supported container services" caption-side="bottom"}

## Ingestion service integrations
{: #Ingestion-integrations}

You can integrate {{site.data.keyword.hscrypto}} with the following ingestion services.

| Service | Integration instructions |
| ------- | ---------------- |
| [{{site.data.keyword.mon_full_notm}}](https://cloud.ibm.com/observe/monitoring){: external} | To use this service to gain operational visibility into the performance and health of your {{site.data.keyword.hscrypto}} instance, see [the instruction](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-mng-data).|
| [{{site.data.keyword.bpfull_notm}}](https://cloud.ibm.com/schematics/overview){: external} | Use {{site.data.keyword.hscrypto}} to encrypted your keys and data in {{site.data.keyword.bpfull_notm}}, follow [the instruction](/docs/schematics?topic=schematics-secure-data#pi-encrypt). |
| [{{site.data.keyword.messagehub}}](https://cloud.ibm.com/catalog/services/event-streams){: external} | To enable a customer-managed key for {{site.data.keyword.messagehub}} by using {{site.data.keyword.hscrypto}}, follow [the instruction](/docs/EventStreams?topic=EventStreams-managing_encryption). |
{: caption="Table 5. Supported ingestion services." caption-side="bottom"}

## Security service integrations
{: #security-service-integrations}

You can integrate {{site.data.keyword.hscrypto}} with the following security-related services.

| Service | Integration instructions |
| ------- | ---------------- |
| [{{site.data.keyword.appid_short_notm}}](https://cloud.ibm.com/catalog/services/app-id){: external} |  To enable customer-managed keys for {{site.data.keyword.appid_short_notm}} by using {{site.data.keyword.hscrypto}}, see [the instruction](/docs/appid?topic=appid-mng-data).|
| [{{site.data.keyword.secrets-manager_short}}](https://cloud.ibm.com/catalog/services/secrets-manager){: external} | To protect the customer-managed keys in {{site.data.keyword.secrets-manager_short}} by using {{site.data.keyword.hscrypto}}, follow [the instruction](/docs/secrets-manager?topic=secrets-manager-mng-data#data-encryption). |
| [{{site.data.keyword.cloudcerts_short}}](https://cloud.ibm.com/catalog/services/certificate-manager){: external} | To enable customer-managed keys for {{site.data.keyword.cloudcerts_short}} by using {{site.data.keyword.hscrypto}}, follow [the instruction](/docs/certificate-manager?topic=certificate-manager-mng-data). |
| [{{site.data.keyword.compliance_short}}](https://cloud.ibm.com/security-compliance/overview){: external} | To protect your sensitive data for {{site.data.keyword.compliance_short}} by using {{site.data.keyword.hscrypto}}, follow [the instruction](/docs/security-compliance?topic=security-compliance-mng-data). |
{: caption="Table 5. Supported security services." caption-side="bottom"}


## Understanding your integration
{: #understand-integration}

When you integrate a supported service with {{site.data.keyword.hscrypto}}, you enable [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) for that service. With this integration, you can use a root key that you store in {{site.data.keyword.hscrypto}} to wrap the data encryption keys that encrypt your data at rest.

For example, you can create a root key, manage the key in {{site.data.keyword.hscrypto}}, and use the root key to protect the data that is stored across different cloud services.

The following diagram illustrates the scene of integrating {{site.data.keyword.hscrypto}} with two services.

![The diagram shows a contextual view of your {{site.data.keyword.hscrypto}} integration.](/images/hpcs-integrations.svg "Cloud services integrates with Hyper Protect Crypto Services"){: caption="Figure 1. Integrating {{site.data.keyword.hscrypto}}" caption-side="bottom"}

Behind the scenes, the {{site.data.keyword.hscrypto}} key management API drives the envelope encryption process.

The following table lists the API methods that add or remove envelope encryption on a resource.

<table>
  <tr>
    <th>Method</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>POST /keys/{root_key_ID}?action=wrap</code></td>
    <td><a href="/docs/hs-crypto?topic=hs-crypto-wrap-keys">Wrap (encrypt) a data encryption key.</a></td>
  </tr>
  <tr>
    <td><code>POST /keys/{root_key_ID}?action=unwrap</code></td>
    <td><a href="/docs/hs-crypto?topic=hs-crypto-unwrap-keys">Unwrap (decrypt) a data encryption key.</a></td>
  </tr>
  <caption style="caption-side:bottom;">Table 5. Describes the {{site.data.keyword.hscrypto}} key management API methods</caption>
</table>

To find out more about programmatically managing your keys in {{site.data.keyword.hscrypto}}, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
{: tip}



## What's next
{: #integration-next-steps}

Add advanced encryption to your cloud resources by creating a root key in {{site.data.keyword.hscrypto}}. Add a resource to a supported cloud data service, and then select the root key that you want to use for advanced encryption.

- To find out more about creating root keys with the {{site.data.keyword.hscrypto}} service, see [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
- To find out more about bringing your own root keys to the {{site.data.keyword.hscrypto}} service, see [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys).
