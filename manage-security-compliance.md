---

copyright:
  years: 2020
lastupdated: "2020-10-28"

keywords: security for Hyper Protect Crypto Services, compliance for Hyper Protect Crypto Services, security and compliance for Hyper Protect Crypto Services, rules for Hyper Protect Crypto Services,

subcollection: hs-crypto

---

{:codeblock: .codeblock}
{:screen: .screen}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:tip: .tip}
{:preview: .preview}
{:deprecated: .deprecated}
{:beta: .beta}
{:term: .term}
{:shortdesc: .shortdesc}
{:script: data-hd-video='script'}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:help: data-hd-content-type='help'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:java: .ph data-hd-programlang='java'}
{:javascript: .ph data-hd-programlang='javascript'}
{:swift: .ph data-hd-programlang='swift'}
{:curl: .ph data-hd-programlang='curl'}
{:video: .video}
{:step: data-tutorial-type='step'}
{:tutorial: data-hd-content-type='tutorial'}



# Managing security and compliance with {{site.data.keyword.hscrypto}}
{: #manage-security-compliance}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is integrated with the {{site.data.keyword.compliance_short}} to help you manage security and compliance for your organization.
{: shortdesc}

With the {{site.data.keyword.compliance_short}}, you can:

* Monitor for controls and goals that pertain to {{site.data.keyword.hscrypto}}
* Define rules for {{site.data.keyword.hscrypto}} that can help to standardize resource configuration

## Monitoring security and compliance posture with {{site.data.keyword.hscrypto}}
{: #monitor-certificate-manager}

As a security or compliance focal, you need to ensure that your organization is adhering to the external and internal standards for your industry. By scanning the configurations in your accounts against a profile, the {{site.data.keyword.compliance_short}} can help you to identify potential issues as they arise.

All of the goals for {{site.data.keyword.hscrypto}} are added to the {{site.data.keyword.cloud_notm}} Best Practices Controls 1.0 profile but can also be mapped to other profiles.
{: note}

To start monitoring your resources, check out [Getting started with {{site.data.keyword.compliance_short}}](/docs/security-compliance?topic=security-compliance-getting-started).

**Available goals for {{site.data.keyword.hscrypto}}**

* Ensure the {{site.data.keyword.hscrypto}} instances are accessible only using private end points.
* Ensure that the rotation policy for the root keys of the {{site.data.keyword.hscrypto}} instances is set.
* Ensure that the dual authorization deletion policy is enabled on the {{site.data.keyword.hscrypto}} instances.
* Ensure that the number of crypto units in the {{site.data.keyword.hscrypto}} instances is 2 or 3.
