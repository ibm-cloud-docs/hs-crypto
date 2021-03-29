---

copyright:
  years: 2020, 2021
lastupdated: "2021-02-01"

keywords: troubleshoot, problems, known issues, can't delete keys

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

# Why can't I delete keys?
{: #troubleshoot-unable-to-delete-keys}
{: troubleshoot}

When you use the {{site.data.keyword.hscrypto}} user interface or REST API, you're unable to delete a key.
{:shortdesc}

From the {{site.data.keyword.cloud_notm}} dashboard, you select your instance of the {{site.data.keyword.hscrypto}} service.
{: tsSymptoms}

You're assigned a _Manager_ access policy for the service instance. You try to delete a key, but the action fails with the following error message.

```
Conflict: Key could not be deleted. Status: 409, Correlation ID: 160cc463-71d1-4b30-a5f2-d3f7e9f2b75e
```
{: screen}

This key is actively protecting one or more cloud resources, such as a Cloud Object Storage bucket.
{: tsCauses}

{{site.data.keyword.hscrypto}} blocks the deletion of any key that's actively protecting a cloud resource. Before you delete a key, [review the resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources) that are associated with the key.
{: tsResolve}

You can [force deletion on a key](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-key-force) that's protecting a cloud resource. However, the action won't succeed if the key's associated resource is non-erasable due to a retention policy. You can verify whether a key is associated with a non-erasable resource by [checking the registration details](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources-api) for the key. Then, you must contact an account owner to remove the retention policy on each resource that is associated with the key before you can delete the key.

If you don't need the resources that are associated with the key any more, you can also first delete the associated resources and then delete the key.
