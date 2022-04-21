---

copyright:
  years: 2022
lastupdated: "2022-04-21"

keywords: troubleshoot, problems, known issues, can't destroy managed keys

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
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Why can't I destroy managed keys?
{: #troubleshoot-destroy-managed-keys}
{: troubleshoot}

You deactivate a managed key first. However, when you try to change the key state to _Destroyed_, an error occurs.
{: shortdesc}

You receive the following error message when you click the Actions icon ![Actions icon](../icons/action-menu-icon.svg "Actions") and choose **Destroyed** from the UI:
{: tsSymptoms}

```
The service was not able to destroy key `<key_ID>`. The requested key has been deactivated within the last 4 hours.
```
{: screen}

The managed key was deactivated less than 4 hours ago. A managed key can be destroyed only after it is deactivated for more than 4 hours.
{: tsCauses}

Wait until it reaches 4 hours, and then try destroying the managed key again by following the same procedure.
{: tsResolve}

