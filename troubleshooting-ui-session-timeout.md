---

copyright:
  years: 2022, 2024
lastupdated: "2024-02-27"

keywords: troubleshoot, problems, known issues, timeout, intermittent issue, session timeout

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}



# Why can't I perform any actions by using the UI?
{: #troubleshoot-ui-session-timeout}
{: troubleshoot}

When you access your {{site.data.keyword.hscrypto}} instance by using the UI, you can't perform any actions.
{: shortdesc}

You might receive an error message similar to one of the following messages:
{: tsSymptoms}

> The service was not able to retrieve the keystores data.
> The service was not able to retrieve the key data.
> The service was not able to retrieve the encryption unit.

You have left the UI open without performing any actions with it for an extended period (for example, 60 minutes), which causes your session timeout.
{: tsCauses}

Refresh the page to start a new session, and then you can continue operations with the UI.
{: tsResolve}
