---

copyright:
  years: 2018, 2022
lastupdated: "2022-02-24"

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

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} for short) is a dedicated key management service and [hardware security module (HSM)](#x6704988){: term} based on {{site.data.keyword.cloud_notm}}. With this service, you can take the ownership of the cloud HSM to fully manage your encryption keys and to perform cryptographic operations. {{site.data.keyword.hscrypto}} is also the only service in the cloud industry that is built on FIPS 140-2 Level 4-certified hardware.
{: shortdesc}
{: hide-dashboard}

{{site.data.keyword.hscrypto}} integrates with {{site.data.keyword.keymanagementserviceshort}} application programming interface (API) to generate and manage keys. The Keep Your Own Key (KYOK) function is also enabled to provide access to cloud-based cryptographic HSMs. You can access the network addressable HSMs by making standard PKCS #11 API calls or Enterprise PKCS #11 over gRPC (GREP11) API calls to perform cryptographic operations.
{: hide-dashboard}


This tutorial shows you the high-level steps on how to set up your service instance by loading your [master keys](#x2908413){: term}, create and manage encryption keys with the {{site.data.keyword.cloud_notm}} console, and perform cryptographic operations with the PKCS #11 API or with the GREP11 API.
{: hide-dashboard}



With {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} that is built on FIPS 140-2 Level 4-certified hardware, you can take the ownership of the cloud HSM to fully manage your encryption keys and to perform cryptographic operations. 
{: hide-in-docs}

This tutorial guides you on how to initialize your service instance by loading your master key, create and manage encryption keys with the {{site.data.keyword.cloud_notm}} console, and perform cryptographic operations with the PKCS #11 API or with the Enterprise PKCS #11 over gRPC (GREP11) API.
{: hide-in-docs}

## Step 1: Initialize your service instance
{: #initialize-crypto-dashboard}
{: hide-in-docs}
{: notoc}

To manage your keys, you need to initialize your service instance first. Depending on where your service instance locates and your security requirements, {{site.data.keyword.hscrypto}} provides you with the following three approaches to initializing your service instance:

- [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)

    This approach gives you the highest security, which enables you to store and manage master key parts using smart cards.

- [Initializing service instances using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)

    If you create your service instance in Dallas (`us-south`) or Washington DC (`us-east`) where the recovery crypto units are enabled, you can choose this approach where the master key is randomly generated within a recovery crypto unit and then exported to other crypto units.

- [Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)

    You can also initialize your service instance using master key parts that are stored in files on your local workstation. You can use this approach regardless of whether or not your service instance includes recovery crypto units. 

## Step 2: Manage your encryption keys with the key management service 
{: #manage-data-key-dashboard}
{: hide-in-docs}
{: notoc}

Follow these steps to manage your encryption keys if you are using {{site.data.keyword.hscrypto}} Standard Plan.

From the {{site.data.keyword.cloud_notm}} console, you can create new root keys or standard keys for data encryption, or you can import your existing keys.

### Creating new keys
{: #create-keys-dashboard}

Complete the following steps to create your first cryptographic key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To create a new key, select **Create a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select <strong>Root key</strong> or <strong>Standard key</strong>.</td>
      </tr>
      <tr>
        <td>Key name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <caption>Table 1. Description of the settings to create a key.</caption>
    </table>

3. When you finish filling out the key's details, click **Add key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-CBC algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified HSMs that are located in secure {{site.data.keyword.cloud_notm}} data centers.

### Importing your own keys
{: #import-keys-dashboard}

You can bring your existing keys to the service, so that you can still use the same encryption keys to protect your applications or data.

Complete the following steps to add an existing key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To upload an existing key, select **Import a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select <strong>Root key</strong> or <strong>Standard key</strong>.</td>
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
      <caption>Table 2. Description of the settings to import your own key.</caption>
    </table>

3. When you finish filling out the key's details, click **Import key** to confirm.

From the {{site.data.keyword.cloud_notm}} console, you can inspect the general characteristics of your new keys.

## Step 3: Encrypte your data with cloud HSM
{: #encrypt-data-hsm-dashboard}
{: hide-in-docs}
{: notoc}

You can remotely access {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations with the PKCS #11 API or with the GREP11 API.

### Performing cryptographic operations with the PKCS #11 API
{: #cryptographic-operations-with-pkcs11-dashboard}

To perform cryptographic operations with the PKCS #11 API, complete the following steps:

1. Generate an API key for accessing your {{site.data.keyword.hscrypto}} instance. Run the following command to create an API key for your {{site.data.keyword.cloud_notm}} account, and save the value of the API key for subsequent steps:

    ```
    ibmcloud iam api-key-create apikeyhpcs -d "API key for {{site.data.keyword.hscrypto}} PKCS11"
    ```
    {: codeblock}

2. Create a configuration file for the {{site.data.keyword.hscrypto}} PKCS #11 feature. The configuration file is named `grep11client.yaml`.

    Adapt the following file template and name the file `grep11client.yaml`:

    - Replace `<instance_id>` with the ID of your {{site.data.keyword.hscrypto}} instance.
    - Replace `<EP11_endpoint_URL>` and `<EP11_endpoint_port_number>` with the respective parameters of the EP11 endpoint address of your {{site.data.keyword.hscrypto}} instance.
    - Replace `<your_api_key>` with the value of the API key that you created previously.

    ```yaml
    iamcredentialtemplate: &defaultiamcredential
              enabled: true
              endpoint: "https://iam.cloud.ibm.com"
              # Keep the 'apikey' empty. It will be overridden by the Anonymous user API key configured later.
              apikey:
              # The Universally Unique IDentifier (UUID) of your Hyper Protect Crypto Services instance.
              instance: "<instance_id>"

    tokens:
      0:
        grep11connection:
          # The EP11 endpoint address starting from 'ep11'. For example: "ep11.us-south.hs-crypto.cloud.ibm.com"
          address: "<EP11_endpoint_URL>"
          port: "<EP11_endpoint_port_number>" # The EP11 endpoint port number
          tls:
            enabled: true # EP11 requires TLS connection.
            # Set it 'true' if you want to enable mutual TLS connections.
            # By default, set it 'false' because EP11 requires server-only authentication.
            mutual: <enable_mtls>
            # 'cacert' is a full-path certificate file. In Linux with the 'ca-ca-certificates' package installed, this is normally not needed.
            cacert:
            # Specify the file path of the client certificate if you enable mutual TLS. Otherwise, keep it empty.
            certfile: <client_certificate>
            # Specify the file path of the client certificate private key if you enable mutual TLS. Otherwise, keep it empty.
            keyfile: <client_certificate_private_key>
        storage:
            # 'remotestore' needs to be enabled if you want to generate keys with the attribute CKA_TOKEN.
          remotestore:
            enabled: true
        users:
          0: # The index of the Security Officer (SO) user MUST be 0.
            # The name for the Security Officer (SO) user. For example: "Administrator".
            name: "<SO_user_name>"
            # NEVER put the API key under the SO user for security reasons.
            iamauth:
              <<: *defaultiamcredential
          1: # The index of the normal user MUST be 1.
            # The name for the normal user. For example: "Normal user".
            name: "<normal_user_name>"
            # The 128-bit UUID of the private keystore. For example: "f00db2f1-4421-4032-a505-465bedfa845b".
            tokenspaceID: "<private_keystore_spaceid>"
            # NEVER put the API key under the normal user for security reasons.
            iamauth:
              <<: *defaultiamcredential
            sessionauth:
              enabled: true # Enable this option to encrypt and authenticate the keystore.
              # Authenticated keystore password; must be 6-8 characters in length
              tokenspaceIDPassword: "<private_keystore_password>"
          2: # The index of the anonymous user MUST be 2.
            # The name for the anonymous user. For example: "Anonymous".
            name: "<anonymous_user_name>"
            # The 128-bit UUID of the public keystore. For example: "ca22be26-b798-4fdf-8c83-3e3a492dc215".
            tokenspaceID: "<public_keystore_spaceid>"
            iamauth:
              <<: *defaultiamcredential
              # The API key for the anonymous user. It will overide the 'apikey' in the previous defaultcredentials.iamauth.apikey field
              apikey: "<apikey_for_anonymous_user>"
            sessionauth:
              enabled: false
              tokenspaceIDPassword: # Authenticated keystore password; must be 6-8 characters in length
    logging:
      # Set the logging level.
      # The supported levels, in an increasing order of verboseness: 'panic', 'fatal', 'error', 'warning'/'warn', 'info', 'debug', 'trace'. The Default value is 'warning'.
      loglevel: "<logging_level>"
      logpath: "<log_file_path>" # The full path of your logging file.

    ```
    {: codeblock}

3. Download and install the latest PKCS #11 library through [the GitHub repository](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external} and move it into a folder that is accessible by your applications. For example, if you are running your application on Linux, you can move the library to `/usr/local/lib`, `/usr/local/lib64` or `/usr/lib`.

4. Pass the API key that you previously create to allow your applications to perform the cryptographic operations.

### Performing cryptographic operations with the GREP11 API
{: #cryptographic-operations-with-grep11-dashboard}

To perform cryptographic operations with the GREP11 API, you need to make sure your applications are developed with programming languages supported by gRPC.

The following procedure uses Golang code as an example to test GREP11 functions.

1. Install Golang by following [the instruction](https://golang.org/doc/install){: external}.
2. Clone the [sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external} into a local directory of your choice. Go modules are used for this repository, so you don't need to place the cloned repository in your `GOPATH`. Refer to the repository's README file for more information about the GREP11 Go code examples.
3. Update the following code snippet in the `examples/server_test.go` file.

    ```Golang
    var (
        Address        = "<grep11_server_address>:<port>"
        APIKey         = "<ibm_cloud_apikey>"
        HPCSInstanceID = "<hpcs_instance_id>"
    )
    ```
    {: codeblock}

    In the code example,
    - Replace `<grep11_server_address>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance console, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**.
    - Replace `<ibm_cloud_apikey>` with the service ID API key that you created. The service ID API Key can be created by following the instruction in [Managing service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.
    - Replace `<instance_ID>` with the instance ID that uniquely identifies your service instance. Retrieve the instance ID by following the instruction in [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

4. From the `<your_repository_path>/hpcs-grep11-go/examples` directory, execute the examples by running the `go test -v -run Example` command.

    The sample program produces output similar to the following:

    ```
    === RUN   Example_getMechanismInfo
    --- PASS: Example_getMechanismInfo (0.11s)
    === RUN   Example_generateGenericKey
    --- PASS: Example_generateGenericKey (0.09s)
    === RUN   Example_encryptAndDecryptUsingAES
    --- PASS: Example_encryptAndDecryptUsingAES (0.28s)
    === RUN   Example_digest
    --- PASS: Example_digest (0.18s)
    === RUN   Example_signAndVerifyUsingRSAKeyPair
    --- PASS: Example_signAndVerifyUsingRSAKeyPair (0.21s)
    === RUN   Example_signAndVerifyUsingDSAKeyPair
    --- PASS: Example_signAndVerifyUsingDSAKeyPair (0.99s)
    === RUN   Example_deriveKeyUsingDHKeyPair
    --- PASS: Example_deriveKeyUsingDHKeyPair (0.64s)
    === RUN   Example_signAndVerifyUsingECDSAKeyPair
    --- PASS: Example_signAndVerifyUsingECDSAKeyPair (0.16s)
    === RUN   Example_signAndVerifyToTestErrorHandling
    --- PASS: Example_signAndVerifyToTestErrorHandling (0.16s)
    === RUN   Example_wrapAndUnwrapKey
    --- PASS: Example_wrapAndUnwrapKey (0.20s)
    === RUN   Example_deriveKey
    --- PASS: Example_deriveKey (0.22s)
    === RUN   Example_tls
    --- PASS: Example_tls (0.14s)
    PASS
    ok      github.com/IBM-Cloud/hpcs-grep11-go/examples    13.106s
    ```
    {: screen}





## Before you begin
{: #get-started-prerequisites}
{: hide-dashboard}

In order to use {{site.data.keyword.hscrypto}}, make sure that you have a Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account. For details about the {{site.data.keyword.cloud_notm}} account types, see [Account types](/docs/account?topic=account-accounts).

1. To check your account type, go to [{{site.data.keyword.Bluemix_notm}}](https://cloud.ibm.com/login){: external} and click **Management** > **Account** > **Account settings**.
2. If you have a Lite account and want to use {{site.data.keyword.hscrypto}}, [upgrade your account](/docs/account?topic=account-upgrading-account) to a Pay-As-You-Go or Subscription account. You can also [apply your promo code](/docs/billing-usage?topic=billing-usage-applying-promo-codes) if you have one.

## Step 1: Provision the service
{: #provision-service}
{: hide-dashboard}

You must first create an instance of {{site.data.keyword.hscrypto}} from the {{site.data.keyword.cloud_notm}} console. 



For detailed steps, see [Provisioning the service](/docs/hs-crypto?topic=hs-crypto-provision).

## Step 2: Initialize your service instance
{: #initialize-crypto}
{: hide-dashboard}
{: help}
{: support}

To manage your keys, you need to initialize your service instance first. Depending on where your service instance locates and your security requirements, {{site.data.keyword.hscrypto}} provides you with the following three approaches to initializing your service instance:

- [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities)

    This approach gives you the highest security, which enables you to store and manage master key parts using smart cards.

- [Initializing service instances using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-recovery-crypto-unit)

    If you create your service instance in Dallas (`us-south`) or Washington DC (`us-east`) where the recovery crypto units are enabled, you can choose this approach where the master key is randomly generated within a recovery crypto unit and then exported to other crypto units.

- [Initializing service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)

    You can also initialize your service instance using master key parts that are stored in files on your local workstation. You can use this approach regardless of whether or not your service instance includes recovery crypto units. 

## Step 3: Manage your encryption keys with the key management service
{: #manage-data-key}
{: hide-dashboard}

Follow these steps to manage your encryption keys if you are using {{site.data.keyword.hscrypto}} Standard Plan.

### Creating new keys
{: #create-keys}
{: help}
{: support}

Complete the following steps to create your first cryptographic key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To create a new key, select **Create a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select <strong>Root key</strong> or <strong>Standard key</strong>.</td>
      </tr>
      <tr>
        <td>Key name</td>
        <td>
          <p>A unique, human-readable alias for easy identification of your key.</p>
          <p>To protect your privacy, ensure that the key name doesn't contain personally identifiable information (PII), such as your name or location.</p>
        </td>
      </tr>
      <caption>Table 1. Description of the settings to create a key.</caption>
    </table>

3. When you finish filling out the key's details, click **Add key** to confirm.

Keys that are created in the service are symmetric 256-bit keys, supported by the AES-CBC algorithm. For added security, keys are generated by FIPS 140-2 Level 4 certified HSMs that are located in secure {{site.data.keyword.cloud_notm}} data centers.

### Importing your own keys
{: #import-keys}
{: help}
{: support}

You can bring your existing keys to the service, so that you can still use the same encryption keys to protect your applications or data.

Complete the following steps to add an existing key.

1. From the {{site.data.keyword.cloud_notm}} console, click **KMS keys** &gt; **Add key**.
2. To upload an existing key, select **Import a key**.

    Specify the key's details:

    <table>
      <tr>
        <th>Setting</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Key type</td>
        <td>The type of key that you would like to manage in {{site.data.keyword.hscrypto}}. You can select <strong>Root key</strong> or <strong>Standard key</strong>.</td>
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
      <caption>Table 2. Description of the settings to import your own key.</caption>
    </table>

3. When you finish filling out the key's details, click **Import key** to confirm.

From the {{site.data.keyword.cloud_notm}} console, you can inspect the general characteristics of your new keys.

## Step 4: Encrypte your data with cloud HSM
{: #encrypt-data-hsm}
{: hide-dashboard}

You can remotely access {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic operations with the PKCS #11 API or with the GREP11 API.

### Performing cryptographic operations with the PKCS #11 API
{: #cryptographic-operations-with-pkcs11-dashboard}
{: help}
{: support}

To perform cryptographic operations with the PKCS #11 API, complete the following steps:

1. Generate an API key for accessing your {{site.data.keyword.hscrypto}} instance. Run the following command to create an API key for your {{site.data.keyword.cloud_notm}} account, and save the value of the API key for subsequent steps:

    ```
    ibmcloud iam api-key-create apikeyhpcs -d "API key for {{site.data.keyword.hscrypto}} PKCS11"
    ```
    {: codeblock}

2. Create a configuration file for the {{site.data.keyword.hscrypto}} PKCS #11 feature. The configuration file is named `grep11client.yaml`.

    Adapt the following file template and name the file `grep11client.yaml`:

    - Replace `<instance_id>` with the ID of your {{site.data.keyword.hscrypto}} instance.
    - Replace `<EP11_endpoint_URL>` and `<EP11_endpoint_port_number>` with the respective parameters of the EP11 endpoint address of your {{site.data.keyword.hscrypto}} instance.
    - Replace `<your_api_key>` with the value of the API key that you created previously.

    ```yaml
    iamcredentialtemplate: &defaultiamcredential
              enabled: true
              endpoint: "https://iam.cloud.ibm.com"
              # Keep the 'apikey' empty. It will be overridden by the Anonymous user API key configured later.
              apikey:
              # The Universally Unique IDentifier (UUID) of your Hyper Protect Crypto Services instance.
              instance: "<instance_id>"

    tokens:
      0:
        grep11connection:
          # The EP11 endpoint address starting from 'ep11'. For example: "ep11.us-south.hs-crypto.cloud.ibm.com"
          address: "<EP11_endpoint_URL>"
          port: "<EP11_endpoint_port_number>" # The EP11 endpoint port number
          tls:
            enabled: true # EP11 requires TLS connection.
            # Set it 'true' if you want to enable mutual TLS connections.
            # By default, set it 'false' because EP11 requires server-only authentication.
            mutual: <enable_mtls>
            # 'cacert' is a full-path certificate file. In Linux with the 'ca-ca-certificates' package installed, this is normally not needed.
            cacert:
            # Specify the file path of the client certificate if you enable mutual TLS. Otherwise, keep it empty.
            certfile: <client_certificate>
            # Specify the file path of the client certificate private key if you enable mutual TLS. Otherwise, keep it empty.
            keyfile: <client_certificate_private_key>
        storage:
            # 'remotestore' needs to be enabled if you want to generate keys with the attribute CKA_TOKEN.
          remotestore:
            enabled: true
        users:
          0: # The index of the Security Officer (SO) user MUST be 0.
            # The name for the Security Officer (SO) user. For example: "Administrator".
            name: "<SO_user_name>"
            # NEVER put the API key under the SO user for security reasons.
            iamauth:
              <<: *defaultiamcredential
          1: # The index of the normal user MUST be 1.
            # The name for the normal user. For example: "Normal user".
            name: "<normal_user_name>"
            # The 128-bit UUID of the private keystore. For example: "f00db2f1-4421-4032-a505-465bedfa845b".
            tokenspaceID: "<private_keystore_spaceid>"
            # NEVER put the API key under the normal user for security reasons.
            iamauth:
              <<: *defaultiamcredential
            sessionauth:
              enabled: true # Enable this option to encrypt and authenticate the keystore.
              # Authenticated keystore password; must be 6-8 characters in length
              tokenspaceIDPassword: "<private_keystore_password>"
          2: # The index of the anonymous user MUST be 2.
            # The name for the anonymous user. For example: "Anonymous".
            name: "<anonymous_user_name>"
            # The 128-bit UUID of the public keystore. For example: "ca22be26-b798-4fdf-8c83-3e3a492dc215".
            tokenspaceID: "<public_keystore_spaceid>"
            iamauth:
              <<: *defaultiamcredential
              # The API key for the anonymous user. It will overide the 'apikey' in the previous defaultcredentials.iamauth.apikey field
              apikey: "<apikey_for_anonymous_user>"
            sessionauth:
              enabled: false
              tokenspaceIDPassword: # Authenticated keystore password; must be 6-8 characters in length
    logging:
      # Set the logging level.
      # The supported levels, in an increasing order of verboseness: 'panic', 'fatal', 'error', 'warning'/'warn', 'info', 'debug', 'trace'. The Default value is 'warning'.
      loglevel: "<logging_level>"
      logpath: "<log_file_path>" # The full path of your logging file.

    ```
    {: codeblock}

3. Download and install the latest PKCS #11 library through [the GitHub repository](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external} and move it into a folder that is accessible by your applications. For example, if you are running your application on Linux, you can move the library to `/usr/local/lib`, `/usr/local/lib64` or `/usr/lib`.

4. Pass the API key that you previously create to allow your applications to perform the cryptographic operations.

### Performing cryptographic operations with the GREP11 API
{: #cryptographic-operations-with-grep11-dashboard}
{: help}
{: support}

To perform cryptographic operations with the GREP11 API, you need to make sure your applications are developed with programming languages supported by gRPC.

The following procedure uses Golang code as an example to test GREP11 functions.

1. Install Golang by following [the instruction](https://golang.org/doc/install){: external}.
2. Clone the [sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go){: external} into a local directory of your choice. Go modules are used for this repository, so you don't need to place the cloned repository in your `GOPATH`. Refer to the repository's README file for more information about the GREP11 Go code examples.
3. Update the following code snippet in the `examples/server_test.go` file.

    ```Golang
    var (
        Address        = "<grep11_server_address>:<port>"
        APIKey         = "<ibm_cloud_apikey>"
        HPCSInstanceID = "<hpcs_instance_id>"
    )
    ```
    {: codeblock}

    In the code example,
    - Replace `<grep11_server_address>` and `<port>` with the value of your GREP11 API endpoint. To find the service endpoint URL, from your provisioned service instance console, click **Overview**  &gt; **Connect** &gt; **Enterprise PKCS #11 endpoint URL**.
    - Replace `<ibm_cloud_apikey>` with the service ID API key that you created. The service ID API Key can be created by following the instruction in [Managing service ID API key](/docs/account?topic=account-serviceidapikeys){: external}.
    - Replace `<instance_ID>` with the instance ID that uniquely identifies your service instance. Retrieve the instance ID by following the instruction in [Retrieving your instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID).

4. From the `<your_repository_path>/hpcs-grep11-go/examples` directory, execute the examples by running the `go test -v -run Example` command.

    The sample program produces output similar to the following:

    ```
    === RUN   Example_getMechanismInfo
    --- PASS: Example_getMechanismInfo (0.11s)
    === RUN   Example_generateGenericKey
    --- PASS: Example_generateGenericKey (0.09s)
    === RUN   Example_encryptAndDecryptUsingAES
    --- PASS: Example_encryptAndDecryptUsingAES (0.28s)
    === RUN   Example_digest
    --- PASS: Example_digest (0.18s)
    === RUN   Example_signAndVerifyUsingRSAKeyPair
    --- PASS: Example_signAndVerifyUsingRSAKeyPair (0.21s)
    === RUN   Example_signAndVerifyUsingDSAKeyPair
    --- PASS: Example_signAndVerifyUsingDSAKeyPair (0.99s)
    === RUN   Example_deriveKeyUsingDHKeyPair
    --- PASS: Example_deriveKeyUsingDHKeyPair (0.64s)
    === RUN   Example_signAndVerifyUsingECDSAKeyPair
    --- PASS: Example_signAndVerifyUsingECDSAKeyPair (0.16s)
    === RUN   Example_signAndVerifyToTestErrorHandling
    --- PASS: Example_signAndVerifyToTestErrorHandling (0.16s)
    === RUN   Example_wrapAndUnwrapKey
    --- PASS: Example_wrapAndUnwrapKey (0.20s)
    === RUN   Example_deriveKey
    --- PASS: Example_deriveKey (0.22s)
    === RUN   Example_tls
    --- PASS: Example_tls (0.14s)
    PASS
    ok      github.com/IBM-Cloud/hpcs-grep11-go/examples    13.106s
    ```
    {: screen}



## What's next
{: #get-started-next}

- {{site.data.keyword.hscrypto}} helps you meet compliance requirements and ensures the security of your data. Check out the [compliance standards and criteria](/docs/hs-crypto?topic=hs-crypto-security-and-compliance) {{site.data.keyword.hscrypto}} has been certified.
- {{site.data.keyword.hscrypto}} provides advanced encryption to your at-rest data with envelope encryption, check out [Protecting your data with envelope encryption](/docs/hs-crypto?topic=hs-crypto-envelope-encryption) to see how it works.
- You can use {{site.data.keyword.hscrypto}} as the encryption key provider for other services such as {{site.data.keyword.cos_full_notm}} to bring your own encryption to your applications or data. Check out [Integrating services](/docs/hs-crypto?topic=hs-crypto-integrate-services) for the full list of supported services.
- To learn more about {{site.data.keyword.hscrypto}} concepts and terminologies, check out [Components and concepts](/docs/hs-crypto?topic=hs-crypto-understand-concepts).
- If you are using the Standard Plan, manage your keys with [{{site.data.keyword.hscrypto}} key management service API](/apidocs/hs-crypto){: external} and [{{site.data.keyword.keymanagementserviceshort}} CLI](/docs/key-protect?topic=key-protect-cli-plugin-key-protect-cli-reference){: external}.
- Encrypt your data and perform cryptographic operations with the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) or the [GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
