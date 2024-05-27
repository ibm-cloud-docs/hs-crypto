---

copyright:
  years: 2018, 2024
lastupdated: "2024-05-27"

keywords: hpcs cli, hyper protect crypto services cli, trusted key entry plug-in, cloud tke, tke plug-in, cli plug-in, tke commands, cloud tke reference, cert manager cli plug-in, key management cli, uko cli, united key orchestrator cli

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} CLI
{: #hpcs-cli-plugin}

{{site.data.keyword.hscrypto}} provides multiple {{site.data.keyword.cloud}} CLI plug-ins for you to perform actions toward your service instances: key management CLI plug-in, Trusted Key Entry (TKE) CLI plug-in, certificate manager CLI plug-in, and {{site.data.keyword.uko_full_notm}} (UKO) CLI plug-in.
{: shortdesc}

## {{site.data.keyword.hscrypto}} key management CLI plug-in
{: #kp-cli-plugin}

{{site.data.keyword.hscrypto}} integrates with the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in so that you can use the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in to manage root keys and standard keys in your {{site.data.keyword.hscrypto}} instances.

- For how to set up the {{site.data.keyword.keymanagementserviceshort}} CLI plug-in for {{site.data.keyword.hscrypto}}, see [Performing key management operations with the CLI](/docs/hs-crypto?topic=hs-crypto-set-up-cli).
- For the complete key management CLI reference, see [{{site.data.keyword.keymanagementserviceshort}} CLI command reference](/docs/key-protect?topic=key-protect-key-protect-cli-reference).

## {{site.data.keyword.hscrypto}} Trusted Key Entry CLI plug-in
{: #tke-cli-plugin}

You can use the TKE CLI plug-in to manage crypto units that are assigned to your account.

### Installing the TKE CLI plug-in
{: #install-tke-cli-plugin}

To install the TKE CLI plug-in, follow these steps:

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cloud-cli-getting-started){: external}.

    {{site.data.keyword.cloud_notm}} CLI requires Java&trade; 1.8.0. The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.

2. Install the latest TKE plug-in with the following command:

    ```
    ibmcloud plugin install tke
    ```
    {: pre}

    You are notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
    {: tip}

3. Set the environment variable `CLOUDTKEFILES` on your workstation. Specify a directory where you want workstation files and signature workstation files to be created and saved. Create the directory if it does not exist.

    - On the Linux&trade; operating system or MacOS, add the following line to the `.bash_profile` file:

        ```
        export CLOUDTKEFILES=<path>
        ```
        {: pre}

        For example, you can specify the *path* to `/Users/tke-files`.

    - On the Windows&trade; operating system, in **Control Panel**, type `environment variable` in the search box to locate the Environment Variables window. Create a CLOUDTKEFILES environment variable and set the value to the path to the key files. For example, `C:\users\tke-files`.

    The private endpoint URL is returned in `private`. For key management endpoint, use the value that is returned in the `kms` section. The KP_PRIVATE_ADDR environment variable is used to set the API endpoint URL both for public endpoint and private endpoint. If you want to use the public endpoint, make sure to set the KP_PRIVATE_ADDR environment variable as the public endpoint URL that is returned in the `public` field in the `kms` section.
    {: important}

### TKE CLI plug-in commands
{: #tke-commands-usage}

| Command name | Description | Example |
| ------------ | ----------- | ------- |
| `tke auto-init` | Automatically initializes the service instance. | `ibmcloud tke auto-init` |
| `tke auto-mk-rotate` | Automatically rotates the master key with a randomly generated master key value in the recovery HSM. | `ibmcloud tke auto-mk-rotate` |
| `tke auto-recover` | Automatically copies the current master key value from the recovery HSM to other crypto units in the same resource group. | `ibmcloud tke auto-recover` |
| `tke` | Manages crypto units in the IBM Cloud. | `ibmcloud tke` |
| `tke cryptounit-add` | Adds crypto units to the set of crypto units to work with. | `ibmcloud tke cryptounit-add` |
| `tke cryptounit-admin-add` | Adds a crypto unit administrator to the selected crypto units. | `ibmcloud tke cryptounit-admin-add` |
| `tke cryptounit-admin-rm` | Removes a crypto unit administrator from the selected crypto units. | `ibmcloud tke cryptounit-admin-rm` |
| `tke cryptounit-admins` | Lists administrators installed in the selected crypto units. | `ibmcloud tke cryptounit-admins` |
| `tke cryptounit-compare` | Compares configuration settings of the selected crypto units. | `ibmcloud tke cryptounit-compare` |
| `tke cryptounit-cp-btc`|Enables bitcoin (BTC) related functions in the selected crypto units.|`ibmcloud tke cryptounit-cp-btc`|
| `tke cryptounit-cp-eddsa`|Enables Edwards-curve digital signature algorithms (EdDSA) functions in the selected crypto units.|`ibmcloud tke cryptounit-cp-eddsa`|
| `tke cryptounit-cp-sig-other`| Enables non-Elliptic-curve DSA, non-Edwards-curve DSA digital signature functions in the selected crypto units.|`ibmcloud tke cryptounit-cp-sig-other`|
| `tke cryptounit-exit-impr` | Exits imprint mode in the selected crypto units. (**Deprecated.** Use `cryptounit-thrhld-set` instead.) | `ibmcloud tke cryptounit-exit-impr` |
| `tke cryptounit-mk` | Displays master key registers for the selected crypto units. | `ibmcloud tke cryptounit-mk` |
| `tke cryptounit-mk-clrcur` | Clears the current master key register. | `ibmcloud tke cryptounit-mk-clrcur` |
| `tke cryptounit-mk-clrnew` | Clears the new master key register. | `ibmcloud tke cryptounit-mk-clrnew` |
| `tke cryptounit-mk-commit` | Commits the new master key register. | `ibmcloud tke cryptounit-mk-commit` |
| `tke cryptounit-mk-load` | Loads the new master key register. | `ibmcloud tke cryptounit-mk-load` |
| `tke cryptounit-mk-rotate` | Promotes the master key in the new master key register to the current master key register after rewrapping root keys and encryption keys in the key management keystore. | `ibmcloud tke cryptounit-mk-rotate` |
| `tke cryptounit-mk-setimm` | Does set immediate on the master key registers. | `ibmcloud tke cryptounit-mk-setimm` |
| `tke cryptounit-rm` | Removes crypto units from the set of crypto units to work with. | `ibmcloud tke cryptounit-rm` |
| `tke cryptounit-thrhld-set` | Sets the signature thresholds for the selected crypto units. | `ibmcloud tke cryptounit-thrhld-set` |
| `tke cryptounit-thrhlds` | Displays signature thresholds for the selected crypto units. | `ibmcloud tke cryptounit-thrhlds` |
| `tke cryptounit-zeroize` | Zeroizes the selected crypto units. | `ibmcloud tke cryptounit-zeroize` |
| `tke cryptounits` | Displays the crypto units for the current resource group. | `ibmcloud tke cryptounits` |
| `tke failover-enable`   | Enable or add failover crypto units after you provision a service instance.  | `ibmcloud tke failover-enable`  |
| `tke mk-add` | Creates and saves a new EP11 master key part. | `ibmcloud tke mk-add` |
| `tke mk-rm` | Removes an EP11 master key part from this workstation. | `ibmcloud tke mk-rm` |
| `tke mks` | Lists EP11 master key parts that are stored on this workstation. | `ibmcloud tke mks` |
| `tke sigkey-add` | Generates and saves a new signature key. | `ibmcloud tke sigkey-add` |
| `tke sigkey-rm` | Removes a signature key from this workstation. | `ibmcloud tke sigkey-rm` |
| `tke sigkey-sel` | Selects the signature keys to use to sign commands. | `ibmcloud tke sigkey-sel` |
| `tke sigkeys` | Lists the signature keys that are stored on this workstation. | `ibmcloud tke sigkeys` |
| `tke help`, `tke h` | Shows help. | `ibmcloud tke help` |
{: caption="Table 1. Describes the TKE CLI plug-in commands" caption-side="top"}

For more information on each command, run the following command in the TKE CLI plug-in:

```
ibmcloud tke help <command_name>
```
{: pre}

## {{site.data.keyword.hscrypto}} certificate manager CLI plug-in
{: #cert-manager-cli-plugin}

For {{site.data.keyword.hscrypto}} Standard Plan, you can use the certificate manager CLI plug-in to manage certificates and administrator signature keys for [the second layer of authentication in GREP11 or PKCS #11 API connections](/docs/hs-crypto?topic=hs-crypto-enable-authentication-ep11).

### Installing the certificate manager CLI plug-in
{: #install-cert-manager-cli-plugin}

To install the certificate manager CLI plug-in, follow these steps:

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.

    {{site.data.keyword.cloud_notm}} CLI requires Java&trade; 1.8.0. The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.

2. Install the latest certificate manager plug-in with the following command:

    ```
    ibmcloud plugin install hpcs-cert-mgr
    ```
    {: pre}

    You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
    {: tip}

### Certificate manager CLI plug-in commands
{: #cert-manager-commands-usage}

The following lists all the available certificate manager CLI commands and their corresponding usage. Use `-h` or `--help` for help information.

#### hpcs-cert-mgr adminkey get
{: #command-cert-manager-get-admin-key}

Use this command to retrieve the administrator signature key of the certificate administrator.

```
ibmcloud hpcs-cert-mgr adminkey get --crn HPCS_CRN [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

    ```
    export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
    ```
    {: pre}

    ```
    ibmcloud hpcs-cert-mgr adminkey get --crn ${HPCS_CRN}
    ```
    {: pre}

- Output

  The command returns the output similar to the following example:

    ```
    connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
    +------------+--------+
    | PROPERTIES | VALUES |
    +------------+--------+
    | PublicKey  |        |
    +------------+--------+

    command completed successfully.
    ```
    {: screen}

#### hpcs-cert-mgr adminkey set
{: #command-cert-manager-set-admin-key}

Use this command to create the administrator signature key for the certificate administrator to connect to the certificate manager server.

```
ibmcloud hpcs-cert-mgr adminkey set --crn HPCS_CRN [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

  ```
  export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
  ```
  {: pre}

  ```
  ibmcloud hpcs-cert-mgr adminkey set --crn ${HPCS_CRN}
  ```
  {: pre}

- Output

  The command returns the output similar to the following example:

  ```
  connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
  +------------+-----------------------------------------------------------------------------------+
  | KEYTYPE    | FILE                                                                              |
  +------------+-----------------------------------------------------------------------------------+
  | PrivateKey | /Users/username/.hpcs-cert-mgr-cfg/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.priv  |
  | PublicKey  | /Users/username/.hpcs-cert-mgr-cfg/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.pub   |
  +------------+-----------------------------------------------------------------------------------+

  An automatically generated keypair is stored locally and configured to node remotely, please keep the keypair carefully!!!

  command completed successfully.
  ```
  {: screen}

#### hpcs-cert-mgr adminkey update
{: #command-cert-manager-update-admin-key}

Use this command to refresh and update the administrator signature key for the certificate administrator.

```
ibmcloud hpcs-cert-mgr adminkey update --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --admin-priv-key ADMIN_PRIV_KEY
    :   Required. The file path of the existing private key that is stored on your local workstation. The private key is used to sign this command action toward your instance certificate manager server.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

  ```
  export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
  ```
  {: pre}

  ```
  export ADMIN_PRIV_KEY=/Users/admin1/.hpcs-cert-mgr-cfg/44de77d2-599b-0089-2f0f-bad8d1c94a7c.priv
  ```
  {: pre}

  ```
  ibmcloud hpcs-cert-mgr adminkey update --crn ${HPCS_CRN} --admin-priv-key ${ADMIN_PRIV_KEY}
  ```
  {: pre}

- Output

  The command returns the output similar to the following example:

  ```
  connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
  +------------+-----------------------------------------------------------------------------------+
  | KEYTYPE    | FILE                                                                              |
  +------------+-----------------------------------------------------------------------------------+
  | PrivateKey | /Users/username/.hpcs-cert-mgr-cfg/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.priv  |
  | PublicKey  | /Users/username/.hpcs-cert-mgr-cfg/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX.pub   |
  +------------+-----------------------------------------------------------------------------------+

  An automatically generated keypair is stored locally and configured to node remotely, please keep the keypair carefully!!!

  command completed successfully.
  ```
  {: screen}

#### hpcs-cert-mgr adminkey delete
{: #command-cert-manager-delete-admin-key}

Use this command to delete the administrator signature key for the certificate administrator.

```
ibmcloud hpcs-cert-mgr adminkey delete --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --admin-priv-key ADMIN_PRIV_KEY
    :   Required. The file path of your current private key that is stored on your local workstation. The private key is used to sign this command action toward your instance certificate manager server.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

  ```
  export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
  ```
  {: pre}

  ```
  export ADMIN_PRIV_KEY=/Users/admin1/.hpcs-cert-mgr-cfg/44de77d2-599b-0089-2f0f-bad8d1c94a7c.priv
  ```
  {: pre}

  ```
  ibmcloud hpcs-cert-mgr adminkey delete --crn ${HPCS_CRN} --admin-priv-key ${ADMIN_PRIV_KEY}
  ```
  {: pre}

- Output

  The command returns the output similar to the following example:

  ```
  connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
  command completed successfully.
  ```
  {: screen}

#### hpcs-cert-mgr cert get
{: #command-cert-manager-get-cert}

Use this command to retrieve the client certificate on your instance certificate manager server.

```
ibmcloud hpcs-cert-mgr cert get --crn HPCS_CRN --cert-id CERT_ID [--cert-store-file CERT_FILE] [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --cert-id CERT_ID
    :   Required. The string ID of the client certificate that you want to retrieve.

    --cert-store-file CERT_FILE
    :   Optional. The file path to store the retrieved certificate. If you specify this option, the file is created on your local workstation and stores the certificate content.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

  ```
  export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
  ```
  {: pre}

  ```
  ibmcloud hpcs-cert-mgr cert get --crn ${HPCS_CRN} --cert-id testcert --cert-store-file c/b/cert.pem
  ```
  {: pre}

- Output

  The command returns the output similar to the following example:

  ```
  connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
  ------------------ The returned certification ------------------
  -----BEGIN CERTIFICATE-----
  MIIFazCCA10gAwIBAgIUVW/gPwBtOKHEwCL.........
  ............................................
  ............................................
  ................................FkQF0tfc6cg=
  -----END CERTIFICATE-----

  command completed successfully.
  ```
  {: screen}

#### hpcs-cert-mgr cert set
{: #command-cert-manager-set-cert}

Use this command to set client certificates for your instance certificate manager server.

```
ibmcloud hpcs-cert-mgr cert set --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY --cert-id CERT_ID --cert CERT_FILE [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --admin-priv-key ADMIN_PRIV_KEY
    :   Required. The file path of your current private key that is stored on your local workstation. The private key is used to sign this command action toward your instance certificate manager server.

    --cert-id CERT_ID
    :   Required. The string ID that you want to assign to the certificate for easy identification.

    --cert CERT_FILE
    :   Required. The certificate file that is stored on your workstation. It is suggested to use the {{site.data.keyword.cloud_notm}} Certificate Manager to order and manage SSL/TLS certificates for your applications and services.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

  ```
  export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
  ```
  {: pre}

  ```
  export CERT=/Users/admin1/cert.pem
  ```
  {: pre}

  ```
  export ADMIN_PRIV_KEY=/Users/admin1/.hpcs-cert-mgr-cfg/44de77d2-599b-0089-2f0f-bad8d1c94a7c.priv
  ```
  {: pre}

  ```
  ibmcloud hpcs-cert-mgr cert set --crn ${HPCS_CRN} --admin-priv-key ${ADMIN_PRIV_KEY} --cert-id testcert --cert ${CERT}
  ```
  {: pre}

- Output

  The command returns the output similar to the following example:

  ```
  connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
  command completed successfully.
  ```
  {: screen}

#### hpcs-cert-mgr cert list
{: #command-cert-manager-list-cert}

Use this command to list all the certificates that are managed by the administrator for your instance certificate manager server.

```
ibmcloud hpcs-cert-mgr cert list --crn HPCS_CRN [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

  ```
  export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
  ```
  {: pre}

  ```
  ibmcloud hpcs-cert-mgr cert list --crn ${HPCS_CRN}
  ```
  {: pre}

- Output

  The command returns the output similar to the following example:

  ```
  connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
  +------------+----------------------------------------+
  | CERTID     | CERT                                   |
  | testcert   | -----BEGIN CERTIFICATE-----            |
  |            | MIIFazCCA10gAwIBAgIUVW/gPwBtOKHEwCL....|
  |            |........................................|
  |            |............................FkQF0tfc6cg=|
  |            | -----END CERTIFICATE-----              |
  |            |                                        |
  | testcert2  | -----BEGIN CERTIFICATE-----            |
  |            | MIIFazCCA10gAwIBAgIUVW/gPwBtOKHEwCL....|
  |            |........................................|
  |            |............................FkQF0tfc6cg=|
  |            | -----END CERTIFICATE-----              |
  |            |                                        |
  +------------+----------------------------------------+

  command completed successfully.
  ```
  {: screen}

#### hpcs-cert-mgr cert delete
{: #command-cert-manager-delete-cert}

Use this command to delete client certificates for your instance certificate manager server.

```
ibmcloud hpcs-cert-mgr cert delete --crn HPCS_CRN --admin-priv-key ADMIN_PRIV_KEY --cert-id CERT_ID [--private]
```

- Command options

    --crn HPCS_CRN
    :   Required. The `crn` of your {{site.data.keyword.hscrypto}} instance. You can use the `ibmcloud resource service-instances --long` command to retrieve the `crn`.

    --admin-priv-key ADMIN_PRIV_KEY
    :   Required. The file path of your current private key that is stored on your local workstation. The private key is used to sign this command action toward your instance certificate manager server.

    --cert-id CERT_ID
    :   Required. The string ID of the certificate that you want to delete.

    --private
    :   Optional. If you use this option, the certificate manager server URL points to the private network. For example,: `cert-mgr.private.<region>.hs-crypto.cloud.ibm.com:443`. The `region` is the abbreviation of the geographic area where you log in to {{site.data.keyword.cloud_notm}}. In this case, you need to use the private network to connect your service instance.

- Example

  ```
  export HPCS_CRN=crn:v1:staging:public:xxx:yyy:zzz
  ```
  {: pre}

  ```
  export ADMIN_PRIV_KEY=/Users/admin1/.hpcs-cert-mgr-cfg/44de77d2-599b-0089-2f0f-bad8d1c94a7c.priv
  ```
  {: pre}

  ```
  ibmcloud hpcs-cert-mgr cert delete --crn ${HPCS_CRN} --admin-priv-key ${ADMIN_PRIV_KEY} --cert-id testcert
  ```
  {: pre}

- Output

  The command returns the output similar to the following example:

  ```
  connecting to server [cert-mgr.us-south.hs-crypto.cloud.ibm.com:443]...
  command completed successfully.
  ```
  {: screen}

## {{site.data.keyword.hscrypto}} {{site.data.keyword.uko_full_notm}} CLI plug-in
{: #uko-cli-plugin}

You can use the {{site.data.keyword.uko_full_notm}} CLI plug-in to manage vaults, keystores, and managed keys for {{site.data.keyword.hscrypto}} instances with the {{site.data.keyword.uko_full_notm}} plan.

### Installing the {{site.data.keyword.uko_full_notm}} CLI plug-in
{: #install-uko-cli-plugin}

To install the {{site.data.keyword.uko_full_notm}} CLI plug-in, follow these steps:

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started){: external}.

    {{site.data.keyword.cloud_notm}} CLI requires Java&trade; 1.8.0. The prefix for running commands by using the {{site.data.keyword.cloud_notm}} CLI is `ibmcloud`.

2. Install the latest {{site.data.keyword.uko_full_notm}} CLI plug-in with the following command:

    ```
    ibmcloud plugin install hpcs
    ```
    {: pre}

    You're notified on the command line when updates to the {{site.data.keyword.cloud_notm}} CLI and plug-ins are available. Be sure to keep your CLI up to date so that you can use the latest commands. You can view the current version of all installed plug-ins by running `ibmcloud plugin list`.
    {: tip}

3. Set the environment variable `UKO_URL` on your workstation.

    ```
    export UKO_URL=<UKO_endpoint_URL>
    ```
    {: pre}

    Replace `<UKO_endpoint_URL>` with your instance UKO endpoint URL. You can get the endpoint URL on your provisioned service instance UI dashboard through **Overview** &gt; **Connect** &gt; **{{site.data.keyword.uko_full_notm}} endpoint URL**. Or, you can dynamically [retrieve the API endpoint URL](/apidocs/uko#endpoint-urls){: external}. 

### {{site.data.keyword.uko_full_notm}} CLI plug-in commands
{: #uko-commands-usage}

The following lists all the available {{site.data.keyword.uko_full_notm}} CLI commands and their corresponding usage. Use `-h` or `--help` for help information.

#### hpcs uko managed-keys
{: #command-uko-list-managed-keys}

List all managed keys in the instance. It is possible to sort by the following parameters: label, algorithm, state, activation-date, deactivation-date, created-at, updated-at, size, vault-id.

If the `--all-pages` option is not set, the command will only retrieve a single page of the collection.
{: note}

```
ibmcloud hpcs uko managed-keys [--vault-id VAULT-ID] [--algorithm ALGORITHM] [--state STATE] [--limit LIMIT] [--offset OFFSET] [--sort SORT] [--label LABEL] [--activation-date ACTIVATION-DATE] [--activation-date-min ACTIVATION-DATE-MIN] [--activation-date-max ACTIVATION-DATE-MAX] [--deactivation-date DEACTIVATION-DATE] [--deactivation-date-min DEACTIVATION-DATE-MIN] [--deactivation-date-max DEACTIVATION-DATE-MAX] [--expiration-date EXPIRATION-DATE] [--expiration-date-min EXPIRATION-DATE-MIN] [--expiration-date-max EXPIRATION-DATE-MAX] [--created-at CREATED-AT] [--created-at-min CREATED-AT-MIN] [--created-at-max CREATED-AT-MAX] [--updated-at UPDATED-AT] [--updated-at-min UPDATED-AT-MIN] [--updated-at-max UPDATED-AT-MAX] [--rotated-at-min ROTATE-AT-MIN] [--rotated-at-max ROTATE-AT-MAX] [--size SIZE] [--size-min SIZE-MIN] [--size-max SIZE-MAX] [--referenced-keystores-type REFERENCED-KEYSTORES-TYPE] [--referenced-keystores-name REFERENCED-KEYSTORES-NAME] [--instances-keystore-type INSTANCES-KEYSTORE-TYPE] [--template-name TEMPLATE-NAME] [--template-id TEMPLATE-ID] [--template-type TEMPLATE-TYPE] [--managing-systems MANAGING-SYSTEMS]
```

- Command options

    --vault-id ([]string)
    :   Optional. The Universally Unique Identifier (UUID) of the vault. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the UUID. The length must be 36 characters. The list items must match the regular expression `/^[-0-9a-z]+$/`.

    --algorithm ([]string)
    :   Optional. The algorithm of returned keys. Values that can be set are `aes`, `rsa`, `hmac`, `ec`, `des`, and `dilithium`.

    --state ([]string)
    :   Optional. The state that returned keys are to be in. The default value is `["pre_activation","active"]`. Values that can be set are: `pre_activation`, `active`, `deactivated`, `destroyed`, `compromised`, and `destroyed_compromised`.

    --limit (int64)
    :   Optional. The number of keys to retrieve. The maximum value is `1000`. The minimum value is `1`. The default value is `20`.

    --offset (int64)
    :   Optional. The number of keys to skip. The minimum value is `0`.

    --sort ([]string)
    :   Optional. The sorting order. The default value is `["-updated_at"]`. The list items must match regular expression `/^-?[a-z0-9_.\\[\\],-]+$/`.

    --label (string)
    :   Optional. The label of the key. The value must match regular expression `/.+/`.

    --activation-date (string)
    :   Optional. Return only managed keys whose activation date matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --activation-date-min (string)
    :   Optional. Return only managed keys whose activation date is at or after the parameter value. This query parameter cannot be used in conjunction with the `activation_date` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --activation-date-max (string)
    :   Optional. Return only managed keys whose activation date is at or before the parameter value. This query parameter cannot be used in conjunction with the `activation_date` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --deactivation-date (string)
    :   Optional. Return only managed keys whose deactivation date matches the parameter. This query parameter cannot be used in conjunction with the `expiration_date` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --deactivation-date-min (string)
    :   Optional. Return only managed keys whose deactivation date is at or after the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `expiration_date_min`, and `expiration_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --deactivation-date-max (string)
    :   Optional. Return only managed keys whose deactivation date is at or before the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `expiration_date_min`, and `expiration_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --expiration-date (string)
    :   Optional. Return only managed keys whose deactivation date matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --expiration-date-min (string)
    :   Optional. Return only managed keys whose deactivation date is at or after the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `deactivation_date_min`, and `deactivation_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --expiration-date-max (string)
    :   Optional. Return only managed keys whose deactivation date is at or before the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `deactivation_date_min`, and `deactivation_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at (string)
    :   Optional. Return only managed keys whose creation time matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at-min (string)
    :   Optional. Return only managed keys whose creation time is at or after the parameter value. This query parameter cannot be used in conjunction with the `created_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at-max (string)
    :   Optional. Return only managed keys whose creation time is at or before the parameter value. This query parameter cannot be used in conjunction with the `created_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at (string)
    :   Optional. Return only managed keys whose update time matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at-min (string)
    :   Optional. Return only managed keys whose update time is after the parameter value. This query parameter cannot be used in conjunction with the `updated_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at-max (string)
    :   Optional. Return only managed keys whose update time is before the parameter value. This query parameter cannot be used in conjunction with the `updated_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --rotated-at-min (string)
    :   Optional. Return only managed keys whose rotation time is after the parameter value.

    --rotated-at-max (string)
    :   Optional. Return only managed keys whose rotation time is before the parameter value.

    --size (int64)
    :   Optional. The size of the key.

    --size-min (int64)
    :   Optional. The minimum size of the key. This query parameter cannot be used in conjunction with the `size` query parameter.

    --size-max (int64)
    :   Optional. The maximum size of the key. This query parameter cannot be used in conjunction with the `size` query parameter.

    --referenced-keystores-type ([]string)
    :   Optional. Type of referenced keystore. Values that can be set are `aws_kms`, `azure_key_vault`, `ibm_cloud_kms`, `google_kms`, and `cca`.

    --referenced-keystores-name ([]string)
    :   Optional. Name of referenced keystore. The list items must match regular expression `/[^,]+/`.

    --instances-keystore-type ([]string)
    :   Optional. Type of keystore supported by one of the instances. Values that can be set are `aws_kms`, `azure_key_vault`, `ibm_cloud_kms`, `google_kms`, and `cca`.

    --template-name (string)
    :   Return only managed keys whose template name begins with the string.

    --template-id (string[])
    :   Return only managed keys with the given template UUID.

    --template-type (string[])
    :   Return only managed keys with the given template type. Values that can be set are `user_defined`, `shadow`, and `system`.

    --managing-systems
    :   Return only managed keys with the given managing systems. Values that can be set are `web` and `workstation`.

    --all-pages (bool)
    :   Optional. Invoke multiple requests to display all pages of the collection for managed keys.

- Example

    ```
    ibmcloud hpcs uko managed-keys --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "total_count": 4,
      "limit": 20,
      "offset": 0,
      "first": {
        "href": "/v4/managed_keys?vault.id=5295ad47-2ce9-43c3-b9e7-e5a9482c362b&limit=20&offset=0'"
      },
      "last": {
        "href": "/v4/managed_keys?vault.id=5295ad47-2ce9-43c3-b9e7-e5a9482c362b&limit=20&offset=0"
      },
      "managed_keys": [
        {
          "id": "35f690df-064a-4758-8694-b2f011810701",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault-1",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "6393e930-562c-4042-b324-45c37d3d49d9",
            "name": "AZURE-template-920",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/6393e930-562c-4042-b324-45c37d3d49d9"
          },
          "version": "1,",
          "description": "AZURE KEY",
          "label": "AZUREproduction2029",
          "state": "active",
          "size": "2048",
          "algorithm": "rsa",
          "verification_patterns": [
            {
              "method": "PUB-HASH-SHA-1",
              "value\"": "947AA69D48EEE487048AF2999DADB8DA55769529"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "AZURE"
            },
            {
              "name": "ENV",
              "value": "production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "AZURE-TAG"
            }
          ],
          "created_at": "2023-06-05T11:33:54Z",
          "updated_at": "2023-06-05T11:33:54Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "keystore": [
                {
                  "id": "2e124fa5-9ef6-406c-bb2f-9ad049ff1073",
                  "name": "Azure Keystore",
                  "type": "azure_key_vault",
                  "href": "v4/managed_keys/3dab42dc-6941-4841-8d27-4dabcc5aa09e"
                }
              ]
            }
          ],
          "instances": [
            {
              "id": "acb332dd-216c-44dd-8593-02bd2119ec62",
              "label_in_keystore\"": "AZUREproduction2029",
              "keystore": {
                "group": "Production AZURE GB",
                "type": "azure_key_vault"
              },
              "azure_key_protection_level": "software"
            }
          ],
          "href": "/v4/managed_keys/35f690df-064a-4758-8694-b2f011810701",
          "status_in_keystores": [
            {
              "keystore": [
                {
                  "id": "2e124fa5-9ef6-406c-bb2f-9ad049ff1073",
                  "name": "Azure Keystore",
                  "type": "azure_key_vault",
                  "href": "v4/managed_keys/3dab42dc-6941-4841-8d27-4dabcc5aa09e"
                }
              ],
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "d1e2525c-62c8-4df2-9173-69e1a7bc8cdb/d1e2525c-62c8-4df2-9173-69e1a7bc8cdb"
            }
          ]
        },
        {
          "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "EXAMPLE-VAULT",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
            "name": "AWS-EXAMPLE-TEMPLATE",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
          },
          "version": 1,
          "description": "AWS key template description",
          "label": "AWS-production-2029",
          "state": "active",
          "size": 256,
          "algorithm": "aes",
          "verification_patterns": [
            {
              "method\"": "ENC-ZERO",
              "value": "C05CA1"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "AWS"
            },
            {
              "name": "ENV",
              "value": "production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "AWS-TAG"
            }
          ],
          "created_at": "2023-06-05T10:40:13Z",
          "updated_at": "2023-06-05T10:40:19Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "id": "0743ae15-c594-476d-8e9a-1564740ace53",
              "name": "AWS KMS Keystore 335",
              "type": "aws_kms",
              "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
            }
          ],
          "instances": [
            {
              "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
              "label_in_keystore": "AWS-production-2029",
              "type": "secret_key",
              "keystore": {
                "group\"": "Production-AWS-DE",
                "type\"": "aws_kms"
              }
            }
          ],
          "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
          "status_in_keystores": [
            {
              "keystore": {
                "id": "0743ae15-c594-476d-8e9a-1564740ace53",
                "name": "AWS KMS Keystore 335",
                "type": "aws_kms",
                "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
              },
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
            }
          ]
        },
        {
          "id": "0beedc06-4608-48ae-8ae3-8b7bf3c2c39f",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault-2",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "64f98479-392d-4af2-a076-77cc21b8c6f3",
            "name": "IBM-CLOUD-TEMPLATE",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/64f98479-392d-4af2-a076-77cc21b8c6f3"
          },
          "version": 1,
          "description": "",
          "label": "IBMCloudProduction2029",
          "state": "active",
          "size": "256",
          "algorithm": "aes",
          "verification_patterns": [
            {
              "method": "ENC-ZERO",
              "value": "4ADDCB"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "IBMCloud"
            },
            {
              "name": "ENV",
              "value": "Production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "AWS-TAG"
            }
          ],
          "created_at": "2023-06-05T11:59:47Z",
          "updated_at": "2023-06-05T11:59:47Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "id": "0743ae15-c594-476d-8e9a-1564740ace53",
              "name": "IBM CLOUD KEYSTORE",
              "type": "ibm_cloud_kms",
              "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
            }
          ],
          "instances": [
            {
              "id": "0c5b14ea-a3dd-407c-af7c-fd74575ccbad",
              "label_in_keystore": "IBMCloudProduction2029",
              "type": "secret_key",
              "keystore": {
                "group": "Production External GB",
                "type": "ibm_cloud_kms"
              }
            }
          ],
          "href": "/v4/managed_keys/0beedc06-4608-48ae-8ae3-8b7bf3c2c39f",
          "status_in_keystores": [
            {
              "keystore": {
                "id": "0743ae15-c594-476d-8e9a-1564740ace53",
                "name": "IBM CLOUD KEYSTORE",
                "type": "ibm_cloud_kms",
                "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
              },
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "804854d0-4eb7-416e-8ae2-45ba56921c8a/804854d0-4eb7-416e-8ae2-45ba56921c8a"
            }
          ]
        },
        {
          "id": "d7b8204c-4f8f-4ba1-b306-5434ae817f51",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault-3",
            "href": "v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "09d229e5-e330-4e85-a7ee-cc8555d38603",
            "name": "GOOGLE-TEMPLATE-86",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/09d229e5-e330-4e85-a7ee-cc8555d38603"
          },
          "version": 1,
          "description": "Google Key",
          "label": "Google-Production-2029",
          "state": "active",
          "size": "256",
          "algorithm": "aes",
          "verification_patterns": [
            {
              "method\"": "ENC-ZERO",
              "value": "C3F432"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "Google"
            },
            {
              "name": "ENV",
              "value": "Production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "Google-TAG"
            }
          ],
          "created_at": "2023-06-05T13:18:28",
          "updated_at": "2023-06-05T13:18:28Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "id": "6e026faa-d44d-4a1a-aeea-0e1ef2840cba",
              "name": "Google Keystore",
              "type": "google_kms",
              "href": "/v4/keystores/6e026faa-d44d-4a1a-aeea-0e1ef2840cba"
            }
          ],
          "instances": [
            {
              "id": "ed74a984-2057-484c-9198-54839f3fec62",
              "label_in_keystore": "Google-Production-2029",
              "type": "secret_key",
              "keystore": {
                "group": "Production Google",
                "type": "google_kms"
              },
              "google_key_protection_level": "software",
              "google_key_purpose": "encrypt_decrypt",
              "google_kms_algorithm": "google_symmetric_encryption"
            }
          ],
          "href": "/v4/managed_keys/d7b8204c-4f8f-4ba1-b306-5434ae817f51",
          "status_in_keystores": [
            {
              "keystore": {
                "id": "6e026faa-d44d-4a1a-aeea-0e1ef2840cba",
                "name": "Google Keystore",
                "type": "google_kms",
                "href": "/v4/keystores/6e026faa-d44d-4a1a-aeea-0e1ef2840cba"
              },
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "projects/plated-field-364019/locations/europe-west3/keyRings/uko-ring/cryptoKeys/ROBOT-Google-Key-05-06-nciYX/cryptoKeyVersions/1"
            }
          ]
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-create
{: #command-uko-create-managed-key}

Create a new key based on the supplied template. The template must exist in your instance before you can run this command.

```
ibmcloud hpcs uko managed-key-create --template-name TEMPLATE-NAME --vault VAULT --label LABEL [--tags TAGS] [--description DESCRIPTION]
```

- Command options

    --template-name (string)
    :   Required. The name of the key template to use when you create a key. The length must be between 1 and 30 characters. The value must match the regular expression `/^[A-Za-z][A-Za-z0-9-]+$/`.

    --vault ([VaultReferenceInCreationRequest](#uko-vault-reference-in-creation-request-example-schema))
    :   Required. The ID of the vault where the managed key is to be created.

    --label (string)
    :   Required. The label of the key. The length must be between 1 and 255 characters. The value must match the regular expression `/^[A-Za-z0-9._ \/-]+$/`.

    --tags ([Tag\[\]](#uko-tag-example-schema))
    :   Optional. Key-value pairs that are associated with the key. The length must be between 0 and 128 items.

    --description (string)
    :   Optional. The description of the managed key. The length must be between 0 and 200 characters. The value must match the regular expression `/(.|\\n)*/`.

- Example

    ```
    ibmcloud hpcs uko managed-key-create \
      --template-name=IBM-CLOUD-EXAMPLE-TEMPLATE \
      --vault='{"id": "93777bca-baef-4070-b9b5-a2e6079df1b4"}' \
      --label='IBM CLOUD KEY' \
      --tags='[{"name": "first-tag", "value": "for-IBM-CLOUD"}]' \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | Location | String | Path to newly created resource, relative to context root. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "AWS-EXAMPLE-VAULT",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "template": {
        "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
        "name": "AWS-EXAMPLE-TEMPLATE",
        "type": [
          "user_defined"
        ],
        "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
      },
      "version": 1,
      "description": "AWS key template description",
      "label": "AWS-production-2029",
      "state": "active",
      "size": 256,
      "algorithm": "aes",
      "verification_patterns": [
        {
          "method\"": "ENC-ZERO",
          "value": "C05CA1"
        }
      ],
      "activation_date": "2028-07-14",
      "expiration_date": "2029-09-25",
      "label_tags": [
        {
          "name": "APP",
          "value": "AWS"
        },
        {
          "name": "ENV",
          "value": "production"
        },
        {
          "name": "lay",
          "value": "2029"
        }
      ],
      "tags": [
        {
          "name": "TAG-1",
          "value": "AWS-TAG"
        }
      ],
      "created_at": "2023-06-05T10:40:13Z",
      "updated_at": "2023-06-05T10:40:19Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "referenced_keystores": [
        {
          "id": "0743ae15-c594-476d-8e9a-1564740ace53",
          "name": "AWS KMS Keystore 335",
          "type": "aws_kms",
          "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
        }
      ],
      "instances": [
        {
          "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
          "label_in_keystore": "AWS-production-2029",
          "type": "secret_key",
          "keystore": {
            "group\"": "Production-AWS-DE",
            "type\"": "aws_kms"
          }
        }
      ],
      "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
      "status_in_keystores": [
        {
          "keystore": {
            "id": "0743ae15-c594-476d-8e9a-1564740ace53",
            "name": "AWS KMS Keystore 335",
            "type": "aws_kms",
            "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
          },
          "status": "active",
          "keystore_sync_flag": "ok",
          "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
          "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-delete
{: #command-uko-delete-managed-key}

Delete a managed key by key ID from the vault. Make sure that the key is in a _Destroyed_ state before you run this command.

```
ibmcloud hpcs uko managed-key-delete --id ID --if-match IF-MATCH
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

- Example

    ```
    ibmcloud hpcs uko managed-key-delete \
      --id=21a7498e-2ae4-47ee-85ac-a19bf64e92fa \
      --if-match=2022-05-27T10:15:38Z
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    ...
    OK
    ```
    {: screen}

#### hpcs uko managed-key
{: #command-uko-retrieve-a-key}

Retrieve a managed key and its details by specifying the key ID.

```
ibmcloud hpcs uko managed-key --id ID
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

- Example

    ```
    ibmcloud hpcs uko managed-key \
      --id=21a7498e-2ae4-47ee-85ac-a19bf64e92fa \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:
  
    ```
    {
      "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "AWS-EXAMPLE-VAULT",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "template": {
        "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
        "name": "AWS-EXAMPLE-TEMPLATE",
        "type": [
          "user_defined"
        ],
        "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
      },
      "version": 1,
      "description": "AWS key template description",
      "label": "AWS-production-2029",
      "state": "active",
      "size": 256,
      "algorithm": "aes",
      "verification_patterns": [
        {
          "method\"": "ENC-ZERO",
          "value": "C05CA1"
        }
      ],
      "activation_date": "2028-07-14",
      "expiration_date": "2029-09-25",
      "label_tags": [
        {
          "name": "APP",
          "value": "AWS"
        },
        {
          "name": "ENV",
          "value": "production"
        },
        {
          "name": "lay",
          "value": "2029"
        }
      ],
      "tags": [
        {
          "name": "TAG-1",
          "value": "AWS-TAG"
        }
      ],
      "created_at": "2023-06-05T10:40:13Z",
      "updated_at": "2023-06-05T10:40:19Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "referenced_keystores": [
        {
          "id": "0743ae15-c594-476d-8e9a-1564740ace53",
          "name": "AWS KMS Keystore 335",
          "type": "aws_kms",
          "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
        }
      ],
      "instances": [
        {
          "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
          "label_in_keystore": "AWS-production-2029",
          "type": "secret_key",
          "keystore": {
            "group\"": "Production-AWS-DE",
            "type\"": "aws_kms"
          }
        }
      ],
      "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
      "status_in_keystores": [
        {
          "keystore": {
            "id": "0743ae15-c594-476d-8e9a-1564740ace53",
            "name": "AWS KMS Keystore 335",
            "type": "aws_kms",
            "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
          },
          "status": "active",
          "keystore_sync_flag": "ok",
          "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
          "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-update
{: #command-uko-managed-key-update}

Update attributes of a managed key. You can only modify the key's state separately from other changes. Changing a key's state affects its availability for cryptographic operations in keystores.

```
ibmcloud hpcs uko managed-key-update --id ID --if-match IF-MATCH [--label LABEL] [--activation-date ACTIVATION-DATE] [--expiration-date EXPIRATION-DATE] [--tags TAGS] [--description DESCRIPTION]
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

    --label (string)
    :   Required. The label of the key. The length must be between 1 and 255 characters. The value must match the regular expression `/^[A-Za-z0-9._ \/-]+$/`.

    --activation-date (strfmt.Date)
    :   Optional. The activation date must be provided in format YYYY-MM-DD.

    --expiration-date (strfmt.Date)
    :   Optional. The expiration date must be provided in format YYYY-MM-DD.

    --tags ([Tag\[\]](#uko-tag-example-schema))
    :   Optional. Key-value pairs that are associated with the key. The length must be between 0 and 128 items.

    --description (string)
    :   Optional. The description of the managed key. The length must be between 0 and 200 characters. The value must match the regular expression `/(.|\\n)*/`.

- Example

    ```
    ibmcloud hpcs uko managed-key-update \
      --id=21a7498e-2ae4-47ee-85ac-a19bf64e92fa \
      --if-match=2022-05-26T14:18:10Z \
      --description="updated description" \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:
  
    ```
    {
      "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "AWS-EXAMPLE-VAULT",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "template": {
        "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
        "name": "AWS-EXAMPLE-TEMPLATE",
        "type": [
          "user_defined"
        ],
        "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
      },
      "version": 1,
      "description": "AWS key template description",
      "label": "AWS-production-2029",
      "state": "active",
      "size": 256,
      "algorithm": "aes",
      "verification_patterns": [
        {
          "method\"": "ENC-ZERO",
          "value": "C05CA1"
        }
      ],
      "activation_date": "2028-07-14",
      "expiration_date": "2029-09-25",
      "label_tags": [
        {
          "name": "APP",
          "value": "AWS"
        },
        {
          "name": "ENV",
          "value": "production"
        },
        {
          "name": "lay",
          "value": "2029"
        }
      ],
      "tags": [
        {
          "name": "TAG-1",
          "value": "AWS-TAG"
        }
      ],
      "created_at": "2023-06-05T10:40:13Z",
      "updated_at": "2023-06-05T10:40:19Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "referenced_keystores": [
        {
          "id": "0743ae15-c594-476d-8e9a-1564740ace53",
          "name": "AWS KMS Keystore 335",
          "type": "aws_kms",
          "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
        }
      ],
      "instances": [
        {
          "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
          "label_in_keystore": "AWS-production-2029",
          "type": "secret_key",
          "keystore": {
            "group\"": "Production-AWS-DE",
            "type\"": "aws_kms"
          }
        }
      ],
      "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
      "status_in_keystores": [
        {
          "keystore": {
            "id": "0743ae15-c594-476d-8e9a-1564740ace53",
            "name": "AWS KMS Keystore 335",
            "type": "aws_kms",
            "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
          },
          "status": "active",
          "keystore_sync_flag": "ok",
          "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
          "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko associated-resources-for-managed-key
{: #command-uko-associated-resources-key}

Obtain a list of resources associated with a managed key in IBM Cloud. These cloud resources are protected by the key that you specify.

If the `--all-pages` option is not set, the command only retrieves a single page of the collection.
{: note}

```
ibmcloud hpcs uko associated-resources-for-managed-key --id ID [--limit LIMIT] [--offset OFFSET] [--sort SORT]
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --limit (int64)
    :   Optional. The number of resources to retrieve. The value must be between 1 and 1000.

    --offset (int64)
    :   Optional. The number of resources to skip. The minimum value is 0.

    --sort ([]string)
    :   Optional. The sorting order. The default value is `["name"]`. The list items must match the regular expression `/^-?[a-z0-9_.\\[\\],-]+$/`.

    --all-pages (bool)
    :   Optional. Invoke multiple requests to display all pages of the collection for the associated resources.

- Example

    ```
    ibmcloud hpcs uko associated-resources-for-managed-key \
    --id=93777bca-baef-4070-b9b5-a2e6079df1b4 \
    --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "total_count": 3,
      "limit": 20,
      "offset": 0,
      "first": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_key/5295ad47-2ce9-43c3-b9e7-e5a9482c362b/associated_resources?limit=20"
      },
      "last": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_key/5295ad47-2ce9-43c3-b9e7-e5a9482c362b/associated_resources?limit=20&offset=0"
      },
      "previous": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys?offset=80"
      },
      "next": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys?offset=120"
      },
      "associated_resources": [
        {
          "vault": {
            "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
            "name": "Test Vault Name",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "managed_key": {
            "id": "93777bca-baef-4070-b9b5-a2e6079df1b4",
            "name": "My Managed Key",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "referenced_keystore": {
            "id": "93777bca-baef-4070-b9b5-a2e6079df1b4",
            "name": "My Managed Key",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "key_id_in_keystore": "93777bca-baef-4070-b9b5-a2e6079df1b4",
          "type": "com_ibm_cloud_kms_registration",
          "com_ibm_cloud_kms_registration": {
            "prevents_key_deletion": false,
            "service_name": "cloud-object-storage",
            "service_instance_name": "Cloud Object Storage-7s",
            "crn": "crn:v1:bluemix:public:cloud-object-storage:global:a/db995d8d9cc715cd99f13b0671d978b6:57da8e3a-a86d-4e01-b840-f22d36e6f23f:bucket:keyprotecttest",
            "description": "some description"
          }
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-keys-from-keystore
{: #command-uko-managed-keys-from-keystore}

List all managed keys that are assigned to the keystore.

If the `--all-pages` option is not set, the command only retrieves a single page of the collection.
{: note}

```
ibmcloud hpcs uko managed-keys-from-keystore --id ID [--algorithm ALGORITHM] [--state STATE] [--limit LIMIT] [--offset OFFSET] [--sort SORT] [--label LABEL] [--activation-date ACTIVATION-DATE] [--activation-date-min ACTIVATION-DATE-MIN] [--activation-date-max ACTIVATION-DATE-MAX] [--deactivation-date DEACTIVATION-DATE] [--deactivation-date-min DEACTIVATION-DATE-MIN] [--deactivation-date-max DEACTIVATION-DATE-MAX] [--expiration-date EXPIRATION-DATE] [--expiration-date-min EXPIRATION-DATE-MIN] [--expiration-date-max EXPIRATION-DATE-MAX] [--created-at CREATED-AT] [--created-at-min CREATED-AT-MIN] [--created-at-max CREATED-AT-MAX] [--updated-at UPDATED-AT] [--updated-at-min UPDATED-AT-MIN] [--updated-at-max UPDATED-AT-MAX] [--rotate-at-min ROTATE-AT-MIN] [--rotate-at-max ROTATE-AT-MAX] [--size SIZE] [--size-min SIZE-MIN] [--size-max SIZE-MAX] [--template-name TEMPLATE-NAME] [--template-id TEMPLATE-ID] [--template-type TEMPLATE-TYPE]
```

- Command options

    --uko-vault (string)
    :   Required. The UUID of the vault where the update is to take place. You can use the `ibmcloud hpcs uko vaults` command to retrieve the UUID.

    --id (string)
    :   Required. The UUID of the keystore. You can use the `ibmcloud hpcs uko keystores` command to retrieve the UUID.

    --algorithm (string)
    :   Optional. The algorithm of the returned keys. Values that can be set are `aes`, `rsa`, `hmac`, and `ec`.

    --state (string)
    :   Optional. The state that returned keys are to be in. The default value is `["pre_activation","active"]`. Values that can be set are: `pre_activation`, `active`, `deactivated`, `destroyed`.

    --limit (int64)
    :   Optional. The number of keys to retrieve. The value must be between 1 and 1000.

    --offset (int64)
    :   Optional. The number of keys to skip. The minimum value is `0`.

    --sort ([]string)
    :   Optional. The sorting order. The default value is `["-updated_at"]`. The list items must match regular expression `/^-?[a-z0-9_.\\[\\],-]+$/`.

    --label (string)
    :   Optional. The label of the key. The value must match regular expression `/.+/`.

    --activation-date (string)
    :   Optional. Return only managed keys whose activation date matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --activation-date-min (string)
    :   Optional. Return only managed keys whose activation date is at or after the parameter value. This query parameter cannot be used in conjunction with the `activation_date` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --activation-date-max (string)
    :   Optional. Return only managed keys whose activation date is at or before the parameter value. This query parameter cannot be used in conjunction with the `activation_date` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --deactivation-date (string)
    :   Optional. Return only managed keys whose deactivation date matches the parameter. This query parameter cannot be used in conjunction with the `expiration_date` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --deactivation-date-min (string)
    :   Optional. Return only managed keys whose deactivation date is at or after the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `expiration_date_min`, and `expiration_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --deactivation-date-max (string)
    :   Optional. Return only managed keys whose deactivation date is at or before the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `expiration_date_min`, and `expiration_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --expiration-date (string)
    :   Optional. Return only managed keys whose deactivation date matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --expiration-date-min (string)
    :   Optional. Return only managed keys whose deactivation date is at or after the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `deactivation_date_min`, and `deactivation_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --expiration-date-max (string)
    :   Optional. Return only managed keys whose deactivation date is at or before the parameter value. This query parameter cannot be used in conjunction with the `deactivation_date`, `expiration_date`, `deactivation_date_min`, and `deactivation_date_max` query parameters. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at (string)
    :   Optional. Return only managed keys whose creation time matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at-min (string)
    :   Optional. Return only managed keys whose creation time is at or after the parameter value. This query parameter cannot be used in conjunction with the `created_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at-max (string)
    :   Optional. Return only managed keys whose creation time is at or before the parameter value. This query parameter cannot be used in conjunction with the `created_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at (string)
    :   Optional. Return only managed keys whose update time matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at-min (string)
    :   Optional. Return only managed keys whose update time is after the parameter value. This query parameter cannot be used in conjunction with the `updated_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at-max (string)
    :   Optional. Return only managed keys whose update time is before the parameter value. This query parameter cannot be used in conjunction with the `updated_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --rotate-at-min (string)
    :   Optional. Return only managed keys whose rotation date is after the parameter value.

    --rotate-at-max (string)
    :   Optional. Return only managed keys whose rotation date is before the parameter value.

    --size (int64)
    :   Optional. The size of the key.

    --size-min (int64)
    :   Optional. The minimum size of the key. This query parameter cannot be used in conjunction with the `size` query parameter.

    --size-max (int64)
    :   Optional. The maximum size of the key. This query parameter cannot be used in conjunction with the `size` query parameter.

    --template-name (string)
    :   Return only managed keys whose template name begins with the string.

    --template-id (string[])
    :   Return only managed keys with the given template UUID.

    --template-type (string[])
    :   Return only managed keys with the given template type. Values that can be set are `user_defined`, `shadow`, and `system`.

    --all-pages (bool)
    :   Optional. Invoke multiple requests to display all pages of the collection for managed keys.

- Example

    ```
    ibmcloud hpcs uko managed-keys-from-keystore \
      --id=f779c44d-b90e-4917-b8b0-28d4591fefda \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "total_count": 4,
      "limit": 20,
      "offset": 0,
      "first": {
        "href": "/v4/managed_keys?vault.id=5295ad47-2ce9-43c3-b9e7-e5a9482c362b&limit=20&offset=0'"
      },
      "last": {
        "href": "/v4/managed_keys?vault.id=5295ad47-2ce9-43c3-b9e7-e5a9482c362b&limit=20&offset=0"
      },
      "managed_keys": [
        {
          "id": "35f690df-064a-4758-8694-b2f011810701",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault-1",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "6393e930-562c-4042-b324-45c37d3d49d9",
            "name": "AZURE-template-920",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/6393e930-562c-4042-b324-45c37d3d49d9"
          },
          "version": "1,",
          "description": "AZURE KEY",
          "label": "AZUREproduction2029",
          "state": "active",
          "size": "2048",
          "algorithm": "rsa",
          "verification_patterns": [
            {
              "method": "PUB-HASH-SHA-1",
              "value\"": "947AA69D48EEE487048AF2999DADB8DA55769529"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "AZURE"
            },
            {
              "name": "ENV",
              "value": "production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "AZURE-TAG"
            }
          ],
          "created_at": "2023-06-05T11:33:54Z",
          "updated_at": "2023-06-05T11:33:54Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "keystore": [
                {
                  "id": "2e124fa5-9ef6-406c-bb2f-9ad049ff1073",
                  "name": "Azure Keystore",
                  "type": "azure_key_vault",
                  "href": "v4/managed_keys/3dab42dc-6941-4841-8d27-4dabcc5aa09e"
                }
              ]
            }
          ],
          "instances": [
            {
              "id": "acb332dd-216c-44dd-8593-02bd2119ec62",
              "label_in_keystore\"": "AZUREproduction2029",
              "keystore": {
                "group": "Production AZURE GB",
                "type": "azure_key_vault"
              },
              "azure_key_protection_level": "software"
            }
          ],
          "href": "/v4/managed_keys/35f690df-064a-4758-8694-b2f011810701",
          "status_in_keystores": [
            {
              "keystore": [
                {
                  "id": "2e124fa5-9ef6-406c-bb2f-9ad049ff1073",
                  "name": "Azure Keystore",
                  "type": "azure_key_vault",
                  "href": "v4/managed_keys/3dab42dc-6941-4841-8d27-4dabcc5aa09e"
                }
              ],
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "d1e2525c-62c8-4df2-9173-69e1a7bc8cdb/d1e2525c-62c8-4df2-9173-69e1a7bc8cdb"
            }
          ]
        },
        {
          "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "EXAMPLE-VAULT",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
            "name": "AWS-EXAMPLE-TEMPLATE",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
          },
          "version": 1,
          "description": "AWS key template description",
          "label": "AWS-production-2029",
          "state": "active",
          "size": 256,
          "algorithm": "aes",
          "verification_patterns": [
            {
              "method\"": "ENC-ZERO",
              "value": "C05CA1"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "AWS"
            },
            {
              "name": "ENV",
              "value": "production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "AWS-TAG"
            }
          ],
          "created_at": "2023-06-05T10:40:13Z",
          "updated_at": "2023-06-05T10:40:19Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "id": "0743ae15-c594-476d-8e9a-1564740ace53",
              "name": "AWS KMS Keystore 335",
              "type": "aws_kms",
              "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
            }
          ],
          "instances": [
            {
              "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
              "label_in_keystore": "AWS-production-2029",
              "type": "secret_key",
              "keystore": {
                "group\"": "Production-AWS-DE",
                "type\"": "aws_kms"
              }
            }
          ],
          "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
          "status_in_keystores": [
            {
              "keystore": {
                "id": "0743ae15-c594-476d-8e9a-1564740ace53",
                "name": "AWS KMS Keystore 335",
                "type": "aws_kms",
                "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
              },
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
            }
          ]
        },
        {
          "id": "0beedc06-4608-48ae-8ae3-8b7bf3c2c39f",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault-2",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "64f98479-392d-4af2-a076-77cc21b8c6f3",
            "name": "IBM-CLOUD-TEMPLATE",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/64f98479-392d-4af2-a076-77cc21b8c6f3"
          },
          "version": 1,
          "description": "",
          "label": "IBMCloudProduction2029",
          "state": "active",
          "size": "256",
          "algorithm": "aes",
          "verification_patterns": [
            {
              "method": "ENC-ZERO",
              "value": "4ADDCB"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "IBMCloud"
            },
            {
              "name": "ENV",
              "value": "Production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "AWS-TAG"
            }
          ],
          "created_at": "2023-06-05T11:59:47Z",
          "updated_at": "2023-06-05T11:59:47Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "id": "0743ae15-c594-476d-8e9a-1564740ace53",
              "name": "IBM CLOUD KEYSTORE",
              "type": "ibm_cloud_kms",
              "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
            }
          ],
          "instances": [
            {
              "id": "0c5b14ea-a3dd-407c-af7c-fd74575ccbad",
              "label_in_keystore": "IBMCloudProduction2029",
              "type": "secret_key",
              "keystore": {
                "group": "Production External GB",
                "type": "ibm_cloud_kms"
              }
            }
          ],
          "href": "/v4/managed_keys/0beedc06-4608-48ae-8ae3-8b7bf3c2c39f",
          "status_in_keystores": [
            {
              "keystore": {
                "id": "0743ae15-c594-476d-8e9a-1564740ace53",
                "name": "IBM CLOUD KEYSTORE",
                "type": "ibm_cloud_kms",
                "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
              },
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "804854d0-4eb7-416e-8ae2-45ba56921c8a/804854d0-4eb7-416e-8ae2-45ba56921c8a"
            }
          ]
        },
        {
          "id": "d7b8204c-4f8f-4ba1-b306-5434ae817f51",
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault-3",
            "href": "v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "template": {
            "id": "09d229e5-e330-4e85-a7ee-cc8555d38603",
            "name": "GOOGLE-TEMPLATE-86",
            "type": [
              "user_defined"
            ],
            "href": "/v4/templates/09d229e5-e330-4e85-a7ee-cc8555d38603"
          },
          "version": 1,
          "description": "Google Key",
          "label": "Google-Production-2029",
          "state": "active",
          "size": "256",
          "algorithm": "aes",
          "verification_patterns": [
            {
              "method\"": "ENC-ZERO",
              "value": "C3F432"
            }
          ],
          "activation_date": "2028-07-14",
          "expiration_date": "2029-09-25",
          "label_tags": [
            {
              "name": "APP",
              "value": "Google"
            },
            {
              "name": "ENV",
              "value": "Production"
            },
            {
              "name": "lay",
              "value": "2029"
            }
          ],
          "tags": [
            {
              "name": "TAG-1",
              "value": "Google-TAG"
            }
          ],
          "created_at": "2023-06-05T13:18:28",
          "updated_at": "2023-06-05T13:18:28Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "referenced_keystores": [
            {
              "id": "6e026faa-d44d-4a1a-aeea-0e1ef2840cba",
              "name": "Google Keystore",
              "type": "google_kms",
              "href": "/v4/keystores/6e026faa-d44d-4a1a-aeea-0e1ef2840cba"
            }
          ],
          "instances": [
            {
              "id": "ed74a984-2057-484c-9198-54839f3fec62",
              "label_in_keystore": "Google-Production-2029",
              "type": "secret_key",
              "keystore": {
                "group": "Production Google",
                "type": "google_kms"
              },
              "google_key_protection_level": "software",
              "google_key_purpose": "encrypt_decrypt",
              "google_kms_algorithm": "google_symmetric_encryption"
            }
          ],
          "href": "/v4/managed_keys/d7b8204c-4f8f-4ba1-b306-5434ae817f51",
          "status_in_keystores": [
            {
              "keystore": {
                "id": "6e026faa-d44d-4a1a-aeea-0e1ef2840cba",
                "name": "Google Keystore",
                "type": "google_kms",
                "href": "/v4/keystores/6e026faa-d44d-4a1a-aeea-0e1ef2840cba"
              },
              "status": "active",
              "keystore_sync_flag": "ok",
              "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
              "key_id_in_keystore": "projects/plated-field-364019/locations/europe-west3/keyRings/uko-ring/cryptoKeys/ROBOT-Google-Key-05-06-nciYX/cryptoKeyVersions/1"
            }
          ]
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-ds
{: #command-uko-key-distribution}

Return the keystore distribution status for a managed key.

```
ibmcloud hpcs uko managed-key-ds --id ID
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

- Example

    ```
    ibmcloud hpcs uko managed-key-ds \
      --id=21a7498e-2ae4-47ee-85ac-a19bf64e92fa \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "status_in_keystores": [
        {
          "keystore": {
            "id": "b28bf13d-f49d-4b00-8b8d-457d38ad1e15",
            "name": "AWS KMS Keystore Name",
            "type": "aws_kms",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/b28bf13d-f49d-4b00-8b8d-457d38ad1e15"
          },
          "status": "not_present"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-update-from-template
{: #command-uko-managed-key-update-from-template}

Update a managed key to match the latest version of the associated key template. You can assign, activate, or deactivate the key on keystores in the group defined by the key template.

```
ibmcloud hpcs uko managed-key-update-from-template --id ID --if-match IF-MATCH [--dry-run DRY-RUN]
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

    --dry-run (boolean)
    : Optional. Do not create, update, or delete a resource, only verify and validate if resource can be created,updated, or deleted with given request successfully. The default value is false.

- Example

    ```
    ibmcloud hpcs uko managed-key-update-from-template \
      --id=22c04c00-0687-4f10-b0ac-b9f01d68ee85 \
      --if-match=2022-05-27T12:27:37Z \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "AWS-EXAMPLE-VAULT",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "template": {
        "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
        "name": "AWS-EXAMPLE-TEMPLATE",
        "type": [
          "user_defined"
        ],
        "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
      },
      "version": 1,
      "description": "AWS key template description",
      "label": "AWS-production-2029",
      "state": "active",
      "size": 256,
      "algorithm": "aes",
      "verification_patterns": [
        {
          "method\"": "ENC-ZERO",
          "value": "C05CA1"
        }
      ],
      "activation_date": "2028-07-14",
      "expiration_date": "2029-09-25",
      "label_tags": [
        {
          "name": "APP",
          "value": "AWS"
        },
        {
          "name": "ENV",
          "value": "production"
        },
        {
          "name": "lay",
          "value": "2029"
        }
      ],
      "tags": [
        {
          "name": "TAG-1",
          "value": "AWS-TAG"
        }
      ],
      "created_at": "2023-06-05T10:40:13Z",
      "updated_at": "2023-06-05T10:40:19Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "referenced_keystores": [
        {
          "id": "0743ae15-c594-476d-8e9a-1564740ace53",
          "name": "AWS KMS Keystore 335",
          "type": "aws_kms",
          "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
        }
      ],
      "instances": [
        {
          "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
          "label_in_keystore": "AWS-production-2029",
          "type": "secret_key",
          "keystore": {
            "group\"": "Production-AWS-DE",
            "type\"": "aws_kms"
          }
        }
      ],
      "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
      "status_in_keystores": [
        {
          "keystore": {
            "id": "0743ae15-c594-476d-8e9a-1564740ace53",
            "name": "AWS KMS Keystore 335",
            "type": "aws_kms",
            "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
          },
          "status": "active",
          "keystore_sync_flag": "ok",
          "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
          "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-activate
{: #command-uko-managed-key-activate}

Activate a managed key and perform key installation or activation operations on keystores in the keystore group associated with the managed key.

```
ibmcloud hpcs uko managed-key-activate --id ID --if-match IF-MATCH
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

- Example

    ```
    ibmcloud hpcs uko managed-key-activate \
      --id=21a7498e-2ae4-47ee-85ac-a19bf64e92fa \
      --if-match=2022-05-27T10:06:27Z \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "AWS-EXAMPLE-VAULT",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "template": {
        "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
        "name": "AWS-EXAMPLE-TEMPLATE",
        "type": [
          "user_defined"
        ],
        "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
      },
      "version": 1,
      "description": "AWS key template description",
      "label": "AWS-production-2029",
      "state": "active",
      "size": 256,
      "algorithm": "aes",
      "verification_patterns": [
        {
          "method\"": "ENC-ZERO",
          "value": "C05CA1"
        }
      ],
      "activation_date": "2028-07-14",
      "expiration_date": "2029-09-25",
      "label_tags": [
        {
          "name": "APP",
          "value": "AWS"
        },
        {
          "name": "ENV",
          "value": "production"
        },
        {
          "name": "lay",
          "value": "2029"
        }
      ],
      "tags": [
        {
          "name": "TAG-1",
          "value": "AWS-TAG"
        }
      ],
      "created_at": "2023-06-05T10:40:13Z",
      "updated_at": "2023-06-05T10:40:19Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "referenced_keystores": [
        {
          "id": "0743ae15-c594-476d-8e9a-1564740ace53",
          "name": "AWS KMS Keystore 335",
          "type": "aws_kms",
          "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
        }
      ],
      "instances": [
        {
          "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
          "label_in_keystore": "AWS-production-2029",
          "type": "secret_key",
          "keystore": {
            "group\"": "Production-AWS-DE",
            "type\"": "aws_kms"
          }
        }
      ],
      "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
      "status_in_keystores": [
        {
          "keystore": {
            "id": "0743ae15-c594-476d-8e9a-1564740ace53",
            "name": "AWS KMS Keystore 335",
            "type": "aws_kms",
            "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
          },
          "status": "active",
          "keystore_sync_flag": "ok",
          "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
          "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-deactivate
{: #command-uko-managed-key-deactivate}

Deactivate a managed key and perform key deactivation operations on keystores in the keystore group associated with the managed key.

```
ibmcloud hpcs uko managed-key-deactivate --id ID --if-match IF-MATCH
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

- Example

    ```
    ibmcloud hpcs uko managed-key-deactivate \
      --id=21a7498e-2ae4-47ee-85ac-a19bf64e92fa \
      --if-match=2022-05-27T10:13:31Z \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "AWS-EXAMPLE-VAULT",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "template": {
        "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
        "name": "AWS-EXAMPLE-TEMPLATE",
        "type": [
          "user_defined"
        ],
        "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
      },
      "version": 1,
      "description": "AWS key template description",
      "label": "AWS-production-2029",
      "state": "active",
      "size": 256,
      "algorithm": "aes",
      "verification_patterns": [
        {
          "method\"": "ENC-ZERO",
          "value": "C05CA1"
        }
      ],
      "activation_date": "2028-07-14",
      "expiration_date": "2029-09-25",
      "label_tags": [
        {
          "name": "APP",
          "value": "AWS"
        },
        {
          "name": "ENV",
          "value": "production"
        },
        {
          "name": "lay",
          "value": "2029"
        }
      ],
      "tags": [
        {
          "name": "TAG-1",
          "value": "AWS-TAG"
        }
      ],
      "created_at": "2023-06-05T10:40:13Z",
      "updated_at": "2023-06-05T10:40:19Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "referenced_keystores": [
        {
          "id": "0743ae15-c594-476d-8e9a-1564740ace53",
          "name": "AWS KMS Keystore 335",
          "type": "aws_kms",
          "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
        }
      ],
      "instances": [
        {
          "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
          "label_in_keystore": "AWS-production-2029",
          "type": "secret_key",
          "keystore": {
            "group\"": "Production-AWS-DE",
            "type\"": "aws_kms"
          }
        }
      ],
      "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
      "status_in_keystores": [
        {
          "keystore": {
            "id": "0743ae15-c594-476d-8e9a-1564740ace53",
            "name": "AWS KMS Keystore 335",
            "type": "aws_kms",
            "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
          },
          "status": "active",
          "keystore_sync_flag": "ok",
          "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
          "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-destroy
{: #command-uko-managed-key-destroy}

Destroy a managed key and perform key destruction operations on keystores in the keystore group associated with the managed key. This operation cannot be undone. Make sure that the managed key is in a `deactivated` state before you run this command.

```
ibmcloud hpcs uko managed-key-destroy --id ID --if-match IF-MATCH
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

- Example

    ```
    ibmcloud hpcs uko managed-key-destroy \
      --id=21a7498e-2ae4-47ee-85ac-a19bf64e92fa \
      --if-match=2022-05-27T10:14:13Z \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "ceb54688-827c-4e31-afa8-4c0122465a5b",
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "AWS-EXAMPLE-VAULT",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "template": {
        "id": "7a4e3659-083b-4d77-8562-7081eb197e90",
        "name": "AWS-EXAMPLE-TEMPLATE",
        "type": [
          "user_defined"
        ],
        "href": "/v4/templates/7a4e3659-083b-4d77-8562-7081eb197e90"
      },
      "version": 1,
      "description": "AWS key template description",
      "label": "AWS-production-2029",
      "state": "active",
      "size": 256,
      "algorithm": "aes",
      "verification_patterns": [
        {
          "method\"": "ENC-ZERO",
          "value": "C05CA1"
        }
      ],
      "activation_date": "2028-07-14",
      "expiration_date": "2029-09-25",
      "label_tags": [
        {
          "name": "APP",
          "value": "AWS"
        },
        {
          "name": "ENV",
          "value": "production"
        },
        {
          "name": "lay",
          "value": "2029"
        }
      ],
      "tags": [
        {
          "name": "TAG-1",
          "value": "AWS-TAG"
        }
      ],
      "created_at": "2023-06-05T10:40:13Z",
      "updated_at": "2023-06-05T10:40:19Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "referenced_keystores": [
        {
          "id": "0743ae15-c594-476d-8e9a-1564740ace53",
          "name": "AWS KMS Keystore 335",
          "type": "aws_kms",
          "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
        }
      ],
      "instances": [
        {
          "id": "8c2bef79-dd15-477c-93f0-0ae62264d4b6",
          "label_in_keystore": "AWS-production-2029",
          "type": "secret_key",
          "keystore": {
            "group\"": "Production-AWS-DE",
            "type\"": "aws_kms"
          }
        }
      ],
      "href": "/v4/managed_keys/ceb54688-827c-4e31-afa8-4c0122465a5b",
      "status_in_keystores": [
        {
          "keystore": {
            "id": "0743ae15-c594-476d-8e9a-1564740ace53",
            "name": "AWS KMS Keystore 335",
            "type": "aws_kms",
            "href": "/v4/keystores/0743ae15-c594-476d-8e9a-1564740ace53"
          },
          "status": "active",
          "keystore_sync_flag": "ok",
          "keystore_sync_flag_detail": "active_key_is_active_in_keystore",
          "key_id_in_keystore": "arn:aws:kms:eu-central-1:584492040385:key/52eca0ad-79ca-4c16-8934-986ac5d14b73"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko managed-key-sync
{: #command-uko-key-sync}

Perform the synchronization operation on a managed key to align the states in the associated keystores.

```
ibmcloud hpcs uko managed-key-sync --id ID --if-match IF-MATCH
```

- Command options

    --id (string)
    :   Required. The UUID of the key. You can use the `ibmcloud hpcs uko managed-keys` command to retrieve the key UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko managed-key` command to retrieve the ETag.

- Example

    ```
    ibmcloud hpcs uko managed-key-sync \
        --id=b28bf13d-f49d-4b00-8b8d-457d38ad1e15 \
        --if-match=2022-05-27T10:14:13Z \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "status_in_keystores": [
        {
          "keystore": {
            "id": "b28bf13d-f49d-4b00-8b8d-457d38ad1e15",
            "name": "AWS KMS Keystore Name",
            "type": "aws_kms",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/b28bf13d-f49d-4b00-8b8d-457d38ad1e15"
          },
          "status": "not_present"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko key-templates
{: #command-uko-key-templates}

List all key templates in the instance.

If the `--all-pages` option is not set, the command only retrieves a single page of the collection.
{: note}

```
ibmcloud hpcs uko key-templates [--name NAME] [--naming-scheme NAME-SCHEME] [--vault-id VAULT-ID] [--key-algorithm KEY-ALGORITHM] [--key-size KEY-SIZE] [--key-size-min KEY-SIZE-MIN] [--key-size-max KEY-SIZE-MAX] [--keystores-type KEYSTORES-TYPE] [--keystores-group KEYSTORES-GROUP] [--created-at CREATED-AT] [--created-at-min CREATED-AT-MIN] [--created-at-max CREATED-AT-MAX] [--updated-at UPDATED-AT] [--updated-at-min UPDATED-AT-MIN] [--updated-at-max UPDATED-AT-MAX] [--type TYPE] [--state STATE] [--sort SORT] [--limit LIMIT] [--offset OFFSET] [--managing-systems MANAGING-SYSTEMS]
```

- Command options

    --name (string)
    :   Optional. Return only templates whose name begin with the string.

    --naming-scheme (string)
    :   Optional. Return only templates whose naming scheme contains the string.

    --vault-id (string)
    :   Optional. The UUID of the vault. The length must be 36 characters. The value must match the regular expression `/^[-0-9a-z]+$/`.

    --key-algorithm (string)
    :   Optional. The algorithm of the returned key templates. Values that can be set are `aes`, `rsa`, `hmac`, `ec`, `des`, and `dilithium`.

    --key-size (string)
    :   Optional. The size of the key

    --key-size-min (string)
    :   Optional. The minimum size of the key. This query parameter cannot be used in conjunction with the `key-size` query parameter.

    --key-size-max (string)
    :   Optional. The maximum size of the key. This query parameter cannot be used in conjunction with the `key-size` query parameter.

    --keystores-type ([]string)
    :   Optional. Type of referenced keystore. Values that can be set are `aws_kms`, `azure_key_vault`, `ibm_cloud_kms`, `google_kms`, and `cca`.

    --keystores-group ([]string)
    :   Optional. Group of referenced keystore.

    --created-at (string)
    :   Optional. Return only managed keys whose creation time matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at-min (string)
    :   Optional. Return only managed keys whose creation time is at or after the parameter value. This query parameter cannot be used in conjunction with the `created_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --created-at-max (string)
    :   Optional. Return only managed keys whose creation time is at or before the parameter value. This query parameter cannot be used in conjunction with the `created_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at (string)
    :   Optional. Return only managed keys whose update time matches the parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at-min (string)
    :   Optional. Return only managed keys whose update time is after the parameter value. This query parameter cannot be used in conjunction with the `updated_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --updated-at-max (string)
    :   Optional. Return only managed keys whose update time is before the parameter value. This query parameter cannot be used in conjunction with the `updated_at` query parameter. The value must match regular expression `/[0-9]{4}-[0-9]{2}-[0-9]{2}/`.

    --type ([]string)
    :   Optional. The types of returned templates. Values can be set are `user_defined`, `shadow`, and `system`.

    --state ([]string)
    :   Optional. Return only template whose state contains the string. Values can be set are `archived` or `unarchived`.

    --sort ([]string)
    :   Optional. The sorting order. The default value is `["-updated_at"]`. The list items must match the regular expression `/^-?[a-z0-9_.\\[\\],-]+$/`.

    --limit (int64)
    :   Optional. The number of key templates to retrieve. The value must be between 1 and 1000.

    --offset (int64)
    :   Optional. The number of keys to skip. The minimum value is `0`.

    --managing-systems
    :   Return only managed keys with the given managing systems. Values that can be set are `web` and `workstation`.

- Example

    ```
    ibmcloud hpcs uko key-templates --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "total_count": 3,
      "limit": 20,
      "offset": 0,
      "first": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/templates?vault.id=5295ad47-2ce9-43c3-b9e7-e5a9482c362b&limit=20"
      },
      "last": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/templates?vault.id=5295ad47-2ce9-43c3-b9e7-e5a9482c362b&limit=20&offset=0"
      },
      "templates": [
        {
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "VAULT 391",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "id": "91caa113-d3ba-4620-a252-1c27aa31fd4e",
          "version": "0",
          "name": "AWS-TEMPLATE-229",
          "naming_scheme": "<APP>-AES256-<ENV>-<GROUP>-<lay>",
          "type": [
            "user_defined"
          ],
          "state": "unarchived",
          "keys_count": "0",
          "key": {
            "size": "256",
            "algorithm": "aes",
            "activation_date": "P5Y1M1W2D",
            "expiration_date": "P1Y2M1W4D",
            "state": "active"
          },
          "description": "AWS KMS KEY TEMPLATE",
          "created_at": "2023-06-05T14:16:07Z",
          "updated_at": "2023-06-05T14:16:07Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "keystores": [
            {
              "group": "Production-AWS-DE",
              "type": "aws_kms"
            }
          ],
          "href": "v4/templates/91caa113-d3ba-4620-a252-1c27aa31fd4e"
        },
        {
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault 391",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "id": "64f98479-392d-4af2-a076-77cc21b8c6f3",
          "version": "0",
          "name": "IBM-template-371",
          "naming_scheme": "IBMCloud<APP><ENV><lay>",
          "type": [
            "user_defined"
          ],
          "state": "unarchived",
          "keys_count": "0",
          "key": {
            "size": "256",
            "algorithm": "aes",
            "activation_date": "P5Y1M1W2D",
            "expiration_date": "P1Y2M1W4D",
            "state": "active"
          },
          "description": "IBM CLOUD key template description",
          "created_at": "2023-06-05T11:59:08Z",
          "updated_at": "2023-06-05T11:59:08Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "keystores": [
            {
              "group": "Production External GB",
              "type": "ibm_cloud_kms"
            }
          ],
          "href": "/v4/templates/64f98479-392d-4af2-a076-77cc21b8c6f3"
        },
        {
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault 391",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "id": "6393e930-562c-4042-b324-45c37d3d49d9",
          "version": "0",
          "name": "AZURE-TEMPLATE-920",
          "naming_scheme": "<APP><ENV><lay>",
          "type": [
            "user_defined"
          ],
          "state": "unarchived",
          "keys_count": "0",
          "key": {
            "size": "2048",
            "algorithm": "rsa",
            "activation_date": "P5Y1M1W2D",
            "expiration_date": "P1Y2M1W4D",
            "state": "active"
          },
          "description": "AZURE MANAGED KEY",
          "created_at": "2023-06-05T11:33:24Z",
          "updated_at": "2023-06-05T11:33:24Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "keystores": [
            {
              "group": "Production AZURE GB",
              "type": "azure_key_vault",
              "azure_key_protection_level": "software"
            }
          ],
          "href": "/v4/templates/6393e930-562c-4042-b324-45c37d3d49d9"
        },
        {
          "vault": {
            "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
            "name": "Vault 391",
            "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
          },
          "id": "09d229e5-e330-4e85-a7ee-cc8555d38603",
          "version": "0",
          "name": "GOOGLE-TEMPLATE-86",
          "naming_scheme": "<APP>-<ENV>-<lay>",
          "type": [
            "user_defined"
          ],
          "state": "unarchived",
          "keys_count": "0",
          "key": {
            "size": "256",
            "algorithm": "aes",
            "activation_date": "P5Y1M1W2D",
            "expiration_date": "P1Y2M1W4D",
            "state": "active"
          },
          "description": "Google Key Template",
          "created_at": "2023-06-05T13:17:01Z",
          "updated_at": "2023-06-05T13:17:01Z",
          "created_by": "IBMid-665000MCAR",
          "updated_by": "IBMid-665000MCAR",
          "keystores": [
            {
              "group": "Production Google",
              "type": "google_kms",
              "google_key_protection_level": "software",
              "google_key_purpose": "encrypt_decrypt",
              "google_kms_algorithm": "google_symmetric_encryption"
            }
          ],
          "href": "/v4/templates/09d229e5-e330-4e85-a7ee-cc8555d38603"
        }
      ]
    }
    ```
    {: screen}

#### ibmcloud hpcs uko key-template-create
{: #command-uko-key-template-create}

Create a new key template. Key templates are used to combine information that is necessary for creating a key. With key templates, you can easily create subsequent keys without specifying any details.

```
ibmcloud hpcs uko key-template-create --vault VAULT --name NAME --type TYPE --state STATE --naming-scheme NAMEING-SCHEME --key KEY --keystores KEYSTORES [--description DESCRIPTION]
```

- Command options

    --vault ([VaultReferenceInCreationRequest](#uko-vault-reference-in-creation-request-example-schema))
    :   Required. The ID of the vault where the key template is to be created.

    --name (string)
    :   Required. The name of the template. You need to reference it when creating managed keys. The length must be between 1 and 30 characters. The value must match the regular expression `/^[A-Za-z][A-Za-z0-9-]*$/`.

    --type (string[])
    :   Required. The type of the template. Values that can be set are `user_defined`, `shadow`, and `system`.

    --state (string)
    :   Required. The state of the template. Values can be set are `archived` or `unarchived`.

    --naming-scheme (string)
    :   Required. The string pattern that your template name needs to follow.

    --key ([KeyProperties](#uko-key-properties-example-schema))
    :   Required. Properties that describe the managed key.

    --keystores ([KeystoresPropertiesCreate\[\]](#uko-keystores-properties-create-example-schema))
    :   Required. An array describing the type and group of keystores that the managed key is to be installed in. The maximum length is `1` item. The minimum length is `1` item. 
    
    --description (string)
    :   Optional. The description of the key template. The length must be between 0 and 200 characters. The value must match the regular expression `/(.|\\n)*/`.

- Example

    ```
    ibmcloud hpcs uko key-template-create \
        --vault='{"id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b"}' \
        --name=IBM-CLOUD-EXAMPLE-TEMPLATE \
        --key='{"size": "256", "algorithm": "aes", "activation_date": "P5Y1M1W2D", "expiration_date": "P1Y2M1W4D", "state": "active"}' \
        --keystores='[{"group": "Production", "type": "ibm_cloud_kms"}]' \
        --state="unarchived" \
        --naming-scheme="A-<APP>-AES256-<ENV>-<GROUP>" \
        --type="user_defined" \
        --description="IBM CLOUD key template description" \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | Location | String | Path to newly created resource, relative to context root. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "VAULT 391",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "id": "91caa113-d3ba-4620-a252-1c27aa31fd4e",
      "version": "0",
      "name": "AWS-TEMPLATE-229",
      "naming_scheme": "<APP>-AES256-<ENV>-<GROUP>-<lay>",
      "type": [
        "user_defined"
      ],
      "state": "unarchived",
      "keys_count": "0",
      "key": {
        "size": "256",
        "algorithm": "aes",
        "activation_date": "P5Y1M1W2D",
        "expiration_date": "P1Y2M1W4D",
        "state": "active"
      },
      "description": "AWS KMS KEY TEMPLATE",
      "created_at": "2023-06-05T14:16:07Z",
      "updated_at": "2023-06-05T14:16:07Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "keystores": [
        {
          "group": "Production-AWS-DE",
          "type": "aws_kms"
        }
      ],
      "href": "v4/templates/91caa113-d3ba-4620-a252-1c27aa31fd4e"
    }
    ```
    {: screen}

#### hpcs uko key-template-delete
{: #command-uko-key-template-delete}

Delete a key template from the vault. Make sure that no managed key is associated with the key template before you run this command.

```
ibmcloud hpcs uko key-template-delete --id ID --if-match IF-MATCH
```

- Command options

    --id (string)
    :   Required. The UUID of the template. You can use the `ibmcloud hpcs uko key-templates` command to retrieve the UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko key-template` command to retrieve the ETag.

- Example

    ```
    ibmcloud hpcs uko key-template-delete \
        --id=07b62c12-75a2-46c9-9259-0cecde3985d2 \
        --if-match=2022-05-11T14:58:26Z
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    ...
    OK
    ```
    {: screen}

#### ibmcloud hpcs uko key-template
{: #command-uko-key-template}

Retrieve a key template and its details by specifying the ID.

```
ibmcloud hpcs uko key-template --id ID
```

- Command options

    --id (string)
    :   Required. The UUID of the template. You can use the `ibmcloud hpcs uko key-templates` command to retrieve the UUID.

- Example

    ```
    ibmcloud hpcs uko key-template \
        --id=07b62c12-75a2-46c9-9259-0cecde3985d2 \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "VAULT 391",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "id": "91caa113-d3ba-4620-a252-1c27aa31fd4e",
      "version": "0",
      "name": "AWS-TEMPLATE-229",
      "naming_scheme": "<APP>-AES256-<ENV>-<GROUP>-<lay>",
      "type": [
        "user_defined"
      ],
      "state": "unarchived",
      "keys_count": "0",
      "key": {
        "size": "256",
        "algorithm": "aes",
        "activation_date": "P5Y1M1W2D",
        "expiration_date": "P1Y2M1W4D",
        "state": "active"
      },
      "description": "AWS KMS KEY TEMPLATE",
      "created_at": "2023-06-05T14:16:07Z",
      "updated_at": "2023-06-05T14:16:07Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "keystores": [
        {
          "group": "Production-AWS-DE",
          "type": "aws_kms"
        }
      ],
      "href": "v4/templates/91caa113-d3ba-4620-a252-1c27aa31fd4e"
    }
    ```
    {: screen}

#### hpcs uko key-template-update
{: #command-uko-key-template-update}

Update attributes of a key template.

```
ibmcloud hpcs uko key-template-update --id ID --if-match IF-MATCH [--keystores KEYSTORES] [--name NAME] [--description DESCRIPTION] [--key KEY]
```

- Command options

    --id (string)
    :   Required. The UUID of the template. You can use the `ibmcloud hpcs uko key-templates` command to retrieve the UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko key-template` command to retrieve the ETag.

    --name (string)
    :   Optional. The updated template name.

    --keystores ([KeystoresPropertiesUpdate\[\]](#uko-keystores-properties-update-example-schema))
    :   Optional. An array describing the type and group of keystores where the managed key is to be installed. The maximum length is `1` item. The minimum length is `1` item.
    
    --description (string)
    :   Optional. The updated description of the key template. The length must be between 0 and 200 characters. The value must match the regular expression `/(.|\\n)*/`.

    --key ([KeyPropertiesUpdate](#uko-key-properties-update-example-schema))
    :   Optional. Properties of the managed key.

- Example

    ```
    ibmcloud hpcs uko key-template-update \
      --id=07b62c12-75a2-46c9-9259-0cecde3985d2 \
      --if-match=2022-05-11T14:58:26Z \
      --description="The update of the template" \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "vault": {
        "id": "1d3b402a-ce40-4b17-b6f0-a7fa26ba72de",
        "name": "VAULT 391",
        "href": "/v4/vaults/1d3b402a-ce40-4b17-b6f0-a7fa26ba72de"
      },
      "id": "91caa113-d3ba-4620-a252-1c27aa31fd4e",
      "version": "0",
      "name": "AWS-TEMPLATE-229",
      "naming_scheme": "<APP>-AES256-<ENV>-<GROUP>-<lay>",
      "type": [
        "user_defined"
      ],
      "state": "unarchived",
      "keys_count": "0",
      "key": {
        "size": "256",
        "algorithm": "aes",
        "activation_date": "P5Y1M1W2D",
        "expiration_date": "P1Y2M1W4D",
        "state": "active"
      },
      "description": "AWS KMS KEY TEMPLATE",
      "created_at": "2023-06-05T14:16:07Z",
      "updated_at": "2023-06-05T14:16:07Z",
      "created_by": "IBMid-665000MCAR",
      "updated_by": "IBMid-665000MCAR",
      "keystores": [
        {
          "group": "Production-AWS-DE",
          "type": "aws_kms"
        }
      ],
      "href": "v4/templates/91caa113-d3ba-4620-a252-1c27aa31fd4e"
    }
    ```
    {: screen}

#### hpcs uko keystores
{: #command-uko-list-keystores}

List all keystores in the instance.

If the `--all-pages` option is not set, the command only retrieves a single page of the collection.
{: note}


```
ibmcloud hpcs uko keystores [--type TYPE] [--name NAME] [--description DESCRIPTION] [--group GROUP] [--groups GROUPS] [--vault-id VAULT-ID] [--location LOCATION] [--limit LIMIT] [--offset OFFSET] [--sort SORT]
```

- Command options

    --type ([]string)
    :   Optional. The type of keystores that you want to retrieve. Values that can be set are: `aws_kms`, `azure_key_vault`, `ibm_cloud_kms`, `google_kms`, and `cca`.

    --name (string)
    :   Optional. Return only keystores whose name contains the string. The length must be between 1 and 100 characters. The value must match regular expression `/.+/`.

    --description (string)
    :   Optional. Return only keystores whose description contains the string. The length must be between 1 and 200 characters. The value must match regular expression `/.+/`.

    --group (string)
    :   Optional. The keystore group. This query parameter cannot be used in conjunction with the `groups[]` query parameter.

    --groups ([]string)
    :   Optional. Keystore groups.

    --vault-id ([]string)
    :   Optional. The UUID of the vault. The list items must match the regular expression `/^[-0-9a-z]+$/`.

    --location (string)
    :   Optional. Keystore location.

    --limit (int64)
    :   Optional. The number of keystores to retrieve. The value must between 1 and 1000.

    --offset (int64)
    :   Optional. The number of keys to skip. The minimum value is `0`.

    --sort ([]string)
    :   Optional. The sorting order. The default value is `["-updated_at"]`. The list items must match regular expression `/^-?[a-z0-9_.\\[\\],-]+$/`.

    --all-pages (bool)
    :   Optional. Invoke multiple requests to display all pages of the collection for keystores.

- Example

    ```
    ibmcloud hpcs uko keystores --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "total_count": 3,
      "limit": 20,
      "offset": 0,
      "first": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores?limit=20"
      },
      "last": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores?limit=20&offset=0"
      },
      "keystores": [
        {
          "vault": {
            "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
            "name": "Test Vault Name",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "id": "5312861e-5b9b-4f40-9264-997afc2cd034",
          "name": "AWS KMS Keystore Name",
          "description": "AWS KMS keystore",
          "groups": [
            "Production-UK",
            "Production-DE"
          ],
          "type": "aws_kms",
          "created_at": "2022-03-09T10:59:44Z",
          "updated_at": "2022-03-09T10:59:44Z",
          "created_by": "IBMid-1308197YB4",
          "updated_by": "IBMid-1308197YB4",
          "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/5312861e-5b9b-4f40-9264-997afc2cd034",
          "aws_region": "eu_central_1",
          "aws_access_key_id": "",
          "aws_secret_access_key": ""
        },
        {
          "vault": {
            "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
            "name": "Test Vault Name",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "id": "314d0c9c-8808-47f0-829a-e63bdbb93854",
          "name": "Azure Keystore Name ",
          "description": "The AZURE keystore for testing.",
          "groups": [
            "Azure Keystore Name "
          ],
          "type": "azure_key_vault",
          "created_at": "2022-03-09T11:00:04Z",
          "updated_at": "2022-03-09T11:00:04Z",
          "created_by": "IBMid-1308197YB4",
          "updated_by": "IBMid-1308197YB4",
          "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/314d0c9c-8808-47f0-829a-e63bdbb93854",
          "azure_resource_group": "EKMF-Web-Tests",
          "azure_location": "europe_north",
          "azure_service_principal_client_id": "c8e8540f-4f15-4b6b-8862-3ccdb389e35d",
          "azure_service_principal_password": "***",
          "azure_tenant": "fcf67057-50c9-4ad4-98f3-ffca64add9e9",
          "azure_subscription_id": "a9867d9b-582f-42f3-9392-26856b06b808",
          "azure_environment": "azure"
        },
        {
          "vault": {
            "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
            "name": "Test Vault Name",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "id": "f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
          "name": "IBM Keystore Name",
          "description": "The description of the created keystore.",
          "groups": [
            "IBM Keystore Name"
          ],
          "type": "ibm_cloud_kms",
          "created_at": "2022-03-09T11:00:11Z",
          "updated_at": "2022-03-09T11:00:11Z",
          "created_by": "IBMid-1308197YB4",
          "updated_by": "IBMid-1308197YB4",
          "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
          "ibm_api_endpoint": "https://us-south.kms.cloud.ibm.com",
          "ibm_iam_endpoint": "https://iam.bluemix.net/identity/token",
          "ibm_api_key": "",
          "ibm_instance_id": "d139ea58-a073-441b-ba4e-dcc8bae58be4",
          "ibm_variant": "hpcs",
          "ibm_key_ring": "IBM-Cloud-KMS-Internal"
        }
      ]
    }
    ```
    {: screen}

#### ibmcloud hpcs uko keystore-create
{: #command-uko-keystore-create}

Create an internal keystore or connect to an external keystore of the requested type. If the `dry_run` query parameter is used, no keystores are created in the database and only a test is performed to verify whether the connection information is correct. It is possible to sort by the following parameters: `name`, `created_at`, `updated_at`, `vault-id`.

```
ibmcloud hpcs uko keystore-create --keystore-body KEYSTORE-BODY [--dry-run DRY-RUN]
```

- Command options

    --keystore-body ([KeystoreCreationRequest](#uko-keystore-creation-request-example-schema))
    :   Required. Properties of the keystore that you want to create or connect to.

    `--dry-run` (bool)
    :   Optional. Perform a test to verify whether a keystore created with given parameters can be communicated with successfully. No keystores are created in the database. The default value is `false`.

- Example

    ```
    ibmcloud hpcs uko keystore-create \
        --keystore-body='{"type": "aws_kms", "vault": {"id": "75d0f626-44b0-4076-80cd-8cb9e485fe73"}, "name": "AWS KMS Keystore", "description": "AWS KMS Keystore", "groups": ["Production", "Production-DE"], "aws_access_key_id": "HSNGYJMKHGFFF", "aws_secret_access_key": "JHGSY766YUG67GFV", "aws_region": "eu_central_1"}' \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | Location | String | Path to newly created resource, relative to context root. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "vault": {
        "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
        "name": "Test Vault Name",
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
      },
      "id": "f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
      "name": "IBM Keystore Name",
      "description": "The description of the created keystore.",
      "groups": [
        "IBM Keystore Name"
      ],
      "type": "ibm_cloud_kms",
      "created_at": "2022-03-09T11:00:11Z",
      "updated_at": "2022-03-09T11:00:11Z",
      "created_by": "IBMid-1308197YB4",
      "updated_by": "IBMid-1308197YB4",
      "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
      "ibm_api_endpoint": "https://us-south.kms.cloud.ibm.com",
      "ibm_iam_endpoint": "https://iam.bluemix.net/identity/token",
      "ibm_api_key": "",
      "ibm_instance_id": "d139ea58-a073-441b-ba4e-dcc8bae58be4",
      "ibm_variant": "hpcs",
      "ibm_key_ring": "IBM-Cloud-KMS-Internal"
    }
    ```
    {: screen}

#### hpcs uko keystore-delete
{: #command-uko-keystore-delete}

Delete an internal keystore or remove a connection to an external keystore. The external keystore on the remote platform still exists after you remove the connection.

```
ibmcloud hpcs uko keystore-delete --id ID --if-match IF-MATCH [--mode MODE]
```

- Command options

    --id (string)
    :   Required. The UUID of the keystore. You can use the `ibmcloud hpcs uko keystores` command to retrieve the UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko keystore` command to retrieve the ETag.

    --mode (string)
    :   Optional. Mode of disconnecting from keystore. The values can be set are `restrict`, `disconnect`, `deactivate`, and `destroy`. The default value is `restrict`.

- Example

    ```
    ibmcloud hpcs uko keystore-delete \
        --id=0325e05e-2b25-4f13-85b2-2d7f85e54359 \
        --if-match=2022-05-11T14:58:26Z
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:
    ```
    ...
    OK
    ```

#### hpcs uko keystore
{: #command-uko-keystore}

Retrieve a target internal keystore or external keystore connection and its details by specifying the ID.

```
ibmcloud hpcs uko keystore --id ID
```

- Command options

    --id (string)
    :   Required. The UUID of the keystore. You can use the `ibmcloud hpcs uko keystores` command to retrieve the UUID.

- Example

    ```
    ibmcloud hpcs uko keystore \
        --id=0325e05e-2b25-4f13-85b2-2d7f85e54359 \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "vault": {
        "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
        "name": "Test Vault Name",
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
      },
      "id": "f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
      "name": "IBM Keystore Name",
      "description": "The description of the created keystore.",
      "groups": [
        "IBM Keystore Name"
      ],
      "type": "ibm_cloud_kms",
      "created_at": "2022-03-09T11:00:11Z",
      "updated_at": "2022-03-09T11:00:11Z",
      "created_by": "IBMid-1308197YB4",
      "updated_by": "IBMid-1308197YB4",
      "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
      "ibm_api_endpoint": "https://us-south.kms.cloud.ibm.com",
      "ibm_iam_endpoint": "https://iam.bluemix.net/identity/token",
      "ibm_api_key": "",
      "ibm_instance_id": "d139ea58-a073-441b-ba4e-dcc8bae58be4",
      "ibm_variant": "hpcs",
      "ibm_key_ring": "IBM-Cloud-KMS-Internal"
    }
    ```
    {: screen}

#### ibmcloud hpcs uko keystore-update
{: #command-uko-keystore-update}

Update attributes of an internal keystore or an external keystore connection.

```
ibmcloud hpcs uko keystore-update --id ID --if-match IF-MATCH --keystore-body KEYSTORE-BODY
```

- Command options

    --id (string)
    :   Required. The UUID of the keystore. You can use the `ibmcloud hpcs uko keystores` command to retrieve the UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko keystore` command to retrieve the ETag.

    --keystore-body ([KeystoreUpdateRequest](#uko-keystore-update-request-example-schema))
    :   Required. Keystore properties that you want to update.

- Example

    ```
    ibmcloud hpcs uko keystore-update \
        --id=0325e05e-2b25-4f13-85b2-2d7f85e54359 \
        --if-match=2022-05-11T14:58:26Z \
        --keystore-body='{"description": "Updated description", "keystore_type": "aws_kms"}' \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}
    
    The command returns the output similar to the following example:

    ```
    {
      "vault": {
        "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
        "name": "Test Vault Name",
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
      },
      "id": "f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
      "name": "IBM Keystore Name",
      "description": "The description of the created keystore.",
      "groups": [
        "IBM Keystore Name"
      ],
      "type": "ibm_cloud_kms",
      "created_at": "2022-03-09T11:00:11Z",
      "updated_at": "2022-03-09T11:00:11Z",
      "created_by": "IBMid-1308197YB4",
      "updated_by": "IBMid-1308197YB4",
      "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/keystores/f6a5ccc1-7fc3-435e-9637-482e470ba8e8",
      "ibm_api_endpoint": "https://us-south.kms.cloud.ibm.com",
      "ibm_iam_endpoint": "https://iam.bluemix.net/identity/token",
      "ibm_api_key": "",
      "ibm_instance_id": "d139ea58-a073-441b-ba4e-dcc8bae58be4",
      "ibm_variant": "hpcs",
      "ibm_key_ring": "IBM-Cloud-KMS-Internal"
    }
    ```
    {: screen}

#### hpcs uko associated-resources-for-target-keystore
{: #command-uko-associated-resources-keystore}

Obtain a list of resources associated with all keys that are activated in this keystore.

If the `--all-pages` option is not set, the command only retrieves a single page of the collection.
{: note}

```
ibmcloud hpcs uko associated-resources-for-target-keystore --id ID [--limit LIMIT] [--offset OFFSET] [--sort SORT]
```

- Command options

    --id (string)
    :   Required. The UUID of the keystore. You can use the `ibmcloud hpcs uko keystores` command to retrieve the UUID.

    --limit (int64)
    :   Optional. The number of resources to retrieve. The value must be between 1 and 1000.

    --offset (int64)
    :   Optional. The number of resources to skip. The minimum value is 0.

    --sort ([]string)
    :   Optional. The sorting order. The default value is `["name"]`. The list items must match the regular expression `/^-?[a-z0-9_.\\[\\],-]+$/`.

    --all-pages (bool)
    :   Optional. Invoke multiple requests to display all pages of the collection for the associated resources for the keystore.

- Example

    ```
    ibmcloud hpcs uko associated-resources-for-target-keystore \
    --id=93777bca-baef-4070-b9b5-a2e6079df1b4 \
    --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "total_count": 3,
      "limit": 20,
      "offset": 0,
      "first": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_key/5295ad47-2ce9-43c3-b9e7-e5a9482c362b/associated_resources?limit=20"
      },
      "last": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_key/5295ad47-2ce9-43c3-b9e7-e5a9482c362b/associated_resources?limit=20&offset=0"
      },
      "previous": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys?offset=80"
      },
      "next": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys?offset=120"
      },
      "associated_resources": [
        {
          "vault": {
            "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
            "name": "Test Vault Name",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "managed_key": {
            "id": "93777bca-baef-4070-b9b5-a2e6079df1b4",
            "name": "My Managed Key",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "referenced_keystore": {
            "id": "93777bca-baef-4070-b9b5-a2e6079df1b4",
            "name": "My Managed Key",
            "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/managed_keys/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
          },
          "key_id_in_keystore": "93777bca-baef-4070-b9b5-a2e6079df1b4",
          "type": "com_ibm_cloud_kms_registration",
          "com_ibm_cloud_kms_registration": {
            "prevents_key_deletion": false,
            "service_name": "cloud-object-storage",
            "service_instance_name": "Cloud Object Storage-7s",
            "crn": "crn:v1:bluemix:public:cloud-object-storage:global:a/db995d8d9cc715cd99f13b0671d978b6:57da8e3a-a86d-4e01-b840-f22d36e6f23f:bucket:keyprotecttest",
            "description": "some description"
          }
        }
      ]
    }
    ```
    {: screen}


#### hpcs uko keystore-status
{: #command-uko-keystore-status}

Retrieve the status of a target internal or external keystore.

```
ibmcloud hpcs uko keystore-status --id ID
```

- Command options

    --id (string)
    :   Required. The UUID of the keystore. You can use the `ibmcloud hpcs uko keystores` command to retrieve the UUID.

- Example

    ```
    ibmcloud hpcs uko keystore-status \
        --id=0325e05e-2b25-4f13-85b2-2d7f85e54359 \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "last_heartbeat": "2022-01-26T00:56:01Z",
      "health_status": "ok",
      "message": "Ping executed successfully."
    }
    ```
    {: screen}


#### hpcs uko vaults
{: #command-uko-vaults}

List all vaults in the instance.

If the `--all-pages` option is not set, the command only retrieves a single page of the collection.
{: note}

```
ibmcloud hpcs uko vaults [--limit LIMIT] [--offset OFFSET] [--sort SORT] [--name NAME] [--description DESCRIPTION]
```

- Command options

    --limit (int64)
    :   Optional. The number of vaults to retrieve. The maximum value is `1000`. The minimum value is `1`.

    --offset (int64)
    :   Optional. The number of vaults to skip. The minimum value is `0`.

    --sort ([]string)
    :   Optional. The sorting order. The default value is `["-updated_at"]`. The list items must match the regular expression `/^-?[a-z0-9_.\\[\\],-]+$/`.

    --name (string)
    :   Optional. Return only vaults whose names begin with the string. The length must be between 1 and 100 characters. The value must match the regular expression `/.+/`.

    --description (string)
    :   Optional. Return only vaults whose description contains the string. The length is must be between 1 and 200 characters. The value must match the regular expression `/.+/`.

    --all-pages (bool)
    :   Optional. Invoke multiple requests to display all pages of the collection for vaults.

- Example

    ```
    ibmcloud hpcs uko vaults --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "total_count": 2,
      "limit": 20,
      "offset": 0,
      "first": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults?limit=20&limit=20&offset=0"
      },
      "last": {
        "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults?limit=20&limit=20&offset=0&offset=0"
      },
      "vaults": [
        {
          "id": "d0564770-1422-420c-945f-10803a2e24de",
          "name": "EXAMPLE_VAULT_NAME",
          "description": "API Test Vault description update.",
          "created_on": "2022-03-07T09:39:17Z",
          "updated_on": "2022-03-07T14:31:09Z",
          "created_by": "IBMid-1308197YB4",
          "updated_by": "IBMid-1308197YB4",
          "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/d0564770-1422-420c-945f-10803a2e24de"
        },
        {
          "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
          "name": "Test Vault Name",
          "description": "'Test Vault Name' description.",
          "created_at": "2022-03-09T10:57:43Z",
          "updated_at": "2022-03-09T10:57:43Z",
          "created_by": "IBMid-1308197YB4",
          "updated_by": "IBMid-1308197YB4",
          "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
        }
      ]
    }
    ```
    {: screen}

#### hpcs uko vault-create
{: #command-uko-vault-create}

Create a vault in the instance with the specified name and description.

```
ibmcloud hpcs uko vault-create --name NAME [--description DESCRIPTION] 
```

- Command options

    --name (string)
    :   Required. A human-readable name to assign to your vault. To protect your privacy, do not use personal data, such as your name or location. The length must be between 1 and 100 characters. The value must match the regular expression `/^[A-Za-z0-9#@!$%'_-][A-Za-z0-9#@!$% '_-]*$/`.

    --description (string)
    :   Optional. The description of the vault. The length must be between 0 and 200 characters. The value must match the regular expression `/(.|\\n)*/`.

- Example

    ```
    ibmcloud hpcs uko vault-create \
        --name='Example Vault' \
        --description='The description of the creating vault' \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
      "name": "Test Vault Name",
      "description": "'Test Vault Name' description.",
      "created_at": "2022-03-09T10:57:43Z",
      "updated_at": "2022-03-09T10:57:43Z",
      "created_by": "IBMid-1308197YB4",
      "updated_by": "IBMid-1308197YB4",
      "recovery_key_label": "TEKMF.AES.RECOVERY.00001",
      "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
      "keys_count": 100,
      "key_templates_count": 10,
      "keystores_count": 0
    }
    ```
    {: screen}

#### hpcs uko vault-delete
{: #command-uko-vault-delete}

Delete a vault from your instance. Make sure that no keys or keystores are attached to the vault before you run this command.

```
ibmcloud hpcs uko vault-delete --id ID --if-match IF-MATCH
```

- Command options

    --id (string)
    :   Required. The UUID of the vault. You can use the `ibmcloud hpcs uko vaults` command to retrieve the UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko vault` command to retrieve the ETag.

- Example

    ```
    ibmcloud hpcs uko vault-delete \
        --id=a88f6e06-c903-4b9f-8ee0-45bd817bf1b6 \
        --if-match=2022-05-11T14:58:26Z
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    ...
    OK
    ```
    {: screen}

#### hpcs uko vault
{: #command-uko-vault}

Retrieve a vault and its details by specifying the ID.

```
ibmcloud hpcs uko vault --id ID 
```

- Command options

    --id (string)
    :   Required. The UUID of the vault. You can use the `ibmcloud hpcs uko vaults` command to retrieve the UUID.

- Example

    ```
    ibmcloud hpcs uko vault \
        --id=06ce6d7e-9edb-431b-8a96-e88e8a4b266b \
        --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
      "name": "Test Vault Name",
      "description": "'Test Vault Name' description.",
      "created_at": "2022-03-09T10:57:43Z",
      "updated_at": "2022-03-09T10:57:43Z",
      "created_by": "IBMid-1308197YB4",
      "updated_by": "IBMid-1308197YB4",
      "recovery_key_label": "TEKMF.AES.RECOVERY.00001",
      "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
      "keys_count": 100,
      "key_templates_count": 10,
      "keystores_count": 0
    }
    ```
    {: screen}

#### hpcs uko vault-update
{: #command-uko-vault-update}

Update attributes of a vault.

```
ibmcloud hpcs uko vault-update --id ID --if-match IF-MATCH [--name NAME] [--description DESCRIPTION]
```

- Command options

    --id (string)
    :   Required. The UUID of the vault. You can use the `ibmcloud hpcs uko vaults` command to retrieve the UUID.

    --if-match (string)
    :   Required. The precondition of the update, which is the value of the ETag from the header on a GET request. You can use the `ibmcloud hpcs uko vault` command to retrieve the ETag.

    --name (string)
    :   Optional. Updated name of the vault.The length must be between 1 and 100 characters. The value must match the regular expression `/^[A-Za-z0-9#@!$%'_-][A-Za-z0-9#@!$% '_-]*$/`.

    --description (string)
    :   Optional. Updated description of the vault. The length must be between 0 and 200 characters. The value must match the regular expression `/(.|\\n)*/`.

- Example

    ```
    ibmcloud hpcs uko vault-update \
      --id=06ce6d7e-9edb-431b-8a96-e88e8a4b266b \
      --if-match=2022-05-11T14:58:26Z \
      --description='Updated description of the vault' \
      --name="Jakub's Vault" \
      --output json
    ```
    {: pre}

- Output

    Headers:

    | Name | Type | Description |
    | ---- | ---- | ----------- |
    | X-Correlation-ID | String | A unique identifier that is attached to requests and messages that allow reference to a particular transaction or event chain. |
    | ETag | String | Identifier for a specific version of the resource. |
    {: caption="Table. Command output headers" caption-side="bottom"}

    The command returns the output similar to the following example:

    ```
    {
      "id": "5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
      "name": "Test Vault Name",
      "description": "'Test Vault Name' description.",
      "created_at": "2022-03-09T10:57:43Z",
      "updated_at": "2022-03-09T10:57:43Z",
      "created_by": "IBMid-1308197YB4",
      "updated_by": "IBMid-1308197YB4",
      "recovery_key_label": "TEKMF.AES.RECOVERY.00001",
      "href": "https://uko.us-south.hs-crypto.cloud.ibm.com:9549/api/v4/vaults/5295ad47-2ce9-43c3-b9e7-e5a9482c362b",
      "keys_count": 100,
      "key_templates_count": 10,
      "keystores_count": 0
    }
    ```
    {: screen}

### {{site.data.keyword.uko_full_notm}} CLI plug-in commands schema examples
{: #uko-schema-examples}

The following schema examples represent the data that you need to specify for some command options. These examples show the data structure and include placeholder values for the expected value types. When you run a command, replace these values with the values that apply to your environment as appropriate.

#### KeyProperties
{: #uko-key-properties-example-schema}

The following example shows the format of the `KeyProperties` object.

```json
{
  "size" : "256",
  "algorithm" : "aes",
  "activation_date" : "P5Y1M1W2D",
  "expiration_date" : "P1Y2M1W4D",
  "state" : "active"
}
```
{: codeblock}

#### KeyPropertiesUpdate
{: #uko-key-properties-update-example-schema}

The following example shows the format of the `KeyPropertiesUpdate` object.

```json
{
  "size" : "256",
  "activation_date" : "P5Y1M1W2D",
  "expiration_date" : "P1Y2M1W4D",
  "state" : "active"
}
```
{: codeblock}

#### KeystoreCreationRequest
{: #uko-keystore-creation-request-example-schema}

The following example shows the format of the `KeystoreCreationRequest` object.

```json
{
  "name": "IBM Cloud Keystore",
  "description": "IBM Cloud Keystore description.",
  "groups": [
    "Production"
  ],
  "ibm_api_endpoint": "https://us-south.kms.cloud.ibm.com",
  "ibm_iam_endpoint": "https://iam.bluemix.net/identity/token",
  "ibm_api_key": "bxgstahGH8273662-HGD8765ghsvv-hsjbv786KJHV",
  "ibm_instance_id": "r64jshf0a4-jh87-8476-jks3-9752hgdvs",
  "vault": {
    "id": "75d0f626-44b0-4076-80cd-8cb9e485fe73"
  },
  "ibm_variant": "hpcs",
  "ibm_key_ring": "IBM-Cloud-KMS-Internal",
  "type": "ibm_cloud_kms"
}
```
{: codeblock}

#### KeystoreUpdateRequest
{: #uko-keystore-update-request-example-schema}

The following example shows the format of the `KeystoreUpdateRequest` object.

```json
{
  "name": "IBM Cloud Keystore",
  "description": "IBM Cloud Keystore description.",
  "groups": [
    "Production"
  ],
  "ibm_api_endpoint": "https://us-south.kms.cloud.ibm.com",
  "ibm_iam_endpoint": "https://iam.bluemix.net/identity/token",
  "ibm_api_key": "***",
  "ibm_instance_id": "c9e2e2d5-013a-409f-93cf-5393972263d7",
  "ibm_key_ring": "Key-Ring-1"
}
```
{: codeblock}

#### KeystoresPropertiesCreate[]
{: #uko-keystores-properties-create-example-schema}

The following example shows the format of the `KeystoresPropertiesCreate[]` object.

```json

[ {
  "group" : "Production",
  "type" : "ibm_cloud_kms",
  "google_key_protection_level" : "software",
  "google_key_purpose" : "encrypt_decrypt",
  "google_kms_algorithm" : "google_symmetric_encryption"
} ]
```
{: codeblock}

#### KeystoresPropertiesUpdate[]
{: #uko-keystores-properties-update-example-schema}

The following example shows the format of the `KeystoresPropertiesUpdate[]` object.

```json
[ {
  "group" : "Production",
  "google_key_protection_level" : "software",
  "google_key_purpose" : "encrypt_decrypt",
  "google_kms_algorithm" : "google_symmetric_encryption"
} ]
```
{: codeblock}

#### Tag[]
{: #uko-tag-example-schema}

The following example shows the format of the `Tag[]` object.

```json
[ {
  "name" : "exampleString",
  "value" : "exampleString"
} ]
```
{: codeblock}

#### VaultReferenceInCreationRequest
{: #uko-vault-reference-in-creation-request-example-schema}

The following example shows the format of the `VaultReferenceInCreationRequest` object.

```json
{
  "id" : "5295ad47-2ce9-43c3-b9e7-e5a9482c362b"
}
```
{: codeblock}
