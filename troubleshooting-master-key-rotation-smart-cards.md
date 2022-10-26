---

copyright:
  years: 2021, 2022
lastupdated: "2022-10-26"

keywords: failed master key rotation, failed to use smart cards to rotate master keys, failed to use the Management Utilities to rotate master keys, master key rotation failure, troubleshoot master key rotation failure

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Why can't I rotate master keys by using smart cards?
{: #troubleshoot-master-key-rotation-key-smart-cards}
{: troubleshoot}
{: support}

When you run smart cards and the Management Utilities to rotate master keys, you might be not able to complete the rotation.
{: shortdesc}

During master key rotation, the new master key registers are loaded with the new master key value to be used. The contents of key storage are reencrypted by using the current and new master key values. When the reencryption of key storage is complete, the new master key value is promoted to the current master key registers and the new master key registers are cleared.
{: tsSymptoms}

For detailed instructions on how to rotate the master key, see [Rotating master keys by using workstation files](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part).

If an error occurs during master key rotation, the action you take to recover depends on how much of the process is completed. An incorrect recovery action can cause the master key value for key storage to be lost and contents of key storage to become unusable. You need to carefully check the command output before the error occurred to determine what recovery action to take.

Some errors are detected before the command starts to work with key storage or the master key registers. For example, if your authentication token is expired, an error is reported. To recover, you need to log in to the IBM Cloud. Similarly, if the initial conditions needed to run the command are not met, an error is reported. Correct the initial conditions and run the command again.

The following initial conditions can be reported as an error when you click the **Rotate** button on the **Master keys** tab of the Trusted Key Entry application:

* Not all crypto units in a single service instance are selected. Or, crypto units in more than one service instance are selected.
* One or more crypto units are in imprint mode.
* Signature thresholds on the crypto units are not set the same.
* A common set of administrators is not selected and installed in all crypto units large enough to meet the signature threshold value.
* The current master key registers are not all in the `Valid` state with the same verification pattern.
* When you rotate your master key by using workstation files, the new master key registers are not all in the `Valid` state with the same verification pattern.

Operational workloads cannot be run until master key rotation has completed.

If an error occurs when you rotate master keys, check whether the error is an expired authentication token or failed pre-check. If it is not, check whether the following messages are displayed:
{: tsResolve}

```
KMS CRK rewrap successful, waiting on cryptounit-mk-setimm.
```
{: screen}

* If this message is not present, you can recover from the error by clicking the **Rotate** button again.

* If the message is present, the reencryption of key storage is complete. The only remaining step in the command is to promote the values in the new master key registers to the current master key registers.

    Check the state of the new and current master key registers. If all the new master key registers are in the `Full Committed` state with the same verification pattern and all the current master key registers are in the `Valid` state with a different same verification pattern, click the **Set immediate** button to finish the master key rotation.

    If for some crypto units the new master key value is moved to the current master key register, clear those crypto units by clicking the **Remove crypto units** button on the Crypto units tab. Then, click the **Set immediate** button on the **Master keys** tab to finish the master key rotation.

    In both cases, it is safe to continue past the warning when you click the **Set immediate** button. Key storage is prepared to accept the new master key value.
