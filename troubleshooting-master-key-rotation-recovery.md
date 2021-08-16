---

copyright:
  years: 2021
lastupdated: "2021-08-16"

keywords: failed master key rotation, failed to use recovery crypto unit to rotate master keys, tke auto-mk-rotate failure, troubleshoot master key rotation failure

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

# Why can't I rotate master keys by using recovery crypto units?
{: #troubleshoot-master-key-rotation-recovery-crypto-units}
{: troubleshoot}
{: support}

When you run the `ibmcloud tke auto-mk-rotate` command to rotate master keys by using recovery crypto units, you might be not able to complete the rotation.
{: shortdesc}

During master key rotation, the new master key registers are loaded with the new master key value to be used. The contents of key storage are reencrypted by using the current and new master key values. When the reencryption of key storage is complete, the new master key value is promoted to the current master key registers and the new master key registers are cleared.
{: tsSymptoms}

For detailed instructions on how to rotate the master key, see [Rotating master keys by using recovery crypto units](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-recovery-crypto-unit).

If an error occurs during master key rotation, the action you take to recover depends on how much of the process has completed. An incorrect recovery action can cause the master key value for key storage to be lost and contents of key storage to become unusable. You need to carefully check the command output before the error occurred to determine what recovery action to take.

Some errors are detected before the command starts to work with key storage or the master key registers. For example, if your authentication token has expired, an error is reported. To recover, you need to log in to the IBM Cloud. Similarly, if the initial conditions needed to run the command are not met, an error is reported. Correct the initial conditions and run the command again.

The following initial conditions can be reported as an error by the `ibmcloud tke auto-mk-rotate` command:

* When you rotate your master key by using key part files, an invalid set of crypto units is selected.
* One or more crypto units are in imprint mode.
* Signature thresholds on the crypto units are not set the same.
* A common set of administrators is not selected and installed in all crypto units large enough to meet the signature threshold value.
* The current master key registers are not all in the `Valid` state with the same verification pattern.
*  When you rotate your master key using key part files, the new master key registers are not all in the `Valid` state with the same verification pattern.

Operational workloads cannot be run until master key rotation has completed.

If an error occurs when you run the `ibmcloud tke auto-mk-rotate` command to rotate master keys, check whether the error is an expired authentication token or failed pre-check. If it is not, check whether the following messages are displayed:
{: tsResolve}

- The following message indicates that all new master key registers have been set with a randomly generated new master key value:

    ```
    Delaying 30 seconds to allow server to discover new master key values
    ```
    {: codeblock}

- The following message indicates that the reencryption of key storage is completed:

    ```
    KMS CRK rewrap successful, waiting on cryptounit-mk-setimm
    ```
    {: codeblock}

Depending on the presence of the described messages, perform one of the following tasks:

* If neither message is present, you can recover from the error by running the `ibmcloud tke auto-mk-rotate` command again. Rerunning this command loads a new random master key value in the new master key registers and overwrites the previous value. This command then continues by reencrypting key storage. When the reencryption is done, the value in the new master key registers is moved to the current master key registers and the new master key registers are cleared.

* If the first message is present but the second message is not, reencryption of key storage has started. To recover, run the `ibmcloud tke cryptounit-mk-rotate` command. This command restarts the process with a request to reencrypt key storage and does not replace the master key value in the new master key registers.

    Do not rerun the `ibmcloud tke auto-mk-rotate` command. If you do, the contents of key storage becomes unusable.
    {: important}

* If both messages are present, the reencryption of key storage is complete. The only remaining step is to promote the values in the new master key registers to the current master key registers. Run the `ibmcloud tke cryptounit-mks` command.  If all the new master key registers are in the `Valid` state with the same verification pattern and all the current master key registers are in the `Valid` state with a different same verification pattern, run the `ibmcloud tke cryptounit-mk-setimm` command to finish the master key rotation.

    If for some crypto units the new master key value has already been moved to the current master key register, clear those crypto units by using the `ibmcloud tke cryptounit-rm` command. Then, run the `ibmcloud tke cryptounit-mk-setimm` command to finish the master key rotation.

    In both cases, it is safe to continue past the warning on the `ibmcloud tke cryptounit-mk-setimm` command. Key storage has been prepared to accept the new master key value.
