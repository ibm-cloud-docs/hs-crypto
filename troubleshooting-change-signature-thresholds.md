---

copyright:
  years: 2020, 2022
lastupdated: "2022-11-21"

keywords: troubleshoot, problems, known issues, unable to change signature thresholds

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

# Why can't I change signature thresholds?
{: #troubleshoot-unable-to-change-signature-thresholds}
{: troubleshoot}

You get an error when you try to change the signature threshold or revocation signature threshold. The error can be reported by either the TKE plug-in or the Trusted Key Entry application.
{: shortdesc}

You receive an error message similar to the following one:
{: tsSymptoms}

> FAILED
> Error reported by EP11 crypto module.
> Return code: 209
> Reason code: 71
> Error message: Change not allowed.  You are not allowed to change a threshold value if the corresponding attribute control bit is reset.


The TKE plug-in through version 0.0.11 restricts the ability to set the signature threshold and revocation signature threshold to a value other than one. The restriction can be removed by zeroizing the crypto unit.
{: tsCauses}

To set the signature threshold or revocation signature threshold to a value greater than one, [zeroize the crypto unit](/docs/hs-crypto?topic=hs-crypto-delete-instance#zeroize-crypto-unit-step). This removes the restriction. Then reinstall the administrators that you want to use and set the threshold values by using either the latest version of the TKE plug-in or the Trusted Key Entry application.
{: tsResolve}

Zeroizing a crypto unit clears the master key registers. To fully recover the state of a crypto unit after zeroizing it, you need to reload the master key registers and the administrators. Depending on your loading method, see [Loading master keys with the TKE CLI plug-in](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#load-master-keys) or [Initializing service instances using smart cards and the Management Utilities](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities#load-master-key-management-utilities) for instructions.
