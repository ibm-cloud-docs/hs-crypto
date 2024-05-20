---

copyright:
  years: 2020, 2024
lastupdated: "2024-05-20"

keywords: troubleshoot, problems, known issues, unauthorized when starting the Trusted Key Entry application

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}




# Why am I not authorized when I start the Trusted Key Entry application?
{: #troubleshoot-unauthorized-token-tke-application}
{: troubleshoot}
{: support}

You receive an error message when you start the Trusted Key Entry application.
{: shortdesc}

You might receive the following error message:
{: tsSymptoms}

![Unauthorized when you run TKE CLI plug-in commands](/images/tke_401.gif "Unauthorized when you run TKE CLI plug-in commands."){: caption="Figure 3. Unauthorized when you start the Trusted Key Entry application." caption-side="bottom"}

A valid authentication token is needed for the TKE application to send requests to {{site.data.keyword.cloud_notm}}. You must log in to {{site.data.keyword.cloud_notm}} with the {{site.data.keyword.cloud_notm}} CLI to create a valid authentication token before you can run the TKE application, which might be the causes of this error:
{: tsCauses}

- You do not log in to {{site.data.keyword.cloud_notm}} to create an authentication token.
- Your authentication token is expired.

From the command line, log in to the {{site.data.keyword.cloud_notm}} with the `ibmcloud login` command. Click **Refresh Panel** on the **Crypto units** tab to retry the query of your service instance.
{: tsResolve}
