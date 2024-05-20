---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-20"

keywords: securing connection, disabling public service endpoint

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Using service endpoints to privately connect to {{site.data.keyword.hscrypto}}
{: #secure-connection}

To ensure that you have enhanced control and security over your data when you use {{site.data.keyword.hscrypto}}, you have the option of using private routes to {{site.data.keyword.cloud}} service endpoints. Private routes are not accessible or reachable over the internet. By using the {{site.data.keyword.cloud_notm}} private service endpoints feature, you can protect your data from threats from the public network and logically extend your private network.
{: shortdesc}

## Understanding the network access policy
{: #understand-network-access-policies}

A network access policy for {{site.data.keyword.hscrypto}}
instances is an extra policy that customers can use to block a
{{site.data.keyword.hscrypto}} instance from getting API
requests from public or private networks.

The network access policy applies to newly provisioned and existing instances.
For existing instances the network access policy is enforced after it is set.
{: important}

Two options control network access to
{{site.data.keyword.hscrypto}} instances:

- Public and private network access - this is the default
- Private network access only

### Public and private network access
{: #public-and-private}

The {{site.data.keyword.hscrypto}} instance accepts API
requests from both `public and private` endpoints.

Public and private network access is the default setting and is used if a policy
is not set.

For example, multiple teams are testing a solution that uses
{{site.data.keyword.hscrypto}} instances. Development and test
teams issue API requests from both outside (public endpoints) and inside
(private endpoints) the {{site.data.keyword.cloud_notm}}. You allow public and private API requests to
ensure each team has access to {{site.data.keyword.hscrypto}}
instances during this phase of the project.

### Private network access only
{: #private-only}

The {{site.data.keyword.hscrypto}} instance accepts API
requests from only private endpoints.

For example, development and testing are complete and the solution that uses
{{site.data.keyword.hscrypto}} instances is in production. You
want to limit API requests to private networks for security reasons. All
{{site.data.keyword.hscrypto}} API requests must originate from
within the {{site.data.keyword.cloud_notm}}.

After the network access policy is set to `private-only`, you cannot make any
{{site.data.keyword.hscrypto}} API calls from the public
network, including the API to change the policy. Make sure that the private
environment is set up before setting the network access policy to
`private-only`.
{: note}

There are several ways for you to update the network settings. However, before you update the network access policy, you need to initialize the service instance first. See [Initializing service instances with the IBM Cloud TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) for instructions.

* When you [provision a service instance](/docs/hs-crypto?topic=hs-crypto-provision), you can choose between the `private-only` and `public-and-private` options using either the UI or CLI.
* [Manage and update the network settings](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies) after you provision and initialize the service instance.

    After you enable a private-only network, you are not able to perform further key management actions in the UI. Use either the CLI or API to switch between a private-only network and a public-and-private network instead.

The instance access policy, which controls access to the instance from either
public or private IP addresses, is not enforced after the `ibmcloud resource service-instance-delete (NAME | ID)` command to
delete the instance is issued.

After you enable the following network settings, both the key management operations using key management service API and the cryptographic operations using GREP11 and PKCS #11 APIs are affected.
{: important}

## Before you begin
{: #private-endpoint-prereqs}

1. Ensure that your {{site.data.keyword.cloud_notm}} infrastructure account is enabled for [virtual routing and forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf).

    When you enable VRF, a separate routing table is created for your account, and connections to and from your account's resources are routed separately on the {{site.data.keyword.cloud_notm}} network. To learn more about VRF technology, see [Virtual routing and forwarding on {{site.data.keyword.cloud_notm}}](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud).

    Enabling VRF permanently alters networking for your account. Be sure that you understand the impact to your account and resources. After you enable VRF, it cannot be disabled.
    {: important}
    
2. Ensure that your {{site.data.keyword.cloud_notm}} infrastructure account is enabled for [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).

    When you enable service endpoints, you can connect to {{site.data.keyword.hscrypto}} by using a private IP that is accessible only through the private network of {{site.data.keyword.cloud_notm}}. To find out more, see [Service endpoints for private connections](/docs/account?topic=account-service-endpoints-overview).

    After you enable service endpoints for your account, all existing and future {{site.data.keyword.hscrypto}} resources and service instances become available from both the public and private endpoint.
    {: note}

## Step 1: Configure the private network of {{site.data.keyword.cloud_notm}} on your virtual server
{: #configure-network}

Prepare your VSI or test machine by configuring your routing table for the private network of {{site.data.keyword.cloud_notm}}.

1. To route traffic to the private network of {{site.data.keyword.cloud_notm}}, run the following command on your VSI:

    ```sh
    route add -net 166.9.0.0/16 gw <gateway> dev <gateway_interface>
    ```
    {: pre}

    Replace `<gateway>` (for example, `10.x.x.x`) and `<gateway_interface>` (for example, `eth10`) with the appropriate values.

2. Optional: Verify that the route was added successfully by displaying your new routing table.

    ```sh
    route -n
    ```
    {: pre}

## Step 2: Provision a service instance and select the network access
{: #service-endpoint-private-endpoints}

When you [provision a service instance](/docs/hs-crypto?topic=hs-crypto-provision), you can choose between the `private-only` and `public-and-private` options using either the UI or CLI.

You can always [manage and update the network settings](/docs/hs-crypto?topic=hs-crypto-managing-network-access-policies) after you provision and initialize the service instance. Use either the CLI or API to switch between a private-only network and a public-and-private network.
{: tip}

## Step 3:  Target the {{site.data.keyword.hscrypto}} private endpoint for the TKE CLI plug-in
{: #target-tke-private-endpoint}

To perform key management and cryptographic operations thought a private endpoint, you need to first target the private endpoint for the Trusted Key Entry (TKE) CLI plug-in.

1. From the command line, log in to {{site.data.keyword.cloud_notm}}.

    ```sh
    ibmcloud login
    ```
    {: pre}

    If the login fails, run the `ibmcloud login --sso` command to try again. The `--sso` parameter is required when you log in with a federated ID. If this option is used, go to the link listed in the CLI output to generate a one-time passcode.
    {: note}

2. Set the TKE_PRIVATE_ADDR environment variable to target the private endpoint for the Trusted Key Entry (TKE) plug-in. Replace *<region>* with the [short name of the location](/docs/hs-crypto?topic=hs-crypto-regions#available-regions) that your service instance is created in.

    ```
    export TKE_PRIVATE_ADDR=https://tke.private.<region>.hs-crypto.cloud.ibm.com
    ```
    {: pre}

    The TKE_PRIVATE_ADDR environment variable is used to set the API endpoint URL both for public endpoint and private endpoint. If you want to use the public endpoint, unset the TKE_PRIVATE_ADDR environment variable or set the TKE_PRIVATE_ADDR environment variable as the public endpoint URL: `https://tke.<region>.hs-crypto.cloud.ibm.com`.
    {: important}

## Step 4: Initialize the service instance
{: #secure-connection-key-ceremony}

If you select the `private-only` option when you provision the service instance, all subsequent actions are performed in a private network, including [initializing a service instance](/docs/hs-crypto?topic=hs-crypto-introduce-service). You can use either [the key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) or [smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities) to initialize the service instance. If you select the `public-and-private` option, you can initialize the service instance in a public network.

After the service initialization is done, you can still update your network settings by following Managing the network settings.

## Step 5: Target the {{site.data.keyword.hscrypto}} private endpoint for key management service
{: #target-internal-endpoint}

If you are using the key management service of {{site.data.keyword.hscrypto}}, after you configure your VSI to accept the private network traffic of {{site.data.keyword.cloud_notm}}, you can target the private endpoint for {{site.data.keyword.hscrypto}} by using the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in.

If you are using the GREP11 service, the service handles the private endpoint connection. You need to only switch your GREP11 service endpoint to the private endpoint per instructions in [Generating a GREP11 API request](/docs/hs-crypto?topic=hs-crypto-set-up-grep11-api#form-grep11-api-request).
{: note}

1. Optional: Ensure that your account is enabled for VRF and service endpoints.

    ```sh
    ibmcloud account show
    ```
    {: pre}

    The following CLI output shows the account details of a VRF and service endpoint-enabled account.

    ```
    Retrieving account John Doe's Account of john.doe@email.com...
    OK

    Account ID:                   d154dfbd0bc2edefthyufffc9b5ca318
    Currently Targeted Account:   true
    Linked Softlayer Account:     1008967
    Service Endpoint Enabled:     true
    ```
    {: screen}

    See [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint){: external} to learn how to set up your account for connecting to a private network.
    {: tip}

2. Set the environment variable to target the {{site.data.keyword.hscrypto}} private endpoint.

    Use the following commands on the [Linux]{: tag-linux} operating system or [macOS]{: tag-macos} only. For how to set environment variables on the [Windows]{: tag-windows} operating system, see [Accessing {{site.data.keyword.keymanagementserviceshort}} CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli).
    {: note}

    Set the KP_PRIVATE_ADDR environment variable to target the private endpoint for the key management service:

    ```
    export KP_PRIVATE_ADDR=https://api.private.<region>.hs-crypto.cloud.ibm.com:<port>
    ```
    {: pre}

    You can find the Key management private endpoint URL listed in the service dashboard under **Overview** &gt; **Connect** &gt; **Key management private endpoint URL**.

    Alternatively, you can dynamically [retrieve the API endpoint URL](/apidocs/hs-crypto#getinstance){: external}. The returned value includes the following:

    ```
    {
      "instance_id": "<instance_ID>",
      "kms": {
        "public": "api.<region>.hs-crypto.cloud.ibm.com:<port>",
        "private":"api.private.<region>.hs-crypto.cloud.ibm.com:<port>"
        },
        "ep11": {
        "public": "ep11.<region>.hs-crypto.cloud.ibm.com:<port>",
        "private":"ep11.private.<region>.hs-crypto.cloud.ibm.com:<port>"
      }
    }
    ```
    {: screen}

    The private endpoint URL is returned in `private`. For key management endpoint, use the value that is returned in the `kms` section. The KP_PRIVATE_ADDR environment variable is used to set the API endpoint URL both for public endpoint and private endpoint. If you want to use the public endpoint, make sure to set the KP_PRIVATE_ADDR environment variable as the public endpoint URL that is returned in the `public` field in the `kms` section.
    {: important}

## Step 6: Test your private network connection
{: #Test-private-connection}

You might want to test your network connection after you set up your private network.

To test the private network connection for the key management service, use {{site.data.keyword.keymanagementserviceshort}} CLI to perform an action towards the {{site.data.keyword.hscrypto}} service instance. The following example shows how to create a [root key](#x6946961){: term} on the private network.

1. [Create a root key](/docs/hs-crypto?topic=hs-crypto-create-root-keys) by targeting the private endpoint.

    ```sh
    ibmcloud kp create <key_name> -i <instance_ID>
    ```
    {: pre}

    Replace `<key_name>` with a human-readable alias for easy identification of your key. Replace `<instance_ID>` with [the {{site.data.keyword.cloud_notm}} instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID) that identifies your {{site.data.keyword.hscrypto}} service instance.

2. Optional: Verify that the key was created successfully by listing the keys that are available in your {{site.data.keyword.hscrypto}} service instance.

    ```sh
    ibmcloud kp list -i <instance_ID>
    ```
    {: pre}

    Replace `<instance_ID>` with the {{site.data.keyword.cloud_notm}} instance ID that identifies your {{site.data.keyword.hscrypto}} service instance.

## What's next
{: #secure-connection-next}

To perform key management operations, see:

* [The key management service API](/apidocs/hs-crypto){: external}
* [{{site.data.keyword.keymanagementserviceshort}} CLI](/docs/key-protect?topic=key-protect-key-protect-cli-reference)

To perform cryptographic operations, see:

* [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref)
* [GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref)
