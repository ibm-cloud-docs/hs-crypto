---

copyright:
  years: 2022, 2023
lastupdated: "2023-07-14"

keywords: master key, restore master key, master key backup, recovery crypto unit, master key recover

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Recovering a master key from a recovery crypto unit
{: #uko-recover-master-key-recovery-crypto-unit}

If your service instance includes [recovery crypto units](/docs/hs-crypto?topic=hs-crypto-uko-initialize-instance-mode#uko-understand-recovery-crypto-unit), the current master key value in a recovery crypto unit can be used as a backup value for your operational crypto units. If you initialize service instances by using recovery crypto units (with the `ibmcloud tke auto-init` command) or rotate master keys using recovery crypto units (with the `ibmcloud tke auto-mk-rotate` command), this is the only backup value of the master key that exists for your service instance.
{: shortdesc}

The value in the current master key register of a recovery crypto unit can be securely transferred to other current master key registers in service instances that are assigned to the current resource group by using the `ibmcloud tke auto-mk-recover` command.

You might need to use the command to recover the master key value in the following situations:

* You inadvertently zeroize a crypto unit and need to reinitialize it.
* You inadvertently clear the current master key register in a crypto unit.
* Your hardware fails and a crypto unit needs to be replaced.
* You need different service instances in the same resource group to use the same master key value.

Currently only the `us-south` and `us-east` regions support recovery crypto units. Only service instances in these regions can use this command. For more information about supported regions, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions).
{: note}

## Before you begin
{: #uko-recover-master-key-prerequisites}

To use the command, you need to make sure that the recovery crypto unit and all target crypto units meet the following requirements:

* They are not in imprint mode.
* They have the same signature threshold value.
* A common set of administrators is added to the recovery crypto unit and all target crypto units, which can meet the signature threshold value.

To check that initial conditions are met, select the source and target crypto units by using the `ibmcloud tke cryptounit-add` command, and then run the `ibmcloud tke cryptounit-compare` command.

## Recovering master keys
{: #uko-recover-master-key-step}

Run the following command to recover a master key value from a recovery crypto unit:

```
ibmcloud tke auto-mk-recover
```
{: pre}

With this command, you can transfer the value in the current master key register of a recovery crypto unit to the current master key registers of any other crypto units in the same resource group. These can be operational crypto units or other recovery crypto units. With this command, you can use the same master key value in multiple service instances if they are in the same resource group.

To learn more about resource groups, see [Managing resource groups](/docs/account?topic=account-rgs).

## What's next
{: #uko-recover-master-key-next}

For a complete TKE CLI plug-in command reference, see [{{site.data.keyword.cloud_notm}} TKE CLI](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin#tke-cli-plugin){: external}.

