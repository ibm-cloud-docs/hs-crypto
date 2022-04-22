---

copyright:
  years: 2019, 2022
lastupdated: "2022-04-21"

keywords: smart card vulnerabilities, security policy, maintain workstation security, maintain smart card readers security

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:note: .note}
{:external: target="_blank" .external}
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Smart card security considerations
{: #define-smart-card-security-policy}

If you are [initializing {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance by using smart cards](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities), you need to define the security policy for the {{site.data.keyword.IBM_notm}} Management Utilities. Security officers need to document the security policy in a security plan and periodically review the corporate security policy and their current key management system.
{: shortdesc}



## Considerations for defining the Management Utilities security policy
{: #smart-card-security-plan}

The security plan might include these areas:

### General considerations
{: #smart-card-general-considerations}

Taking the following general questions into account when you define the security policy for using the Management Utilities:

* How many security officers does your organization have?
* How often is the master key changed?
* Who is authorized to enter master key parts?
* Do the key parts that you enter from the keyboard need to be masked?
* Who has access to the secure computer facility?
* What are the policies for working with service representatives?
* Will you be using smart card support?

### Workstation consideration
{: #smart-card-workstation-considerations}

Taking the following workstation-related questions into account when you define the security policy for using the Management Utilities:

* Who will use the TKE workstation?
* Where will your workstation be located?
* Is it only accessible to the security administrators or security officers?
* How many workstations will there be?


