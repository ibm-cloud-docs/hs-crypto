---

copyright:
  years: 2018, 2019
lastupdated: "2019-09-23"

Keywords: IBM keys, key management, data security, Hyper Protect Crypto Services, Cloud HSM, hardware security module, PKCS11, openSSL, hsm encryption

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}

# Overview
{: #overview}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} offers advanced cloud key management service and Hardware Security Module (HSM) encryption capability with technology that has attained industry's highest security level to protect your data.
{: shortdesc}

## Why {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}?
{: #why_hpcs}

Data and information security is crucial and essential for IT environments. As more and more data moves to the cloud, keeping data protected becomes a non-trivial challenge. Built on IBM LinuxONE technology, {{site.data.keyword.hscrypto}} helps ensure that only you have access to your keys and data. A single-tenant key management service with key vaulting provided by dedicated customer-controlled HSMs helps you easily create and manage your encryption keys. Alternatively, you can bring your own encryption keys to the cloud. The service uses the same key-provider API as {{site.data.keyword.keymanagementserviceshort}}, a multi-tenant key management service, so as to provide a consistent approach to adopting {{site.data.keyword.cloud_notm}} services.

{{site.data.keyword.hscrypto}} is a dedicated HSM that is controlled by you. {{site.data.keyword.cloud_notm}} administrators have no access. The service is built on FIPS 140-2 Level 4-certified hardware, the highest offered by any cloud provider in the industry. IBM is the first to provide cloud command-line interface (CLI) for HSM master key initialization to help enable you to take ownership of the cloud HSM.

{{site.data.keyword.hscrypto}} can integrate with {{site.data.keyword.cloud_notm}} data and storage services as well as VMware vSphere and VSAN, for providing data-at-rest encryption. The managed cloud HSM supports industry standards, such as Enterprise Public-Key Cryptography Standards (PKCS) #11, so your applications can integrate cryptographic operations such as digital signing and validation via Enterprise PKCS#11 ([EP11](/docs/services/hs-crypto?topic=hs-crypto-enterprise_PKCS11_overview) API). The EP11 library provides an interface very similar to the industry-standard [PKCS #11 application programming interface (API)](http://docs.oasis-open.org/pkcs11/pkcs11-base/v2.40/os/pkcs11-base-v2.40-os.html){: external}. For more information on EP11 library structure, see [the EP11 library structure reference guide](https://www.ibm.com/downloads/cas/WXRDPRAN){: external}.

{{site.data.keyword.hscrypto}} leverages frameworks such as gRPC to enable remote application access. [gRPC](https://grpc.io/){: external} is a modern open source high performance remote procedure call (RPC) framework that can connect services in and across data centers for load balancing, tracing, health checking, and authentication. Applications access {{site.data.keyword.hscrypto}} by calling EP11 API remotely over gRPC.

With the built-in encryption of {{site.data.keyword.hscrypto}}, you can easily build cloud applications with sensitive data. {{site.data.keyword.hscrypto}} provides you with complete control of your data and encryption keys, including the HSM master key, and helps meet regulatory compliance due to technology that provides controls on the external and privilege user access to data and keys.

<!-- With {{site.data.keyword.hscrypto}}, your SSL keys are offloaded to a {{site.data.keyword.hscrypto}} instance to ensure security and protection of those sensitive keys. Besides, the certificate lifecycle management gets common approach to manage certificates and offers the visibility to certificate expiration. -->

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. This cryptography mechanism ensures that the blockchain network is running in a highly protected and isolated environment, and accelerates hashing, sign/verify operations, and node-to-node communications in the network. The success of {{site.data.keyword.blockchainfull_notm}} Platform proves the capability and value of {{site.data.keyword.hscrypto}}. -->

## How does {{site.data.keyword.hscrypto}} work?
{: #architecture}

The following architectural diagram shows how {{site.data.keyword.hscrypto}} works.

![{{site.data.keyword.hscrypto}} architecture](/image/architecture.svg "{{site.data.keyword.hscrypto}} architecture")
*Figure 1. {{site.data.keyword.hscrypto}} architecture*  

The following are a few highlights of the {{site.data.keyword.hscrypto}} architecture:
- Applications connect to {{site.data.keyword.hscrypto}} through EP11 API.
- Dedicated KeyStore in {{site.data.keyword.hscrypto}} is provided to ensure data isolation and security. Privileged users are locked out for protection against abusive use of system administrator credentials or root user credentials.
- [Secure Service Container (SSC)](https://www.ibm.com/marketplace/secure-service-container){: external} provides the enterprise-level of security and impregnability that enterprise customers have come to expect from [IBM LinuxONE](https://www.ibm.com/it-infrastructure/linuxone){: external} technology.
- FIPS 140-2 Level 4 compliant cloud HSM is enabled for highest physical protection of secrets.  

## Key features
{: #key-features}

{{site.data.keyword.hscrypto}} provides both key management and cloud HSM functions:

### Key management
{: #key-management}

* **{{site.data.keyword.cloud_notm}} data services protection with encryption keys**

  {{site.data.keyword.hscrypto}} supports Keep Your Own Keys (KYOK) so that you have more control and authority over your data with encryption keys that you can keep, control, and manage. When the encryption keys are deleted, your data is no longer retrievable, regardless of the application that stored it.

* **{{site.data.keyword.keymanagementservicefull_notm}} API integration**

  {{site.data.keyword.keymanagementservicefull_notm}} API is integrated into {{site.data.keyword.hscrypto}} to generate and protect keys. {{site.data.keyword.hscrypto}} protects these keys and stores them in a highly protected and isolated environment, which protects your data with technology that is certified at industry's highest security level.

* **Access management and auditing**

  {{site.data.keyword.hscrypto}} can integrate with other IBM Cloud services so as to manage key access, log and monitor security events, and support compliance requirements.

### Cloud HSMs
{: #cloud-hsm}

* **Customer-controlled HSM**

  The available support for customer-controlled cloud hardware security modules (HSM) accessible through gRPC APIs, which allows users to access EP11 library for cryptography operations. Customer-controlled HSM provides advanced control and authority for digital keys to be protected in accordance with industry regulations in {{site.data.keyword.cloud_notm}} and to be accessed only by the customer.

* **FIPS 140-2 Level 4 certified technology provided**

  {{site.data.keyword.hscrypto}} provides access to the FIPS 140-2 Level 4 certified technology, highest level of security attainable for cryptographic hardware. Industries, such as financial sector services, require this level of security to protect their data. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access.

* **No privileged user access to your keys and data**

  {{site.data.keyword.hscrypto}} brings the unique capabilities of data protection from IBM LinuxONE to {{site.data.keyword.cloud_notm}}. {{site.data.keyword.hscrypto}} protects your data in SSC that provides the enterprise-level of security and impregnability that enterprise customers have come to expect from IBM Z technology. Hardware virtualization is used to protect your data in an isolated environment. In this way, dedicated service per service instance is provided, so no external access is allowed, including privileged users such as cloud administrators, to your data. Thus, data compromise risk against insider threats is reduced.

<!-- {{site.data.keyword.hscrypto}} also leverages the ACSP solution that enables remote access to the IBM’s cryptographic coprocessors. ACSP allows for utilization of strong hardware-based cryptography as a service in distributed environments where data security cannot be guaranteed. {{site.data.keyword.hscrypto}} utilizes ACSP as a *network hardware security module (NetHSM)* that provides access to HSM via PKCS#11 standard API.-->

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

## What's next
{: #overview-next}

- To get an overall tutorial about using {{site.data.keyword.hscrypto}}, check out [Getting started with {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto?topic=hs-crypto-get-started).
- To find out more about programmatically managing your keys, check out the [{{site.data.keyword.hscrypto}} key management API reference doc](https://{DomainName}/apidocs/hs-crypto){: external}.
- To find out more about encrypting your data using the cloud HSM function of {{site.data.keyword.hscrypto}}, check out the [GREP11 API reference doc](/docs/services/hs-crypto?topic=hs-crypto-grep11-api-ref).
