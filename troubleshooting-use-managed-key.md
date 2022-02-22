---

copyright:
  years: 2022
lastupdated: "2022-02-22"

keywords: troubleshoot, problems, known issues, can't encrypt data using managed keys

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

# Why can't I encrypt the resources using the managed key?
{: #troubleshoot-use-managed-key}
{: troubleshoot}

You are not able to associate the cloud resources with the managed key that you create for data encryption and decryption.
{: shortdesc}

You receive the following error message when you try to associate the cloud resources with your managed key:
{: tsSymptoms}

```
message placeholder
```

You can use a managed key only when it is installed in at least one keystore.
{: tsCauses}

To install a managed key, follow the steps in [Creating and installing managed keys](/docs/hs-crypto?topic=hs-crypto-create-managed-keys).
{: tsResolve}
