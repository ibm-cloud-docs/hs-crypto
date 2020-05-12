---

copyright:
  years: 2020
lastupdated: "2020-05-12"

keywords: shared responsibilities, disaster recovery, incident management

subcollection: hs-crypto
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Understanding your responsibilities when using {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #shared-responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}. For a high-level view of the service types in {{site.data.keyword.cloud_notm}} and the breakdown of responsibilities between the customer and {{site.data.keyword.IBM_notm}} for each type, see [Shared responsibilities for {{site.data.keyword.cloud_notm}} offerings](/docs/overview?topic=overview-shared-responsibilities).
{:shortdesc}

Review the following sections for the specific responsibilities for you and for {{site.data.keyword.IBM_notm}} when you use {{site.data.keyword.hscrypto}}. For the overall terms of use, see [{{site.data.keyword.cloud_notm}} Terms and Notices](/docs/overview/terms-of-use?topic=overview-terms).


## Incident and operations management
{: #incident-and-ops}

You and IBM share responsibilities for the set up and maintenance of your {{site.data.keyword.hscrypto}} service instance for your application workloads. You are responsible for incident and operations management of your application data.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Availability | Provide high availability capabilities, such as IBM-owned infrastructure in multizone regions, to meet local access and low latency requirements for each supported region. | Use the list of [available regions](/docs/hs-crypto?topic=hs-crypto-regions) to plan for and create new instances of the service. |
| Monitoring | Provide integration with select third-party partnership technologies, such as {{site.data.keyword.at_full}}. | Use the provided tools to [review instance logs and activities](/docs/hs-crypto?topic=hs-crypto-at-events). |
| Incidents | Provide notifications for planned maintenance, security bulletins, or unplanned outages.  | Set preferences to [receive emails about platform notifications](/docs/overview?topic=overview-ui#email-prefsl), and monitor the [IBM Cloud status page](https://{DomainName}/status?selected=announcement) for general announcements.
{: caption="Table 1. Responsibilites for incident and operations" caption-side="top"}


## Change management
{: #change-management}

You and IBM share responsibilities for keeping {{site.data.keyword.hscrypto}} service components at the latest version. You are responsible for change management of your application data.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Applications| Provide major, minor, and patch version updates for {{site.data.keyword.hscrypto}} interfaces. | Use the [API](https://{DomainName}/apidocs/hs-crypto){: external}, [CLI](https://{DomainName}/docs/key-protect?topic=key-protect-cli-reference)
/hs-crypto-cli-plugin/hs-crypto-cli-plugin-tke_cli_plugin){: external}, or console tools to apply the provided updates, including version updates, new features, and security patches. |
{: caption="Table 2. Responsibilites for change management" caption-side="top"}


## Identity and access management
{: #iam-responsibilities}

You and IBM share responsibilities for controlling access to your {{site.data.keyword.hscrypto}} instances and resources. You are responsible for identity and access management to your application data.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Applications| IBM does not have access to your resources but provides you with the ability to restrict user access to resources.   | Depending on your needs, restrict access to resources and service functionality by using Cloud IAM access policies. For more information, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).
{: caption="Table 3. Responsibilites for identity and access management" caption-side="top"}

## Security and regulation compliance
{: #security-compliance}

IBM is responsible for the security and compliance of {{site.data.keyword.hscrypto}}. You are responsible for the security and compliance of your application data.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Applications| Maintain controls that are commensurate to [various industry compliance standards](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#compliance-ready).  | Set up and maintain security and regulation compliance for your apps and data. For example, you can enable extra security settings to meet your compliance needs by choosing how and when to [import](/docs/hs-crypto?topic=hs-crypto-importing-keys#plan-ahead), [wrap](/docs/hs-crypto?topic=hs-crypto-wrap-keys), [rotate](/docs/hs-crypto?topic=hs-crypto-importing-keys#plan-ahead), [rewrap](/docs/hs-crypto?topic=hs-crypto-rewrap-keys), and [delete](/docs/hs-crypto?topic=hs-crypto-delete-keys) keys. |
|Encryption| IBM is responsible for the encryption of data and keys. | Keep your root of trust, the master key parts, on either your workstation or smart cards. |
{: caption="Table 4. Responsibilites for security and regulation compliance" caption-side="top"}

## Disaster recovery
{: #disaster-recovery}

IBM is responsible for the recovery of {{site.data.keyword.hscrypto}} components in case of disaster. You are responsible for the recovery of the workloads that run {{site.data.keyword.hscrypto}} and your application data.

| Task | {{site.data.keyword.IBM_notm}} responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Applications | Continuously perform in-region and cross-region backups of key resources, automatically recover and restart service components after any in-region disaster event, and restore your data in another supported region based on opened customer tickets.| If a regional disaster that affects all available zones occurs, open a support ticket for IBM to [restore your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data), and manually load your master key to the new service instance. |
{: caption="Table 5. Responsibilites for disaster recovery" caption-side="top"}
