---

copyright:
  years: 2020, 2026
lastupdated: "2026-06-16"

keywords: shared responsibilities, shared responsibility model, disaster recovery, incident management, operation management

subcollection: hs-crypto
---


{{site.data.keyword.attribute-definition-list}}




# Understanding your responsibilities when using IBM Cloud Hyper Protect Crypto Services
{: #shared-responsibilities}

Learn about the management responsibilities and terms and conditions that you have when you use IBM Cloud&reg; Hyper Protect Crypto Services. For a high-level view of the service types in IBM Cloud and the breakdown of responsibilities between the customer and IBM for each type, see [Shared responsibilities for IBM Cloud offerings](/docs/overview?topic=overview-shared-responsibilities).
{: shortdesc}

Review the following sections for the specific responsibilities for you and for IBM when you use Hyper Protect Crypto Services. For the overall terms of use, see [IBM Cloud Terms and Notices](/docs/overview/terms-of-use).


## Incident and operations management
{: #incident-and-ops}

Incident and operations management includes tasks such as high availability, monitoring, and incident management. You and IBM share responsibilities for the set up and maintenance of your Hyper Protect Crypto Services service instance for your application workloads. You are responsible for incident and operations management of your application data.

| Task | IBM responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Monitoring | Provide integration with select third-party partnership technologies, such as IBM Cloud&reg; Activity Tracker. | Use the provided tools to [review instance logs and activities](/docs/hs-crypto?topic=hs-crypto-at-events). |
| Incidents | Provide notifications for planned maintenance, security bulletins, or unplanned outages.  | Set preferences to [receive emails about platform notifications](/docs/overview?topic=overview-ui#email-prefsl), and monitor the [IBM Cloud status page](https://{DomainName}/status?selected=announcement) for general announcements.|
|Firmware updates| Provide firmware updates for multiple crypto units in a sequential manner with no impact to running workloads. | Perform tasks as usual. |
|Connecting to third-party cloud | Provide error messages when access to the third-party keystores does not work. | Contact affected third-party cloud service provider to resolve access or connection issues. |
{: caption="Responsibilities for incident and operations" caption-side="bottom"}

## Change management
{: #change-management}

Change management includes tasks such as deployment, configuration, upgrades, patching, configuration changes, and deletion. You and IBM share responsibilities for keeping Hyper Protect Crypto Services service components at the latest version. You are responsible for change management of your application data.

| Task | IBM responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Applications| Provide major, minor, and patch version updates for Hyper Protect Crypto Services interfaces. | Use the [API](/apidocs/hs-crypto){: external}, [CLI](/docs/hs-crypto?topic=hs-crypto-hpcs-cli-plugin){: external}, or UI tools to perform updated functions. |
{: caption="Responsibilities for change management" caption-side="bottom"}


## Identity and access management
{: #iam-responsibilities}

Identity and access management includes tasks such as authentication, authorization, access control policies, and approving, granting, and revoking access. You and IBM share responsibilities for controlling access to your Hyper Protect Crypto Services instances and resources. You are responsible for identity and access management to your application data.

| Task | IBM responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| User management| IBM does not have access to your resources but provides you with the ability to restrict user access to resources.   | Depending on your needs, restrict access to resources and service functionality by using Cloud IAM access policies. For more information, see [Managing user access](/docs/hs-crypto?topic=hs-crypto-manage-access).|
| Service and key policies| IBM does not have access to your resources but provides you with the ability to set service and key policies.   | Manage your [service instance policies](/docs/hs-crypto?topic=hs-crypto-manage-dual-auth) and [key policies](/docs/hs-crypto?topic=hs-crypto-set-dual-auth-key-policy).|
|Connecting to third-party cloud | Provide error messages when access to the third-party keystores does not work. | Make sure the connection information and access credentials for the third-party cloud service provider are always up to date in your Hyper Protect Crypto Services instance. |
{: caption="Responsibilities for identity and access management" caption-side="bottom"}

## Security and regulation compliance
{: #security-compliance}

Security and regulation compliance includes tasks such as security controls implementation and compliance certification. IBM is responsible for the security and compliance of Hyper Protect Crypto Services. You are responsible for the security and compliance of your application data.

| Task | IBM responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Applications| Maintain controls that are commensurate to [various industry compliance standards](/docs/hs-crypto?topic=hs-crypto-security-and-compliance#compliance-ready).  | Set up and maintain security and regulation compliance for your apps and data. For example, you can enable extra security settings to meet your compliance needs by choosing how and when to [import](/docs/hs-crypto?topic=hs-crypto-importing-keys#plan-ahead), [wrap](/docs/hs-crypto?topic=hs-crypto-wrap-keys), [rotate](/docs/hs-crypto?topic=hs-crypto-importing-keys#plan-ahead), [rewrap](/docs/hs-crypto?topic=hs-crypto-rewrap-keys), and [delete](/docs/hs-crypto?topic=hs-crypto-delete-keys) keys. |
|Encryption| IBM is responsible for the encryption of keys. | Keep your root of trust, the master key parts, on either your workstation or smart cards. |
|Master key backups| IBM never touches your master key. | Backup your master key in a regular basis to your smart card or workstation. |
|Smart cards and smart card readers| IBM never touches your smart cards and smart card readers. | Store smart cards, the associated PINs, and the smart card readers in secure vaults to prevent unauthorized access. |
|Key part files| IBM never touches your key part files. | Secure key part files in the directory associated with CLOUDTKEFILES in an approved file storage vault and securely store the respective passwords. |
{: caption="Responsibilities for security and regulation compliance" caption-side="bottom"}

## Disaster recovery
{: #disaster-recovery}

Disaster recovery includes tasks such as providing dependencies on disaster recovery sites, provision disaster recovery environments, data and configuration backup, replicating data and configuration to the disaster recovery environment, and failover on disaster events. IBM is responsible for the recovery of Hyper Protect Crypto Services components in case of disaster. You are responsible for the recovery of the workloads that run Hyper Protect Crypto Services and your application data.

| Task | IBM responsibilities | Your responsibilities |
|----------|-----------------------|--------|
| Instance backups | Continuously perform in-region and cross-region backups of key resources and perform continuous testing of backups. |Back up your master key; validate the backups and restore data when needed. |
| Disaster recovery | When an in-region disaster occurs, automatically recover and restart service components. When a regional disaster that affects all available zones occurs, ensure that all data except the master key is replicated to another region. IBM will also make additional crypto units available in a different region and manage routing requests to the new crypto units. | When a regional disaster that affects all available zones occurs, load your master key to the new crypto units that IBM provisions in a different region for restoring data. You can also enable and initialize failover crypto units before a disaster occurs, which reduces the downtime.|
| Availability | Provide high availability capabilities, such as IBM-owned infrastructure in multizone regions, to meet local access and low latency requirements for each supported region. | Use the list of [available regions](/docs/hs-crypto?topic=hs-crypto-regions) to plan for and create new instances of the service. |
{: caption="Responsibilities for disaster recovery" caption-side="bottom"}
