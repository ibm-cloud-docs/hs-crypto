---

copyright:
  years: 2022
lastupdated: "2022-05-06"

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

# Why can't I continue performing actions by using the {{site.data.keyword.cloud_notm}} console?
{: #troubleshoot-ui-session-timeout}
{: troubleshoot}

When you access your {{site.data.keyword.hscrypto}} instance by using the {{site.data.keyword.cloud_notm}} console, you can't continue performing actions.
{: shortdesc}

You might receive an error message similar to one of the following messages:
{: tsSymptoms}

```
The service was not able to retrieve the keystores data.
```

```
The service was not able to retrieve the key data.
```

```
The service was not able to retrieve the encryption unit.
```

You have left the console open without performing any actions with it for an extended period of time, which causes your session timeout.
{: tsCauses}

Refresh the page to start a new session, then you can continue operations with the console.
{: tsResolve}
