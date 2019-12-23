---

copyright:
  years: 2018, 2019
lastupdated: "2019-12-12"

keywords: Hyper Protect Crypto Services integration, integrate service with Hyper Protect Crypto Services

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
{:table: .aria-labeledby="caption"}
{:term: .term}

# Integrating services
{: #integrate-services}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} integrates with data and storage solutions to help you bring and manage your own encryption in the cloud.
{: shortdesc}

After you [create an instance of the service](/docs/services/hs-crypto?topic=hs-crypto-provision) and [initialize the service instance](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm), you can integrate {{site.data.keyword.hscrypto}} with the following supported services:

|Service|Description|
|-------|-----------|
|[{{site.data.keyword.ihsdbaas_postgresql_full}}](https://cloud.ibm.com/catalog/services/hyper-protect-dbaas-for-postgresql){: external}|Associate the encryption keys that you manage in {{site.data.keyword.hscrypto}} with your {{site.data.keyword.ihsdbaas_postgresql_full}} service instance to encrypt your database, so that you have full control over your keys and data. </br></br> To learn more about integrating {{site.data.keyword.ihsdbaas_postgresql_full}}, check out [{{site.data.keyword.hscrypto}} integration](/docs/services/hyper-protect-dbaas-for-postgresql?topic=hyper-protect-dbaas-for-postgresql-hpcs-byok).|
|[{{site.data.keyword.ihsdbaas_mongodb_full}}](https://cloud.ibm.com/catalog/services/hyper-protect-dbaas-for-mongodb){: external}|Associate the encryption keys that you manage in {{site.data.keyword.hscrypto}} with your {{site.data.keyword.ihsdbaas_mongodb_full}} service instance to encrypt your database, so that you have full control over your keys and data. </br></br> To learn more about integrating {{site.data.keyword.ihsdbaas_mongodb_full}}, check out [{{site.data.keyword.hscrypto}} integration](/docs/services/hyper-protect-dbaas-for-mongodb?topic=hyper-protect-dbaas-for-mongodb-hpcs-byok).|
{: caption="Table 1. Supported database services" caption-side="top"}
{: #table-1}
{: tab-title="Databases"}
{: tab-group="supported-services"}
{: class="simple-tab-table"}

|Service|Description|
|-------|-----------|
|[{{site.data.keyword.cos_full_notm}}](https://cloud.ibm.com/catalog/services/cloud-object-storage){: external}|Add [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) to your storage buckets by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest. </br></br> A demo video is available at [IBM Demos](https://www.ibm.com/demos/collection/IBM-Cloud-Hyper-Protect-Crypto-Services/){: external} and [YouTube](https://www.youtube.com/watch?v=e_4RO7r_t8M){: external} for you to better understand how the integration works. To learn more about integrating {{site.data.keyword.cos_short}}, check out [Server-side encryption with {{site.data.keyword.keymanagementservicelong_notm}} or {{site.data.keyword.hscrypto}}](/docs/services/cloud-object-storage?topic=cloud-object-storage-encryption#encryption-kp).|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} for Virtual Private Cloud](https://cloud.ibm.com/vpc/storage/storageVolumes){: external}|Add [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) to your block storage volume by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest. </br></br> To learn more about integrating {{site.data.keyword.block_storage_is_short}}, check out [Creating block storage volumes with customer-managed encryption](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-encryption).|
{: caption="Table 2. Supported storage services" caption-side="bottom"}
{: #table-2}
{: tab-title="Storage"}
{: tab-group="supported-services"}
{: class="simple-tab-table"}

|Service|Description|
|-------|-----------|
|[{{site.data.keyword.cloud_notm}} {{site.data.keyword.BluVirtServers_short}} for Virtual Private Cloud](https://cloud.ibm.com/vpc/compute/vs){: external}|Create an encrypted block storage volume when you create a virtual server instance by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest. </br></br> To learn more about integrating {{site.data.keyword.vsi_is_short}}, check out [Creating virtual server instances with customer-managed encryption](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-creating-instances-byok).|
|[Key Management Interoperability Protocol (KMIP) for VMware on {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/infrastructure/vmware-solutions/console/gettingstarted/KMIPAdapter){: external}|Use {{site.data.keyword.hscrypto}} to provide highly secured key management capability for {{site.data.keyword.vmwaresolutions_full_notm}}. </br></br> To learn more about integrating VMware Solutions, check out [KMIP for VMware on {{site.data.keyword.cloud_notm}} overview](/docs/services/vmwaresolutions/services?topic=vmware-solutions-kmip_standalone_considerations) and the [Overview video on {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} and VMware on {{site.data.keyword.cloud_notm}} solutions](https://www.youtube.com/watch?v=9n8-hQBMYWQ){: external}. For detailed tutorials, see [Use {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} to encrypt VMware disks](https://developer.ibm.com/tutorials/use-hyper-protect-crypto-services-to-encrypt-vmware-disks/) and the [demo video](https://www.youtube.com/watch?v=huQ5wUfrW4c){: external}.|
|[HyTrust DataControl for {{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/infrastructure/vmware-solutions/console/gettingstarted/HyTrustDC){: external}|The HyTrust DataControl service integrates with {{site.data.keyword.hscrypto}} to protect your data with strong encryption and scalable key management. The service provides encryption at both the operating system level and at the data level to secure your workloads throughout their lifecycles. </br></br> To learn more about HyTrust DataControl, see the [HyTrust DataControl overview](/docs/services/vmwaresolutions?topic=vmware-solutions-htdc_considerations) and [HyTrust website](https://www.hytrust.com/datacontrol-ibm-cloud/){: external}.|
{: caption="Table 3. Supported compute services" caption-side="bottom"}
{: #table-3}
{: tab-title="Compute"}
{: tab-group="supported-services"}
{: class="simple-tab-table"}

|Service|Description|
|-------|-----------|
|[{{site.data.keyword.containerlong_notm}} (IKS)](https://cloud.ibm.com/kubernetes/catalog/cluster){: external}|Leverage [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) to add a layer of security to your data in your {{site.data.keyword.containershort_notm}} cluster. Use your own root keys managed by {{site.data.keyword.hscrypto}} to protect Kubernetes secrets and enable more granular control over user access. </br></br> To learn more about integrating IKS, check out [Encrypting the Kubernetes master's local disk and secrets by using a KMS provider](/docs/containers?topic=containers-encryption#keyprotect).|
|[{{site.data.keyword.openshiftlong_notm}}](https://cloud.ibm.com/kubernetes/catalog/openshiftcluster){: external}|Leverage [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) to add a layer of security to your data in your {{site.data.keyword.openshiftshort}} cluster. Use your own root keys managed by {{site.data.keyword.hscrypto}} to protect {{site.data.keyword.openshiftshort}} secrets and enable more granular control over user access. </br></br> To learn more about integrating {{site.data.keyword.openshiftshort}}, check out [Encrypting the {{site.data.keyword.openshiftshort}} master's local disk and secrets by using a KMS provider](/docs/openshift?topic=openshift-encryption#keyprotect).|
{: caption="Table 4. Supported container services" caption-side="bottom"}
{: #table-4}
{: tab-title="Container"}
{: tab-group="supported-services"}
{: class="simple-tab-table"}

## Understanding your integration
{: #understand-integration}

When you integrate a supported service with {{site.data.keyword.hscrypto}}, you enable [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) for that service. This integration allows you to use a root key that you store in {{site.data.keyword.hscrypto}} to wrap the data encryption keys that encrypt your data at rest.

For example, you can create a root key, manage the key in {{site.data.keyword.hscrypto}}, and use the root key to protect the data that is stored across different cloud services.

![The diagram shows a contextual view of your {{site.data.keyword.hscrypto}} integration.](/image/hpcs-integrations.svg "Cloud services integrates with Hyper Protect Crypto Services"){: caption="Figure 1. Integrating {{site.data.keyword.hscrypto}}" caption-side="bottom"}

### {{site.data.keyword.hscrypto}} API methods
{: #envelope-encryption-api-methods}

Behind the scenes, the {{site.data.keyword.hscrypto}} API drives the envelope encryption process.  

The following table lists the API methods that add or remove envelope encryption on a resource.

<table>
  <tr>
    <th>Method</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>POST /keys/{root_key_ID}?action=wrap</code></td>
    <td><a href="/docs/services/hs-crypto?topic=hs-crypto-wrap-keys">Wrap (encrypt) a data encryption key</a></td>
  </tr>
  <tr>
    <td><code>POST /keys/{root_key_ID}?action=unwrap</code></td>
    <td><a href="/docs/services/hs-crypto?topic=hs-crypto-unwrap-keys">Unwrap (decrypt) a data encryption key</a></td>
  </tr>
  <caption style="caption-side:bottom;">Table 5. Describes the {{site.data.keyword.hscrypto}} API methods</caption>
</table>

To find out more about programmatically managing your keys in {{site.data.keyword.hscrypto}}, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
{: tip}

<!--
## Integrating a supported service
{: #grant-access}

To add an integration, create an authorization between services by using the {{site.data.keyword.iamlong}} dashboard. Authorizations enable service to service access policies, so you can associate a resource in your cloud data service with a [root key](/docs/services/hs-crypto/envelope-encryption?topic=hs-crypto-envelope-encryption#key-types) that you manage in {{site.data.keyword.hscrypto}}.

Be sure to provision both services in the same region before you create an authorization. To learn more about service authorizations, see [Granting access between services](/docs/iam?topic=iam-serviceauth){: external}.
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

- To find out more about creating root keys with the {{site.data.keyword.hscrypto}} service, see [Creating root keys](/docs/services/hs-crypto?topic=hs-crypto-create-root-keys).
- To find out more about bringing your own root keys to the {{site.data.keyword.hscrypto}} service, see [Importing root keys](/docs/services/hs-crypto?topic=hs-crypto-import-root-keys).
