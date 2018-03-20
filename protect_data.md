---

copyright:
  years: 2018
lastupdated: "2018-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protecting your data

> _**Disclaimer: {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is still in experimental phase and it might change at anytime. At the current stage, {{site.data.keyword.hscrypto}} provides only self-signed certificates.**_

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} protects your data at rest, in use, and in flight.
{:shortdesc}



## Data at rest and in use

No matter you store your data in your own data center or in {{site.data.keyword.cloud_notm}} storage, you can use {{site.data.keyword.hscrypto}} to encrypt your data at the highest security level. {{site.data.keyword.hscrypto}} binds the [{{site.data.keyword.keymanagementservicefull_notm}} ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/keymgmt/keyprotect_about.html){:new_window} service, which can generate and manage your keys. {{site.data.keyword.hscrypto}} protects these keys and stores them in a highly protected and isolated environment on IBM Z, which protects your data with technology that is certified at industry's highest security level.

If you store your data in cloud consuming Database-as-a-Service (DBaaS), your data is protected even when it's in use. [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://console.bluemix.net/docs/services/keymgmt/keyprotect_about.html){:new_window} leverages zHSM and the SSC technology on IBM Z to provide high security and data protection. Data is protected in an isolated LPAR with no external access including privileged users.

![data at rest](image/data_at_rest.png "Data at rest and in use")
*Figure 1. Protecting data at rest and in use*


## Data in transit

{{site.data.keyword.hscrypto}} protects sensitive transactions to ensure security of data while in transit. Customers can terminate TLS connections for their applications at the front door. {{site.data.keyword.hscrypto}} also protects all communications between micro services inside a container cluster. You can enable this function through policies.

{{site.data.keyword.hscrypto}} offloads SSL/TLS keys to a Hardware Security Module (HSM) in cloud and protects those sensitive keys. {{site.data.keyword.hscrypto}} manages certificate lifecycle from start to end and ensures the visibility to certificate expiration.

![data in transit](image/data_in_flight.png "Data in transit")
*Figure 2. Protecting data in transit*
