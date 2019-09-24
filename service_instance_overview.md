---

copyright:
  years: 2018, 2019
lastupdated: "2019-08-02"

Keywords: Hyper Protect Crypto Services, hsm, Trusted Key Entry plug-in, service instance, imprint mode, smart card, master key, load master key

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

Before you start initializing the service instance of {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, you might want to understand the process logic first.  
{:shortdesc}

A {{site.data.keyword.hscrypto}} instance (service instance for short) is a group of crypto units that are assigned to an {{site.data.keyword.cloud_notm}} user account. If you are setting up a production environment, it is suggested to assign at least two crypto units per service instance for high availability. The crypto units should be on different physical Hardware security modules (HSMs). All crypto units in a service instance should be configured the same. If one part of the IBM Cloud cannot be accessed, the crypto units in a service instance can be used interchangeably.

Crypto units contain master keys that encrypt the contents of key storage. With the Keep You Own Keys technology, the service instance administrators are the only person who can access the master key. To load the master key to the service instance, you must use the *Trusted Key Entry plug-in*. The Trusted Key Entry plug-in provides a set of functions for managing crypto units assigned to an {{site.data.keyword.cloud_notm}} user account.

The following diagram illustrates a services instance with two crypto units.

![Service instance components](/image/kms_service.png "Service instance components")
*Figure 1. Service instance components*

## Understanding the master key and master key parts
{: #understand-master-key}

Master keys are used to encrypt the service instances for key storage. With the master key, you own the root of trust that encrypts the entire chain of keys including root keys and standard keys. IBM does not back up or touch the master key, and has no way to copy it or restore it to a different machine or data center. One service instance can have only one master key. If you delete the master key of the service instance, you can effectively crypto-shred all data that was encrypted with the keys managed in the service.

A master key is composed of at least two master key parts. For security considerations, each key part can be owned by a different administrators. The key part owner should be the only person who knows the password associated with the key part file. In the Trusted Key Entry plugin, each master key part is stored in a master key part file.

<!-- ## Understanding smart cards
{: #understand-smart-cards}

Each of the smart card is protected by a PIN code and contains the following elements:

* A signature key for an individual administrator
* A unique master key part  

In a production environment, the master key has to be built from at least three key parts that are hosted by three administrators, which means, you will need to have three smart cards in a production environment.

The smart card chip is a Hardware Security Module (HSM) with encryption capability. The key part is generated inside the smart card's HSM and never leaves the smart cards HSM unless it is encrypted. The administrator's signature key is generated in the smart card's HSM and the private part never leaves the smart card's HSM. -->

## Understanding imprint mode
{: #understand-imprint-mode}

On a {{site.data.keyword.hscrypto}} service instance, the crypto units start their life in a clear state known as *Imprint Mode*. A crypto unit in imprint mode is not secure. You can only set up crypto unit administrators and create administrator signature keys in imprint mode. Each administrator owns a signature key, and needs to be added to the crypto unit. Commands issued to a crypto unit in imprint mode do not need to be signed by administrators.

The master key can be loaded only after the crypto unit exits imprint mode. The command to exit imprint mode must be signed by one of the added crypto unit administrators using the signature key.

## Understanding how master key is loaded
{: #understand-key-ceremony}

After the crypto unit exits imprint mode, you need to create at least two key parts that will be used to build your master key. In a production environment, it is suggested to create at least three key parts that are owned by different administrators for security considerations.

After you create the required number of master key parts to use, you can load your master key. These are the steps used to create and run the load key command. A command is needed for every crypto unit that is being updated.

Each crypto unit has two master key registers: a new master key register and a current master key register. The value in the current master key register encrypts the contents of the user's key storage. The new master key register is used to change the value in the current master key register. When changing the value in the current master key register, the contents of key storage need to be re-enciphered with the new master key value. Both the current master key value and the new master key value are needed to do this. Key values in key storage are deciphered using the value in the current master key register and then re-enciphered using the value in the new master key register. The re-enciphering takes place inside the HSM, so it is secure. After the full contents of key storage have been re-enciphered, the value in the new master key register can be moved into the current master key register.

Do the following for each crypto unit to build the master key:

1. Load the New Master Key Register with the master key. After the master key is loaded, the New Master Key Register is in FULL UNCOMMITTED state.  
2. Commit the New Master Key Register. After it is committed, the New Master Key Register is in FULL COMMITTED state.
3. Activate the Current Master Key Register. By doing so, the New Master Key Register value is copied into the Current Master Key Register, and the New Master Key Register is cleared.     

The following diagram illustrates how the master key register state changes, and how the master key is loaded.

![Loading master keys](/image/master_key_register.png "How to load a master key")
*Figure 2. Loading master keys*

For detailed steps of loading master keys, see [Initializing service instances](/docs/services/hs-crypto?topic=hs-crypto-initialize-hsm).
