---

copyright:
  years: 2020
lastupdated: "2020-07-17"

keywords: troubleshoot, problems, known issues, unauthorized when starting the Trusted Key Entry application

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

# Why am I not authorized when starting the Trusted Key Entry application?
{: #troubleshoot-unauthorized-token-tke-application}
{: troubleshoot}
{: support}

You receive an error message when you start the Trusted Key Entry application.
{:shortdesc}

You might receive the following error message:
{: tsSymptoms}

![Unauthorized when you run TKE CLI plug-in commands](/image/tke_401.gif "Unauthorized when you run TKE CLI plug-in commands"){: caption="Figure 3. Unauthorized when you start the Trusted Key Entry application" caption-side="bottom"}

A valid authentication token is needed for the TKE application to send requests to {{site.data.keyword.cloud_notm}}. You must log in to {{site.data.keyword.cloud_notm}} with the {{site.data.keyword.cloud_notm}} CLI to create a valid authentication token before you can run the TKE application. These might be the causes of this error:
{: tsCauses}

- You've not logged in to {{site.data.keyword.cloud_notm}} to create an authentication token.
- Your authentication token has expired after 1 hour.

From the command line, log in to the {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command. Click **Refresh Panel** on the **Crypto units** tab to retry the query of your service instance.
{: tsResolve}
