---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: troubleshoot, problems, known issues, failed to activate the new master key during the master key rotation process

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:external: target="_blank" .external}
{:support: data-reuse='support'}
{:term: .term}

# Why can't I activate the new master key during the master key rotation process?
{: #troubleshoot-master-key-rotation}
{: troubleshoot}
{: support}

After you run the `cryptounit-mk-rotate` command in the TKE CLI, you might not be able to activate the new master key. 
{:shortdesc}

You are not able to activate the new master key after you run the `cryptounit-mk-rotate` command.
{: tsSymptoms}

You accidentally exit the TKE CLI window when the root keys are being rewrapped by the new master key after you run the `cryptounit-mk-rotate` command.
{: tsCauses}

Run the `cryptounit-mk-rotate` command again to resume the root key rewrap operations. When prompted, enter the password for the current signature key file to activate the new master key.
{: tsResolve}
