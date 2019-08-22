---

copyright:
  years: 2018, 2019
lastupdated: "2019-07-01"

Keywords: hsm, Trusted Key Entry plug-in, service instance, imprint mode

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}

# Introduction to service instance initialization
{: #introduce-service}

Before you start initializing the service instance of {{site.data.keyword.hscrypto}}, you might want to understand the basic concepts and the process logic first.  
{:shortdesc}

A {{site.data.keyword.hscrypto}} instance (service instance for short) is a group of crypto units that are assigned to an IBM Cloud user account. If you are setting up a production environment, it is suggested to assign at least two crypto units per service instance for high availability. The crypto units should be on different physical Hardware security modules (HSMs). All crypto units in a service instance should be configured the same. If one part of the IBM Cloud cannot be accessed, the crypto units in a service instance can be used interchangeably. Crypto units contain master keys that encrypt the contents of key storage. With the Keep You Own Keys technology, the service instance administrators are the only person who can access the master key.

The following diagram illustrates a services instance with two crypto units.

![Service instance components](/image/service_instance.png "Service instance components")
*Figure 1. Service instance components*

## Hardware security module
{: #introduce-HSM}

Hardware security module (HSM) is a physical device that safeguards and manages digital keys for strong authentication and provides crypto-processing. HSMs of  {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} are FIPS 140-2 Level 4 certified, which is the highest level of security for cryptographic hardware. At this security level, the physical security mechanisms provide a complete envelope of protection around the cryptographic module with the intent of detecting and responding to all unauthorized attempts at physical access.

## Crypto unit
{: #introduce-crypto-unit}

A crypto unit is a single unit that represents an HSM and the corresponding software stack dedicated to HSM. Each crypto unit can manage up to 5000 digital keys. If you are setting up a production environment, it is suggested to assign at least two crypto units per service instance for high availability. The two crypto units are located in different [availability zones](https://www.ibm.com/cloud/blog/announcements/expansion-availability-zones-global-regions){: external} within the region that you select when creating the service instance. If one part of availability zones cannot be accessed, the crypto units in a service instance can be used interchangeably. All crypto units in a service instance should be configured the same.

## Trusted Key Entry plug-in
{: #introduce-TKE}

Trusted Key Entry (TKE) plug-in is a CLI plugin working with {{site.data.keyword.cloud_notm}} CLI. The TKE plug-in provides a set of functions for managing crypto units assigned to an {{site.data.keyword.cloud_notm}} user account. Use the TKE plug-in to set up administrators and load the master key. For more information, see [Initializing service instances](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm) and [Trusted Key Entry CLI plug-in reference](/docs/services/hs-crypto?topic=hs-crypto-tke_cli_plugin).

## Administrators
{: #introduce-administrators}

Administrators can be added to the target crypto units for issuing commands to the crypto units. You can add multiple administrators to one crypto unit to increase security. Each administrator owns one private [signature key](#introduce-signature-keys) for identity authentication. After signature keys are generated, you need to add the administrators with the signature keys to the target crypto unit.

## Signature keys
{: #introduce-signature-keys}

An administrator must sign any commands issued to the crypto unit with a signature. The private part of the signature key file is used to create signatures. The public part is placed in a certificate that is installed in a target crypto unit to define a crypto unit administrator. Commands issued in [imprint mode](#introduce-imprint-mode) do not need to be signed.

## Imprint mode
{: #introduce-imprint-mode}

Crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user start in a cleared state known as imprint mode. A crypto unit in imprint mode is not secure. You can only set up crypto unit administrators and signature keys in imprint mode. Commands issued to a crypto unit in imprint mode do not need to be signed. However, the command to exit imprint mode must be signed by one of the added crypto unit administrators using the signature key. Make sure to exit imprint mode before you configure [master keys](#introduce-master-key).

## Master keys
{: #introduce-master-key}

Master keys are used to encrypt the service instances for key storage. With the master key, you take the full control of the cloud HSM and own the root of trust that encrypts the entire chain of keys including root keys and standard keys. You need to configure the master key first before you can manage root keys and standard keys. {{site.data.keyword.IBM_notm}} does not back up or touch the master key, and has no way to copy it or restore it to a different machine or data center. One service instance can have only one master key. If you delete the master key of the service instance, you can effectively crypto-shred all data that was encrypted with the keys managed in the service.

A master key is composed of several master key parts. For security considerations, each key part can be owned by a different person. The key part owner should be the only person who knows the password associated with the key part file.

For more information on the key types that {{site.data.keyword.hscrypto}} manages, see [Introduction to keys](/docs/services/hs-crypto?topic=hs-crypto-introduce-keys#introduce-keys).

## Master key parts
{: #introduce-key-parts}

Multiple master key parts compose a master key. The new master key register is loaded using multiple master key parts. In the Trusted Key Entry plugin, each master key part is stored in a master key part file. Either two or three master key parts can be used to load the new master key register. For security considerations, each key part can be owned by a different person. The key part owner should be the only person who knows the password associated with the key part file.

## Master key registers
{: #introduce-key-registers}

Each crypto unit has two master key registers: a new master key register and a current master key register. The value in the current master key register encrypts the contents of the user's key storage. The new master key register is used to change the value in the current master key register. When changing the value in the current master key register, the contents of key storage need to be re-enciphered with the new master key value. Both the current master key value and the new master key value are needed to do this. Key values in key storage are deciphered using the value in the current master key register and then re-enciphered using the value in the new master key register. The re-enciphering takes place inside the HSM, so it is secure. After the full contents of key storage have been re-enciphered, the value in the new master key register can be moved into the current master key register.

The following diagram illustrates how the master key register state changes, and how the master key is loaded.

![Loading master keys](/image/master_key_register.png "How to load a master key")
*Figure 1. Loading master keys*  
