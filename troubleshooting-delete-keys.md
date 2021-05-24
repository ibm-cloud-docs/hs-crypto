---

copyright:
  years: 2020, 2021
lastupdated: "2021-05-24"

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

You're assigned a _Manager_ access policy for the service instance. You try to delete a key, but the action fails with either of the following 2 error messages.

- Error message 1:

  ```
  Conflict: Key could not be deleted. Status: 409, Correlation ID: 160cc463-71d1-4b30-a5f2-d3f7e9f2b75e
  ```
  {: screen}

- Error message 2:

  ```
  The service was not able to delete key "<key_name>". Because the key is enabled with the dual authorization policy and you set the key for deletion, a second approver needs to continue with the key deletion operation.
  ```
  {: screen}

The following reasons cause the errors:
{: tsCauses}

- Error message 1:

  This key is actively protecting one or more cloud resources, such as a Cloud Object Storage bucket.

- Error message 2:

  This key is enabled with the dual authorization policy that requires a deletion authorization from two users. You set the key for deletion and you need to contact the second approver to complete the deletion.

See the following instructions to solve the problems:
{: tsResolve}

- Error message 1:

  {{site.data.keyword.hscrypto}} blocks the deletion of any key that's actively protecting a cloud resource. Before you delete a key, [review the resources](/docs/hs-crypto?topic=hs-crypto-view-protected-resources) that are associated with the key.

  You can [force deletion on a key](/docs/hs-crypto?topic=hs-crypto-delete-keys#delete-key-force) that's protecting a cloud resource. However, the action won't succeed if the key's associated resource is non-erasable due to a retention policy. You can verify whether a key is associated with a non-erasable resource by [checking the registration details](/docs/hs-crypto?topic=hs-crypto-view-protected-resources#view-protected-resources-api) for the key. Then, you must contact an account owner to remove the retention policy on each resource that is associated with the key before you can delete the key.

  If you don't need the resources that are associated with the key any more, you can also first delete the associated resources and then delete the key.

- Error message 2:

  If you enable the dual authorization policy [for your instance](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) or [for a key](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy), you need to assign two approvers to delete a key. The first approver must have a _Writer_ or _Manager_ role to first schedule the key deletion and the second approver must have a _Manager_ role to complete the deletion within 7 days. For more information, see [Deleting keys by using dual authorization](/docs/hs-crypto?topic=hs-crypto-delete-dual-auth-keys).
