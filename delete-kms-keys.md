---

copyright:
  years: 2022
lastupdated: "2022-01-11"

keywords: Unified Key Orchestrator, delete key, key management, kms key

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}


# Deleting internal KMS keys
{: #delete-kms-keys}

You can delete your internal KMS keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

## Deleting internal KMS keys through the UI
{: #delete-kms-keys-ui}

To delete an internal KMS key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. In the left navigation panel, go to **Vaults** &gt; **Managed keys** to view all the available keys.
3. If the key that you want to delete is in _active_ state, click the icon and choose **Deactivated** to deactivate the key first.
4. To destroy a _pre-active_ or _deactivated_ key, click the icon and choose **Destroyed.**
5. Click **Destroy key** to confirm.
6. To remove the key and its metadata, click the icon and choose **Remove from vault.**


## What's next
{: #delete-kms-keys-next}


  


