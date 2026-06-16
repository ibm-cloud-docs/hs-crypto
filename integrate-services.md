---

copyright:
  years: 2018, 2026
lastupdated: "2026-06-16"

keywords: integration, encryption at rest, cloud object storage, object storage, kmip, containers, vmware, database, compute

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Integrating IBM Cloud services with Hyper Protect Crypto Services
{: #integrate-services}

You can integrate IBM Cloud services with IBM Cloud&reg; Hyper Protect Crypto Services to build solutions for you to bring and manage your own encryption in the cloud.
{: shortdesc}

After you [create an instance of the service](/docs/hs-crypto?topic=hs-crypto-provision) and [initialize the service instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm), you need to establish [service-to-service authorizations](/docs/solution-tutorials?topic=solution-tutorials-resource-sharing#resource-sharing-implementation-s2sauth) to allow one service to access another one through either single-account authorization or cross-account authorization. For detailed instructions on how to establish authorizations, see [Creating an authorization in the UI](/docs/account?topic=account-serviceauth). Make sure that you follow the process and select Hyper Protect Crypto Services as the target service.

Refer to the following integration instructions to integrate Hyper Protect Crypto Services with each supported service.

## Storage service integrations
{: #storage-integration}

The data that you store in IBM Cloud storage services is encrypted by default by using randomly generated keys. If you want to control the encryption keys and use your own keys to encrypt your storage, you can associate root keys that you manage in Hyper Protect Crypto Services to your storage service and leverage [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to add another layer of protection to your data. As root keys are encrypted by the master key that is owned by the user, no one else including IBM Cloud administrators can access your data.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [IBM Cloud Object Storage](/docs/cloud-object-storage){: external} | IBM Cloud Object Storage is a highly available, durable, and secure platform for storing unstructured data. Object storage is the most efficient way to store PDFs, media files, database backups, disk images, or even large structured datasets. | <ul><li>Demo video: [Integrating IBM Cloud Object Storage with Hyper Protect Crypto Services](https://mediacenter.ibm.com/media/0_mgxwp16v){: external}</li><li>Instruction: [Server-side encryption with Hyper Protect Crypto Services](/docs/cloud-object-storage?topic=cloud-object-storage-hpcs){: external}</li></ul> |
| [IBM&reg; Cloud Block Storage for Virtual Private Cloud](/docs/vpc?topic=vpc-block-storage-about){: external}  | Block Storage for VPC provides hypervisor-mounted, high-performance data storage for your virtual server instances that you can provision within your VPC. | [Creating block storage volumes with customer-managed encryption](/docs/vpc?topic=vpc-block-storage-vpc-encryption){: external} |
| [IBM Cloud&reg; File Storage for VPC](/docs/vpc?topic=vpc-file-storage-vpc-about){: external} | IBM Cloud&reg; File Storage for VPC is a zonal file storage offering that provides NFS-based file storage services. | [Creating file shares with customer-managed encryption](/docs/vpc?topic=vpc-file-storage-vpc-encryption){: external} | 
{: caption="Supported storage services" caption-side="bottom"}

## Database service integrations
{: #database-integration}

The data that you store in IBM Cloud database services is encrypted by default by using randomly generated keys. If you want to control the encryption keys and use your own keys to encrypt your databases, you can associate root keys that you manage in Hyper Protect Crypto Services to your database service and leverages [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to add another layer of protection to your data. As root keys are encrypted by the master key that is owned by the user, no one else including IBM Cloud administrators can access your data.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [IBM Cloud Databases for Elasticsearch](/docs/databases-for-elasticsearch){: external} | IBM Cloud Databases for Elasticsearch is an enterprise-ready and fully managed Elasticsearch service that is built with native integration into IBM Cloud. | [Hyper Protect Crypto Services integration](/docs/cloud-databases?topic=cloud-databases-hpcs&interface=ui){: external} |
| [IBM Cloud Databases for EnterpriseDB](/docs/databases-for-enterprisedb){: external} | IBM Cloud Databases for EnterpriseDB is a database engine that optimizes the built-in features of PostgreSQL. You can gain greater scalability, security, and reliability along with enhancements that improve database administrator and developer productivity.  | [Hyper Protect Crypto Services integration](/docs/cloud-databases?topic=cloud-databases-hpcs&interface=ui){: external} |
| [IBM Cloud Databases for etcd](https://cloud.ibm.com/docs/databases-for-etcd){: external} | IBM Cloud Databases for etcd is an enterprise-ready and fully managed etcd service that is built with native integration into the IBM Cloud. | [Hyper Protect Crypto Services integration](/docs/cloud-databases?topic=cloud-databases-hpcs&interface=ui){: external} |
| [IBM Cloud Databases for MongoDB](/docs/databases-for-mongodb){: external} | IBM Cloud Databases for MongoDB is an enterprise-ready and fully managed MongoDB service that is built with native integration into the IBM Cloud. | [Hyper Protect Crypto Services integration](/docs/cloud-databases?topic=cloud-databases-hpcs&interface=ui){: external} |
| [IBM Cloud Databases for PostgreSQL](/docs/databases-for-postgresql){: external} | IBM Cloud Databases for PostgreSQL is an enterprise-ready and fully managed PostgreSQL service that is built with native integration into the IBM Cloud. | [Hyper Protect Crypto Services integration](/docs/cloud-databases?topic=cloud-databases-hpcs&interface=ui){: external} |
| [IBM Cloud Databases for Redis](/docs/databases-for-redis){: external} | IBM Cloud Databases for Redis is an open source, in-memory key value store designed for the modern application stack. With Databases for Redis, you can use counters, queues, lists, and HyperLogLogs to handle complex data issues simply. | [Hyper Protect Crypto Services integration](/docs/cloud-databases?topic=cloud-databases-hpcs&interface=ui){: external} |
| [IBM Cloud Messages for RabbitMQ](/docs/messages-for-rabbitmq){: external} | IBM Cloud Messages for RabbitMQ is an enterprise-ready and fully managed RabbitMQ service with native integration into the IBM Cloud. It supports multiple messaging protocols as a broker. | [Hyper Protect Crypto Services integration](/docs/cloud-databases?topic=cloud-databases-hpcs&interface=ui){: external} |
| [IBM Db2 as a Service](/docs/Db2onCloud){: external} | IBM Db2 as a Service is an SQL database that is provisioned for you in the cloud. You can use IBM Db2 SaaS just as you use any database software, but without the time and expense of hardware setup or software installation and maintenance. | [Hyper Protect Crypto Services integration](/docs/Db2onCloud?topic=Db2onCloud-hpcs){: external}  |
{: caption="Supported database services" caption-side="bottom"}


## Compute service integrations
{: #compute-integration}

Use Hyper Protect Crypto Services to bring your own keys to compute services.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [IBM Cloud image templates](/docs/image-templates?topic=image-templates-getting-started-with-image-templates#getting-started-with-image-templates){: external} | You can use IBM Cloud image templates to capture an image of a virtual server to quickly replicate its configuration with minimal changes in the order process. With the End to End (E2E) Encryption feature, you can bring your own encrypted, cloud-init enabled operating system image. | [Using End to End Encryption to provision an encrypted instance](/docs/image-templates?topic=image-templates-using-end-to-end-e2e-encryption-to-provision-an-encrypted-instance#using-end-to-end-e2e-encryption-to-provision-an-encrypted-instance){: external} |
| [IBM Cloud Virtual Servers for Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-about-advanced-virtual-servers){: external} | Virtual Servers for VPC is an Infrastructure-as-a-Service (IaaS) offering that gives you access to all of the benefits of IBM Cloud VPC, including network isolation, security, and flexibility. By integrating with Hyper Protect Crypto Services, you can create an encrypted block storage volume when you create a virtual server instance and use your own root keys to protect the data encryption keys that encrypt your data at rest. | [Creating virtual server instances with customer-managed encryption volumes](/docs/vpc?topic=vpc-creating-virtual-servers&interface=ui){: external} |
| [Key Management Interoperability Protocol (KMIP) for VMware&reg; on IBM Cloud](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations){: external} | KMIP for VMware&reg; works together with VMware native vSphere encryption and vSAN encryption to provide simplified storage encryption management. By integrating with Hyper Protect Crypto Services, you can use Hyper Protect Crypto Services to manage encryption keys that are used by VMware&reg; solutions on IBM Cloud. | <ul><li>Overview: [KMIP for VMware&reg; on IBM Cloud](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations){: external}</li><li>Tutorial: [Use IBM Cloud Hyper Protect Crypto Services to encrypt VMware disks](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware){: external}</li><li>Overview video: [IBM Cloud Hyper Protect Crypto Services and VMware&reg; on IBM Cloud solutions](https://mediacenter.ibm.com/media/0_4wm4bq4s){: external}</li><li>Demo video: [Configuring KMIP in Hyper Protect Crypto Services for key management and distribution](https://mediacenter.ibm.com/media/1_e5gk6ktn){: external}</li></ul> |
| [Entrust DataControl for IBM Cloud](/docs/vmwaresolutions?topic=vmwaresolutions-entrust-dc_considerations){: external} - formerly known as HyTrust CloudControl | The Entrust DataControl service integrates with Hyper Protect Crypto Services to protect your data with strong encryption and scalable key management. The service provides encryption at both the operating system level and at the data level to secure your workloads throughout their lifecycles. | <ul><li>[Entrust CloudControl on IBM Cloud overview](/docs/vmwaresolutions?topic=vmwaresolutions-entrust-cc_considerations){: external}</li><li>Entrust official website: [Entrust DataControl for IBM Cloud](https://www.entrust.com/digital-security/multi-cloud-encryption/datacontrol-ibm-cloud){: external}</li></ul>|
| [Power Virtual Server](/docs/power-iaas?topic=power-iaas-getting-started){: external} | Power Virtual Server is a Power Systems offering. You can use Power Virtual Server to integrate with Hyper Protect Crypto Services to securely store and protect encryption key information for AIX and Linux. | [Integrating Power Virtual Server with Hyper Protect Crypto Services](/docs/power-iaas?topic=power-iaas-integrate-hpcs){: external}|
{: caption="Supported compute services" caption-side="bottom"}

## Container service integrations
{: #container-integration}

By integrating with Hyper Protect Crypto Services, you can encrypt the Kubernetes secrets and etcd component of your Kubernetes master with your own root keys that are managed in Hyper Protect Crypto Services.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [IBM Cloud Kubernetes Service](/docs/containers){: external} | IBM Cloud Kubernetes Service is a managed offering that is built for creating a Kubernetes cluster of compute hosts to deploy and manage containerized applications on IBM Cloud.  | [Encrypting the Kubernetes master's local disk and secrets by using a KMS provider](/docs/containers?topic=containers-encryption#keyprotect){: external} |
| [Red Hat OpenShift on IBM Cloud](/docs/openshift){: external} | Red Hat OpenShift on IBM Cloud is a managed offering to create your own Red Hat OpenShift on IBM Cloud cluster of compute hosts to deploy and manage containerized apps on IBM Cloud. In addition to using Hyper Protect Crypto Services to protect the Kubernetes secrets, you can also deploy the Hyper Protect Crypto Services Router, which uses the `GREP11` OpenSSL Engine to access private keys that are stored in your Hyper Protect Crypto Services instance to encrypt routes. | <ul><li>[Encrypting the Red Hat OpenShift on IBM Cloud master's local disk and secrets by using a KMS provider](/docs/openshift?topic=openshift-encryption#keyprotect){: external}</li><li>OpenShift Data Foundation: [Setting up encryption by using Hyper Protect Crypto Services](/docs/openshift?topic=openshift-deploy-odf-vpc&interface=ui#odf-create-hscrypto-vpc){: external}</li></ul> |
{: caption="Supported container services" caption-side="bottom"}

## Ingestion service integrations
{: #Ingestion-integrations}

You can integrate Hyper Protect Crypto Services with the following ingestion services.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [IBM Cloud Monitoring](/docs/monitoring){: external} | IBM Cloud Monitoring is a cloud-native, and container-intelligence management system. You can use it to gain operational visibility into the performance and health of your Hyper Protect Crypto Services instance. | [Getting started tutorial](/docs/monitoring?topic=monitoring-getting-started){: external} |
| [IBM Cloud Schematics](/docs/schematics){: external} | IBM Cloud Schematics provides powerful tools to automate your cloud infrastructure provisioning and management process, the configuration and operation of your cloud resources, and the deployment of your application workloads. All data, user inputs, and the data that is generated at runtime during execution of automation code, are stored in IBM Cloud Object Storage. This data is encrypted by default by using encryption keys from Schematics. If you need to control the encryption keys, you can integrate with your Hyper Protect Crypto Services instance to use your own root keys. | [Enabling customer-managed keys for Schematics](/docs/schematics?topic=schematics-secure-data#data-storage){: external} |
| [Event Streams](/docs/EventStreams){: external} | The Event Streams service is a high-throughput message bus that is built with Apache Kafka. You can use it for event ingestion into IBM Cloud and event stream distribution between your services and applications. By default, message payload data in Event Streams is encrypted at rest by using a randomly generated key. If you need to control the encryption keys, you can integrate with your Hyper Protect Crypto Services instance to use your own root keys. | [Enabling a customer-managed key for Event Streams](/docs/EventStreams?topic=EventStreams-managing_encryption#enabling_encryption){: external} |
{: caption="Supported ingestion services." caption-side="bottom"}

## Security service integrations
{: #security-service-integrations}

You can integrate Hyper Protect Crypto Services with the following security-related services. By default, the data that you store in these services is encrypted at rest by using an IBM-managed key. You can add a higher level of encryption control to your data at rest by enabling integration with Hyper Protect Crypto Services to use your own root keys.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [App ID](/docs/appid){: external} | App ID stores and encrypts user profile attributes. As a multi-tenant service, every tenant has a designated encryption key and user data in each tenant is encrypted with only that tenant's key. | [Enabling customer-managed keys for App ID by using Hyper Protect Crypto Services](/docs/appid?topic=appid-mng-data#enable-customer-keys-hpcs){: external} |
| [Secrets Manager](/docs/secrets-manager){: external} | With Secrets Manager, you can centrally manage your secrets in a single-tenant, dedicated instance. | [Protecting your sensitive data in Secrets Manager](/docs/secrets-manager?topic=secrets-manager-mng-data#data-encryption){: external} |
| [Compliance Manager](/docs/security-compliance){: external} | With Compliance Manager, you can govern cloud resource configurations and centrally manage your compliance with organization and regulatory guidelines. When you work with the Compliance Manager, data is generated by the service as you interact with it. | [Protecting your sensitive data in Compliance Manager](/docs/security-compliance?topic=security-compliance-mng-data#data-encryption){: external} |
{: caption="Supported security services." caption-side="bottom"}

## Developer tools service integrations
{: #devtools-integrations}

You can integrate Hyper Protect Crypto Services with the following developer tools services.

| Service | Description | Integration instruction |
| ------- | ----------- | ----------------------- |
| [IBM Cloud&reg; Continuous Delivery](/docs/ContinuousDelivery?topic=ContinuousDelivery-getting-started){: external} | The Continuous Delivery service provides a suite of tools that support DevOps best practices. You can use the service to manage toolchains, operate delivery pipelines, gain insights into code quality and vulnerabilities, integrate third-party tools, and more. | <ul><li>[Creating a Continuous Delivery service instance](/docs/ContinuousDelivery?topic=ContinuousDelivery-create_cd_service){: external}</li> <li>[Protecting your personal data when you use the Professional plan](/docs/ContinuousDelivery?topic=ContinuousDelivery-cd_data_security#cd_professional_plan){: external}</li></ul> |
{: caption="Supported developer tools services." caption-side="bottom"}


## Understanding your integration
{: #understand-integration}

When you integrate a supported service with Hyper Protect Crypto Services, you enable [envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) for that service. With this integration, you can use a root key that you store in Hyper Protect Crypto Services to wrap the data encryption keys that encrypt your data at rest.

For example, you can create a root key, manage the key in Hyper Protect Crypto Services, and use the root key to protect the data that is stored across different cloud services.

The following diagram illustrates the scene of integrating Hyper Protect Crypto Services with two services.

![The diagram shows a contextual view of your Hyper Protect Crypto Services integration.](/images/hpcs-integrations.svg "Cloud services integrate with Hyper Protect Crypto Services"){: caption="Integrating Hyper Protect Crypto Services" caption-side="bottom"}

Behind the scenes, the Hyper Protect Crypto Services key management service API drives the envelope encryption process.

The following table lists the API methods that add or remove envelope encryption on a resource.

| Method | Description |
| --- | --- |
| `POST /keys/{root_key_ID}?action=wrap` | [Wrap (encrypt) a data encryption key.](/docs/hs-crypto?topic=hs-crypto-wrap-keys){: external} |
| `POST /keys/{root_key_ID}?action=unwrap` | [Unwrap (decrypt) a data encryption key.](/docs/hs-crypto?topic=hs-crypto-unwrap-keys){: external} |
{: caption="Describes the Hyper Protect Crypto Services key management service API methods" caption-side="bottom"}

To find out more about programmatically managing your keys in Hyper Protect Crypto Services, check out the [Hyper Protect Crypto Services key management service API reference doc](/apidocs/hs-crypto){: external}.
{: tip}

## What's next
{: #integration-next-steps}

Add advanced encryption to your cloud resources by creating a root key in Hyper Protect Crypto Services. Add a resource to a supported cloud data service, and then select the root key that you want to use for advanced encryption.

- To find out more about creating root keys with the Hyper Protect Crypto Services service, see [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
- To find out more about bringing your own root keys to the Hyper Protect Crypto Services service, see [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys).
