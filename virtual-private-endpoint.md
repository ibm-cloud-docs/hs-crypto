---

copyright:
  years: 2021, 2024
lastupdated: "2024-12-12"

keywords: vpc, vpe, network access policy, virtual private endpoints, private gateway

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}






# Using virtual private endpoints for VPC to privately connect to {{site.data.keyword.hscrypto}}
{: #virtual-private-endpoints-for-vpc}

{{site.data.keyword.cloud}} Virtual Private Endpoints (VPE) for Virtual Private Cloud (VPC) enables you to connect to {{site.data.keyword.hscrypto}} from your VPC network by using the IP addresses of your choosing, allocated from a subnet within your VPC.
{: shortdesc}

VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally, is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud. For more information, see [About virtual private endpoint gateways](/docs/vpc?topic=vpc-about-vpe).

To connect to {{site.data.keyword.hscrypto}} by using a virtual private endpoint, you must use the {{site.data.keyword.hscrypto}} API, CLI, or Terraform. The {{site.data.keyword.hscrypto}} UI needs to be accessed through the public network from your VPC.
{: note}

## Before you begin
{: #virtual-private-endpoints-for-vpc-prereqs}

Before you target a virtual private endpoint for {{site.data.keyword.hscrypto}}, you must complete the following tasks:

- Ensure that you have [provisioned a Virtual Private Cloud](/docs/vpc?topic=vpc-getting-started).
- Make a [plan for your virtual private endpoints](/docs/vpc?topic=vpc-planning-considerations).
- Ensure that correct access controls are set for your virtual private endpoint.
- Understand the [limitations](/docs/vpc?topic=vpc-limitations-vpe) of having a virtual private endpoint.
- Understand how to [view details](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway) about a virtual private endpoint.

## Setting up a VPE for {{site.data.keyword.hscrypto}}
{: #virtual-private-endpoints-for-vpc-setup}

When you create a VPE gateway by using the CLI or API, you must specify the [Cloud Resource Name (CRN)](/docs/account?topic=account-crn) of the region in which you want to connect to {{site.data.keyword.hscrypto}}. Review the following table for the available regions and CRNs to create your VPE gateways.

 

<table>
    <tr>
      <th scope="col">{{site.data.keyword.hscrypto}} feature</th>
      <th scope="col">Supported endpoints</th>
      <th scope="col">CRN</th>
    </tr>
    <tr>
      <td rowspan="9">Key management service</td>
      <td><code><instance_ID>api.private.au-syd.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:<instance_ID>.api.private.au-syd.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.eu-de.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:<instance_ID>.api.private.eu-de.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.us-east.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:<instance_ID>.api.private.us-east.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.us-south.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:<instance_ID>.api.private.us-south.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.eu-gb.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-gb:::endpoint:<instance_ID>.api.private.eu-gb.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.jp-tok.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:jp-tok:::endpoint:api.private.jp-tok.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.eu-es.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-es:::endpoint:api.private.eu-es.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.br-sao.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:br-sao:::endpoint:api.private.jbr-sao.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>api.private.ca-tor.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:ca-tor:::endpoint:api.private.ca-tor.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td rowspan="9">Enterprise PKCS #11 (EP11)</td>
      <td><code><instance_ID>.ep11.private.au-syd.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:<instance_ID>.ep11.private.au-syd.hs-crypto.appdomain.cloud</td>
      </tr>
    <tr>
      <td><code><instance_ID>ep11.private.eu-de.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:<instance_ID>.ep11.private.eu-de.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>ep11.private.us-east.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:<instance_ID>.ep11.private.us-east.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>ep11.private.us-south.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:<instance_ID>.ep11.private.us-south.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>ep11.private.eu-gb.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-gb:::endpoint:ep11.vpc.private.eu-gb.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>ep11.private.jp-tok.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:jp-tok:::endpoint:ep11.vpc.private.jp-tok.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>ep11.private.eu-es.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-es:::endpoint:ep11.vpc.private.eu-es.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>ep11.private.br-sao.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:br-sao:::endpoint:ep11.vpc.private.jbr-sao.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>ep11.private.ca-tor.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:ca-tor:::endpoint:ep11.vpc.private.ca-tor.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td rowspan="9">Trusted Key Entry (TKE)</td>
      <td><code><instance_ID>tke.private.au-syd.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:tke.private.au-syd.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.eu-de.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:tke.private.eu-de.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.us-east.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:tke.private.us-east.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.us-south.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:tke.private.us-south.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.eu-gb.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-gb:::endpoint:tke.vpc.private.eu-gb.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.jp-tok.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:jp-tok:::endpoint:tke.vpc.private.jp-tok.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.eu-es.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-es:::endpoint:tke.vpc.private.eu-es.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.br-sao.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:br-sao:::endpoint:tke.vpc.private.jbr-sao.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td><code><instance_ID>tke.private.ca-tor.hs-crypto.cloud.ibm.com</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:ca-tor:::endpoint:tke.vpc.private.ca-tor.hs-crypto.cloud.ibm.com</td>
    </tr>
    <tr>
      <td rowspan="9">Key Management Interoperability Protocol (KMIP) adapter</td>
      <td><code><instance_ID>kmip.private.au-syd.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:au-syd:::endpoint:<instance_ID>.kmip.private.au-syd.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.eu-de.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-de:::endpoint:<instance_ID>.kmip.private.eu-de.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.us-east.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-east:::endpoint:<instance_ID>.kmip.private.us-east.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.us-south.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:us-south:::endpoint:<instance_ID>.kmip.private.us-south.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.eu-gb.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-gb:::endpoint:kmip.private.eu-gb.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.jp-tok.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:jp-tok:::endpoint:kmip.private.jp-tok.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.eu-es.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:eu-es:::endpoint:kmip.private.eu-es.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.br-sao.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:br-sao:::endpoint:kmip.private.jbr-sao.hs-crypto.appdomain.cloud</td>
    </tr>
    <tr>
      <td><code><instance_ID>kmip.private.ca-tor.hs-crypto.appdomain.cloud</code></td>
      <td>crn:v1:bluemix:public:hs-crypto:ca-tor:::endpoint:kmip.private.ca-tor.hs-crypto.appdomain.cloud</td>
    </tr>
    <caption>Table 1. Available region endpoints and CRNs for creating VPE gateways</caption>
</table>

### Configuring an endpoint gateway
{: #vpe-gateway-configure-for-hpcs}

To configure a virtual private endpoint gateway, follow these steps:

1. List the available services, including {{site.data.keyword.cloud_notm}} infrastructure services available (by default) for all VPC users.
2. [Create an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway) for your {{site.data.keyword.hscrypto}} instance that you want to be privately available to the VPC.

    If you are creating a VPE gateway by using the [UI](https://{DomainName}/infrastructure){: external}, perform the following steps:

    1. Select the **Menu** icon ![Menu icon](../icons/icon_hamburger.svg "Menu"), and then click **VPC Infrastructure > Virtual private endpoint gateways** in the Network section, and then click **Create**. The **New virtual private endpoint gateway for VPC** page is displayed.
    2. In the **Cloud service** section, enable your {{site.data.keyword.hscrypto}} instance:

        - Under **Cloud service offerings**, select **Hyper Protect Crypto Services**.
        - Under **Cloud service regions**, verify the corresponding [region](/docs/hs-crypto?topic=hs-crypto-regions#available-regions) is pre-filled for your provisioned {{site.data.keyword.hscrypto}} instance.
        - Select the [private endpoint](/docs/hs-crypto?topic=hs-crypto-regions#service-endpoints) that you are going to use to connect with your VPC instance.
            If you are connecting to an EP11 private endpoint, make sure that you select all EP11 private endpoints for all available zones.
            {: important} 

3. [Bind a reserved IP address](/docs/vpc?topic=vpc-bind-unbind-reserved-ip) to the endpoint gateway.
4. View the created VPE gateways associated with the {{site.data.keyword.hscrypto}} instance. For more information, see [Viewing details of an endpoint gateway](/docs/vpc?topic=vpc-vpe-viewing-details-of-an-endpoint-gateway).

Now your virtual server instances in the VPC can access your {{site.data.keyword.hscrypto}} instance privately through it.

## Using your VPE for {{site.data.keyword.hscrypto}}
{: #use-vpe-for-hpcs}

After you create an endpoint gateway for your {{site.data.keyword.hscrypto}} instance, follow these steps to use private endpoints.

### Using the VPE with the CLI
{: #use-vpe-for-hpcs-cli}
{: cli}

- Using the VPE for the [TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#tke-cli-plugin)

    1. Update the TKE CLI plug-in to the latest version with the following command:

        ```
        ibmcloud plugin update tke
        ```
        {: pre}

    2. To initialize service instances with the TKE CLI plug-in, set the TKE_PRIVATE_ADDR environment variable to target the TKE private endpoint:

        ```
        export TKE_PRIVATE_ADDR=https://tke.private.<region>.hs-crypto.cloud.ibm.com
        ```
        {: pre}

- Using the VPE for the [{{site.data.keyword.keymanagementserviceshort}} CLI plug-in](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#kp-cli-plugin)

    1. Update the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in to the latest version with the following command:

        ```
        ibmcloud plugin update key-protect -r "IBM Cloud"
        ```
        {: pre}

    2. To perform key management operations with the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in, set the KP_PRIVATE_ADDR environment variable to target the key management service private endpoint:

        ```
        export KP_PRIVATE_ADDR=https://<instance_ID>.api.private.<region>.hs-crypto.appdomain.cloud
        ```
        {: pre}

### Using the VPE with the API
{: #use-vpe-for-hpcs-api}
{: api}

- Using the VPE for the [key management service API](/apidocs/hs-crypto)

    To perform key management operations with the key management service API, use the key management service private endpoints in the API request URL to access the service. For example,

    ```
    curl GET \
      https://<instance_ID>.api.private.<region>.hs-crypto.appdomain.cloud/api/v2/keys   \
      -H 'authorization: Bearer <IAM_token>'   \
      -H 'bluemix-instance: <instance_ID>'   \
      -H 'accept: application/vnd.ibm.kms.key+json'
    ```
    {: codeblock}

- Using the VPE for the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref)

    To perform cryptographic operations with the PKCS #11 API, set the `address` field to the EP11 private endpoint in the configuration file. For more information, see [Set up the PKCS #11 configuration file](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file).

- Using the VPE for the [GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref)

    To perform cryptographic operations with the GREP11 API, specify the server address with the EP11 private endpoint in the code. For more information, see [Generating a GREP11 API request](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api#form-grep11-api-request).

### Using the VPE with Terraform
{: #use-vpe-for-hpcs-terraform}
{: terraform}

To use VPE with Terraform, set the `service_endpoints` parameter to `private-only` in the resource block. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs).

- If you plan to use private endpoints to initialize your service instance, make sure to set the `IBMCLOUD_HPCS_TKE_ENDPOINT` environment variable to target the TKE private endpoint. For example,:

    ```
    export IBMCLOUD_HPCS_TKE_ENDPOINT=https://tke.private.<region>.hs-crypto.cloud.ibm.com
    ```
    {: pre}

- If you plan to use private endpoints to manage your key management service keys, make sure to set the `IBMCLOUD_KP_API_ENDPOINT` environment variable to target the key management service private endpoint. For example,:

    ```
    export IBMCLOUD_KP_API_ENDPOINT=https://<instance_ID>.api.private.<region>.hs-crypto.appdomain.cloud
    ```
    {: pre}
