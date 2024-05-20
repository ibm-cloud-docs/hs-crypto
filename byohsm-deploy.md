---

copyright:
  years: 2024
lastupdated: "2024-05-20"

keywords: bring your own hsm, byohsm, hybrid hpcs, deploy hsm, configure own hsm

subcollection: hs-crypto

---

{{site.data.keyword.attribute-definition-list}}


# Setting up BYOHSM
{: #deploy-hsm-for-byohsm}

You can enable the Bring Your Own HSM (BYOHSM) function in {{site.data.keyword.hscrypto}} to use your own on-premises hardware security modules (HSMs). To do so, you need to first configure and deploy the HSMs to work with your service instance.
{: shordesc}

The Bring Your Own HSM (BYOHSM) function is available only in the Standard Plan service instances in the VPC-based regions. For the VPC region list, see [Regions and locations](/docs/hs-crypto?topic=hs-crypto-regions#available-regions).
{: note}

## Before you begin
{: #deploy-byohsm-prerequisites}

Before you can configure and deploy your on-premises HSMs, make sure that you complete the HSM purchase and initial setup based on your providers guidelines. Currently, {{site.data.keyword.hscrypto}} supports Thales HSM A7xx models only. For more information, see [supported types of HSMs](/docs/hs-crypto?topic=hs-crypto-introduce-bring-your-own-hsm#byohsm-limitation-scope).

## Creating partitions
{: #deploy-byohsm-partition}

To use your own HSMs for {{site.data.keyword.hscrypto}}, you need to create and initialize an application partition in each HSM. The application partition is used to store cryptographic objects and perform operations. Make sure that you set the same partition label and partition crypto officer password for the application partitions in all HSMs. The password is used by {{site.data.keyword.hscrypto}} as part of the PKCS #11 session API login process.

The Thales SafeNet Luna Network HSM uses two types of partitions:

- Administrative partition

    Each Luna Network HSM has only one administrative partition. It is created when you initialize the HSM. The administrative partition is used to set and change HSM-wide policies, create or destroy application partitions, update HSM firmware and capabilities, and so on.

- Application partition

    Each Luna Network HSM has at least one application partition. The application partition is used to perform cryptographic operations and store cryptographic objects for your applications. For multi-tenancy use cases, you can create multiple application partitions with each having its own security and access controls. For the A750 model, you can create up to five application partitions. If you need more application partitions, you need to [purchase extra partition licenses](https://thalesdocs.com/gphsm/luna/7/docs/network/Content/admin_hsm/updates/licensing/capabilities_sa.htm){: external}.

For more information about partitions, see the [Partition Administration Guide](https://thalesdocs.com/gphsm/luna/7/docs/network/Content/admin_partition/Preface.htm){: external}.

## Creating keys
{: #deploy-byohsm-key}

To use your own HSMs for {{site.data.keyword.hscrypto}}, you need to create the following keys on your HSMs and store them as persistent token objects in the partition memory. Make sure to set a label for each key. You need to provide the labels to IBM when you provision an instance afterward.

| Key type	| Description |
| --------  | ----------- |
| Master Key Encryption Key (MKEK) |	(256-bit AES key) A root level encryption key for wrapping and unwrapping instance keys in {{site.data.keyword.hscrypto}}. |
| Signing key (SKEY) |	(256-bit AES key) Used for signing and verification of instance keys and user keys in {{site.data.keyword.hscrypto}}. |
| Import Key (IKEY)	| (192-bit DES3 key) Used to encrypt and decrypt the key materials to be imported into {{site.data.keyword.hscrypto}}. |
| Transit Key Encryption Keys (TKEKs)	| (10 pairs of RSA asymmetric keys) Used to securely import your own keys into {{site.data.keyword.hscrypto}}. |
{: caption="Table 1. Keys needed for Bring Your Own HSM" caption-side="bottom"}

You need to set some specific parameters when you create these keys. Contact IBM for details by [creating a support case](/docs/get-support?topic=get-support-open-case).

You can use some tools to create these keys. Consult with Thales technical support to find a secure way to create these keys based on your organization's security policy and compliance requirements.
{: tip}

## Network connectivity best practice
{: #deploy-byohsm-network-connection}

For a better network performance when you connect on-premises HSMs to {{site.data.keyword.hscrypto}}, you can refer to the following best practice:

- Use {{site.data.keyword.cloud_notm}} Direct Link Connect to quickly establish and deliver private connectivity to {{site.data.keyword.cloud_notm}} infrastructure. For more information, see [Ordering {{site.data.keyword.cloud_notm}} Direct Link Connect](/docs/dl?topic=dl-how-to-order-ibm-cloud-dl-connect).
- Use {{site.data.keyword.cloud_notm}} Transit Gateway to connect your on-premises network that uses Direct Link to your {{site.data.keyword.cloud_notm}} networks. For more information, see [Getting started with {{site.data.keyword.cloud_notm}} Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started).
- Use 10 GB links for cryptographic traffic between {{site.data.keyword.hscrypto}} and your HSMs.
- Use a bond of 2 GB links for management and administration traffic. Note that bonding provides standby fault tolerance reliability, but does not provide load balancing.

    {{site.data.keyword.hscrypto}} requires a TCP connectivity to HSM on port 1792 for NTLS protocol. To check the connectivity, issue the following `netcat` command:

    ```
    nc -vz <HSM-ip-addr> 1792
    ```
    {: pre}

    Where `HSM-ip-addr` is the IP address of your HSM.

## Preparing information for HSM connection
{: #deploy-byohsm-prepare-info}

Before you can [provision a {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-provision&interface=ui), you need to prepare the following information:

To provision an instance with BYOHSM, you need to contact IBM to add your account to the allowlist and provide this information for all HSMs that you want to use for {{site.data.keyword.hscrypto}}.
{: important}

| Attribute | Description |
| --------- | ----------- |
| HSM IP address | The IP address of your HSM. |
| HSM server certificate | The NTLS communications that are used by the Thales HSM require certificate exchanges between the HSM and {{site.data.keyword.hscrypto}}. You need to create a TLS certificate on your HSM and provide the certificate for {{site.data.keyword.hscrypto}} to verify communications from the HSM. |
| Partition label | The name of the application partition that you create for {{site.data.keyword.hscrypto}} to use. |
| Partition crypto officer password | The credential for {{site.data.keyword.hscrypto}} to log in to the corresponding application partition to perform key operations. |
| Master key label | The label or name of the Master Key Encryption Key (MKEK). The label is used by {{site.data.keyword.hscrypto}} to refer to the master key in PKCS #11 API calls. |
| Signing key label | The label or name of the Signing key (SKEY). It is used for data authentication such as data signing and verification. |
| Import key label | The label or name of the Import key (IKEY). {{site.data.keyword.hscrypto}} uses this key to encrypt or decrypt key materials to be imported. |
| Transit Key Encryption Key label prefix | The label prefix of the Transit Key Encryption Key that is used for securely importing your own keys. |
{: caption="Table 2. Information needed for Bring Your Own HSM" caption-side="bottom"}

## What's next
{: #deploy-hsm-next}

After you collect all the information needed and set up the network connectivity, you can contact IBM and [provision a {{site.data.keyword.hscrypto}} instance with Bring Your Own HSM](/docs/hs-crypto?topic=hs-crypto-provision&interface=ui).

