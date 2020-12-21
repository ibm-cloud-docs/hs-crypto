---

copyright:
  years: 2018, 2020
lastupdated: "2020-12-09"

keywords: ibm cloud hyper protect crypto services, hyper protect crypto services, hpcs, crypto, crypto services, key management, kms, dedicated key management, hsm, hardware security module, cloud hsm, dedicated hsm, keep your own key, kyok, cryptographic operation, key storage, encryption key, cloud encryption, encryption at rest

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:external: target="_blank" .external}
{:term: .term}
{:note: .note}
{:help: data-hd-content-type='help'}
{:support: data-reuse='support'}
{:hide-in-docs: .hide-in-docs}
{:hide-dashboard: .hide-dashboard}

# Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) is a dedicated key management service and [hardware security module (HSM)](#x6704988){: term} based on {{site.data.keyword.cloud_notm}}. This service allows you to take the ownership of the cloud HSM to fully manage your encryption keys and to perform cryptographic operations. {{site.data.keyword.hscrypto}} is also the only service in the cloud industry that is built on FIPS 140-2 Level 4-certified hardware.
{: shortdesc}
{: hide-dashboard}

{{site.data.keyword.hscrypto}} integrates with {{site.data.keyword.keymanagementserviceshort}} application programming interface (API) to generate and manage keys. The Keep Your Own Key (KYOK) function is also enabled to provide access to cloud-based cryptographic HSMs. You can access the network addressable HSMs by making standard PKCS #11 API calls or Enterprise PKCS #11 over gRPC (GREP11) API calls to perform cryptographic operations.
{: hide-dashboard}

<!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.-->

<!--{{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS](https://cloud.ibm.com/docs/hypersecure-dbaas/index.html){: external}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service](https://cloud.ibm.com/docs/containers/container_index.html){: external}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}}](https://cloud.ibm.com/docs/hypersecure-platform/index.html){: external}. -->

This tutorial guides you how to set up your service instance by loading your [master keys](#x2908413){: term}, create and manage encryption keys with the {{site.data.keyword.cloud_notm}} console, and perform cryptographic operations with the PKCS #11 API or with the GREP11 API.
{: hide-dashboard}

<!-- the following is shown on the dashboard-->

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, built on FIPS 140-2 Level 4-certified hardware, allows you to take the ownership of the cloud HSM to fully manage your encryption keys and to perform cryptographic operations. This tutorial guides you how to initialize your service instance by loading your master key, create and manage encryption keys with the {{site.data.keyword.cloud_notm}} console, and perform cryptographic operations with the PKCS #11 API or with the Enterprise PKCS #11 over gRPC (GREP11) API.
{: hide-in-docs}

## Step 1: Initialize your service instance
{: #initialize-crypto-dashboard}
{: hide-in-docs}
{: notoc}

To manage your keys, you need to initialize your service instance first. Two options are provided for initializing a service instance. You can use the {{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities to initialize a service instance by using master key parts stored on smart cards. This provides the highest level of security. You can also use the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in to initialize your service instance.

For detailed steps and best practices of using the Management Utilities, see [Setting up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities). The [video of initializing {{site.data.keyword.hscrypto}} with smart cards](https://www.youtube.com/watch?v=FtRPRzF0dSs&feature=youtu.be){: external} also demonstrates the detailed procedure.

For detailed steps and best practices of using the TKE CLI plug-in, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) and watch the [demonstration video of initializing {{site.data.keyword.hscrypto}} with {{site.data.keyword.cloud_notm}} TKE CLI](https://www.youtube.com/watch?v=_qP2HZ4u5Kg&feature=youtu.be){: external}.

## Step 2: Using the key management service and cloud hardware security module
{: #manage-data-key-dashboard}
{: hide-in-docs}
{: notoc}

### Managing your encryption keys through key management service
{: #manage-keys-dashboard}

From the {{site.data.keyword.cloud_notm}} console, you can create new root keys or standard keys for data encryption, or you can import your existing keys. For more information about root keys and standard keys, see [Key management service components and concepts](/docs/hs-crypto?topic=hs-crypto-understand-concepts#key-management-concepts).

This tutorial walks you through the procedure in the console. If you want to manage encryption keys using the key management API or CLI, check out [the API reference](/apidocs/hs-crypto){: external} and [the CLI reference](/docs/key-protect?topic=key-protect-cli-reference){: external}.
{: note}

#### Creating new keys
{: #create-keys-dashboard}

Complete the following steps to create your first cryptographic key.

1. From the {{site.data.keyword.cloud_notm}} console, click **Manage keys** &gt; **Add key**.
2. To create a new key, select **Create a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can seletct <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#root-key-concept">Root key</a> or <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept">Standard key</a>.</td>
      </tr>
      <tr>
        <td>Key name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Description of the settings to create a key</caption>
    </table>

3. When you finish filling out the key's details, click **Add key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-CBC algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified HSMs that are located in secure {{site.data.keyword.cloud_notm}} data centers.

#### Importing your own keys
{: #import-keys-dashboard}

You can bring your existing keys to the service, so that you can still use the same encryption keys to protect your applications or data.

Complete the following steps to add an existing key.

1. From the {{site.data.keyword.cloud_notm}} console, click **Manage keys** &gt; **Add key**.
2. To upload an existing key, select **Import a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can seletct <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#root-key-concept">Root key</a> or <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept">Standard key</a>.</td>
      </tr>
      <tr>
        <td>Key name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>The key material, such as a symmetric key, that you want to store in the {{site.data.keyword.hscrypto}} service. The key that you provide must be base64 encoded.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 2. Description of the settings to import your own key</caption>
    </table>

3. When you finish filling out the key's details, click **Import key** to confirm.

From the {{site.data.keyword.cloud_notm}} console, you can inspect the general characteristics of your new keys.

### Encrypting your data with cloud HSM
{: #encrypt-data-hsm-dashboard}

You can remotely access {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations with the PKCS #11 API or with the GREP11 API.

#### Performing cryptographic operations with the PKCS #11 API
{: #cryptographic-operations-with-pkcs11-dashboard}

To perform cryptographic operations with the PKCS #11 API, complete the following steps:

1. Follow the [Best practices for setting up PKCS #11 user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access) to create different service ID API keys for the various PKCS #11 user types.
2. [Download the latest PKCS #11 library](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external} and move it into a folder that is accessible by your applications. For example, if you are running your application on Linux, you can move the library to `/usr/local/lib`, `/usr/local/lib64` or `/usr/lib`.
3. Create a configuration file named `grep11client.yaml` based on the [template](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file) and move the configuration file into the same folder as the PKCS #11 library. Optionally, the PKCS #11 library can be placed in the `/etc/ep11client` directory. Create the `/etc/ep11client` directory if it does not already exist.
4. Depending on features and security requirements of your application, pass different service ID API keys that you previously create to allow your applications to perform the corresponding cryptographic operations.

For detailed instructions, see [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api).

#### Performing cryptographic operations with the GREP11 API
{: #cryptographic-operations-with-grep11-dashboard}

To perform cryptographic operations with the GREP11 API, you need to make sure your applications are developed with programming languages supported by [gRPC](https://grpc.io/docs/languages/){:external}. A [sample Github repository](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){:external} is provided for you to test the GREP11 API in Golang and JavaScript. The following procedure takes the Golang code as an example to test GREP11 functions.

Before you use the samples, perform the following tasks:

1. Set up the Go environment:

  - [Install Go tools](https://golang.org/doc/install){:external}.
  - [Set up your workspace directory](https://golang.org/doc/code.html#Workspaces){:external}.
  - [Set the GOPATH environment variable](https://golang.org/doc/code.html#GOPATH){:external}.

2. Clone the [sample repository](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){:external} to the `$GOPATH/src/github.com/ibm-developer/` directory.

To run the sample code, perform the following steps:

1. Update the following code snippet in the `server_test.go` file of the `src/github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/golang/examples` directory:

  ```Golang
  const address = "ep11.<region>.hs-crypto.cloud.ibm.com:<port>"

  var callOpts = []grpc.DialOption{
    grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{})),
    grpc.WithPerRPCCredentials(&util.IAMPerRPCCredentials{
      APIKey:   "<service_ID_API_key>",
      Endpoint: "https://iam.cloud.ibm.com",
      Instance: "<instance_ID>",
    }),
  }
  ```
  {: codeblock}

  In the code example,
  - Replace `<region>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance console, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**.
  - Replace `<service_ID_API_key>` with the service ID API key that is created. The service ID API Key can be created by following the instruction in [Managing service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.
  - Replace `<instance_ID>` with the instance ID that uniquely identified your service instance. Retrieve the instance ID that uniquely identifies your {{site.data.keyword.hscrypto}} service instance by following the instruction in [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

2. Change the directory with the following command:

  ```
  cd $GOPATH/src/github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/golang/examples
  ```
  {: pre}

3. Execute the example by running the `go test -v` command.

  The sample program generates output similar to the following one:

  ```Bash
	=== RUN   Example_getMechanismInfo
	--- PASS: Example_getMechanismInfo (0.02s)
	=== RUN   Example_encryptAndDecrypt
	--- PASS: Example_encryptAndDecrypt (0.03s)
	=== RUN   Example_digest
	--- PASS: Example_digest (0.02s)
	=== RUN   Example_signAndVerifyUsingRSAKeyPair
	--- PASS: Example_signAndVerifyUsingRSAKeyPair (0.66s)
	=== RUN   Example_signAndVerifyUsingECDSAKeyPair
	--- PASS: Example_signAndVerifyUsingECDSAKeyPair (0.04s)
	=== RUN   Example_signAndVerifyToTestErrorHandling
	--- PASS: Example_signAndVerifyToTestErrorHandling (0.04s)
	=== RUN   Example_wrapAndUnwrapKey
	--- PASS: Example_wrapAndUnwrapKey (0.65s)
	=== RUN   Example_deriveKey
	--- PASS: Example_deriveKey (0.11s)
	=== RUN   Example_tls
	--- PASS: Example_tls (0.05s)
	PASS
  ok  	github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/golang/examples	1.667s
  ```

## (Optional) Step 3: Create a {{site.data.keyword.hscrypto}} VPE gateway for VPC
{: #get-started-vpe-gateway-dashboard}
{: hide-in-docs}
{: notoc}

If you have an [{{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance](/docs/vpc?topic=vpc-getting-started), you can connect the VPC instance to your {{site.data.keyword.hscrypto}} instance through [a virtual private endpoint (VPE) gateway](/docs/vpc?topic=vpc-about-vpe), so that you can manage your keys using {{site.data.keyword.hscrypto}} through a private network.

Follow these steps:

1. [Provision a generation 2 VPC instance](/docs/vpc?topic=vpc-getting-started).
2. [Enable a private endpoint for your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-secure-connection).
3. [Create a {{site.data.keyword.hscrypto}} VPE gateway for your VPC instance](/docs/vpc?topic=vpc-ordering-endpoint-gateway).

<!-- The following is shown in docs app-->

## Before you begin
{: #get-started-prerequisites}
{: hide-dashboard}

In order to use {{site.data.keyword.hscrypto}}, make sure that you have a [Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account](/docs/account?topic=account-accounts).

1. To check your account type, go to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/login){: external} and click **Management** > **Account** > **Account settings**.
2. If you have a Lite account and want to use {{site.data.keyword.hscrypto}}, [upgrade your account to a Pay-As-You-Go or Subscription account](/docs/account?topic=account-upgrading-account). You can also [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) if you have one.

## Step 1: Provision the service
{: #provision-service}
{: help}
{: support}
{: hide-dashboard}

You must first create an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console. For detailed steps, see [Provisioning the service](/docs/hs-crypto?topic=hs-crypto-provision).

## Step 2: Initialize your service instance
{: #initialize-crypto}
{: help}
{: support}
{: hide-dashboard}

To manage your keys, you need to initialize your service instance first. Two options are provided for initializing a service instance. You can use the {{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities to initialize a service instance by using master key parts stored on smart cards. This provides the highest level of security. You can also use the {{site.data.keyword.cloud_notm}} Trusted Key Entry (TKE) command-line interface (CLI) plug-in to initialize your service instance.

For detailed steps and best practices of using the Management Utilities, see [Setting up the Management Utilities](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities) and [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities). The [video of initializing {{site.data.keyword.hscrypto}} with smart cards](https://www.youtube.com/watch?v=FtRPRzF0dSs&feature=youtu.be){: external} also demonstrates the detailed procedure.

For detailed steps and best practices of using the TKE CLI plug-in, see [Initializing service instances with the {{site.data.keyword.cloud_notm}} TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm) and watch the [demonstration video of initializing {{site.data.keyword.hscrypto}} with {{site.data.keyword.cloud_notm}} TKE CLI](https://www.youtube.com/watch?v=_qP2HZ4u5Kg&feature=youtu.be){: external}.

## Step 3: Manage your data and keys
{: #manage-data-key}
{: hide-dashboard}

### Manage your encryption keys through key management service
{: #manage-keys}

From the {{site.data.keyword.cloud_notm}} console, you can create new [root keys](#x6946961){: term} or standard keys for data encryption, or you can import your existing keys. For more information about root keys and standard keys, see [Key management service components and concepts](/docs/hs-crypto?topic=hs-crypto-understand-concepts#key-management-concepts).

This tutorial walks you through the procedure in the console. If you want to manage encryption keys using the key management API or CLI, check out [the API reference](/apidocs/hs-crypto){: external} and [the CLI reference](/docs/key-protect?topic=key-protect-cli-reference){: external}.
{: note}

#### Creating new keys
{: #create-keys}
{: help}
{: support}

Complete the following steps to create your first cryptographic key.

1. From the {{site.data.keyword.cloud_notm}} console, click **Manage keys** &gt; **Add key**.
2. To create a new key, select **Create a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can seletct <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#root-key-concept">Root key</a> or <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept">Standard key</a>.</td>
      </tr>
      <tr>
        <td>Key name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Table 1. Description of the settings to create a key</caption>
    </table>

3. When you finish filling out the key's details, click **Add key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-CBC algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified HSMs that are located in secure {{site.data.keyword.cloud_notm}} data centers.

#### Importing your own keys
{: #import-keys}
{: help}
{: support}

You can bring your existing keys to the service, so that you can still use the same encryption keys to protect your applications or data.

Complete the following steps to add an existing key.

1. From the {{site.data.keyword.cloud_notm}} console, click **Manage keys** &gt; **Add key**.
2. To upload an existing key, select **Import a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can seletct <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#root-key-concept">Root key</a> or <a href="/docs/hs-crypto?topic=hs-crypto-understand-concepts#standard-key-concept">Standard key</a>.</td>
      </tr>
      <tr>
        <td>Key name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>The key material, such as a symmetric key, that you want to store in the {{site.data.keyword.hscrypto}} service. The key that you provide must be base64 encoded.</td>
      </tr>
      <caption style="caption-side:bottom;">Table 2. Description of the settings to import your own key</caption>
    </table>

3. When you finish filling out the key's details, click **Import key** to confirm.

From the {{site.data.keyword.cloud_notm}} console, you can inspect the general characteristics of your new keys.

### Encrypt your data with cloud HSM
{: #encrypt-data-hsm}
{: help}
{: support}

You can remotely access {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations with the PKCS #11 API or with the GREP11 API.

#### Performing cryptographic operations with the PKCS #11 API
{: #cryptographic-operations-with-pkcs11}

To perform cryptographic operations with the PKCS #11 API, complete the following steps:

1. Follow the [Best practices for setting up PKCS #11 user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access) to create different service ID API keys for the various PKCS #11 user types.
2. [Download the latest PKCS #11 library](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external} and move it into a folder that is accessible by your applications. For example, if you are running your application on Linux, you can move the library to `/usr/local/lib`, `/usr/local/lib64` or `/usr/lib`.
3. Create a configuration file named `grep11client.yaml` based on the [template](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file) and move the configuration file into the same folder as the PKCS #11 library. Optionally, the PKCS #11 library can be placed in the `/etc/ep11client` directory. Create the `/etc/ep11client` directory if it does not already exist.
4. Depending on features and security requirements of your application, pass different service ID API keys that you previously create to allow your applications to perform the corresponding cryptographic operations.

For detailed instructions, see [Performing cryptographic operations with the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api).

#### Performing cryptographic operations with the GREP11 API
{: #cryptographic-operations-with-grep11}

To perform cryptographic operations with the GREP11 API, you need to make sure your applications are developed with programming languages supported by [gRPC](https://grpc.io/docs/languages/){:external}. A [sample Github repository](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){:external} is provided for you to test the GREP11 API in Golang and JavaScript. The following procedure takes the Golang code as an example to test GREP11 functions.

Before you use the samples, perform the following tasks:

1. Set up the Go environment:

  - [Install Go tools](https://golang.org/doc/install){:external}.
  - [Set up your workspace directory](https://golang.org/doc/code.html#Workspaces){:external}.
  - [Set the GOPATH environment variable](https://golang.org/doc/code.html#GOPATH){:external}.

2. Clone the [sample repository](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){:external} to the `$GOPATH/src/github.com/ibm-developer/` directory.

To run the sample code, perform the following steps:

1. Update the following code snippet in the `server_test.go` file of the `src/github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/golang/examples` directory:

  ```Golang
  const address = "ep11.<region>.hs-crypto.cloud.ibm.com:<port>"

  var callOpts = []grpc.DialOption{
    grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{})),
    grpc.WithPerRPCCredentials(&util.IAMPerRPCCredentials{
      APIKey:   "<service_ID_API_key>",
      Endpoint: "https://iam.cloud.ibm.com",
      Instance: "<instance_ID>",
    }),
  }
  ```
  {: codeblock}

  In the code example,
  - Replace `<region>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance dashboard, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**.
  - Replace `<service_ID_API_key>` with the service ID API key that is created. The service ID API Key can be created by following the instruction in [Managing service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.
  - Replace `<instance_ID>` with the instance ID that uniquely identified your service instance. Retrieve the instance ID that uniquely identifies your {{site.data.keyword.hscrypto}} service instance by following the instruction in [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

2. Change the directory with the following command:

  ```
  cd $GOPATH/src/github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/golang/examples
  ```
  {: pre}

3. Execute the example by running the `go test -v` command.

  The sample program generates output similar to the following one:

  ```Bash
	=== RUN   Example_getMechanismInfo
	--- PASS: Example_getMechanismInfo (0.02s)
	=== RUN   Example_encryptAndDecrypt
	--- PASS: Example_encryptAndDecrypt (0.03s)
	=== RUN   Example_digest
	--- PASS: Example_digest (0.02s)
	=== RUN   Example_signAndVerifyUsingRSAKeyPair
	--- PASS: Example_signAndVerifyUsingRSAKeyPair (0.66s)
	=== RUN   Example_signAndVerifyUsingECDSAKeyPair
	--- PASS: Example_signAndVerifyUsingECDSAKeyPair (0.04s)
	=== RUN   Example_signAndVerifyToTestErrorHandling
	--- PASS: Example_signAndVerifyToTestErrorHandling (0.04s)
	=== RUN   Example_wrapAndUnwrapKey
	--- PASS: Example_wrapAndUnwrapKey (0.65s)
	=== RUN   Example_deriveKey
	--- PASS: Example_deriveKey (0.11s)
	=== RUN   Example_tls
	--- PASS: Example_tls (0.05s)
	PASS
  ok  	github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/golang/examples	1.667s
  ```

## (Optional) Step 4: Create a {{site.data.keyword.hscrypto}} VPE gateway for VPC
{: #get-started-vpe-gateway}
{: hide-dashboard}

If you have an [{{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC) instance](/docs/vpc?topic=vpc-getting-started), you can connect the VPC instance to your {{site.data.keyword.hscrypto}} instance through [a virtual private endpoint (VPE) gateway](/docs/vpc?topic=vpc-about-vpe), so that you can manage your keys using {{site.data.keyword.hscrypto}} through a private network.

Follow these steps:

1. [Provision a generation 2 VPC instance](/docs/vpc?topic=vpc-getting-started).
2. [Enable a private endpoint for your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-secure-connection).
3. [Create a {{site.data.keyword.hscrypto}} VPE gateway for your VPC instance](/docs/vpc?topic=vpc-ordering-endpoint-gateway).

## What's next
{: #get-started-next}

- {{site.data.keyword.hscrypto}} helps you meet compliance requirements and ensures the security of your data. Check out the [compliance standards and criteria](/docs/hs-crypto?topic=hs-crypto-security-and-compliance) {{site.data.keyword.hscrypto}} has been certified.
- {{site.data.keyword.hscrypto}} provides advanced encryption to your at-rest data with envelope encryption, check out [Protecting your data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to see how it works.
- You can use {{site.data.keyword.hscrypto}} as the root key provider for other services such as {{site.data.keyword.cos_full_notm}} to bring your own encryption to your applications or data. Check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services) for the full list of supported services.
- To learn more about {{site.data.keyword.hscrypto}} concepts and terminologies, check out [Components and concepts](/docs/hs-crypto?topic=hs-crypto-understand-concepts).
- Manage your keys with [{{site.data.keyword.hscrypto}} key management API](/apidocs/hs-crypto){: external} and [{{site.data.keyword.keymanagementserviceshort}} CLI](/docs/key-protect?topic=key-protect-cli-reference){: external}. Encrypt your data and perform cryptographic operations with the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) or the [GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).

<br>
<p class="hide-dashboard" style="background-color: #e0e0e0; border: 1px solid #161616; padding: 10px; font-weight: bold">
<img src="/image/survey.svg" alt="survey" style="vertical-align:middle"> Let us know your feedback by taking a <a href="https://surveys.hotjar.com/587f4609-7eeb-48cb-85dc-95f81906513b" target="_blank">one-minute survey</a>.
</p>

<!-- ## Installing ACSP client libraries -->

<!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client. Complete the following steps to install the ACSP client libraries in your local environment. -->

<!-- 1. Download the installation package from the [GitHub repository](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){: external}. In the **packages** folder, choose the installation package file that is suitable for your operation system and CPU architecture. For example, for Ubuntu on x86, choose `acsp-pkcs11-client_1.5-3.5_amd64.deb`.
2. Install the package to install the ACSP client libraries with the `dpkg` command. For example, `dpkg -i acsp-pkcs11-client_1.5-3.5_amd64.deb`. -->

<!-- ## Configuring ACSP client -->

<!-- At the current stage, {{site.data.keyword.hscrypto}} provides only self-signed certificates.

You need to configure the ACSP client to enable a proper secure communication channel (mutual TLS) to your service instance in the cloud. -->

<!-- 1. In your {{site.data.keyword.hscrypto}} service instance in {{site.data.keyword.cloud_notm}}, select **Manage** from the left navigator.
2. On the "Manage" screen, click the **Download Config** button to download the `acsp_client_credentials.uue` file.
3. Copy the `acsp_client_credentials.uue` file to the `/opt/ibm/acsp-pkcs11-client/config` directory in your local environment.
4. In the `/opt/ibm/acsp-pkcs11-client/config` directory, decode the file with the following command:
       `base64 --decode acsp_client_credentials.uue > acsp_client_credentials.tar`
5. Extract the client credentials file with the following command:
       `tar xf acsp_client_credentials.tar`
6. Move the `server-config` files into the default place with the following command:
       `mv server-config/* ./`
7. Rename the client credentials file with the following command:
       `mv acsp.properties.client acsp.properties`
8. (Optional:) Change group ID of the files with the following command:
       `chown root.pkcs11 *`
9. Enable ACSP to use the proper config for the service instance in the cloud:
       `export ACSP_P11=/opt/ibm/acsp-pkcs11-client/config/acsp.properties` -->

<!-- Now your ACSP client is operational and your {{site.data.keyword.hscrypto}} is ready to use!

For more information about ACSP client installation and configuration, see [ACSP Client Installation and Configuration Guide](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/blob/master/doc/ACSP-client-config-guide.pdf){: external}. -->
