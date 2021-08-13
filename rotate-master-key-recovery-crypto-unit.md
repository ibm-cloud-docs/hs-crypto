---

copyright:
  years: 2020, 2021
lastupdated: "2021-08-12"

keywords: rotate, rotate master key, master key rotation, master key rolling, rewrap root key, reencrypt root key

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}


# Rotating master keys by using recovery crypto units
{: #rotate-master-key-cli-recovery-crypto-unit}

To rotate the master key by using recovery crypto units, follow these steps. In this case, a random master key value is generated in a recovery crypto unit, securely transferred to other crypto units, and rotated automatically with the `ibmcloud tke auto-mk-rotate` command.
{: shortdesc}

When master key rotation is taking place, you are temporarily not able to access your keystore. To learn how master key rotation works, see [the introduction to the master key rotation](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).

Make sure that you are assigned the **Manager** or **Crypto unit administrator** service access role to perform TKE CLI operations. For more information about the access management, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).

Use the `ibmcloud tke auto-mk-rotate` command to rotate your master key only when you have recovery crypto units set up and PKCS #11 keystores are not enabled in your service instance. Otherwise, see [Rotating master keys by using key parts](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-key-parts) for instructions. For the recovery crypto unit supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).
{: important}

## Rotating master keys
{: #rotate-master-key-cli-recovery-crypto-unit-steps}

Before you rotate the master key by using recovery crypto units, make sure that you complete the [steps to set up the IBM Cloud CLI with TKE plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-prerequisite).

To rotate master keys by using recovery crypto units, use the following command:

```
ibmcloud tke auto-mk-rotate
```
{: pre}

If multiple service instances are assigned to your resource group, select the service instance where the master key is to be rotated from the service instance list displayed.

After you select a service instance, all crypto units in the service instance become selected. The command checks the initial state of the crypto units to make sure that the master keys can be rotated:

* If the required initial conditions are not met, an error is reported and the command ends. In this case, you can check how your crypto units are configured by running the `ibmcloud tke cryptounit-compare` command.
* If the required initial conditions are met, a random master key value is generated in the new master key register of one of the recovery crypto units. The value is securely copied to the other crypto units of the service instance. A command is issued to reencrypt the contents of key storage for your service instance by using the current and new master key register values.

When key storage is completely reencrypted, the value in the new master key register is promoted to the current master key register in all crypto units and the new master key registers are cleared. A success message is displayed when the master key rotation is completed.

It might take approximately 60 seconds to reencrypt 3000 root keys. When the master key is being rotated, you cannot perform any key-related actions except for deleting keys.
{: note}

If an error occurs during master key rotation, see [Why can't I rotate master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation-recovery-crypto-units).

## What's next
{: #rotate-master-key-cli-recovery-crypto-unit-next}

- To learn more about master key rotation, check out [Master key rotation introduction](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).
- Go to the **KMS keys** tab of your instance dashboard to [manage root keys and standard keys](/docs/hs-crypto?topic=hs-crypto-get-started#manage-keys). To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management API reference doc](/apidocs/hs-crypto){: external}.
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
