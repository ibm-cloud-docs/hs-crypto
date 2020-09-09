---

copyright:
  years: 2019
lastupdated: "2020-09-09"

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

# Smart card security considerations
{: #define-smart-card-security-policy}

If you are [initializing {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance using smart cards](/docs/hs-crypto?topic=hs-crypto-initialize-hsm-management-utilities), you need to define the security policy for the {{site.data.keyword.IBM_notm}} Management Utilities. Security officers need to document the security policy in a security plan and periodically review the corporate security policy and their current key management system.
{: shortdesc}

<!-- ## Smart card vulnerabilities
{: #smart-card-vulnerabilities}

If a security policy is not in place or the physical security of the workstation and the smart card readers are not maintained, your smart cards might be exposed to the following vulnerability issues:

* Unauthenticated encryption: Your data in the smart cards might be encrypted by unauthenticated users. [More description is needed]
* Use of PKCS #11 v1.5 RSA padding scheme: [Description is needed on what PKCS #11 v1.5 RSA padding scheme means to the user. Is it only a vulnerability issue to PKCS11 V1.5?]
* Use of anonymous Diffie-Hellman key exchange: [Diffie–Hellman key exchange](https://en.wikipedia.org/wiki/Diffie%E2%80%93Hellman_key_exchange){: external} is a method of securely exchanging cryptographic keys over a public channel. However, if it is used in an anonymous way, the smart cards are exposed to security issues. [More description is needed] -->

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
