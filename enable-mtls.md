---

copyright:
  years: 2021, 2023
lastupdated: "2023-06-16"

keywords: second authentication, tls connection, certificate manager, second layer of authentication for grep11

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Enabling the second layer of authentication for EP11 connections - Standard Plan only
{: #enable-authentication-ep11}

To ensure the exclusive control on the execution of cryptographic operations, you can use the {{site.data.keyword.hscrypto}} certificate manager CLI to enable the second layer of authentication for EP11 (GREP11 or PKCS #11 API) connections. By enabling this function, you add an extra layer of access control on top of the Identity and Access Management (IAM) token to the EP11 applications. A mutual TLS connection is established to ensure that only EP11 applications with a valid client certificate can perform EP11 operations.
{: shortdesc}

The second layer of authentication for EP11 connections is currently only supported by the {{site.data.keyword.hscrypto}} Standard Plan.
{: note}

## Security and availability best practices for enabling mutual TLS authentication
{: #enable-authentication-ep11-security-best-practices}

With mutual TLS as a second layer of authentication for accessing EP11, you need to be aware of the following security and availability considerations:

- If you need to prevent certain people from accessing EP11, separate certificate administrators from service users. Control access by assigning the _Certificate Manager_ role only to the people that manage the client certificates, and assigning other service users the corresponding roles for operational usage. To manage user access, you need to be assigned the _Administrator_ role with account management access.
- EP11 APIs are not accessible if you use invalid client certificates or use unavailable private keys to sign client certificates. To ensure the availability, assign more than one person the _Certificate Manager_ role as a backup. Certificate administrators need to securely maintain their unique administrator private keys. Certificate administrators also need to maintain a backup of all client certificates outside of the {{site.data.keyword.hscrypto}} instance, for example, by using [{{site.data.keyword.cloud_notm}} Secrets Manager](https://www.ibm.com/cloud/secrets-manager){: external}. It is also suggested to monitor the expiration of the certificates.

## Before you begin
{: #enable-authentication-ep11-prerequisites}

Before you can enable the second layer of authentication for GREP11 or PKCS #11 API connections, make sure that you complete the following prerequisites:

1. You are assigned the _Certificate Manager_ IAM role to perform the corresponding actions. For more information about assigning IAM roles, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access) and [Managing access to resources](/docs/account?topic=account-assign-access-resources).
2. You have a client certificate prepared on your workstation that is used for the TLS authentication. It is suggested to use the [{{site.data.keyword.cloud_notm}} Secrets Manager](https://www.ibm.com/cloud/secrets-manager){: external} to manage SSL/TLS certificates for your applications and services. It is free and provides persistent storage for your certificates. With the {{site.data.keyword.cloud_notm}} Certificate Manager service, you can [order free certificates](/docs/certificate-manager?topic=certificate-manager-ordering-certificates), [import your certificates](/docs/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#importing-a-certificate), and [enable notifications for expiring certificates](/docs/certificate-manager?topic=certificate-manager-configuring-notifications).
3. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.
4. Install the latest certificate manager CLI plug-in with the following command:

    ```
    ibmcloud plugin install hpcs-cert-mgr
    ```
    {: pre}

5. [Log in to {{site.data.keyword.cloud_notm}} with the CLI](/docs/cli?topic=cli-getting-started#step3-configure-idt-env){: external}. If you have multiple accounts, select the account that your service instance is created with. Make sure that you log in to the correct region and resource group where the service instance is located with the following command:

    ```
    ibmcloud target -r <region> -g <resource_group>
    ```
    {: pre}

## Step 1: Configure the administrator signature key
{: #enable-authentication-ep11-step1-signature}

To enable the second layer of authentication, you need to first configure the administrator signature key. The signature key is used for you to connect to your instance certificate manager server that processes the certificate manager CLI commands.

1. Generate the signature key pair with the following command:

    ```
    ibmcloud hpcs-cert-mgr adminkey set --crn HPCS_CRN [--private]
    ```
    {: pre}

    Replace the `HPCS_CRN` variable with the Cloud Resource Name (CRN) of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the CRN. The parameter `--private` is optional. If you use this option, the certificate manager server URL points to the private endpoint and you need to use the private network to connect your service instance.

    After the execution of this command, a public and private key pair is generated and stored on your local workstation. The default file path is `/Users/<username>/.hpcs-cert-mgr-cfg/`. Make sure that you store the signature key securely, for example with password protection. The public key is automatically uploaded to your instance certificate manager server for signature verification.

    If you want to refresh and update your signature key, you can use the `ibmcloud hpcs-cert-mgr adminkey update` command to perform the action. For more information about the CLI usage, see [{{site.data.keyword.hscrypto}} certificate manager CLI reference](/docs/hs-crypto?topic=hs-crypto-cli-plugin-hpcs-cli-plugin#cert-manager-cli-plugin).
    {: tip}

2. (Optional) Check and confirm whether the public key is uploaded to the server with the following command:

    ```
    ibmcloud hpcs-cert-mgr adminkey get --crn HPCS_CRN [--private]
    ```
    {: pre}

    If this command returns the public key value, it means that you upload the public key successfully.

## Step 2: Set up the client CA certificate for authentication
{: #enable-authentication-ep11-step2-certificate}

After you configure the administrator signature key, you need to upload the client [certificate authority (CA)](#x2016383){: term} certificate to your instance certificate manager server for TLS client authentication. 

After you set up the client CA certificate, you are no longer able to access EP11 keystores and EP11 keys through the {{site.data.keyword.cloud_notm}} console.
{: important}

1. (Optional) Prepare CA and client certificates

   You can generate CA certificates for the GREP11 infrastructure by using the OpenSSL utility. 
   
   Make sure that you install the OpenSSL on a workstation that you can use to generate the certificates. Complete the following steps on your workstation:

   1. Generate the CA key by running the following command:
      ```
      openssl genrsa -out ca.key 2048
      ```
      {: pre}

   2. Create the CA certificate by running the following command:
      ```
      openssl req -new -x509 -key ca.key -days 730 -out ca.pem
      ```
      {: pre}

   3. Create the client key by running the following command:
      ```
      openssl genrsa -out client-key.pem 2048
      ```
      {: pre}

   4. Create the client certificate signing request by running the following command:
      ```
      openssl req -new -key client-key.pem -out client.csr
      ```
      {: pre}

   5. Create the client certificate by running the following command:
      ```
      openssl x509 -req -days 730 -in client.csr -CA ca.pem -CAcreateserial -CAkey ca.key -out client.pem
      ```
      {: pre}

2. Upload the client CA certificate to the server with the following command:
   
    If your client certificate is signed by an intermediate CA certificate in a certificate chain, you need to upload that intermediate CA certificate. 
    {: note}

    ```
    ibmcloud hpcs-cert-mgr cert set --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY --cert-id CERT_ID --cert CERT_FILE [--private]
    ```
    {: pre}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `HPCS_CRN` | **Required.** The Cloud Resource Name (CRN) of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the CRN. |
    | `ADMIN_PRIV_KEY` | **Required.** The file path of your current private key on your local workstation that you generate or update in [Step 1](#enable-authentication-ep11-step1-signature). The private key is used to sign this command action towards your instance certificate manager server. |
    | `CERT_ID` | **Required.** The string ID that you want to assign to the client CA certificate for easy identification. |
    | `CERT_FILE` | **Required.** The file path of the client CA certificate on your local workstation. |
    {: caption="Table 1. Describes the variables needed to upload the TLS certificate" caption-side="bottom"}

    The parameter `--private` is optional. If you use this option, the certificate manager server URL points to the private endpoint and you need to use the private network to connect your service instance.

3. (Optional) Check and confirm whether the client CA certificate is uploaded to the server with the following command:

    ```
    ibmcloud hpcs-cert-mgr cert list --crn HPCS_CRN [--private]
    ```
    {: pre}

    This command lists all the available client CA certificates that are managed by you on the server. If the list contains the certificate that is previously uploaded, it means the action is successfully completed.

## Step 3: Establish mutual TLS connections for EP11 applications
{: #enable-authentication-ep11-step3-enable-tls}

After you set up the administrator signature key and the client CA certificate, EP11 users can establish mutual TLS connections for applications that use the GREP11 or PKCS #11 API. Before EP11 users can do this, they need to configure the GREP11 or PKCS #11 applications with the client certificate.

To use the GREP11 or PKCS #11 API, make sure that EP11 users are assigned the proper IAM roles to perform EP11 operations. For more information, see the HSM APIs tab in [IAM service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles).
{: note}

- Configure GREP11 applications

    Depending on the programming language that you use for the GREP11 application, the configuration method varies based on the corresponding gRPC package. The following provides examples for Golang and JavaScript.

    - Golang example code snippet

      ```go
      cert, _ := tls.LoadX509KeyPair("client.pem", "client-key.pem")
      var callOpts = []grpc.DialOption{
        grpc.WithTransportCredentials(credentials.NewTLS(&tls.Config{Certificates: []tls.Certificate{cert}}))
      }
      ```
      {: codeblock}

      The `tls.Config{}` needs to be properly defined based on the [`Config` type struct](https://pkg.go.dev/crypto/tls#Config){: external}. You need to set at least the `Certificates` field. Make sure to use your client key and client certificate. For the complete Golang example code, see [The sample GitHub repository for Golang](https://github.com/IBM-Cloud/hpcs-grep11-go/blob/master/examples/server_test.go){: external}.
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

    | Variable | Description |
    | --- | --- |
    | `client_certificate` | **Required.** The file path of the client certificate that is uploaded to the server by the certificate administrator. |
    | `client_certificate_private_key` | **Required.** The file path of the client certificate private key that is used to sign the certificate. |
    {: caption="Table 3. Describes the variables needed to configure PKCS #11 applications" caption-side="bottom"}

After the configuration, when the applications use the GREP11 or PKCS #11 API to perform cryptographic operations, a mutual TLS connection is established and the client certificate is validated for the additional layer of authentication.

## (Optional) Disabling mutual TLS connections
{: #enable-authentication-ep11-disable-tls}

If you no longer need the second layer of authentication, you can disable the function by deleting all the client CA certificates on the server.

1. Delete a CA certificate with the following command. Repeat this step to delete all the available certificates on the server to disable the TLS connections from EP11 applications.

    ```
    ibmcloud hpcs-cert-mgr cert delete --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY --cert-id CERT_ID [--private]
    ```
    {: pre}

    Replace the variables in the example request according to the following table.

    | Variable | Description |
    | --- | --- |
    | `HPCS_CRN` | **Required.** The Cloud Resource Name (CRN) of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the CRN. |
    | `ADMIN_PRIV_KEY` | **Required.** The file path of your current private key that is stored on your local workstation. The private key is used to sign this command action towards your instance certificate manager server. |
    | `CERT_ID` | **Required.** The string ID of the CA certificate that you want to delete. You can first use the `ibmcloud hpcs-cert-mgr cert list --crn HPCS_CRN` command to list all the certificates including their IDs. |
    {: caption="Table 2. Describes the variables needed to delete CA certificates" caption-side="bottom"}

    The parameter `--private` is optional. If you use this option, the certificate manager server URL points to the private endpoint and you need to use the private network to connect your service instance.

    If multiple certificate administrators are set up for your service instance, make sure to delete all the CA certificates under these administrators.

    If you delete a CA certificate from the certificate manager server, all applications using the client certificates that are issued by this CA certificate do not have access to the GREP11 instance through mutual TLS connection.

    After you delete all CA certificates from the certificate manager server, the mutual TLS authentication for the GREP11 instance is disabled. Applications then do not need mutual TLS connection to connect to the GREP11 instance.


2. (Optional) Check and confirm whether all the CA certificates are deleted with the following command:

    ```
    ibmcloud hpcs-cert-mgr cert list --crn HPCS_CRN [--private]
    ```
    {: pre}

    If no certificate is returned, it means all the certificates of your service instance are deleted.

3. (Optional) Update the GREP11 or PKCS #11 applications to delete the certificate configurations, so that the applications no longer use the certificate for future API connections.

## What's next
{: #enable-authentication-ep11-whats-next}

- For the complete certificate manager CLI command reference, see [{{site.data.keyword.hscrypto}} certificate manager CLI plug-in](/docs/hs-crypto?topic=hs-crypto-cli-plugin-hpcs-cli-plugin#cert-manager-cli-plugin).
- For the GREP11 API and PKCS #11 API reference, see [Cryptographic operations: GREP11 API](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref) and [Cryptographic operations: PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
