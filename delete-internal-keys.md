---

copyright:
  years: 2022
lastupdated: "2022-01-19"

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


# Deleting internal keys
{: #delete-internal-keys}

You can delete your internal KMS keys in {{site.data.keyword.uko_full_notm}} through the user interface (UI), or programmatically with the {{site.data.keyword.hscrypto}} key management API.
{: shortdesc}

If you enable [dual authorization](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) settings for your {{site.data.keyword.hscrypto}} instance, keep in mind that any keys that you add to the service require an authorization from two users to delete keys.
{: note}


## Deleting internal keys through the UI
{: #delete-internal-keys-ui}

You can only remove _Destroyed_ keys from vaults. To delete an internal KMS key through the UI, complete the following steps:

1. [Log in to the {{site.data.keyword.hscrypto}} instance](https://cloud.ibm.com/login){: external}.
2. Click **Managed keys** from the navigation to view all the available keys.
3. If the key that you want to delete is in _active_ state, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Deactivated** to deactivate the key first.
4. To destroy a _pre-active_ or _deactivated_ key, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Destroyed**.
5. Click **Destroy key** to confirm.
6. To remove the key and the metadata from the vault, click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Remove from vault**.

The key has been deleted and uninstalled from all target keystores. All key materials have been destroyed. 


## Deleting internal keys with the API
{: #delete-internal-keys-api}




## What's next
{: #delete-internal-keys-next}


  


