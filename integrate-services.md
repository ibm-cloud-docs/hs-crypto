---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-18"

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

# Integrating services
{: #integrate-services}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} integrates with data and storage solutions to help you bring and manage your own encryption in the cloud.
{: shortdesc}


After you [create an instance of the service](/docs/services/hs-crypto?topic=hs-crypto-provision) and [initialize the service instance](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm), you can integrate {{site.data.keyword.hscrypto}} with the following supported services:

<table>
    <tr>
        <th>Service</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>
          <p>{{site.data.keyword.cos_full_notm}}</p>
        </td>
        <td>
          <p>Add [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) to your storage buckets by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest.</p>
          <p>Before using {{site.data.keyword.hscrypto}} instance as the root keys provider, make sure to [authorize access](/docs/iam?topic=iam-serviceauth) between {{site.data.keyword.cos_full_notm}} (source service) and {{site.data.keyword.hscrypto}} (target source). To learn more, check out [Manage encryption](/docs/services/cloud-object-storage?topic=cloud-object-storage-encryption).</p>
        </td>
    </tr>
    <tr>
        <td>
          <p>{{site.data.keyword.cloud_notm}} Block Storage for Virtual Private Cloud</p>
        </td>
        <td>
          <p>Add [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) to your block storage volume by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest.</p>
          <p>Before using {{site.data.keyword.hscrypto}} instance as the root keys provider, make sure to [authorize access](/docs/iam?topic=iam-serviceauth) between {{site.data.keyword.blockstorageshort}} (source service) and {{site.data.keyword.hscrypto}} (target source). To learn more, check out [Creating block storage volumes with customer-managed encryption](/docs/vpc-on-classic-block-storage?topic=vpc-on-classic-block-storage-block-storage-encryption).</p>
        </td>
    </tr>
    <tr>
        <td>
          <p>{{site.data.keyword.cloud_notm}} Virtual Private Cloud</p>
        </td>
        <td>
          <p>Create an encrypted block storage volume when you create a virtual server instance by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest.</p>
          <p>Before using {{site.data.keyword.hscrypto}} instance as the root keys provider, make sure to [authorize access](/docs/iam?topic=iam-serviceauth) between {{site.data.keyword.blockstorageshort}} (source service) and {{site.data.keyword.hscrypto}} (target source). To learn more, check out [Creating virtual server instances with customer-managed encryption](/docs/vpc-on-classic-vsi?topic=vpc-on-classic-vsi-creating-instances-byok).</p>
        </td>
    </tr>
    <tr>
        <td>
          <p>Key Management Interoperability Protocol (KMIP) for VMware on {{site.data.keyword.cloud_notm}}</p>
        </td>
        <td>
          <p>Use {{site.data.keyword.hscrypto}} to provide highly secured key management capability for {{site.data.keyword.vmwaresolutions_full_notm}}. To learn more, check out [KMIP for VMware on {{site.data.keyword.cloud_notm}} overview](/docs/services/vmwaresolutions/services?topic=vmware-solutions-kmip_standalone_considerations).</p>
        </td>
    </tr>

    <!--
    <tr>
        <td>
          <p>{{site.data.keyword.containerlong_notm}}</p>
        </td>
        <td>
          <p>Use [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) to protect secrets in your {{site.data.keyword.containershort_notm}} cluster. To learn more, check out [Encrypting Kubernetes secrets by using {{site.data.keyword.keymanagementserviceshort}} ](/docs/containers?topic=containers-encryption#keyprotect).</p>
        </td>
    </tr>
    <tr>
        <td>
          <p>{{site.data.keyword.databases-for-postgresql_full_notm}}</p>
        </td>
        <td>
          <p>Protect your databases by associating root keys with your {{site.data.keyword.databases-for-postgresql}} deployment. To learn more, check out the [{{site.data.keyword.databases-for-postgresql}} documentation](/docs/services/databases-for-postgresql?topic=databases-for-postgresql-key-protect).</p>
        </td>
    </tr>
    <tr>
        <td>
          <p>{{site.data.keyword.cloudant_short_notm}} for {{site.data.keyword.cloud_notm}} ({{site.data.keyword.cloud_notm}} Dedicated)</p>
        </td>
        <td>
          <p>Strengthen your encryption at rest strategy by associating root keys with your {{site.data.keyword.cloudant_short_notm}} Dedicated Hardware instance. To learn more, check out the [{{site.data.keyword.cloudant_short_notm}} documentation](/docs/services/Cloudant/offerings?topic=cloudant-security#secure-access-control).</p>
        </td>
    </tr>
    -->

    <caption style="caption-side:bottom;">Table 1. Describes the integrations that are available for {{site.data.keyword.hscrypto}}</caption>
</table>


## Understanding your integration
{: #understand-integration}

When you integrate a supported service with {{site.data.keyword.hscrypto}}, you enable [envelope encryption](/docs/services/hs-crypto?topic=hs-crypto-envelope-encryption) for that service. This integration allows you to use a root key that you store in {{site.data.keyword.hscrypto}} to wrap the data encryption keys that encrypt your data at rest.

For example, you can create a root key, manage the key in {{site.data.keyword.hscrypto}}, and use the root key to protect the data that is stored across different cloud services.

![The diagram shows a contextual view of your {{site.data.keyword.hscrypto}} integration.](image/hpcs-integrations.png)

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
  <caption style="caption-side:bottom;">Table 2. Describes the {{site.data.keyword.hscrypto}} API methods</caption>
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

    With _Reader_ permissions, your source service can browse the root keys that are provisioned in the specified instance of {{site.data.keyword.hscrypto}}.

6. Click **Authorize**.
-->

## What's next
{: #integration-next-steps}

Add advanced encryption to your cloud resources by creating a root key in {{site.data.keyword.hscrypto}}. Add a new resource to a supported cloud data service, and then select the root key that you want to use for advanced encryption.

- To find out more about creating root keys with the {{site.data.keyword.hscrypto}} service, see [Creating root keys](/docs/services/hs-crypto?topic=hs-crypto-create-root-keys).
- To find out more about bringing your own root keys to the {{site.data.keyword.hscrypto}} service, see [Importing root keys](/docs/services/hs-crypto?topic=hs-crypto-import-root-keys).
