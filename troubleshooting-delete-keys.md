---

copyright:
  years: 2020
lastupdated: "2020-07-17"

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

For your protection, {{site.data.keyword.hscrypto}} prevents the deletion of a key that's actively encrypting data in the cloud.
{: tsResolve}

To delete the key, first delete the resources that are associated with the key, and then delete the key.
