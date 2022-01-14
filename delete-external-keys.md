---

copyright:
  years: 2022
lastupdated: "2022-01-14"

keywords: Unified Key Orchestrator, delete key, key management, external key

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


# Deleting external keys
{: #delete-external-keys}

You can delete external keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

## Deleting external keys through the UI
{: #delete-external-keys-ui}

To delete an external key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Go to **Managed keys** to view all the available keys.
3. If the key that you want to delete is in _active_ state, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Deactivated** to deactivate the key first.
4. To destroy a _pre-active_ or _deactivated_ key, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Destroyed.**
5. Click **Destroy key** to confirm.
6. To remove the key and its metadata, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Remove from vault.**


## What's next
{: #delete-external-keys-next}


  


