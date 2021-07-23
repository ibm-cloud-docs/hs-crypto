---

copyright:
  years: 2021
lastupdated: "2021-07-23"

keywords: second authentication, tls connection, certificate manager, second layer of authentication for grep11

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:hide-in-docs: .hide-in-docs}
{:hide-dashboard: .hide-dashboard}
{:external: target="_blank" .external}
{:term: .term}

# Enabling the second layer of authentication for EP11 connections
{: #enable-authentication-ep11}

To ensure the exclusive control on the execution of cryptographic operations, you can use the {{site.data.keyword.hscrypto}} certificate manager CLI to enable the second layer of authentication for EP11 (GREP11 or PKCS #11 API) connections. By enabling this function, you enable an extra layer of access control on top of the Identity and Access Management (IAM) token to the EP11 applications. A mutual TLS connection is established to ensure that only EP11 applications with a valid client certificate can perform EP11 operations.
{: shortdesc}

## Before you begin
{: #enable-authentication-ep11-prerequisites}

Before you can enable the second layer of authentication for GREP11 or PKCS #11 API connections, make sure that you complete the following prerequisites:

1. You are assigned the _Certificate Manager_ IAM role to perform the corresponding actions. For more information about assigning IAM roles, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access) and [Managing access to resources](/docs/account?topic=account-assign-access-resources).
2. You have a client certificate prepared on your workstation that is used for the TLS authentication. It is suggested to use the [{{site.data.keyword.cloud_notm}} Certificate Manager](https://www.ibm.com/cloud/certificate-manager){: external} to manage SSL/TLS certificates for your applications and services. It is free and provides persistent storage for your certificates. With the Certificate Manager, you can [order free certificates](/docs/certificate-manager?topic=certificate-manager-ordering-certificates), [import your certificates](/docs/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#importing-a-certificate), and [enable notifications for expiring certificates](/docs/certificate-manager?topic=certificate-manager-configuring-notifications).
3. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external} and the latest certificate manager CLI plug-in with the following command:

  ```
  ibmcloud plugin install hpcs-cert-mgr
  ```
  {: pre}
4. [Log in to {{site.data.keyword.cloud_notm}} with the CLI](/docs/cli?topic=cli-getting-started#step3-configure-idt-env){: external}. If you have multiple accounts, select the account that your service instance is created with. Make sure that you log in to the correct region and resource group where the service instance is located with the following command:

  ```
  ibmcloud target -r <region> -g <resource_group>
  ```
  {: pre}

## Step 1: Configure the administrator signature key
{: #enable-authentication-ep11-step1-signature}

To enable the second layer of authentication, you need to first configure the administrator signature key. The signature key is used for you to connect to your instance certificate manager server.

1. Generate the signature key pair and upload the public key with the following command:

  ```
  ibmcloud hpcs-cert-mgr adminkey set --crn HPCS_CRN [--private]
  ```
  {: pre}

  Replace the `HPCS_CRN` variable with the Cloud Resource Name (CRN) of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the CRN. The parameter `--private` is optional. If you use this option, the certificate manager server URL points to the private endpoint and you need to use the private network to connect your service instance.

  After the execution of this command, a public and private key pair is generated and stored on your local workstation. The default file path is `/Users/<username>/hpcs-cert-mgr-cfg/`. Make sure that you store the signature key securely, for example with password protection. The public key is automatically uploaded to your instance certificate manager server.

  If you want to refresh and update your signature key, you can use the `ibmcloud hpcs-cert-mgr adminkey update` command to perform the action. For more information about the CLI usage, see [{{site.data.keyword.hscrypto}} certificate manager CLI reference](/docs/hs-crypto?topic=hs-crypto-cli-plugin-hpcs-cli-plugin#cert-manager-cli-plugin).
  {: tip}

2. (Optional) Check and confirm whether the public key is uploaded to the server with the following command:

  ```
  ibmcloud hpcs-cert-mgr adminkey get --crn HPCS_CRN [--private]
  ```
  {: pre}

  If this command returns the public key value, it means that you upload the public key successfully.

## Step 2: Set up the client certificate for authentication
{: #enable-authentication-ep11-step2-certificate}

After you configure the administrator signature key, you need to upload the client certificate to your instance certificate manager server for TLS client authentication.

1. Upload the certificate to the server with the following command:

  ```
  ibmcloud hpcs-cert-mgr cert set --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY --cert-id CERT_ID --cert CERT_FILE [--private]
  ```
  {: pre}

  Replace the variables in the example request according to the following table.

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><varname>HPCS_CRN</varname></td>
      <td>**Required.** The Cloud Resource Name (CRN) of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the CRN.</td>
    </tr>
    <tr>
      <td><varname>ADMIN_PRIV_KEY</varname></td>
      <td>**Required.** The file path of your current private key that you generate or update in [Step 1](#enable-authentication-ep11-step1-signature). The private key is used to sign this command action towards your instance certificate manager server.</td>
    </tr>
    <tr>
      <td><varname>CERT_ID</varname></td>
      <td>**Required.** The string ID that you want to assign to the client certificate for easy identification.</td>
    </tr>
    <tr>
      <td><varname>CERT_FILE</varname></td>
      <td>**Required.** The client certificate file that you store on your local workstation.</td>
    </tr>
    <caption>Table 1. Describes the variables that are needed to upload the TLS certificate</caption>
  </table>

  The parameter `--private` is optional. If you use this option, the certificate manager server URL points to the private endpoint and you need to use the private network to connect your service instance.

2. (Optional) Check and confirm whether the client certificate is uploaded to the server with the following command:

  ```
  ibmcloud hpcs-cert-mgr cert list --crn HPCS_CRN [--private]
  ```
  {: pre}

  This command lists all the available client certificates that are managed by you on the server. If the list contains the certificate that is previously uploaded, it means the action is successfully completed.

## Step 3: Establish mutual TLS connections for EP11 applications
{: #enable-authentication-ep11-step3-enable-tls}

After you set up the administrator signature key and the client certificate, EP11 users can establish mutual TLS connections for applications that use the GREP11 or PKCS #11 API. Before EP11 users can do this, they need to configure the GREP11 or PKCS #11 applications with the client certificate.

To use the GREP11 or PKCS #11 API, make sure that EP11 users are assigned the proper IAM roles to perform EP11 operations. For more information, see the HSM APIs tab in [IAM service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
{: note}

- Configure GREP11 applications

  Depending on the programming language that you use for the GREP11 application, the configuration method varies based on the corresponding gRPC package. The following provides examples for Golang and JavaScript.

  - Golang example code snippet

    ```go
    var callOpts = []grpc.DialOption{
      grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{}))
    }
    ```
    {: codeblock}

    The `tls.Config{}` needs to be properly defined based on the [`Config` type struct](https://pkg.go.dev/crypto/tls#Config){: external}. You need to set at least the `Certificates` field. For the complete Golang example code, see [The sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go/blob/master/examples/server_test.go){: external}.

  - JavaScript example code snippet

    ```javascript
    credentials.push(grpc.credentials.createSsl());
    ```
    {: codeblock}

    You can refer to the [Credentials module documentation](https://grpc.github.io/grpc/node/grpc.credentials.html){: external} for detailed information on functions and parameters. You need to set the `private_key` and `cert_chain` parameters for `createSsl()` function. For the complete JavaScript example code, see [The sample GitHub repository for JavaScript](https://github.com/IBM-Cloud/hpcs-grep11-js/blob/master/examples/credentials.js){: external}.

- Configure PKCS #11 applications

  PKCS #11 handles mutual TLS in its [configuration file](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api#step3-setup-configuration-file). Update the `tls` field according to the following example:

  ```yaml
  tls:
    enabled: true
    mutual: true
    cacert:
    certfile: "<client_certificate>"
    keyfile: "<client_certificate_private_key>"
  ```
  {: codeblock}

  Replace the variables in the example based on the following table:

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><varname>client_certificate</varname></td>
      <td>**Required.** The file path of the client certificate that is uploaded to the server by the certificate administrator.</td>
    </tr>
    <tr>
      <td><varname>client_certificate_private_key</varname></td>
      <td>**Required.** The file path of the client certificate private key.</td>
    </tr>
    <caption>Table 3. Describes the variables that are needed to configure PKCS #11 applications</caption>
  </table>

After the configuration, when the applications use the GREP11 or PKCS #11 API to perform cryptographic operations, a mutual TLS connection is established and the client certificate is validated for the additional layer of authentication.

## (Optional) Disabling mutual TLS connections
{: #enable-authentication-ep11-disable-tls}

If you no longer need the second layer of authentication, you can disable the function by removing all the client certificates on the server.

1. Remove client certificates with the following command:

  ```
  ibmcloud hpcs-cert-mgr cert delete --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY --cert-id CERT_ID [--private]
  ```
  {: pre}

  Replace the variables in the example request according to the following table.

  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><varname>HPCS_CRN</varname></td>
      <td>**Required.** The Cloud Resource Name (CRN) of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the CRN.</td>
    </tr>
    <tr>
      <td><varname>ADMIN_PRIV_KEY</varname></td>
      <td>**Required.** The file path of your current private key that is stored on your local workstation. The private key is used to sign this command action towards your instance certificate manager server.</td>
    </tr>
    <tr>
      <td><varname>CERT_ID</varname></td>
      <td>**Required.** The string ID of the client certificate that you want to delete. You can first use the `ibmcloud hpcs-cert-mgr cert list --crn HPCS_CRN` command to list all the certificates including their IDs.</td>
    </tr>
    <caption>Table 2. Describes the variables that are needed to delete client certificates</caption>
  </table>

  The parameter `--private` is optional. If you use this option, the certificate manager server URL points to the private endpoint and you need to use the private network to connect your service instance.

  Repeat the step to remove all the available certificates on the server to disable the TLS connections from EP11 applications.

  If multiple certificate administrators are set up for your service instance, make sure to remove all the client certificates under these administrators. After you remove all the certificates for your service instance, the mutual TLS is disabled for all new EP11 connections and the second layer of authentication is inactive.
  {: note}

2. (Optional) Check and confirm whether all the client certificates are removed with the following command:

  ```
  ibmcloud hpcs-cert-mgr cert list --crn HPCS_CRN [--private]
  ```
  {: pre}

  If no certificate is returned, it means all the certificates of your service instance are removed.

3. (Optional) Update the GREP11 or PKCS #11 applications to remove the certificate configurations, so that the applications are no longer use the certificate for future API connections.

## Security and availability considerations
{: #enable-authentication-ep11-security-considerations}

With mutual TLS as a second layer of authentication for accessing EP11, you need to be aware of the following security and availability considerations:

- If you need to prevent some persons from accessing EP11, separate certificate administrators from service users. Control access by assigning the _Certficate Manager_ role only to the persons who manage the client certificates and assigning other service users the corresponding roles for operational usage. To manage user access, you need to be assigned the _Administrator_ role with account management access.
- EP11 APIs become inaccessible if you use invalid client certificates or use unavailable private keys to sign client certificates. To ensure the availability, assign more than one person the _Certificate Manager_ role as a backup. Each certificate administrator needs to maintain his or her unique administrator private key securely. In addition, certificate administrators need to maintain a backup of all client certificates outside of the {{site.data.keyword.hscrypto}} instance, for example, by using [{{site.data.keyword.cloud_notm}} Certificate Manager](https://www.ibm.com/cloud/certificate-manager){: external}. It is also suggested to monitor the expiration of the certificates.

## What's next
{: #enable-authentication-ep11-whats-next}

- For the complete certificate manager CLI command reference, see [{{site.data.keyword.hscrypto}} certificate manager CLI plug-in](/docs/hs-crypto?topic=hs-crypto-cli-plugin-hpcs-cli-plugin#cert-manager-cli-plugin).
- For the GREP11 API and PKCS #11 API reference, see [Cryptographic operations: GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref) and [Cryptographic operations: PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
