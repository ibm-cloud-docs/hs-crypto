---

copyright:
  years: 2021
lastupdated: "2021-06-30"

keywords: vpc, vpe, network access policy, virtual private endpoints, private gateway

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}


# Using a virtual private endpoint for VPC
{: #virtual-private-endpoints-for-vpc}

If you have an [{{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance](/docs/vpc?topic=vpc-getting-started) and want to connect the VPC instance to your {{site.data.keyword.hscrypto}} instance for your data encryption needs, you can create a virtual private endpoint (VPE) for your VPC to access {{site.data.keyword.hscrypto}} within your VPC network.
{: shortdesc}

You can configure the VPE to use the IP addresses of your choice, which are allocated from a subnet within your VPC. VPEs are bound to a [VPE gateway](/docs/vpc?topic=vpc-about-vpe) and serve as an intermediary that enables your workload in VPC to connect to the private endpoints of your {{site.data.keyword.hscrypto}} instance.

To connect to {{site.data.keyword.hscrypto}} by using a virtual private endpoint, you must use the {{site.data.keyword.hscrypto}} API, CLI, or Terraform. The {{site.data.keyword.hscrypto}} UI needs to be accessed through the public network from your VPC.
{: note}

## Before you begin
{: #virtual-private-endpoints-for-vpc-prereqs}

Before you target a virtual private endpoint for {{site.data.keyword.hscrypto}}:

- Ensure that you have [provisioned a Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started){: external}.
- Ensure that you have conducted [planning for Virtual Private Endpoints](/docs/vpc?topic=vpc-planning-considerations){: external}.
- Ensure that [correct access controls](/docs/vpc?topic=vpc-vpe-configuring-acls){:external} are set for your virtual private endpoint.
- Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe){: external} of having a virtual private endpoint.
- Ensure that you have [created](/docs/vpc?topic=vpc-ordering-endpoint-gateway){: external} and understand how to
  [access](/docs/vpc?topic=vpc-accessing-vpe-after-setup){: external} a VPE gateway.
- Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway){: external} of
  a Virtual Private Endpoint.

## Virtual Private Service Endpoints
{: #virtual-private-endpoints-for-vpc-endpoints}

The table lists {{site.data.keyword.hscrypto}} private endpoints that are supported from the following VPC regions:

- Dallas (`us-south`)
- Frankfurt (`eu-de`)
- London (`eu-gb`)
- Sydney (`au-syd`)
- Tokyo (`jp-tok`)
- Washington DC (`us-east`)

You can connect to your {{site.data.keyword.hscrypto}} instance in another region using supported endpoints that corresponds to the service region. For example, from the Dallas VPC region, you can connect to your {{site.data.keyword.hscrypto}} instance created in the `us-east` region using the corresponding `us-east` endpoints.

When connecting to a VPE through [CLI](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-cli) or [API](/docs/vpc?topic=vpc-ordering-endpoint-gateway#vpe-ordering-api), you will need to specify the CRN of the region that you will use to connect to the {{site.data.keyword.hscrypto}}. Use the following table to locate the CRN of the target region.
{: note}

<table>
  <tr>
    <th>{{site.data.keyword.hscrypto}} feature</th>
    <th>Supported endpoints</th>
    <th>CRN</th>
  </tr>

  <tr>
    <td rowspan="5">Key management service</td>
    <td>api.private.au-syd.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:api.private.au-syd.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>api.private.eu-de.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:api.private.eu-de.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>api.private.us-east.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:api.private.us-east.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>api.private.us-south.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:api.private.us-south.hs-crypto.cloud.ibm.com</td>
  </tr>
  
  

  <tr>
    <td rowspan="5">Enterprise PKCS #11</td>
    <td>ep11.private.au-syd.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:ep11.private.au-syd.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>ep11.private.eu-de.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:ep11.private.eu-de.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>ep11.private.us-east.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:ep11.private.us-east.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>ep11.private.us-south.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:ep11.private.us-south.hs-crypto.cloud.ibm.com</td>
  </tr>
  
  
  <tr>
    <td rowspan="5">Trusted Key Entry (TKE)</td>
    <td>tke.private.au-syd.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:tke.private.au-syd.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>tke.private.eu-de.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:tke.private.eu-de.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>tke.private.us-east.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:tke.private.us-east.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>tke.private.us-south.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:tke.private.us-south.hs-crypto.cloud.ibm.com</td>
  </tr>
  
  
  <tr>
    <td rowspan="5">Key Management Interoperability Protocol (KMIP) adapter</td>
    <td>kmip.private.au-syd.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:kmip.private.au-syd.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>kmip.private.eu-de.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:kmip.private.eu-de.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>kmip.private.us-east.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:kmip.private.us-east.hs-crypto.cloud.ibm.com</td>
  </tr>
  <tr>
    <td>kmip.private.us-south.hs-crypto.cloud.ibm.com</td>
    <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:kmip.private.us-south.hs-crypto.cloud.ibm.com</td>
  </tr>
  
  
  <caption>Table 1. Private endpoints for connecting {{site.data.keyword.hscrypto}} over {{site.data.keyword.cloud_notm}} private network</caption>
</table>
