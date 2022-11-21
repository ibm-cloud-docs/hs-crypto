---

copyright:
  years: 2022
lastupdated: "2022-11-21"

keywords: troubleshoot, problems, known issues, can't rotate master key 

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

# Why can't I rotate the master key when using the {{site.data.keyword.uko_full_notm}} Plan?
{: #troubleshoot-master-key-rotation-uko}
{: troubleshoot}

You are not able to rotate the master key successfully by using the TKE CLI commands.
{: shortdesc}

When you are using a {{site.data.keyword.uko_full_notm}} service plan, master key rotation using the TKE CLI commands fails with the following messages: 
{: tsSymptoms}

> FAILED
> Error sending start key rotate request to target service instance.
> Status code: 400
> Message: Bad Request

Master key rotation is not currently supported by the {{site.data.keyword.uko_full_notm}} Plan.
{: tsCauses}

