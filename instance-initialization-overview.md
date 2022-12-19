---

copyright:
  years: 2018, 2022
lastupdated: "2022-12-19"

keywords: initialize service, key ceremony, hsm, tke, cloud tke, tke cli, management utilities, imprint mode, smart card, master key, key part, load master key

subcollection: hs-crypto

---


{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:external: target="_blank" .external}
{:term: .term}
{:ui: .ph data-hd-interface="ui"}
{:cli: .ph data-hd-interface="cli"}
{:api: .ph data-hd-interface="api"}
{:terraform: .ph data-hd-interface="terraform"}

# Initializing your service instance
{: #introduce-service}

Before you can use {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} to manage encryption keys and perform cryptographic operations, you need to initialize your service instance first.
{: shortdesc}

Service instance initialization is the process of loading the master key, so that you can take the ownership of the cloud [hardware security module (HSM)](#x6704988){: term} of {{site.data.keyword.hscrypto}} and own the root of trust that encrypts the entire hierarchy of encryption keys.

To initialize your service instance, you need to create [signature keys](#x8250375){: term} for [crypto unit](#x9860404){: term} administrators, set quorum authentication thresholds to exit the [imprint mode](#x9860399){: term}, and load the [master key](#x2908413){: term} to the crypto units.

## Understanding administrators and signature keys
{: #understand-crypto-unit-admin}

A crypto unit is composed of an HSM and the corresponding software stack that is dedicated to the HSM. Each crypto unit can manage up to 5000 digital keys. If you're setting up a production environment, it is suggested to assign at least two crypto units for high availability when you create a {{site.data.keyword.hscrypto}} instance. The crypto units are located in different availability zones within the region that you select when you create the service instance. All crypto units in a service instance need to be configured the same. If one availability zone cannot be accessed, the crypto units in a service instance can be used interchangeably. Crypto units contain the master key that encrypts the contents of key storage, including root keys and standard keys in the key management keystore and Enterprise PKCS #11 (EP11) keys in the EP11 keystore.

To issue commands for crypto units to perform actions, you need to assign administrators to the crypto units. Each administrator has an associated signature key for identity authentication. The following flow chart shows how the signature keys are created and assigned to a service instance with two crypto units.

![Creating and assigning signature keys](/images/sigkey-flow.svg "How to create and assign signature keys"){: caption="Figure 2. Creating and assigning signature keys" caption-side="bottom"}

Signature keys are created and assigned by following this procedure:

1. The administrator creates the signature key pairs. The private and public key parts are stored on your local workstation or smart card depending on how you initialize your service instance.
2. The administrator is added by assigning the public signature key part to the crypto unit. The public key part is placed in a certificate that is installed in a target crypto unit to define a crypto unit administrator.

## Understanding imprint mode and signature thresholds
{: #understand-imprint-mode}

The crypto units start in a clear state that is known as Imprint Mode. A crypto unit in imprint mode is less secure because actions towards a crypto unit in imprint mode don't need to be signed with any administrator signature keys. After you assign crypto unit administrators, you can set signature thresholds to control how many administrator signatures are needed to run a command. In imprint mode, the signature thresholds are set to zero. To exit imprint mode and secure the crypto unit, set the signature thresholds to a value greater than zero.

There are two types of signature thresholds on a crypto unit. The main signature threshold controls how many signatures are needed to run most administrative commands. The revocation signature threshold controls how many signatures are needed to remove an administrator. Some commands need only one signature, regardless of how the signature threshold is set.

Setting the signature thresholds to a value greater than one enables quorum authentication from multiple administrators for sensitive operations. The maximum value that you can set the signature threshold and revocation signature threshold is eight, which is also the maximum number of administrators that can be added to a crypto unit.

When you configure crypto units, you are automatically prompted for the required number of signatures based on the operation type and whether the crypto units are in imprint mode.  For reference, the following table includes the required number of signatures of each operation.

| Operation | Commands | Required signatures in imprint mode |Required signatures after leaving imprint mode |
| ------- | ----------- | ----------------------- |----------------------- |
|Add administrator  | 	`tke cryptounit-admin-add`  | No signature needed. | The current signature threshold value.  |
|Remove administrator |`tke cryptounit-admin-rm`   | No signature needed. | The current revocation threshold value.  |
|Set signature threshold  | `tke cryptounit-thrhld-set`  | When leaving imprint mode, the new signature threshold value. | The current signature threshold value.  |
|Clear new master key register  | `tke cryptounit-mk-clrnew`  | Not allowed. |  One signature. |
|Clear current master key register  | `tke cryptounit-mk-clrcur`  | Not allowed. | One signature.  |
|Load new master key register  | `tke cryptounit-mk-load`  | Not allowed. | One signature per key part. This command generates an importer key, which also requires one signature. The same administrator can be used for all signatures.  |
|Commit new master key register  | `tke cryptounit-mk-commit`  | Not allowed. | The current signature threshold value.  |
|Set immediate (finalize master key register)  | `tke cryptounit-mk-setimm`  | Not allowed.|  	One signature. |
|Set control point  | `tke cryptounit-cp-btc` `tke cryptounit-cp-eddsa` `tke cryptounit-cp-sig-other`  | Not allowed. |  The current signature threshold value. |
|Zeroize crypto unit  | tke cryptounit-zeroize  | No signature needed. | 	One signature.   |
{: caption="Table 1. Required number of signatures for TKE operations" caption-side="bottom"}

## Understanding the master key
{: #understand-key-ceremony}

After the crypto units exit the imprint mode, you can load the master key to the crypto units. A master key is used to encrypt data in key storage. With the master key, you own the root of trust that encrypts the entire key hierarchy, including root keys and standard keys in the key management keystore and Enterprise PKCS #11 (EP11) keys in the EP11 keystore. Each service instance has only one master key.

To load the master key, each crypto unit has two master key registers: a new master key register and a current master key register. The value in the current master key register encrypts the contents of the user's key storage. The new master key register is used to change the value in the current master key register for [master key rotation](/docs/hs-crypto?topic=hs-crypto-master-key-rotation-intro).

The following flow chart illustrates how the master key register state changes, and how the master key is loaded.

![Loading master keys](/images/master-key-register.svg "How to load a master key"){: caption="Figure 3. Loading master key" caption-side="bottom"}

In the chart, each crypto unit loads the master key with the following steps:

1. Load the new master key register with the master key. After the master key is loaded, the new master key register is in `Full uncommitted` state.
2. Commit the new master key register. After it is committed, the new master key register is in `Full committed` state.
3. Activate the current master key register. By doing so, the new master key register value is copied into the current master key register, and the new master key register is cleared.

## What's next
{: #introduce-instance-initialization-next}

Depending on your business needs and security requirements, {{site.data.keyword.hscrypto}} provides you with two tools and three options to initialize your service instance. For more information, see [Introducing service instance initialization approaches](/docs/hs-crypto?topic=hs-crypto-initialize-instance-mode).
