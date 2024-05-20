---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-20"

keywords: troubleshoot, problems, known issues, can't delete service, no smart card readers found when you start application

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why am I receiving a no smart card readers found error when I use the Management Utilities?
{: #troubleshoot-no-smart-card}
{: troubleshoot}
{: support}

You get an error when you start the Smart Card Utility Program or the Trusted Key Entry application. The error can occur even when two Identiv SPR332 V2 smart card readers are attached to USB ports on your workstation.
{: shortdesc}

You might receive the following error message:
{: tsSymptoms}

![No smart card readers found when you start the application](/images/no-smart-card-readers.gif "Blocked PIN on EP11 smart card"){: caption="Figure 2. No smart card readers found when you start the application." caption-side="bottom"}

The Identiv SPR332 smart card readers are not attached to your workstation, or the device driver for the smart card reader is not correctly installed on your workstation.
{: tsCauses}

Attach two Identiv SPR332 smart card readers to the USB ports of your workstation. If you attach two Identiv SPR332 smart card readers to your workstation and still get this error, [install the device driver](/docs/hs-crypto?topic=hs-crypto-prepare-management-utilities#install-smart-card-reader-driver).
{: tsResolve}


