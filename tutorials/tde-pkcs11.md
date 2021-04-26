---

copyright:
  years: 2020, 2021
lastupdated: "2021-04-26"

keywords: encrypt Oracle Transparent Database, database encryption, PKCS11, Db2 native encryption using PKCS11

subcollection: hs-crypto

content-type: tutorial
services: hs-crypto
account-plan: paid
completion-time: 2h

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
{:step: data-tutorial-type='step'}

# Tutorial: Using {{site.data.keyword.hscrypto}} PKCS #11 for Oracle Transparent Database Encryption
{: #tutorial-tde-pkcs11}
{: toc-content-type="tutorial"}
{: toc-completion-time="2h"}

Transparent Data Encryption (TDE) is a well-established technology to encrypt sensitive data in databases. TDE is supported by various popular database systems, both in the cloud and on premises, like Oracle&reg; database. With TDE, a database system encrypts data on database storage media, such as tablespaces and files, and on backup media. The database system automatically and transparently encrypts and decrypts data when it is used by authorized users and applications. Database users do not need to be aware of TDE and database applications do not need to be adapted specifically for TDE.
{: shortdesc}

Typically, TDE uses a two-tiered key hierarchy, composed of a TDE master encryption key and a TDE data encryption key. The TDE data encryption key is used to encrypt and decrypt data, while the TDE master encryption key is used to encrypt and decrypt the TDE data encryption key.

One important question when planning for TDE therefore is: Where do you keep the TDE master encryption key, and how do you secure it?

## Objectives
{: #tutorial-tde-objectives}

This tutorial shows how you can keep complete and exclusive control of your TDE master encryption keys by storing them in {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}. For this purpose, you need to use the PKCS #11 integration feature of {{site.data.keyword.hscrypto}}.



With this tutorial, you are going to implement the setup that is depicted in the following illustration.

![Transparent Database Encryption using the standard PKCS #11 API](../images/pkcs_database.svg "Transparent Database Encryption using the standard PKCS #11 API"){: caption="Figure 1. Transparent Database Encryption using the standard PKCS #11 API" caption-side="bottom"}

In this setup, the Oracle Database is to call operations to manage the TDE master encryption keys on the {{site.data.keyword.hscrypto}} PKCS #11 library. The {{site.data.keyword.hscrypto}} PKCS #11 library interacts with your {{site.data.keyword.hscrypto}} instance, which provides the best of class technology for storing and managing your TDE master encryption keys.

## Before you begin
{: #tutorial-tde-prerequisites}

To complete this tutorial, you need to meet the following prerequisites:

- [Sign up an {{site.data.keyword.cloud_notm}} account](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts#signing_required_accounts-cloud)
- [Provision a {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-provision)

## Task flow
{: #tutorial-tde-steps}

To complete this solution, we'll walk through the following steps:

1. [Initialize your {{site.data.keyword.hscrypto}} instance](#tutorial-tde-initialize)
1. [Set up the {{site.data.keyword.hscrypto}} PKCS #11 library in your Oracle Database environment](#tutorial-tde-pkcs11-setup)
1. [Set up Oracle Database TDE and encrypt your data](#tutorial-dte-encrypt)

Let's start with the {{site.data.keyword.hscrypto}} instance initialization process.

## Initialize your {{site.data.keyword.hscrypto}} instance
{: #tutorial-tde-initialize}
{: step}

1. For this tutorial, you need to [initialize a {{site.data.keyword.hscrypto}} instance first](/docs/hs-crypto?topic=hs-crypto-initialize-hsm).

  Note down the ID of your {{site.data.keyword.hscrypto}} instance and the EP11 endpoint address. You need this information for the subsequent steps.

2. Generate an API key for accessing your {{site.data.keyword.hscrypto}} instance. Run the following command to create an API key for your {{site.data.keyword.cloud_notm}} account:

```
ibmcloud iam api-key-create apikeyhpcs -d "API key for {{site.data.keyword.hscrypto}} PKCS11"
```
{: codeblock}

3. Save the value of the API key for subsequent steps.

## Set up the {{site.data.keyword.hscrypto}} PKCS #11 library in your Oracle Database environment
{: #tutorial-tde-pkcs11-setup}
{: step}

### 1. Set up the Oracle Database
{: #tutorial-tde-db-setup}

You need an Oracle Database Enterprise Edition installation with Oracle Advanced Security.
This tutorial uses a single instance Oracle Database 19.3 Enterprise Edition Docker container. See [Oracle Database on Docker](https://github.com/oracle/docker-images/tree/master/OracleDatabase){: external} for further information about Oracle Database containers and instructions on building a respective container.

1. Start the Oracle Database container:
  ```
  docker run --name oradb -p 1521:1521 -p 5500:5500 -e ORACLE_PWD=password oracle/database:19.3.0-ee
  ```
  {: codeblock}

  Wait until instance and database creation are completed.

2. Run the following command from a command line on your host system:
  ```
  docker exec -it --user root --workdir / oradb bash
  ```
  {: codeblock}

  This shell will be used to run the commands as `root` for the subsequent steps.

### 2. Configure the {{site.data.keyword.hscrypto}} PKCS #11 library
{: #tutorial-tde-library-setup}

Now create a configuration file for the {{site.data.keyword.hscrypto}} PKCS #11 feature.
The configuration file is named `grep11client.yaml`.

Adapt the following file template and name the file `grep11client.yaml`:
- Replace `<instance_id>` with the ID of your {{site.data.keyword.hscrypto}} instance
- Replace `<EP11_endpoint_URL>` and `<EP11_endpoint_port_number>` with the respective parameters of the EP11 endpoint address of your {{site.data.keyword.hscrypto}} instance
- Replace `<your_api_key>` with the value of the API key that you created previously

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
      # The EP11 endpoint address starting from 'ep11'.
      # For example: "ep11.us-south.hs-crypto.cloud.ibm.com"
      address: "<EP11_endpoint_URL>"
      # The EP11 endpoint port number
      port: "<EP11_endpoint_port_number>"
      tls:
        # Grep11 requires TLS connection.
        enabled: true
        # Grep11 requires server only authentication, so 'mutual' should be set as 'false'.
        mutual: false
        # 'cacert' is a full-path certificate file.
        # In Linux with the 'ca-ca-certificates' package installed, this is normally not needed.
        cacert:
        # Grep11 requires the server-only authentication, so 'certfile' and 'keyfile' should be empty.
        certfile:
        keyfile:
    storage:
      filestore:
        enabled: false
        storagepath:
        # 'remotestore' should be enabled if you want to generate keys with the attribute CKA_TOKEN.
      remotestore:
        enabled: true
    users:
      0: # The index of the Security Officer (SO) user MUST be 0.
        # The name for the Security Officer (SO) user. For example: "Administrator".
        # NEVER put the API key under the SO user for security reasons.
        name: "Administrator"
        iamauth:
          <<: *defaultiamcredential
      1: # The index of the normal user MUST be 1.
        # The name for the normal user. For example: "Normal user".
        # NEVER put the API key under the normal user for security reasons.
        name: "Normal user"
         # The Space ID is a 128-bit UUID and can be chosen freely.
         # The UUID can be generated by third-party tools, such as 'https://www.uuidgenerator.net/'.
         # For example: "f00db2f1-4421-4032-a505-465bedfa845b".
         # 'tokenspaceID' under the normal user is to identify the private keystore.
        tokenspaceID: "f00db2f1-4421-4032-a505-465bedfa845b"
        iamauth:
          <<: *defaultiamcredential
      2: # The index of the anonymous user MUST be 2.
        # The name for the anonymous user. For example: "Anonymous".
        name: "Anonymous"
        # The Space ID is a 128-bit UUID and can be chosen freely.
        # The UUID can be generated by third-party tools, such as 'https://www.uuidgenerator.net/'.
        # For example: "ca22be26-b798-4fdf-8c83-3e3a492dc215".
        # 'tokenspaceID' under the anonymous user is to identify the public keystore.
        tokenspaceID: "ca22be26-b798-4fdf-8c83-3e3a492dc215"
        iamauth:
          <<: *defaultiamcredential
          # This API key for the Anonymous user must be provided.
          # It will overide the 'apikey' in the previous defaultcredentials.iamauth.apikey field
          apikey: "<your_api_key>"
logging:
  # Set the logging level.
  # The supported levels, in an increasing order of verboseness, are:
  # 'panic', 'fatal', 'error', 'warning'/'warn', 'info', 'debug', 'trace'.
  # The Default value is 'debug'.
  loglevel: debug
  # The full path of your logging file.
  # For example: /tmp/grep11client.log
  logpath: /tmp/grep11client.log

```
{: codeblock}

### 3. Install the {{site.data.keyword.hscrypto}} PKCS #11 library
{: #tutorial-tde-install-library}

1. [Download the latest PKCS #11 library](https://github.com/IBM-Cloud/hpcs-pkcs11/releases){: external}.

2. Copy the previously created configuration file `grep11client.yaml` and the PKCS #11 library `pkcs11-grep11-<platform>.so.<version>` into the home folder in your Oracle Database container.

3. Run the following commands as `root` to install the {{site.data.keyword.hscrypto}} PKCS #11 library in your Oracle Database setup.

  ```linux
  mkdir /etc/ep11client
  chmod a+rx /etc/ep11client/
  cp grep11client.yaml /etc/ep11client/grep11client.yaml
  chmod a+r /etc/ep11client/grep11client.yaml

  mkdir -p /opt/oracle/extapi/64/hsm/ibm
  cp pkcs11-grep11.so.1.1.3 /opt/oracle/extapi/64/hsm/ibm/pkcs11-grep11.so
  chown -R oracle:oinstall /opt/oracle/extapi

  touch /tmp/grep11client.log
  chmod a+rw /tmp/grep11client.log
  chown oracle:oinstall /tmp/grep11client.log
  ```
  {: codeblock}

The directory `/opt/oracle/extapi/64/hsm` and the subdirectories can contain only one library file. Remove any other library files that exist in that directory and the subdirectories.
{: note}

### 4. Check the library setup
{: #tutorial-tde-library-check}

1. Install the command-line utility OpenSC (pkcs11-tool) with the following command:

  ```linux
  sudo yum install opensc
  ```
  {: codeblock}

2. Run the following command as `root` to check the library setup:

  ```linux
  pkcs11-tool --module=/opt/oracle/extapi/64/hsm/ibm/pkcs11-grep11.so -I
  ```
  {: codeblock}

  This command prints information about the manufacturer and the library, for example:

   ```
  Cryptoki version 2.40
  Manufacturer     IBM ...
  Library          GREP11 PKCS11 client ...
  ```
  {: codeblock}

### 5. Initialize the {{site.data.keyword.hscrypto}} PKCS #11 library
{: #tutorial-tde-initialize-library}

1. Run the following command from a command line on your host system:

  ```
  docker exec -it oradb bash
  ```
  {: codeblock}

  This shell will be used to run the commands as user `oracle` for the subsequent steps.

2. To initialize a token, run the following commands and replace `<your_api_key>` by the API key that you created.

  ```
  pkcs11-tool  --module /opt/oracle/extapi/64/hsm/ibm/pkcs11-grep11.so --init-token --label dbtoken --so-pin=<your_api_key>
  ```
  {: codeblock}

  This command prints the following status message, for example:

  ```
  Using slot 0 with a present token (0x0)
  Token successfully initialized
  ```
  {: codeblock}

## Set up Oracle Database TDE and encrypt your data
{: #tutorial-dte-encrypt}
{: step}

Now let's take on the role of the database administrator.

1. Update file 'sqlnet.ora' in directory '$ORACLE_HOME/network/admin' by adding line:

  ```
  encryption_wallet_location=(source=(method=hsm))
  ```
  {: codeblock}

  To do so you can for example run the following command:
  ```
  echo "encryption_wallet_location=(source=(method=hsm))" >> $ORACLE_HOME/network/admin/sqlnet.ora
  ```
  {: codeblock}

  Make sure that file 'sqlnet.ora' does not contain another setting for `encryption_wallet_location`.
  {: note}

2. Open the keystore with the following command. Replace `<your_api_key>` by the API key you created:

  ```sql
  export ORACLE_SID=<your SID, e.g. ORCLCDB>
  sqlplus / as sysdba
  SQL> ADMINISTER KEY MANAGEMENT SET KEYSTORE OPEN IDENTIFIED BY "<your_api_key>" CONTAINER=ALL;
  ```
  {: codeblock}

3. Create the master keys with the following command. Replace `<your_api_key>` by the API key you created:

  ```sql
  SQL> ADMINISTER KEY MANAGEMENT SET KEY IDENTIFIED BY "<your_api_key>" WITH BACKUP CONTAINER=ALL;
  ```
  {: codeblock}

4. create an encrypted tablespace with the following command:

  ```sql
  SQL> CREATE TABLESPACE encrypted_ts DATAFILE 'tbs1_data.dbf' SIZE 128K AUTOEXTEND ON NEXT 64K ENCRYPTION USING 'AES256' DEFAULT STORAGE(ENCRYPT);
  ```
  {: codeblock}

5. To verify the setup, you can create a table in the encrypted tablespace and insert some test data:

  ```sql
  SQL> CREATE TABLE tde_ts_test (id    NUMBER(10), data  VARCHAR2(50)) TABLESPACE encrypted_ts;
  SQL> INSERT INTO tde_ts_test VALUES (1, 'This is a secret!');
  SQL> COMMIT;
  SQL> SELECT * FROM TDE_TS_TEST;
  ```
  {: codeblock}

6. You can also create a table with an encrypted column and insert some test data:

  ```sql
  SQL> CREATE USER C##test IDENTIFIED BY test;
  SQL> GRANT UNLIMITED TABLESPACE TO C##test;
  SQL> CREATE TABLE C##test.tde_test (id NUMBER(10), data VARCHAR2(50) ENCRYPT);
  SQL> INSERT INTO C##test.tde_test VALUES (1, 'This is also a secret!');
  SQL> COMMIT;
  SQL> SELECT * FROM C##test.tde_test;

  # Verify encrypted tablespace and encrypted column
  SQL> SELECT TABLESPACE_NAME, ENCRYPTED FROM DBA_TABLESPACES;
  SQL> SELECT * FROM dba_encrypted_columns ;
  ```
  {: codeblock}

## Next steps
{: #tutorial-tde-summary}

Your sensitive data is now stored safely in encrypted tablespaces and encrypted columns. And the TDE master encryption key is kept in {{site.data.keyword.hscrypto}} in a highly secure and tamper-proof manner.

In this tutorial, you learned how to set up Oracle Database TDE with {{site.data.keyword.hscrypto}}.

- Learn more about [PKCS #11](/docs/hs-crypto?topic=hs-crypto-pkcs11-intro).
- Learn more about the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
- [Start to use the PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api).
