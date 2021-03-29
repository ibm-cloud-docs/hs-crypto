---

copyright:
  years: 2018, 2021
lastupdated: "2021-03-24"

keywords: regions, location, regional service endpoint, resource group, api endpoints, public service endpoint, private service endpoint, available regions, network connection

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}

# Regions and locations
{: #regions}

You can connect your applications with the {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} by specifying a regional service endpoint.
{: shortdesc}

 ## Available regions
{: #available-regions}

{{site.data.keyword.hscrypto}} is available in the following regions and locations:

- Dallas, US: `us-south`
- Frankfurt, Germany: `eu-de`
- Sydney, Australia: `au-syd`
- Washington DC, US: `us-east`

You can create {{site.data.keyword.hscrypto}} resources in one of the supported {{site.data.keyword.cloud_notm}} regions, which represent the
geographic area where your {{site.data.keyword.hscrypto}} requests are handled and processed. To learn more, see
[Locations, tenancy, and availability](/docs/hs-crypto?topic=hs-crypto-ha-dr#availability).

Currently, the `us-south` and `us-east` regions are enabled with recovery crypto units by default, which means, when a service instance is provisioned in either regions, you are enabled with the option to back up your master keys in the recovery crypto units located in both regions. For details, see [Introducing service instance initialization modes](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode#instance-initialization-recovery-crypto-unit).
{: note}

## Connectivity options
{: #connectivity-options}

{{site.data.keyword.hscrypto}} offers two connectivity options for interacting with its service APIs.

<dl>
    <dt>Public endpoints</dt>
        <dd>By default, you can connect to resources in your account over the {{site.data.keyword.cloud_notm}} public network. Your data is encrypted in transit by using the Transport Security Layer (TLS) 1.2 protocol.
        </dd>
    <dt>Private endpoints</dt>
        <dd>
        <p>For added benefits, you can also enable <a href="/docs/account?topic=account-vrf-service-endpoint" target="_blank" class="external"> virtual routing and forwarding (VRF) and service endpoints</a> for your infrastructure account. When you enable VRF for your account, you can connect to {{site.data.keyword.hscrypto}} by using a private IP that is accessible only through the {{site.data.keyword.cloud_notm}} private network.</p>
        <p>To learn how to connect to {{site.data.keyword.hscrypto}} by using a private endpoint, see <a href="/docs/hs-crypto?topic=hs-crypto-secure-connection">Connecting to {{site.data.keyword.hscrypto}} on the {{site.data.keyword.cloud_notm}} private network</a>.</p>
        </dd>
</dl>

## Service endpoints
{: #service-endpoints}

If you are managing your {{site.data.keyword.hscrypto}} resources programmatically, see the following table to determine the API endpoints to use when you connect to the [Key management API](https://{DomainName}/apidocs/hs-crypto), [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref), and  [GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

| Region        | Public key management service endpoints             |Public GREP11 service endpoints|
| ------------- | ---------------------------- |---------------------------- |
| Dallas        | `api.us-south.hs-crypto.cloud.ibm.com` |`ep11.us-south.hs-crypto.cloud.ibm.com` |
| Frankfurt     | `api.eu-de.hs-crypto.cloud.ibm.com`    |`ep11.eu-de.hs-crypto.cloud.ibm.com`    |
| Sydney        | `api.au-syd.hs-crypto.cloud.ibm.com`   |`ep11.au-syd.hs-crypto.cloud.ibm.com`   |
| Washington DC | `api.us-east.hs-crypto.cloud.ibm.com`  |`ep11.us-east.hs-crypto.cloud.ibm.com`  |
{: caption="Table 1. Lists public endpoints for interacting with {{site.data.keyword.hscrypto}} APIs over IBM Cloud's public network" caption-side="bottom"}
{: #table-1}
{: tab-title="Public"}
{: tab-group="region-endpoint"}
{: class="comparison-tab-table"}
{: row-headers}

| Region        | Private key management service endpoints             |Private GREP11 service endpoints|
| ------------- | ------------------------------------ |------------------------------------ |
| Dallas        | `api.private.us-south.hs-crypto.cloud.ibm.com` | `ep11.private.us-south.hs-crypto.cloud.ibm.com` |
| Frankfurt     | `api.private.eu-de.hs-crypto.cloud.ibm.com`    | `ep11.private.eu-de.hs-crypto.cloud.ibm.com`    |
| Sydney        | `api.private.au-syd.hs-crypto.cloud.ibm.com`   | `ep11.private.au-syd.hs-crypto.cloud.ibm.com`   |
| Washington DC | `api.private.us-east.hs-crypto.cloud.ibm.com`  | `ep11.private.us-east.hs-crypto.cloud.ibm.com`  |
{: caption="Table 2. Lists private endpoints for interacting with {{site.data.keyword.hscrypto}} APIs over IBM Cloud's private network" caption-side="bottom"}
{: #table-2}
{: tab-title="Private"}
{: tab-group="region-endpoint"}
{: class="comparison-tab-table"}

For more information about authenticating with {{site.data.keyword.hscrypto}}, see the following topics:

* [Setting up the key management API](/docs/hs-crypto?topic=hs-crypto-set-up-kms-api)
* [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api)
* [Performing cryptographic operations with the GREP11 API](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api).
