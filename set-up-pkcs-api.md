---

copyright:
  years: 2020, 2023
lastupdated: "2023-09-04"

keywords: set up api, pkcs api, pkcs11 library, cryptographic operations, use pkcs11 api, access pkcs api, pkcs11, cryptographic functions

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Performing cryptographic operations with the PKCS #11 API
{: #set-up-pkcs-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} provides the standard PKCS #11 API to access the {{site.data.keyword.hscrypto}} cloud HSM for cryptographic operations.
{: shortdesc}

## Prerequisites
{: #prerequisite-pkcs-api}

Before you can set up and use the PKCS #11 API, first follow the [Best practices for setting up PKCS #11 user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access) to create different service ID API keys for the various PKCS #11 user types.

## Step 1: Set up the PKCS #11 library
{: #step1-setup-pkcs-library}

You need to set up the PKCS #11 library on your workstation to make it available for your applications to call the standard PKCS #11 functions.

The PKCS #11 library, for both the amd64 and s390x platforms, is supported only on [Linux]{: tag-linux}.
{: note}

If you are running a Java PKCS #11 application using the SunPKCS11 provider on the IBM Z (s390x) platform, make sure that you use the latest IBM Semeru JVM and specify the `-Xjit:noResumableTrapHandler` Java option when starting your application. You can download the latest s390x version of the IBM Semeru JVM by changing the **Architecture** filter field to **s390x** on the [IBM Semeru Runtime Downloads page](https://developer.ibm.com/languages/java/semeru-runtimes/downloads/?license=IBM){: external}.
{: note}

1. [Download the latest PKCS #11 library](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external}. The library file names use the naming convention: `pkcs11-grep11-<platform>.so.<version>`. The platform is either *amd64* or *s390x* and the version is the standard *major.minor.build* syntax.
2. Move the library into a folder that is accessible by your applications. For example, if you are running your application on Linux, you can move the library to `/usr/local/lib`, `/usr/local/lib64`, or `/usr/lib`.

## Step 2: (Optional) Verify the integrity and authenticity of the PKCS #11 library
{: #step2-verify-pkcs-library}

For maximum security, verify the integrity and authenticity of the PKCS #11 library before you run your PKCS #11 applications to use the library.

{{site.data.keyword.hscrypto}} enables [signed code verification](https://en.wikipedia.org/wiki/Code_signing){: external} to ensure that the signature matches the original code. If the downloaded PKCS #11 library file is altered or corrupted, a different signature is produced and the verification fails. To make sure that the files are not tampered with or corrupted during the download process, complete the following steps by using the [OpenSSL command-line tool](https://wiki.openssl.org/index.php/Binaries){: external}.

1. Download the latest version of the following files from the [library repository](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external} to the same directory where you store the PKCS #11 library:

    - `pkcs11-grep11-<platform>.so.<version>.sig`: The signed cryptographic hash of the PKCS #11 library, where platform is either *amd64* or *s390x* and version is the *major.minor.build* of the signature file. Both **platform** and **version** must match the respective **platform** and **version** of the PKCS #11 library that you use.

    - `signing_cert.pem`: The signing certificate of the {{site.data.keyword.hscrypto}} PKCS #11 client files.

    - `digicert_cert.pem`: An intermediate code signing certificate to prove the signing certificate of the {{site.data.keyword.hscrypto}} PKCS #11 client files.

2. Extract the public key from the signing certificate `signing_cert.pem` to the `sigkey.pub` file with the following command:

    ```
    openssl x509 -pubkey -noout -in signing_cert.pem -out sigkey.pub
    ```
    {: pre}

3. Verify the integrity of the PKCS #11 library file with the following command:

    ```
    openssl dgst -sha256 -verify sigkey.pub -signature pkcs11-grep11-<platform>.so.<version>.sig pkcs11-grep11-<platform>.so.<version>
    ```
    {: pre}

    Replace **platform** with either *amd64* or *s390x* and replace **version** with the *major.minor.build* of the library.

    When the verification is successful, `Verified OK` is displayed.

4. Verify the authenticity and validity of the signing certificate with the following command:

    ```
    openssl ocsp -no_nonce -issuer digicert_cert.pem -cert signing_cert.pem -VAfile digicert_cert.pem -text -url http://ocsp.digicert.com -respout ocsptest
    ```
    {: pre}

    When the verification is successful, `Response verify OK` and `signing_cert.pem: good` are displayed in the output.

5. If the verification fails, cancel the installation and [contact IBM for support](/docs/hs-crypto?topic=hs-crypto-getting-help).

## Step 3: Set up the PKCS #11 configuration file
{: #step3-setup-configuration-file}

In order to connect the PKCS #11 library to the {{site.data.keyword.hscrypto}} cloud HSM to perform cryptographic functions, you need to complete the following steps to set up the configuration file.

1. Create a configuration file that is named `grep11client.yaml` based on the following example. The [library repository](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external} also provides a template for you to adapt. You can refer to the comments in the code to understand each field.

    ```yaml
    iamcredentialtemplate: &defaultiamcredential
      enabled: true
      endpoint: "https://iam.cloud.ibm.com"
    
    sessionauthtemplate: &defaultsessionauth
      enabled: false
      tokenspaceIDPassword:  # Authenticated keystore password 6-8 characters in length

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
            iamauth: *defaultiamcredential
          1: # The index of the normal user MUST be 1.
            # The name for the normal user. For example: "Normal user".
            name: "<normal_user_name>"
            # The 128-bit UUID of the private keystore. For example: "f00db2f1-4421-4032-a505-465bedfa845b".
            tokenspaceID: "<private_keystore_spaceid>"
            iamauth: *defaultiamcredential
            # Do not override the defaultsessionauth template
            # The same values must be used for both the private (normal user) and public (anonymous) keystores
            sessionauth: *defaultsessionauth
          2: # The index of the anonymous user MUST be 2.
            # The name for the anonymous user. For example: "Anonymous".
            name: "<anonymous_user_name>"
            # The 128-bit UUID of the public keystore. For example: "ca22be26-b798-4fdf-8c83-3e3a492dc215".
            tokenspaceID: "<public_keystore_spaceid>"
            iamauth:
              <<: *defaultiamcredential
              # The API key for the anonymous user. All other users can specify API key using the C_Login command.
              apikey: "<apikey_for_anonymous_user>"
            # Do not override the defaultsessionauth template
            # The same values must be used for both the private (normal user) and public (anonymous) keystores
            sessionauth: *defaultsessionauth

    logging:
      # Set the logging level.
      # The supported levels, in an increasing order of verboseness: 'panic', 'fatal', 'error', 'warning'/'warn', 'info', 'debug', 'trace'. The Default value is 'warning'.
      loglevel: "<logging_level>"
      logpath: "<log_file_path>" # The full path of your logging file.

    ```
    {: codeblock}

    If authenticated keystores are used, the `sessionauth` configuration option must be enabled for both keystores and the text passwords that are 6-8 characters in length must be identical for both keystores in the `tokenspaceIDPassword` field.
    {: important}

    Replace the variables in the example according to the following table:

    | Variable | Description |
    | --- | --- |
    | `EP11_endpoint_URL` | The {{site.data.keyword.hscrypto}} Enterprise PKCS #11 (EP11) API endpoint. You can get it through **Overview** > **Connect** > **EP11 endpoint URL** in the {{site.data.keyword.cloud_notm}} console, or you can dynamically [retrieve the endpoint URL](/apidocs/hs-crypto#getinstance) with the API. Depending on whether you are using a public or [private network](/docs/hs-crypto?topic=hs-crypto-secure-connection), use the public or private EP11 endpoint URL. |
    | `EP11_endpoint_port_number` | The port number of the EP11 API endpoint. It is located after the colon in the endpoint URL. |
    | `enable_mtls` | Valid values are `true` or `false` to indicate whether you want to enable mutual TLS to add a second layer of authentication for PKCS #11 API access for {{site.data.keyword.hscrypto}} Standard Plan. By default, set it `false` as EP11 requires server-only authentication. For more information about the mutual TLS connections, see [Enabling the second layer of authentication for EP11 connections](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11). |
    | `client_certificate` | If you enable mutual TLS connections, specify the file path of the client certificate that is uploaded to your instance by the certificate administrator. Otherwise, keep this field empty. |
    | `client_certificate_private_key` | If you enable mutual TLS connections, specify the file path of the client certificate private key that is used to sign the certificate. Otherwise, keep this field empty. |
    | `SO_user_name` | The name for the Security Officer (SO) user type. The PKCS #11 standard defines two types of users for login: the security officer (SO) and the normal user. For more information about the PKCS #11 user types, see [PKCS #11 Cryptographic Token Interface Usage Guide Version 2.40 - Users](http://docs.oasis-open.org/pkcs11/pkcs11-ug/v2.40/cn02/pkcs11-ug-v2.40-cn02.html#_Toc406759984). |
    | `normal_user_name` | The name for the normal user type. The PKCS #11 standard defines two types of users for login: the security officer (SO) and the normal user. For more information about the PKCS #11 user types, see [PKCS #11 Cryptographic Token Interface Usage Guide Version 2.40 - Users](http://docs.oasis-open.org/pkcs11/pkcs11-ug/v2.40/cn02/pkcs11-ug-v2.40-cn02.html#_Toc406759984). |
    | `private_keystore_spaceid` | The 128-bit [Universally Unique IDentifier (UUID)](https://www.cryptosys.net/pki/uuid-rfc4122.html) of the private keystore. You can generate the UUID with a third-party tool, such as [UUID generator](https://www.uuidgenerator.net/). \n \n {{site.data.keyword.hscrypto}} provides you with two database-backed EP11 keystores for enhanced security and better user access management: the private keystore that only the normal user type can access and the public keystore that all user types can access. The UUID must be different from the UUID specified for the `public_keystore_spaceid` parameter. |
    | `private_keystore_password` | Authorized sessions can be used by enabling the `sessionauth` configuration option. If the `sessionauth` option is enabled, it must be enabled for both keystores. In addition, a text password that is 6-8 characters in length is required for the `tokenspaceIDPassword` field and the password must be identical for both keystores. Authorized sessions are specific to the HSM and are used in the PKCS #11 flow to login and logout, and they are required for authenticated key operations. All keys generated using authorized sessions are stored in an authenticated and encrypted keystore. The `tokenspaceIDPassword` field is used to protect the keys in an authenticated and encrypted keystore. For each service instance, a maximum of five authenticated keystores are supported. |
    | `anonymous_user_name` | The name for the anonymous user. The PKCS #11 standard defines two types of users for login: the security officer (SO) and the normal user. If a user does not log in by using the `C_Login` Cryptoki function, then the user is known as an anonymous user. For more information about the PKCS #11 user types, see [PKCS #11 Cryptographic Token Interface Usage Guide Version 2.40 - Users](http://docs.oasis-open.org/pkcs11/pkcs11-ug/v2.40/cn02/pkcs11-ug-v2.40-cn02.html#_Toc406759984). |
    | `public_keystore_spaceid` | The 128-bit [Universally Unique IDentifier (UUID)](https://www.cryptosys.net/pki/uuid-rfc4122.html) of the public keystore. You can generate the UUID with a third-party tool, such as [UUID generator](https://www.uuidgenerator.net/). \n \n {{site.data.keyword.hscrypto}} provides you with two database-backed EP11 keystores for enhanced security and better user access management: the private keystore that only the normal user type can access and the public keystore that all user types can access. The UUID must be different from the UUID specified for the `private_keystore_spaceid` parameter. \n \n **Important:** The UUID string value must match the UUID string used to set up access policies for the anonymous user. See [anonymous user access policy creation](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access#assign-custom-role-anonymous-user-service). |
    | `apikey_for_anonymous_user` | The service ID API key that you create for the anonymous user type in the [previous prerequisites step](#prerequisite-pkcs-api). |
    | `logging_level` | The supported logging levels, in an increasing order of verboseness: `panic`, `fatal`, `error`, `warning`/`warn`, `info`, `debug`, and `trace`. The Default value is `warning`. |
    | `log_file_path` | The full path of your logging file. It saves all the logs that are generated when your applications interact with the {{site.data.keyword.hscrypto}} cloud HSM to execute PKCS #11 functions. |
    {: caption="Table 1. Describes the variables needed to create the PKCS #11 configuration file" caption-side="bottom"}

    To encrypt and authenticate the keystore that is used by PKCS #11, enable the `sessionauth` parameter and configure the password for the keystore. For each service instance, a maximum of five authenticated keystores are supported. The password can be 6-8 characters. The keystore passwords are not stored in the service instance. You, as the keystore administrator, are responsible for maintaining a local copy of the passwords. If a password is lost, you need to contact IBM Support to reset the keystore, which means all data in the keystore is cleared.
    {: note}

2. Move the configuration file into the same directory as the application (for example, pkcs11-tool) that uses the PKCS #11 library. Optionally, the PKCS #11 configuration file can be placed in the `/etc/ep11client` directory. Create the `/etc/ep11client` directory if it does not exist.

## Step 4: Use the PKCS #11 library to make PKCS #11 API calls
{: #step4-use-pkcs-library}

After you set up the library and the configuration file, the keystores must be initialized. To initialize the keystores, the security officer (SO) user needs to perform a `C_InitToken` operation.
{: important}

After the keystores are initialized, use the PKCS #11 library to call the standard PKCS #11 functions to generate, store, and list keys. For the detailed list of supported PKCS #11 functions, see [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).

Depending on features and security requirements of your application, pass different service ID API keys that you created in the [previous prerequisites step](#prerequisite-pkcs-api) so that your applications can perform the corresponding operations. For example, if your application needs to delete a keystore, provide the SO user API key. If your application needs to access the private keystore to store new keys, you need to provide the normal user API key. For more information about user access management for the PKCS #11 API, see [Best practices for setting up PKCS #11 user types](/docs/hs-crypto?topic=hs-crypto-best-practice-pkcs11-access).

If you are running a Java PKCS #11 application using the SunPKCS11 provider on the IBM Z (s390x) platform, make sure that you use the latest IBM Semeru JVM and specify the `-Xjit:noResumableTrapHandler` Java option when starting your application. You can download the latest s390x version of the IBM Semeru JVM by changing the **Architecture** filter field to **s390x** on the [IBM Semeru Runtime Downloads page](https://developer.ibm.com/languages/java/semeru-runtimes/downloads/?license=IBM){: external}.
{: note}

## What's next
{: #set-up-pkcs-api-next-steps}

- Check out the tutorial that shows how to [use {{site.data.keyword.hscrypto}} PKCS #11 library for Oracle Database Transparent Database Encryption](/docs/hs-crypto?topic=hs-crypto-tutorial-tde-pkcs11) to better understand the PKCS #11 library usage.
- Check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) for the detailed information about cryptographic functions.
