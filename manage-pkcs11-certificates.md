---

copyright:
  years: 2023, 2024
lastupdated: "2024-10-09"

keywords: pkcs11 certificate, view ep11 certificate, delete ep11 certificate

subcollection: hs-crypto

---


{{site.data.keyword.attribute-definition-list}}



# Managing EP11 certificates with the UI
{: #manage-ep11-certificate-ui}

Enterprise PKCS #11 (EP11) certificates store public key or attribute certificates. Apart from using the {{site.data.keyword.hscrypto}} [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-set-up-pkcs-api) to manage EP11 certificates, you can also use the UI to view, download, and delete EP11 certificates.
{: shortdesc}

Currently, creating EP11 certificates with the UI is not supported. If you want to create EP11 certificates, you need to use the [PKCS #11 API](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
{: note}

## Before you begin
{: #manage-ep11-certificate-ui-before}

Before you can manage EP11 certificates with the UI, complete the following steps to open your {{site.data.keyword.hscrypto}} dashboard:

1. [Log in to the UI](https://cloud.ibm.com/login){: external}.
2. Go to **Menu** &gt; **Resource list** to view a list of your resources.
3. From your {{site.data.keyword.cloud_notm}} resource list, select your provisioned instance of {{site.data.keyword.hscrypto}} and click the instance name.

## Viewing EP11 certificates
{: #view-ep11-certificate-ui}

For default service access roles that support viewing EP11 certificates, see [service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles). If you are to create custom roles, make sure to assign the following action to the custom role:

* `hs-crypto.keystore.listkeystoresbyids`
* `hs-crypto.keystore.listkeysbyids`

For instructions on creating custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

### Viewing EP11 certificate list
{: #view-ep11-certificate-list-ui}

To view a list of created EP11 certificates, on the {{site.data.keyword.hscrypto}} dashboard, select the **EP11 certificates** tab in the side menu.

An EP11 certificate table is displayed with the following details.

To customize how the table is to be presented, click the **Settings icon** ![Settings icon](../icons/settings.svg "Settings") and check the columns to be displayed.
{: tip}

| Property | Description |
| --- | --- |
| Common name  | A human-readable alias for easy identification of your certificate. The certificate name might not be unique. You can assign multiple certificates with the same name. |
| Organization | The organization that the certificate belongs to. |
| Organizational unit | The organization unit that the certificate belongs to. |
| Country | The country where the certificate locates. |
| State or province |  The state or province where the certificate locates.  |
| Locality | The specific location where the certificate locates. |
| Serial number |  The serial number of the certificate. |
| Certificate type | The type of the certificate. Three certificate types are available: X.509 public key certificate, WTLS public key certificate, and X.509 attribute certificate. |
| Certificate category | The category of the certificate. Available certificate categories are: user certificate, CA certificate, and other end-entity certificate. By default, the category is unspecified. |
| Issue date | The date when the certificate is issued. |
| Expiration date | The expiration date of the certificate. If the certificate is expired, an error icon is displayed. |
| Issuer | The issuer of the certificate. |
| Label | The description of the certificate. |
| Version | The version number of the certificate. |
| Keystore | The keystore ID where the certificate is stored. |
{: caption="The properties displayed in the EP11 certificates table" caption-side="bottom"}

### Viewing EP11 certificate details
{: #view-ep11-certificate-details-ui}

To view more details about each certificate, complete the following steps:

1. Select the **EP11 certificates** tab in the side menu, and find the certificate that you want to view in the list.
2. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then select **View certificate details**.
3. A side panel is displayed to show the following certificate details. 

    Depending on the method of creating your EP11 certificate, the attributes shown in the details side panel might vary.
    {: note}

    | Attribute | Description |
    | --- | --- |
    | Common name  | A human-readable alias for easy identification of your certificate. The certificate name might not be unique. You can assign multiple certificates with the same name. |
    | Certificate | The certificate body. You can download the certificate by clicking **Download**. You can also copy the certificate body by clicking the copy icon.  |
    | CKA_MODIFIABLE | Indicates whether the certificate can be modified. The valid value is `true` or `false`, with `true` indicating the certificate can be modified. |
    | CKA_CERTIFICATE_TYPE | The type of the certificate. Three certificate types are available: X.509 public key certificate, WTLS public key certificate, and X.509 attribute certificate. |
    | CKA_CLASS |  Object class. For certificates, the value is `Certificate`.  |
    | CKA_TOKEN | Indicates whether the certificate is a token object. The valid value is `true` or `false`, with `true` indicating the certificate is a token object and `false` indicating the certificate is a session object. |
    | CKA_PRIVATE |  Indicates whether the certificate is a private object. The valid value is `true` or `false`, with `true` indicating the certificate is a private object and `false` indicating the certificate is a public object. |
    | CKA_CERTIFICATE_CATEGORY | The category of the certificate. Available certificate categories are: user certificate, CA certificate, and other end-entity certificate. By default, the value is `Unspecified`. |
    | CKA_SERIAL_NUMBER | DER-encoding of the certificate serial number. By default, the value is empty. |
    | CKA_ISSUER | DER-encoding or WTLS-encoding of the certificate issuer depending on the certificate type. By default, the value is empty.  |
    | CKA_SUBJECT | DER-encoding or WTLS-encoding of the certificate subject depending on the certificate type. By default, the value is empty.  |
    | CKA_ID | Key identifier for public and private key pair. By default, the value is empty. |
    | CKA_LABEL | Description of the certificate. By default, the value is empty. |
    {: caption="The attributes for each certificate" caption-side="bottom"}

## Downloading EP11 certificates
{: #download-ep11-certificate-ui}

For default service access roles that support downloading EP11 certificates, see [service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles). If you are to create custom roles, make sure to assign the following action to the custom role:

* `hs-crypto.keystore.listkeystoresbyids`
* `hs-crypto.keystore.listkeysbyids`

For instructions on creating custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

To download an EP11 certificate, complete either of the following procedures:

- Procedure 1

    1. Select the **EP11 certificates** tab in the side menu, and find the certificate that you want to download in the list.
    2. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then select **Download certificate**.

- Procedure 2

    1. Select the **EP11 certificates** tab in the side menu, and find the certificate that you want to download in the list.
    2. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then select **View certificate details**.
    3. A side panel is displayed to show the certificate details. Click **Download** to download the certificate.

After you download an EP11 certificate, you can find the certificate in your web browser's default download folder. The name of the certificate is in a format of `certificate-<serial number>.pem`. If the serial number is empty, the file name is `certificate-<YYYYMMDD>.pem` where the `YYYYMMDD` is the timestamp of the download.


## Deleting EP11 certificates
{: #delete-ep11-certificate-ui}

For default service access roles that support deleting EP11 certificates, see [service access roles](/docs/hs-crypto?topic=hs-crypto-manage-access#service-access-roles). If you are to create custom roles, make sure to assign the following actions to the custom role:

* `hs-crypto.keystore.listkeystoresbyids`
* `hs-crypto.keystore.listkeysbyids`
* `hs-crypto.keystore.deletekey`

For instructions on creating custom roles, see [Creating custom roles](/docs/account?topic=account-custom-roles).

If you want to delete an EP11 certificate, complete the following steps:

After you delete a certificate, you are not able to access any resources that are associated with the certificate. This action cannot be undone.
{: important}

1. Select the **EP11 certificates** tab in the side menu, and find the certificate that you want to delete in the list.
2. Click the **Actions** icon ![Actions icon](../icons/action-menu-icon.svg "Actions"), and then select **Delete certificate**.
3. Verify the name of the certificate to be deleted, and check the box to confirm the deletion.
4. Click **Delete certificate**.

## What's next
{: #manage-ep11-certificate-ui-next}

To learn more about the PKCS #11 API, see [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref).
