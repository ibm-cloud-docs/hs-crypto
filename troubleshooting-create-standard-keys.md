---

copyright:
  years: 2022, 2026
lastupdated: "2026-07-01"

keywords: troubleshoot, problems, known issues, can't create standard keys

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why can't I create a standard key after I load another master key?
{: #troubleshoot-unable-to-create-standard-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is deprecated. As of 28 March 2026, you can't create new instances, and access to free instances will be removed. Existing premium plan instances are supported until 28 March 2027. Any instances that still exist on that date will be deleted.
{: deprecated}
{: troubleshoot}
{: support}

You are not able to create a standard key through either the UI or the API after you load another master key to the service instance.
{: shortdesc}

You see the following error message when you try to create a standard key:
{: tsSymptoms}

> The service was not able to add key "<key_ID>". The HTTP status is 500.

You load another master key to your service instance after you create the root key. Because of this, the root key fails to wrap the standard key, and the standard key creation fails. 
{: tsCauses}

If you want to change the master key in a regular basis for security reasons, rotate the master key by following [the instructions](/docs/hs-crypto?topic=hs-crypto-rotate-master-key-cli-key-part).
{: tip}

Load the original master key that is used to wrap the root key to the service instance again by following [the instructions](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#load-master-keys).
{: tsResolve}
