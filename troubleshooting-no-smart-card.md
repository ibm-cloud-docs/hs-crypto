---

copyright:
  years: 2020, 2021
lastupdated: "2021-04-26"

keywords: troubleshoot, problems, known issues, can't delete service, no smart card readers found when you start application

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

# Why am I receiving a no smart card readers found error when using the Management Utilities?
{: #troubleshoot-no-smart-card}
{: troubleshoot}
{: support}

You get an error when you start the Smart Card Utility Program or the Trusted Key Entry application. The error can occur even when two Identiv SPR332 V2 smart card readers are attached to USB ports on your workstation.
{:shortdesc}

You might receive the following error message:
{: tsSymptoms}

![No smart card readers found when you start the application](/images/no_smart_card_readers.gif "Blocked PIN on EP11 smart card"){: caption="Figure 2. No smart card readers found when you start the application" caption-side="bottom"}

The Identiv SPR332 smart card readers are not attached to your workstation, or the device driver for the smart card reader is not correctly installed on your workstation.
{: tsCauses}

Attach two Identiv SPR332 smart card readers to the USB ports of your workstation. If you have attached two Identiv SPR332 smart card readers to your workstation and still get this error, [install the device driver](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver).
{: tsResolve}


