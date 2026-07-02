---

copyright:
  years: 2020, 2026
lastupdated: "2026-07-01"

keywords: troubleshoot, problems, known issues, failed to activate the new master key during the master key rotation process

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why do I fail to load the new master key during the master key rotation process?
{: #troubleshoot-master-key-rotation}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is deprecated. As of 28 March 2026, you can't create new instances, and access to free instances will be removed. Existing premium plan instances are supported until 28 March 2027. Any instances that still exist on that date will be deleted.
{: deprecated}
{: troubleshoot}
{: support}

After you run the `cryptounit-mk-rotate` command in the TKE CLI, you fail to load the new master key to the Current Master Key Register.
{: shortdesc}

The new master key is not in `Valid` state in the current master key register after you run the `cryptounit-mk-rotate` command.
{: tsSymptoms}

You accidentally exit the TKE CLI window when the root keys are being rewrapped by the new master key after you run the `cryptounit-mk-rotate` command.
{: tsCauses}

Run the `cryptounit-mk-rotate` command again to resume the root key rewrap operations. When prompted, enter the password for the current signature key file to activate the new master key.
{: tsResolve}
