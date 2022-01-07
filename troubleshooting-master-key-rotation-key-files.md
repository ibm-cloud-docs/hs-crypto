---

copyright:
  years: 2021, 2022
lastupdated: "2022-01-07"

keywords: failed master key rotation, failed to use key part files to rotate master keys, tke cryptounit-mk-rotate failure, troubleshoot master key rotation failure

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}

# Why can't I rotate master keys by using key part files?
{: #troubleshoot-master-key-rotation-key-part-files}
{: troubleshoot}
{: support}

When you run the `ibmcloud tke cryptounit-mk-rotate` command to rotate master keys by using key part files, you might be not able to complete the rotation.
{: shortdesc}

During master key rotation, the new master key registers are loaded with the new master key value to be used. The contents of key storage are reencrypted by using the current and new master key values. When the reencryption of key storage is complete, the new master key value is promoted to the current master key registers and the new master key registers are cleared.
{: tsSymptoms}

For detailed instructions on how to rotate the master key, see [Rotating master keys by using key parts](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-key-parts).

If an error occurs during master key rotation, the action you take to recover depends on how much of the process is completed. An incorrect recovery action can cause the master key value for key storage to be lost and contents of key storage to become unusable. You need to carefully check the command output before the error occurred to determine what recovery action to take.

Some errors are detected before the command starts to work with key storage or the master key registers. For example, if your authentication token is expired, an error is reported. To recover, you need to log in to the IBM Cloud. Similarly, if the initial conditions needed to run the command are not met, an error is reported. Correct the initial conditions and run the command again.

The following initial conditions can be reported as an error by the `ibmcloud tke cryptounit-mk-rotate` command:

* When you rotate your master key by using key part files, an invalid set of crypto units is selected.
* One or more crypto units are in imprint mode.
* Signature thresholds on the crypto units are not set the same.
* A common set of administrators is not selected and installed in all crypto units large enough to meet the signature threshold value.
* The current master key registers are not all in the `Valid` state with the same verification pattern.
*  When you rotate your master key by using key part files, the new master key registers are not all in the `Valid` state with the same verification pattern.

Operational workloads cannot be run until master key rotation is completed.

If an error occurs when you run the ibmcloud tke cryptounit-mk-rotate command to rotate master keys, check whether the error is an expired authentication token or failed pre-check. If it is not, check whether the following messages are displayed:
{: tsResolve}

```
KMS CRK rewrap successful, waiting on cryptounit-mk-setimm.
```
{: codeblock}

* If this message is not present, you can recover from the error by running the `ibmcloud tke cryptounit-mk-rotate` command again.

* If the message is present, the reencryption of key storage is complete. The only remaining step in the command is to promote the values in the new master key registers to the current master key registers.

    Run the `ibmcloud tke cryptounit-mks` command. If all the new master key registers are in the `Valid` state with the same verification pattern and all the current master key registers are in the `Valid` state with a different same verification pattern, run the `ibmcloud tke cryptounit-mk-setimm` command to finish the master key rotation.

    If for some crypto units the new master key value is moved to the current master key register, clear those crypto units by using the `ibmcloud tke cryptounit-rm` command. And then, run the `ibmcloud tke cryptounit-mk-setimm` command to finish the master key rotation.

    In both cases, it is safe to continue past the warning on the `ibmcloud tke cryptounit-mk-setimm` command. Key storage is prepared to accept the new master key value.
