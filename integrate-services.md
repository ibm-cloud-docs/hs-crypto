---

copyright:
  years: 2018, 2021
lastupdated: "2021-11-02"

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

The data that you store in {{site.data.keyword.cloud_notm}} storage services is encrypted by default by using randomly generated keys. If you want to control the encryption keys and use your own keys to encrypt your storage, you can associate root keys that you manage in {{site.data.keyword.hscrypto}} to your storage service and leverage [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to add another layer of protection to your data. As root keys are encrypted by the master key that is owned by the user, no one else including {{site.data.keyword.cloud_notm}} administrators can access your data.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage){: external} | {{site.data.keyword.cos_full_notm}} is a highly available, durable, and secure platform for storing unstructured data. Object storage is the most efficient way to store PDFs, media files, database backups, disk images, or even large structured datasets. | <ul><li>Demo video: [Integrating {{site.data.keyword.cos_full_notm}} with {{site.data.keyword.hscrypto}}](https://mediacenter.ibm.com/media/0_mgxwp16v){: external}</li><li>Instruction: [Server-side encryption with {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}}](/docs/cloud-object-storage?topic=cloud-object-storage-encryption)</li></ul> |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-block-storage-about){: external}  | {{site.data.keyword.blockstorageshort}} for VPC provides hypervisor-mounted, high-performance data storage for your virtual server instances that you can provision within your VPC. | [Creating block storage volumes with customer-managed encryption](/docs/vpc?topic=vpc-block-storage-vpc-encryption) |
{: caption="Table 1. Supported storage services" caption-side="bottom"}

## Database service integrations
{: #database-integration}

The data that you store in {{site.data.keyword.cloud_notm}} database services is encrypted by default by using randomly generated keys. If you want to control the encryption keys and use your own keys to encrypt your databases, you can associate root keys that you manage in {{site.data.keyword.hscrypto}} to your database service and leverage [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to add another layer of protection to your data. As root keys are encrypted by the master key that is owned by the user, no one else including {{site.data.keyword.cloud_notm}} administrators can access your data.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [{{site.data.keyword.ihsdbaas_postgresql_full}}](/docs/hyper-protect-dbaas-for-postgresql){: external} | {{site.data.keyword.ihsdbaas_postgresql_full}} offers fully managed and highly secure PostgreSQL database environments that have technology-enforced protection and high availability. | [{{site.data.keyword.hscrypto}} integration](/docs/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-hpcs-byok) |
| [{{site.data.keyword.ihsdbaas_mongodb_full}}](/docs/hyper-protect-dbaas-for-mongodb){: external} | {{site.data.keyword.ihsdbaas_mongodb_full}} offers fully managed and highly secure PostgreSQL database environments that have technology-enforced protection and high availability. | [{{site.data.keyword.hscrypto}} integration](/docs/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-hpcs-byok) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-cassandra}}](/docs/databases-for-cassandra){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-cassandra}} is a scale-out NoSQL database service that is built on Apache Cassandra. It is designed to power real-time applications with high availability and massive scalability. | [{{site.data.keyword.hscrypto}} integration](/docs/databases-for-cassandra?topic=cloud-databases-hpcs) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-elasticsearch}}](/docs/databases-for-elasticsearch){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-elasticsearch}} is an enterprise-ready and fully managed Elasticsearch service that is built with native interation into {{site.data.keyword.cloud_notm}}. | [{{site.data.keyword.hscrypto}} integration](/docs/databases-for-elasticsearch?topic=cloud-databases-hpcs) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-enterprisedb}}](/docs/databases-for-enterprisedb){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-enterprisedb}} is a database engine that optimizes the built-in features of PostgreSQL. You can gain greater scalability, security, and reliability along with enhancements that improve database administrator and developer productivity.  | [{{site.data.keyword.hscrypto}} integration](/docs/databases-for-enterprisedb?topic=cloud-databases-hpcs) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-etcd}}](https://cloud.ibm.com/docs/databases-for-etcd){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-etcd}} is an enterprise-ready and fully managed etcd service that is built with native integration into the {{site.data.keyword.cloud_notm}}. | [{{site.data.keyword.hscrypto}} integration](/docs/databases-for-etcd?topic=cloud-databases-hpcs) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-mongodb}}](/docs/databases-for-mongodb){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-mongodb}} is an enterprise-ready and fully managed MongoDB service that is built with native integration into the {{site.data.keyword.cloud_notm}}. | [{{site.data.keyword.hscrypto}} integration](/docs/databases-for-mongodb?topic=cloud-databases-hpcs) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-postgresql}}](/docs/databases-for-postgresql){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-postgresql}} is an enterprise-ready and fully managed PostgreSQL service that is built with native integration into the {{site.data.keyword.cloud_notm}}. | [{{site.data.keyword.hscrypto}} integration](/docs/databases-for-postgresql?topic=cloud-databases-hpcs) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-redis}}](/docs/databases-for-redis){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.databases-for-redis}} is an open source, in-memory key value store designed for the modern application stack. With {{site.data.keyword.databases-for-redis}}, you can use counters, queues, lists, and HyperLogLogs to handle complex data issues simply. | [{{site.data.keyword.hscrypto}} integration](/docs/databases-for-redis?topic=cloud-databases-hpcs) |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.messages-for-rabbitmq}}](/docs/messages-for-rabbitmq){: external} | {{site.data.keyword.cloud_notm}} {{site.data.keyword.messages-for-rabbitmq}} is an enterprise-ready and fully managed RabbitMQ service with native integration into the {{site.data.keyword.cloud_notm}}. It supports multiple messaging protocols as a broker. | [{{site.data.keyword.hscrypto}} integration](/docs/messages-for-rabbitmq?topic=cloud-databases-hpcs) |
{: caption="Table 2. Supported database services" caption-side="bottom"}


## Compute service integrations
{: #compute-integration}

Use {{site.data.keyword.hscrypto}} to bring your own keys to compute services.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [{{site.data.keyword.cloud_notm}} image templates](/docs/image-templates?topic=image-templates-getting-started-with-image-templates#getting-started-with-image-templates){: external} | You can use {{site.data.keyword.cloud_notm}} image templates to capture an image of a virtual server to quickly replicate its configuration with minimal changes in the order process. With the End to End (E2E) Encryption feature, you can bring your own encrypted, cloud-init enabled operating system image. | [Using End to End Encryption to provision an encrypted instance](/docs/image-templates?topic=image-templates-using-end-to-end-e2e-encryption-to-provision-an-encrypted-instance#using-end-to-end-e2e-encryption-to-provision-an-encrypted-instance){: external} |
| [{{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-about-advanced-virtual-servers){: external} | {{site.data.keyword.BluVirtServers_short}} for VPC is an Infrastructure-as-a-Service (IaaS) offering that gives you access to all of the benefits of {{site.data.keyword.vpc_short}}, including network isolation, security, and flexibility. By integrating with {{site.data.keyword.hscrypto}}, you can create an encrypted block storage volume when you create a virtual server instance and use your own root keys to protect the data encryption keys that encrypt your data at rest. | [Creating virtual server instances with customer-managed encryption volumes](/docs/vpc?topic=vpc-creating-instances-byok) |
| [Key Management Interoperability Protocol (KMIP) for VMware&reg; on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations){: external} | KMIP for VMware&reg; works together with VMware native vSphere encryption and vSAN encryption to provide simplified storage encryption management. By integrating with {{site.data.keyword.hscrypto}}, you can use {{site.data.keyword.hscrypto}} to manage encryption keys that are used by VMware&reg; solutions on {{site.data.keyword.cloud_notm}}. | <ul><li>Overview: [KMIP for VMware&reg; on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations)</li><li>Tutorial: [Use {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} to encrypt VMware disks](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware)</li><li>Overview video: [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} and VMware&reg; on {{site.data.keyword.cloud_notm}} solutions](https://mediacenter.ibm.com/media/0_4wm4bq4s){: external}</li><li>Demo video: [Configuring KMIP in {{site.data.keyword.hscrypto}} for key management and distribution](https://mediacenter.ibm.com/media/1_e5gk6ktn){: external}</li></ul> |
| [HyTrust DataControl for {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-htdc_considerations){: external} | The HyTrust DataControl service integrates with {{site.data.keyword.hscrypto}} to protect your data with strong encryption and scalable key management. The service provides encryption at both the operating system level and at the data level to secure your workloads throughout their lifecycles. | <ul><li>HyTrust DataControl overview: [HyTrust DataControl overview](/docs/vmwaresolutions?topic=vmwaresolutions-htdc_considerations)</li><li>HyTrust official website: [HyTrust DataControl for {{site.data.keyword.cloud_notm}}](https://www.hytrust.com/datacontrol-ibm-cloud/){: external}</li></ul>|
{: caption="Table 3. Supported compute services" caption-side="bottom"}

## Container service integrations
{: #container-integration}

By integrating with {{site.data.keyword.hscrypto}}, you can encrypt the Kubernetes secrets and etcd component of your Kubernetes master with your own root keys that are managed in {{site.data.keyword.hscrypto}}.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [{{site.data.keyword.containerlong_notm}}](/docs/containers){: external} | {{site.data.keyword.containerlong_notm}} is a managed offering built for creating a Kubernetes cluster of compute hosts to deploy and manage containerized applications on {{site.data.keyword.cloud_notm}}.  | [Encrypting the Kubernetes master's local disk and secrets by using a KMS provider](/docs/containers?topic=containers-encryption#keyprotect) |
| [{{site.data.keyword.openshiftlong_notm}}](/docs/openshift){: external} | {{site.data.keyword.openshiftlong_notm}} is a managed offering to create your own {{site.data.keyword.openshiftshort}} cluster of compute hosts to deploy and manage containerized apps on {{site.data.keyword.cloud_notm}}. In addition to using {{site.data.keyword.hscrypto}} to protect the Kubernetes secrets, you can also deploy the {{site.data.keyword.hscrypto}} Router, which uses the `GREP11` OpenSSL Engine to access private keys that are stored in your {{site.data.keyword.hscrypto}} instance to encrypt routes. | <ul><li>[Encrypting the {{site.data.keyword.openshiftshort}} master's local disk and secrets by using a KMS provider](/docs/openshift?topic=openshift-encryption#keyprotect)</li><li>[Encrypting routes with keys that are stored in {{site.data.keyword.hscrypto}}](/docs/openshift?topic=openshift-hpcs-router)</li></ul> |
{: caption="Table 4. Supported container services" caption-side="bottom"}

## Ingestion service integrations
{: #Ingestion-integrations}

You can integrate {{site.data.keyword.hscrypto}} with the following ingestion services.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [{{site.data.keyword.bpfull_notm}}](/docs/schematics){: external} | {{site.data.keyword.bpfull_notm}} provides powerful tools to automate your cloud infrastructure provisioning and management process, the configuration and operation of your cloud resources, and the deployment of your application workloads. All data, user inputs and the data that is generated at runtime during execution of automation code, are stored in {{site.data.keyword.cos_full_notm}}. This data is encrypted by default by using encryption keys from Schematics. If you need to control the encryption keys, you can integrate with your {{site.data.keyword.hscrypto}} instance to use your own root keys. | [Enabling customer-managed keys for Schematics](/docs/schematics?topic=schematics-secure-data#using-byok) |
| [{{site.data.keyword.messagehub}}](/docs/EventStreams){: external} | The {{site.data.keyword.messagehub}} service is a high-throughput message bus that is built with Apache Kafka. You can use it for event ingestion into {{site.data.keyword.cloud_notm}} and event stream distribution between your services and applications. By default, message payload data in {{site.data.keyword.messagehub}} is encrypted at rest by using a randomly generated key. If you need to control the encryption keys, you can integrate with your {{site.data.keyword.hscrypto}} instance to use your own root keys. | [Enabling a customer-managed key for Event Streams](/docs/EventStreams?topic=EventStreams-managing_encryption#enabling_encryption) |
{: caption="Table 5. Supported ingestion services." caption-side="bottom"}

## Security service integrations
{: #security-service-integrations}

You can integrate {{site.data.keyword.hscrypto}} with the following security-related services. By default, the data that you store in these services is encrypted at rest by using an IBM-managed key. You can add a higher level of encryption control to your data at rest by enabling integration with {{site.data.keyword.hscrypto}} to use your own root keys.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [{{site.data.keyword.appid_short_notm}}](/docs/appid){: external} | {{site.data.keyword.appid_short_notm}} stores and encrypts user profile attributes. As a multi-tenant service, every tenant has a designated encryption key and user data in each tenant is encrypted with only that tenant's key. | [Enabling customer-managed keys for {{site.data.keyword.appid_short_notm}} by using {{site.data.keyword.hscrypto}}](/docs/appid?topic=appid-mng-data#enable-customer-keys-hpcs) |
| [{{site.data.keyword.secrets-manager_short}}](/docs/secrets-manager){: external} | With {{site.data.keyword.secrets-manager_short}}, you can centrally manage your secrets in a single-tenant, dedicated instance. | [Protecting your sensitive data in {{site.data.keyword.secrets-manager_short}}](/docs/secrets-manager?topic=secrets-manager-mng-data#data-encryption) |
| [{{site.data.keyword.cloudcerts_short}}](/docs/certificate-manager){: external} | You can use {{site.data.keyword.cloudcerts_short}} to order and manage SSL/TLS certificates for your applications and services. | [Protecting your sensitive data in {{site.data.keyword.cloudcerts_short}}](/docs/certificate-manager?topic=certificate-manager-mng-data#data-encryption) |
| [{{site.data.keyword.compliance_short}}](/docs/security-compliance){: external} | With {{site.data.keyword.compliance_short}}, you can govern cloud resource configurations and centrally manage your compliance with organization and regulatory guidelines. When you work with the {{site.data.keyword.compliance_short}}, data is generated by the service as you interact with it. | [Protecting your sensitive data in {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-mng-data#data-encryption) |
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
    <caption>Table 5. Describes the {{site.data.keyword.hscrypto}} key management API methods</caption>
</table>

To find out more about programmatically managing your keys in {{site.data.keyword.hscrypto}}, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](/apidocs/hs-crypto){: external}.
{: tip}



## What's next
{: #integration-next-steps}

Add advanced encryption to your cloud resources by creating a root key in {{site.data.keyword.hscrypto}}. Add a resource to a supported cloud data service, and then select the root key that you want to use for advanced encryption.

- To find out more about creating root keys with the {{site.data.keyword.hscrypto}} service, see [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
- To find out more about bringing your own root keys to the {{site.data.keyword.hscrypto}} service, see [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys).
