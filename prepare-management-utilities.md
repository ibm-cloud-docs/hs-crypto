---

copyright:
  years: 2019, 2020
lastupdated: "2020-03-26"

keywords: smart card, smart card reader, trusted key entry, tke, master key, initialize service, load master key

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}

# Setting up the Management Utilities
{: #prepare-management-utilities}

Using the [{{site.data.keyword.IBM_notm}} {{site.data.keyword.hscrypto}} Management Utilities](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-management-utilities), you can initialize service instances with the highest level of security. The Management Utilities use smart cards for storing [signature keys](#x8250375){: term} and [master key](#x2908413){: term} parts.
{: shortdesc}

To use the Management Utilities, you need to order smart cards and smart card readers, install a smart card reader driver on your workstation, install the management utilities, and initialize the smart cards to use. Complete the following steps to set up the Management Utilities.

## Step 1: Order smart cards and smart card readers
{: #order-smart-card-and-reader}

Before you can configure smart cards, you need to first order [smart cards](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-smart-cards) and [smart card readers](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-smart-card-reader) online.

### Ordering smart cards
{: #order-smart-card}

Complete the following steps to order smart cards:

1. On the [{{site.data.keyword.IBM_notm}} Maintenance Parts Retail shop web page](https://www-store.shop.ibm.com/shop/en-US/partsusretail){: external}, enter part number **00RY790** in the search box.
2. Enter the quantity of packages. Each package contains two smart cards.

  A minimum of two smart cards is needed to use the Management Utilities: a certificate authority smart card and an Enterprise PKCS#11 (EP11) smart card. The certificate authority smart card defines a set of smart cards that can work together. This set of smart cards is called a smart card zone. EP11 smart cards hold a signature key and one or more master key parts that are used to configure service instances. Currently, the Management Utilities support 2 or 3 master key parts to be loaded.

  For added security, the 2 or 3 master key parts that are used to configure a service instance can be generated on separate EP11 smart cards that are assigned to different people. The signature key used to sign commands to the crypto module can be generated on a separate EP11 smart card. Three or four EP11 smart cards would then be needed to configure a service instance.

  It is also suggested to create backup copies of all used smart cards and to save the backup smart cards in a secure place. For maximum security, 10 smart cards would be needed, including backup smart cards (two certificate authority smart cards and eight EP11 smart cards).

3. Click **Add to Current Order** and continue to check out.

Online smart card ordering is currently only available in the United States. For procurement from other countries, contact IBM Part Sales through one of the following email addresses, and provide the Field Replaceable Unit (FRU) number of the smart card, which is 00RY790 in this case.

|Country| Email address |
|--------------|-----------------------|
|Germany | partsale@de.ibm.com|
|Switzerland | pasa@ch.ibm.com|
|Belgium  | parts@be.ibm.com|
|Spain    | ventadepiezas@es.ibm.com|
|UK | parts_sales@uk.ibm.com|
{: caption="Table 1. IBM Part Sales contacts" caption-side="top"}

### Ordering smart card readers

Complete the following steps to order smart card readers:

1. On the [Identiv SPR332 V2.0 smart card readers online shop web page](https://shop.identiv.com/smart-card-readers/contact-contactless/spr332v2.htm){: external}, enter the number of the smart card readers.

  You need at least two smart card readers. Smart card reader 1 for initializing the certificate authority smart card and retrieving the signature key to sign commands. And smart card reader 2 for initializing EP11 smart cards and retrieving master key parts to be loaded.
2. Click **Add to Cart** and continue to check out.

## Step 2: Install the smart card reader driver
{: #install-smart-card-reader-driver}

You need to install the Identiv SPR332 V2 smart card reader driver on your local workstation. Currently, only the Linux&reg; operating system is supported.

<!--
Currently, you can choose to install it on the Microsoft Windows&reg; 10 or the Linux&reg; operating system.

### Installing smart card reader driver on Windows 10
{: #reader-driver-windows}

By default, the Windows 10 operating system uses the Microsoft USB CCID smart card reader driver, which, however, does not support secure personal identification number (PIN) entry. To upgrade the driver to Identiv SPR332 V2, take the following steps:

1. Plug the Identiv SPR332 V2 smart card readers into the USB ports on the Windows workstation.
2. Open the Device Manager by typing **Device Manager** in the search box on the Windows taskbar and selecting it from the menu.
3. Expand **Smart card readers** in Device Manager. If any entry says **Microsoft Usbccid Smartcard Reader (WUDF)**, select **Update driver** and double click **Search automatically for updated driver software**.
4. Repeat step 3 for all entries under the **Smart card readers** section.
5. Check and update the firmware level of the smart card driver to 7.06 by downloading **SPR332v2 Firmware Update 7.06** from the [Identiv SPR332 v2.0 Support website](https://support.identiv.com/spr332/){: external}.

  Firmware prior to 7.06 might cause misinterpretation of some PIN entry actions, such as cancellation or time-out.

### Installing smart card reader driver on Linux
{: #reader-driver-linux}
-->

Before you install the smart card reader driver on a Linux operating system, download and extract the driver package from the [Identiv SPR332 v2.0 Support website](https://support.identiv.com/spr332/){: external}. And then, install the smart card reader driver by completing the following steps:

<!--depending on your Linux distributions:

- Fedora 30

  1. Install the `pcsc-lite` package with the following command:

    ```
    sudo dnf install pcsc-lite
    ```
    {:pre}

  2. Install the `libusb` package with the following command:

    ```
    sudo dnf install libusb
    ```
    {:pre}

  3. Run the `install.sh` script, which is included in the downloaded driver package.

- openSUSE Leap 15.1

  1. Install the `pcsc-ccid` package with the following command:

    ```
    sudo zypper install pcsc-ccid
    ```
    {:pre}

  2. Run the `install.sh` script, which is included in the downloaded driver package.

  3. Restart the system to restart the `pcsc` daemon.
-->

- Red Hat Enterprise Linux 8.0.0

  1. Install the `pcsc-lite` package with the following command:

    ```
    sudo yum install pcsc-lite
    ```
    {:pre}

  2. Install the `libusb` package with the following command:

    ```
    sudo yum install libusb
    ```
    {:pre}

  3. Check and make sure that the `opensc` and `esc` packages are not installed. These packages can cause unexpected errors to occur during the operations of the smart card readers.

    Run the following command to display all installed `opensc` or `esc` packages. Replace `<package_name>` with `opensc` or `esc`:

    ```
    sudo yum list installed <package_name>
    ```
    {: pre}

    If any packages are listed, remove them using the following commands. Replace `<package_name>` with `opensc` or `esc`:

    ```
    sudo yum remove <package_name>
    ```
    {: pre}

  4. Run the `install.sh` script, which is included in the downloaded driver package.

  5. Start the `pcsc` daemon with the `sudo pcscd` command.

<!--
- Ubuntu 18.04.3 LTS

  1. Install the `pcscd` package with the following command:

    ```
    sudo apt install pcscd
    ```
    {:pre}

  2. Run the `install.sh` script, which is included in the downloaded driver package.
-->

## Step 3: Install the Management Utilities
{: #install-management-utility-application}

Two applications are provided as part of the Management Utilities: the [Smart Card Utility Program](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-smart-card-application) and the [Trusted Key Entry (TKE) application](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-tke-application). The Smart Card Utility Program allows you to initialize the smart cards to use. The TKE application uses the smart cards to load master keys in service instances.

<!--
### Installing the Management Utilities on Windows 10
{: #install-application-windows}

To install the utilities on Windows 10, complete the following steps:

1. Download the installation file `cloudtke.exe` from [GitHub](https://github.com/IBM-Cloud/hpcs-management-utilities/){:external} to your workstation.
2. In the directory that the downloaded installation file is located, double click the file to install.

### Installing the Management Utilities on Linux
{: #install-application-linux}
-->

To install the applications on Linux, complete the following steps:

1. Download the installation file, `cloudtke.bin`, from [GitHub](https://github.com/IBM-Cloud/hpcs-management-utilities/releases){: external} to your workstation.
2. (Optional) [Verify the integrity and authenticity of the downloaded `cloudtke.bin` file](#verify-code-signing).
3. Open the terminal, enter the directory that the downloaded installation file is located, and perform the following steps to install the applications:

  1. Add the execute permission to the installation file by running the following command:

    ```
    chmod +x cloudtke.bin
    ```
    {: pre}

  2. Install the applications by running the following command:

    ```
    ./cloudtke.bin
    ```
    {: pre}

  3. When prompted, choose not to install links to the Management Utilities applications, and then install the applications to any subdirectories.

### Optional: Verifying the integrity and authenticity of the installation file
{: #verify-code-signing}

For maximum security, it is recommended that you verify the integrity and authenticity of the Management Utilities installation file before you install or update the applications. If the verification fails, cancel the installation and [contact IBM for support](/docs/hs-crypto?topic=hs-crypto-troubleshooting#getting-help).

{{site.data.keyword.hscrypto}} Management Utilities enable [signed code verification](https://en.wikipedia.org/wiki/Code_signing){: external} to ensure that the signature matches the original code. If the downloaded installation file is altered or corrupted, a different signature is produced and the verification fails.

Complete the following steps to make sure the applications are not tampered with or corrupted during the download process:

Perform step 2 to step 4 by using the [OpenSSL command-line tool](https://wiki.openssl.org/index.php/Binaries){: external}.
{: tip}

1. Download the following files from [GitHub](https://github.com/IBM-Cloud/hpcs-management-utilities/releases){: external} to the same directory where you store the `cloudtke.bin` file:
  * `cloudtke.sig`: The signed cryptographic hash of `cloudtke.bin` (SHA-256).
  * `digicert_cert.pem`: An intermediate code signing certificate to prove the Management Utilities signing certificate.
  * `signing_cert.pem`: The signing certificate of the Management Utilities.

2. Extract the public key from the signing certificate `signing_cert.pem` to the `sigkey.pub` file with the following command by using the [OpenSSL command-line tool](https://wiki.openssl.org/index.php/Binaries):

  ```
  openssl x509 -pubkey -noout -in signing_cert.pem -out sigkey.pub
  ```
  {: pre}

3. Verify the integrity of the `cloudtke.bin` file with the following command:

  ```
  openssl dgst -sha256 -verify sigkey.pub -signature cloudtke.sig cloudtke.bin
  ```
  {: pre}
  When the verification is successful, `Verified OK` is displayed.

4. Verify the authenticity and validity of the signing certificate with the following command:

  ```
  openssl ocsp -no_nonce -issuer digicert_cert.pem -cert signing_cert.pem -VAfile digicert_cert.pem -text -url http://ocsp.digicert.com -respout ocsptest
  ```
  {: pre}
  When the verification is successful, `Response verify OK` and `signing_cert.pem: good` are displayed in the output.

## Step 4: Configure smart cards with the Smart Card Utility Program
{: #configure-smart-card-utility}

Two types of smart cards are used in the Management Utilities, the certificate authority smart card and EP11 smart cards. The certificate authority smart card is used to define a smart card zone and create a set of EP11 smart cards in the zone, while an EP11 smart card is used to generate and store an administrator signature key and master key parts.

To configure smart cards, use the Smart Card Utility Program to complete the following tasks.

### Initializing the certificate authority smart card
{: #initialize-ca-smart-card}

To create and initialize a certificate authority smart card, follow these steps:

1. To start the Smart Card Utility Program, go to the subdirectory where you install the Management Utilities applications and run the following command:
  ```
  ./scup
  ```
  {: pre}

2. After the Smart Card Utility Program is started, from the **CA Smart Card** menu,  select **Initialize and personalize CA smart card**.
3. Insert the smart card to be initialized into a smart card reader 1, and click **OK**.

  If you receive a message similar to **No smart card inserted**, try the following solutions:
  * Insert the smart card into another smart card reader. The smart card reader that you picked might not be smart card reader 1.
  * Reinsert the smart card into the same smart card reader. The smart card reader might not be reading the smart card properly.
4. Enter a six-digit personal identification number (PIN) twice on the smart card reader PIN pad as the first certificate authority card PIN.
5. Enter a six-digit PIN twice on the smart card reader PIN pad as the second certificate authority card PIN. You need to enter both PINs later when you use the certificate authority smart card.
6. Enter a description for the smart card zone that holds the EP11 smart cards.
7. Enter a description for the certificate authority smart card.

The certificate authority is created.

It is recommended to create a backup copy of your certificate authority smart card. You can create a backup copy by clicking **CA Smart Card** &gt; **Backup CA smart card**.
{: important}

### Initializing the EP11 smart card
{: #initialize-ep11-smart-card}

To create and initialize an EP11 smart card, follow these steps:

1. Select **EP11 Smart Card** &gt; **Initialize and enroll EP11 smart card** from the menu.
2. Insert the smart card to be initialized as the EP11 smart card in smart card reader 2 and click **OK**.
3. Select **EP11 Smart Card** &gt; **Personalize EP11 smart card** from the menu bar.
4. Enter a six-digit PIN twice on the smart card reader PIN pad. You need to enter this PIN later when you use the EP11 smart card.
5. Enter a description for the EP11 smart card.
6. If you have more than one EP11 smart card, repeat step 1 to step 5 to initialize other EP11 smart cards.

Your EP11 smart cards are created and personalized.

<!--
### Unblocking an EP11 smart card
{: #unblock-ep11-smart-card}

If you enter a wrong PIN for an EP11 smart card continuously for three times, the EP11 smart card becomes blocked. You need to use the certificate authority smart card that sets the EP11 smart card zone to unblock the EP11 smart card.

1. Select **EP11 Smart Card** &gt; **Unblock EP11 smart card** from the menu.
2. Insert the certificate authority smart card associated with the EP11 smart card in smart card reader 1, and click **OK**.
3. Enter the PIN of the certificate authority smart card on the smart card reader PIN pad.
4. Insert the EP11 smart card that you want to unblock in smart card reader 2, and click **OK**.
-->

## What's next
{: #prepare-management-utilities-next}

- After you set up the Management Utilities, you can start to load the master key with the TKE application. For detailed instructions, see [Loading master keys with the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities).
- If you need to uninstall the Management Utilities, refer to [Uninstall the Management Utilities](/docs/hs-crypto?topic=hs-crypto-delete-instance#uninstall-management-utilities).
