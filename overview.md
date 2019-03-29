---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

Keywords: IBM Key, data security, Hyper Protect Crypto Services, HSM

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} overview
{: #overview}

Data and information security is crucial and essential for IT environments. As more and more data moves to the cloud, keeping data protected becomes a non-trivial challenge.  {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} offers cryptography with technology that has attained industry's highest security level to protect your data.
{: shortdesc}

## Why {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?

Built on IBM LinuxONE technology, {{site.data.keyword.hscrypto}} helps ensure that only you have access to your keys. A single-tenant key-management service with key vaulting provided by dedicated customer-controlled HSMs helps you create encryption keys with ease. Alternatively, you can bring your own encryption keys to manage. The managed cloud HSM supports industry standards, <!-- such as PKCS #11,--> so your applications can integrate cryptographic operations like digital signing and validation.

<!-- via PKCS#11 application programming interfaces (APIs). You can access {{site.data.keyword.hscrypto}} with several popular programming languages such as Java, JavaScript, and Swift. -->

{{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. This cryptography mechanism ensures that the blockchain network is running in a highly protected and isolated environment, and accelerates hashing, sign/verify operations, and node-to-node communications in the network. The success of {{site.data.keyword.blockchainfull_notm}} Platform proves the capability and value of {{site.data.keyword.hscrypto}}

## How does {{site.data.keyword.hscrypto}} work?
{: #architecture}

The following architectural diagram shows how {{site.data.keyword.hscrypto}} works.

![{{site.data.keyword.hscrypto}} architecture](image/architecture.png "{{site.data.keyword.hscrypto}} architecture")
*Figure 1. {{site.data.keyword.hscrypto}} architecture*  

The following are a few highlights of the {{site.data.keyword.hscrypto}} architecture:

<!-- * Applications connect to {{site.data.keyword.hscrypto}} through PKCS#11 APIs. -->

- Dedicated KeyStore in {{site.data.keyword.hscrypto}} is provided to ensure data isolation and security. Privileged users are locked out for protection against abusive use of system administrator or root user credentials.  
- Secure Service Container (SSC) provides the enterprise-level of security and impregnability that enterprise customers have come to expect from IBM Z technology.  
- FIPS 140-2 Level 4 compliant cloud HSM is enabled for highest physical protection of secrets.  

## Key features
{: #key-features}

The following are the key features of {{site.data.keyword.hscrypto}}:

### {{site.data.keyword.cloud_notm}} data services protection using encryption keys with customer-controlled cloud HSMs
{: #key-feature-1}

{{site.data.keyword.hscrypto}} supports Keep Your Own Keys (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. The available support for customer-controlled cloud hardware security modules (HSM) allows for digital keys to be protected in accordance with industry regulations in {{site.data.keyword.cloud_notm}} and to be access only by the customer.<!-- The HSM provides PKCS#11 APIs, which makes {{site.data.keyword.hscrypto}} accessible by several popular programming languages such as Java, JavaScript, and Swift.-->

### FIPS 140-2 Level 4 certified technology provided
{: #key-feature-2}

{{site.data.keyword.hscrypto}} provides access to the FIPS 140-2 Level 4 certified technology, highest level attainable of security for cryptographic hardware. <!-- Industries, such as financial sector services, require this level of security to protect their data.--> At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access.

### No privileged user access to your keys and data
{: #key-feature-3}

{{site.data.keyword.hscrypto}} brings the unique capabilities of data protection from IBM Z to {{site.data.keyword.cloud_notm}}. {{site.data.keyword.hscrypto}} protects your data in SSC that provides the enterprise-level of security and impregnability that enterprise customers have come to expect from IBM Z technology. Hardware virtualization is used to protect your data in an isolated environment. In this way, dedicated service per service instance is provided, so no external access is allowed, including privileged users such as cloud administrators, to your data. Thus, data compromise risk against insider threats is reduced.

### {{site.data.keyword.keymanagementservicefull_notm}} integration to secure {{site.data.keyword.cloud_notm}} data and storage services
{: #key-feature-4}

{{site.data.keyword.keymanagementservicefull_notm}} APIs are integrated into {{site.data.keyword.hscrypto}} to generate and protect keys. {{site.data.keyword.hscrypto}} protects these keys and stores them in a highly protected and isolated environment on IBM Z, which protects your data with technology that is certified at industry's highest security level.

<!-- {{site.data.keyword.hscrypto}} also leverages the **IBM Advanced Crypto Service Provider (ACSP)** solution that enables remote access to the IBM’s cryptographic coprocessors. ACSP allows for utilization of strong hardware-based cryptography as a service in distributed environments where data security cannot be guaranteed. {{site.data.keyword.hscrypto}} utilizes ACSP as a *network hardware security module (NetHSM)* that provides access to HSM via PKCS#11 standard APIs.-->

<!-- With {{site.data.keyword.hscrypto}}, your **SSL keys are offloaded** to a {{site.data.keyword.hscrypto}} to ensure security and protection of those sensitive keys.  Besides, the certificate lifecycle management gets common approach to manage certificates and offers the visibility to certificate expiration.-->

## Roles and responsibilities
{: #roles-responsibilities}

The following table shows the roles that {{site.data.keyword.hscrypto}} supports.

<table>
  <tr>
    <th>Roles</th>
    <th>Responsibilities</th>
  </tr>
  <tr>
    <td>Crypto unit administrator</td>
    <td>
      Signs administrative commands such as for installing another crypto unit administrator, and provides signature keys.
    </td>
  </tr>
  <tr>
    <td>Key owner</td>
    <td>Provides master key parts for initializing a service instance.</td>
  </tr>
  <tr>
    <td>Service user</td>
    <td>Stores, retrieves, and generates root keys and standard keys through user interface and APIs.</td>
  </tr>
  <caption style="caption-side:bottom;">Table 1. Roles and responsibilities</caption>
</table>
