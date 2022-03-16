---

copyright:
  years: 2022
lastupdated: "2022-03-16"

keywords: troubleshoot, problems, known issues, can't create standard keys

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

# Why can't I create a standard key after I load another master key?
{: #troubleshoot-unable-to-create-standard-keys}
{: troubleshoot}
{: support}

You are not able to create a standard key through either the {{site.data.keyword.hscrypto}} user interface or the API after you load another master key to the service instance.
{: shortdesc}

You see the following error message when you try to create a standard key:
{: tsSymptoms}

```
The service was not able to add key "<key_ID>". The HTTP status is 500.
```

You load another master key to your service instance after you create the root key. Because of this, the root key fails to wrap the standard key. 
{: tsCauses}

[Rotate the master key](/docs/hs-crypto?topic=hs-crypto-uko-rotate-master-key-cli-key-part) instead of loading another master key if you want to change the master key in a regular basis for security requirements.
{: tip}

Load the old master key that is used to wrap the root key to the service instance again by following [the instructions](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#load-master-keys).
{: tsResolve}
