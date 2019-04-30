---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-23"

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

# Integrating services
{: #integrate-services}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} integrates with data and storage solutions to help you bring and manage your own encryption in the cloud.
{: shortdesc}

[After you create an instance of the service](/docs/services/hs-crypto/provision.html), you can integrate {{site.data.keyword.hscrypto}} with the following supported services:

<table>
    <tr>
        <th>Service</th>
        <th>Description</th>
    </tr>
<!--<tr>
        <td>
          <p>{{site.data.keyword.cos_full_notm}}</p>
        </td>
        <td>
          <p>Add [envelope encryption](/docs/services/hs-crypto/envelope-encryption.html) to your storage buckets by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest. To learn more, check out [Integrating with {{site.data.keyword.cos_full_notm}}](/docs/services/
            hs-crypto/integrate-cos.html).</p>
        </td>
    </tr> -->
    <tr>
            <td>
              <p>{{site.data.keyword.blockstoragefull}}</p>
            </td>
            <td>
              <p>Add envelope encryption<!--[envelope encryption](/docs/services/hs-crypto/envelope-encryption.html)--> to your storage buckets by using {{site.data.keyword.hscrypto}}. Use root keys that you manage in {{site.data.keyword.hscrypto}} to protect the data encryption keys that encrypt your data at rest.</p>
            </td>
        </tr>
<!--    <tr>
        <td>
          <p>{{site.data.keyword.containerlong_notm}}</p>
        </td>
        <td>
          <p>Use envelope encryption[envelope encryption](/docs/services/hs-crypto/envelope-encryption.html) to protect secrets in your {{site.data.keyword.containershort_notm}} cluster. To learn more, check out [Encrypting Kubernetes secrets by using {{site.data.keyword.keymanagementserviceshort}} ](/docs/containers?topic=containers-encryption#keyprotect).</p>
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
    </tr> -->
   <caption style="caption-side:bottom;">Table 1. Describes the integrations that are available for {{site.data.keyword.hscrypto}}</caption>
</table>

## Understanding your integration
{: #understand-integration}

When you integrate a supported service with {{site.data.keyword.hscrypto}}, you enable envelope encryption<!--[envelope encryption](/docs/services/hs-crypto/envelope-encryption.html)--> for that service. This integration allows you to use a root key that you store in {{site.data.keyword.hscrypto}} to wrap the data encryption keys that encrypt your data at rest.

For example, you can create a root key, manage the key in {{site.data.keyword.hscrypto}}, and use the root key to protect the data that is stored across different cloud services.

![The diagram shows a contextual view of your {{site.data.keyword.hscrypto}} integration.](../image/hpcs-integrations.png)

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
    <td><a href="/docs/services/hs-crypto/wrap-keys.html">Wrap (encrypt) a data encryption key</a></td>
  </tr>
  <tr>
    <td><code>POST /keys/{root_key_ID}?action=unwrap</code></td>
    <td><a href="/docs/services/hs-crypto/unwrap-keys.html">Unwrap (decrypt) a data encryption key</a></td>
  </tr>
  <caption style="caption-side:bottom;">Table 2. Describes the {{site.data.keyword.hscrypto}} API methods</caption>
</table>

To find out more about programmatically managing your keys in {{site.data.keyword.hscrypto}}, check out the [{{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
{: tip}

## Integrating a supported service
{: #grant-access}

To add an integration, create an authorization between services by using the {{site.data.keyword.iamlong}} dashboard. Authorizations enable service to service access policies, so you can associate a resource in your cloud data service with a root key<!--[root key](/docs/services/hs-crypto/envelope-encryption?topic=hs-crypto-envelope-encryption#key-types)--> that you manage in {{site.data.keyword.hscrypto}}.

Be sure to provision both services in the same region before you create an authorization. To learn more about service authorizations, see [Granting access between services ![External link icon](../../../icons/launch-glyph.svg "External link icon")](/docs/iam?topic=iam-serviceauth){: new_window}.
{: note}

When you're ready to integrate a service, use the following steps to create an authorization:

1. From the menu bar, click **Manage** &gt; **Access (IAM)**, and select **Authorizations**.
2. Click **Create**.
3. Select a source and target service for the authorization.

  For **Source service**, select the cloud data service that you want to integrate with {{site.data.keyword.hscrypto}}. For **Target service**, select **{{site.data.keyword.cloud_notm}}{{site.data.keyword.hscrypto}}**.

5. Enable the **Reader** role.

    With _Reader_ permissions, your source service can browse the root keys that are provisioned in the specified instance of {{site.data.keyword.hscrypto}}.

6. Click **Authorize**.

## What's next
{: #integration-next-steps}

Add advanced encryption to your cloud resources by creating a root key in {{site.data.keyword.hscrypto}}. Add a new resource to a supported cloud data service, and then select the root key that you want to use for advanced encryption.

- To find out more about creating root keys with the {{site.data.keyword.hscrypto}} service, see [Creating root keys](/docs/services/hs-crypto/create-root-keys.html).
- To find out more about bringing your own root keys to the {{site.data.keyword.hscrypto}} service, see [Importing root keys](/docs/services/hs-crypto/import-root-keys.html).
