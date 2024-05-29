---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-29"

keywords: rotate, rotate master key, master key rotation, master key rolling, rewrap root key, reencrypt root key

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}





# Rotating master keys by using recovery crypto units
{: #rotate-master-key-cli-recovery-crypto-unit}

To rotate the master key by using recovery crypto units, follow these steps. In this case, a random master key value is generated in a recovery crypto unit, securely transferred to other crypto units, and rotated automatically with the `ibmcloud tke auto-mk-rotate` command.
{: shortdesc}

When master key rotation is taking place, you are temporarily not able to access your keystore. To learn how master key rotation works, see the introduction to the master key rotation [for the standard plan](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro) or [for the {{site.data.keyword.uko_full_notm}} plan](/docs/hs-crypto?topic=hs-crypto-uko-master-key-rotation-intro).

Make sure that you are assigned the **Manager** service access role or the **Crypto unit administrator** role to perform TKE CLI operations. For more information about the access management, see Managing user access [for the standard plan](/docs/hs-crypto?topic=hs-crypto-manage-access) or [for the {{site.data.keyword.uko_full_notm}} plan](/docs/hs-crypto?topic=hs-crypto-uko-manage-access).

When the master key is being rotated, you can still perform some KMS key actions such as listing keys, retrieving key metadata, or deleting keys, but you cannot create or rotate keys. You cannot call either the PKCS #11 API or GREP11 API during the master key rotation.
{: note}

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

When key storage is completely reencrypted, the value in the new master key register is promoted to the current master key register in all crypto units and the new master key registers are cleared. A success message is displayed when the master key rotation is completed. It might take approximately 60 seconds to reencrypt 3000 keys.


Key objects in the in-memory keystore are not automatically rotated after the master key rotation. If PKCS #11 keystores are enabled in your service instance, you need to restart all active PKCS #11 applications to clear the in-memory keystore after the master key rotation is complete. For detailed information, see [PKCS #11 implementation components](/docs/hs-crypto?topic=hs-crypto-uko-pkcs11-intro#uko-pkcs11-components).
{: important}


If an error occurs during master key rotation, see [Why can't I rotate master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-troubleshoot-master-key-rotation-recovery-crypto-units).

## What's next
{: #rotate-master-key-cli-recovery-crypto-unit-next}


- To find out more about programmatically managing your keys, check out the {{site.data.keyword.hscrypto}} [key management service API reference doc](/apidocs/hs-crypto){: external} or the [{{site.data.keyword.uko_full_notm}} API reference doc](/apidocs/uko){: external}.
- To find out more about encrypting your data by using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [PKCS #11 API reference](/docs/hs-crypto?topic=hs-crypto-pkcs11-api-ref) and [GREP11 API reference doc](/docs/hs-crypto?topic=hs-crypto-grep11-api-ref).
