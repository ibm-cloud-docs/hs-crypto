---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-30"

keywords: initialize service instance, load master key, key ceremony, recovery crypto unit

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Initializing service instances using recovery crypto units
{: #initialize-hsm-recovery-crypto-unit}

Before you can use your {{site.data.keyword.hscrypto}} instance, you need to first initialize your service instance by loading the master key. This topic guides you through the steps to initialize your service instance by using recovery crypto units through {{site.data.keyword.cloud_notm}} TKE CLI plug-in.
{: shortdesc}

For an introduction to the approaches of service instance initialization and the related fundamental concepts, see [Initializing service instances](/docs/hs-crypto?topic=hs-crypto-introduce-service) and [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode).

Currently, service instances in the `eu-es` region don't support recovery crypto units. When a service instance is provisioned in other supported regions, you are by default enabled with the option to back up your master keys in the recovery crypto units located in the disaster recovery region. For more information about supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).

If smart cards are used to initialize the service instance, the recovery crypto units are not applicable and can be ignored. The backup of the master key relies on the backup of the smart cards in that case.

You can automate the instance initialization with recovery crypto units by using Terraform. For more information, see [Setting up Terraform for {{site.data.keyword.hscrypto}}](/docs/hs-crypto?topic=hs-crypto-terraform-setup-for-hpcs).

It is your responsibility to secure assets used to initialize the {{site.data.keyword.hscrypto}} instance. For best practices, see [the FAQ](/docs/hs-crypto?topic=hs-crypto-faq-support-maintenance#faq-manage-smartcards).
{: note}

## Initializing service instances
{: #initialize-hsm-recovery-crypto-unit-steps}

To initialize your service instance using recovery crypto units, complete the following steps:

1. Complete [the prerequisite steps](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite).
2. Run the following command:

    ```
    ibmcloud tke auto-init
    ```
    {: pre}

    Follow this procedure to initialize your service instance. Complete the steps by following the prompts:

    1. Select the instance that you want to initialize.

        If you have multiple service instances in the current resource group, this command lists all the available instances with a number that is associated to each instance. Enter the INSTANCE NUM to select the instance that you want to initialize and press enter to continue.

        The following output is an example that is displayed:

        ```
        More than one service instance is assigned to the current resource group.

        INSTANCE NUM   INSTANCE ID
        1              0a08af7e-02d0-4122-9146-4179b15f9bfb
        2              0f130264-12f5-45bf-9bac-975cdb605804
        3              bc712c1b-8ff5-4ea0-9cf4-fd74233ceaaf

        Enter the INSTANCE NUM of the service instance you want to initialize.
        > 3
        ```
        {: screen}

        After you choose the service instance, all crypto units, including failover crypto units if any, for the service instance become selected. These crypto units must be in the zeroized state, also referred to as _imprint mode_. If not, an error is reported and the command ends. If this happens, you can use the `ibmcloud tke cryptounit-compare` command to see how the crypto units are configured. If current master key registers are not set, you can zeroize the crypto units with the `ibmcloud tke cryptounit-zeroize` command and rerun the `ibmcloud tke auto-init` command.

        You must not zeroize the crypto units if key storage for the service instance contains data. Otherwise, all data in key storage will be lost and you will be not able to access any keys or data in your service instance.
        {: important}

    2. Set the value of two [signature thresholds](/docs/hs-crypto?topic=hs-crypto-understand-concepts#signature-thresholds-concept): signature threshold and revocation signature thresholds.

        When prompted, enter the number for the signature threshold first and then for the revocation signature threshold. The numbers must be between one and eight. The two threshold numbers can be different. Setting the signature thresholds to a value greater than one is a way to enforce [quorum authentication](/docs/hs-crypto?topic=hs-crypto-understand-concepts#quorum-authenticaion-concept) for sensitive operations.

        The following output is an example that is displayed:

        ```
        ENTER SIGNATURE THRESHOLD VALUES

        Enter the number of signatures to be required on commands sent to the service instance.  This must be a number between 1 and 8.  To enforce dual control, this must be at least 2:
        > 1

        Enter the number of signatures to be required on commands to remove an administrator.  This must be a number between 1 and 8.  To enforce dual control, this must be at least 2:
        > 1
        ```
        {: screen}

    3. Add [crypto unit administrators](/docs/hs-crypto?topic=hs-crypto-understand-concepts#admin-concept).

        When prompted, enter the number of administrators that you want to add to the crypto units. The number needs to be equal to or greater than the signature threshold values that you set in the previous step.

        The command then lists existing signature key files available on your workstation. You can create administrators by selecting the existing signature key files, or by generating new signature keys. The new signature key files are also saved in the directory that you specify with the `CLOUDTKEFILES` environment variable on your local workstation.

        The following output is an example that is displayed:

        ```
        ENTER NUMBER OF ADMINISTRATORS TO INSTALL

        To initialize and maintain your crypto units, administrators  must be installed. Each administrator has an associated signature key. Signature keys are stored in files protected by a password. To use the signature key, you must supply the password.

        To enforce dual control, each signature key file needs to be assigned to a different user and only that user needs to know the password.

        You can install up to eight administrators in a crypto unit.  To set a signature threshold value of 1 and a revocation signature threshold of 1, you must install at least 1 administrator.

        Enter the number of administrators you want to install:
        > 1

        SELECT EXISTING SIGNATURE KEY FILES TO USE

        The following signature key files were found on this workstation:

        KEYNUM   DESCRIPTION   SUBJECT KEY IDENTIFIER
        1        admin1        665527ed7e97c2a083dab035f40c65...
        2        admin2        741a60c0a875cd91195b71f6db3cb5...

        Enter the KEYNUM of any existing signature key files you want to use to create administrators. If you don't want to use existing signature key files, press enter without entering any KEYNUM values.

        If you want to use a combination of existing and new signature keys, enter the KEYNUM values of the existing signature key files you want to use.  You will be prompted to enter information for any new signature key files after that.

        Enter the KEYNUM of the existing signature key files you want to use to create administrators:
        > 1
        Enter the password for the signature key identified by:
        admin1 (665527ed7e97c2a083dab035f40c65...)
        >
        ```
        {: screen}

        The signature key file is protected by password. You need to remember the passwords that you enter when creating new signature key files and make sure the files are not removed from your workstation. Otherwise, you are not able to perform future administrative actions that need to be signed, such as [rotating master keys](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit).
        {: important}

    4. Load the master key to crypto units.

        A random master key value is generated in a recovery crypto unit and is then transferred to all the other crypto units in the service instance.

        The following output is an example that is displayed:

        ```
        You asked to install one administrator and selected one existing signature key to use.  No new signature key files will be created.

        Installing 1 of 1 administrators....
        Setting signature thresholds....
        Generating a random master key value....
        Transferring the master key value to 1 of 3 crypto units....
        Transferring the master key value to 2 of 3 crypto units....
        Transferring the master key value to 3 of 3 crypto units....

        OK
        The selected service instance has been initialized.
        To see what administrators are installed and what signature threshold and master key register values are set, use the 'ibmcloud tke cryptounit-compare' command.
        ```
        {: screen}

3. (Optional) Use the following command to check the status of crypto units to make sure all the current master key registers are in the `VALID` state:

    ```
    ibmcloud tke cryptounit-compare
    ```
    {: pre}

    For the complete master key loading process, see [understanding the master key](/docs/hs-crypto?topic=hs-crypto-introduce-service#understand-key-ceremony).


## What's next
{: #initialize-hsm-recovery-crypto-unit-whats-next}

- After you have a master key loaded to your service instance, you can rotate the master key on demand to meet industry standards and cryptographic best practices. For detailed instructions, see [Rotating master keys using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit).
- Recovery crypto units contain a backup copy of the master key value that can be used to recover the master key. For the detailed instructions, see [Recovering a master key from a recovery crypto unit](/docs/hs-crypto?topic=hs-crypto-recover-master-key-recovery-crypto-unit).
- For a complete TKE CLI plug-in command reference, see [{{site.data.keyword.cloud_notm}} TKE CLI](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#tke-cli-plugin){: external}.
