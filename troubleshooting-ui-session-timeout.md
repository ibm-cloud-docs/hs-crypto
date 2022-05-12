---

copyright:
  years: 2022
lastupdated: "2022-05-12"

keywords: troubleshoot, problems, known issues, timeout, intermittent issue, session timeout

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

# Why can't I perform any actions by using the {{site.data.keyword.cloud_notm}} console?
{: #troubleshoot-ui-session-timeout}
{: troubleshoot}

When you access your {{site.data.keyword.hscrypto}} instance by using the {{site.data.keyword.cloud_notm}} console, you can't perform any actions.
{: shortdesc}

You might receive an error message similar to one of the following messages:
{: tsSymptoms}

```
The service was not able to retrieve the keystores data.
```
{: screen}

```
The service was not able to retrieve the key data.
```
{: screen}

```
The service was not able to retrieve the encryption unit.
```
{: screen}

You have left the console open without performing any actions with it for an extended period of time (for example, 60 minutes), which causes your session timeout.
{: tsCauses}

Refresh the page to start a new session, and then you can continue operations with the console.
{: tsResolve}
