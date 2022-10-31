---

copyright:
  years: 2019, 2022
lastupdated: "2022-10-31"

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

# Security considerations for initializing a service instance
{: #initialization-security-policy}

When you initialize your {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance, you need to make decisions that affect the security of your instance. 
{: shortdesc}

## Considerations for storing signature keys and master key parts
{: #consideration-key-parts}

You need to decide the following aspects:

- Are you going to use smart cards to store signature keys and master key parts, or use workstation files?
- If you use workstation files, are you going to use recovery crypto units to generate a random master key value and hold the backup copy of the master key?
- How many signatures are required for sensitive commands?
- How many key parts are you going to use to load the master key registers?
- How often are you going to change the master key value?

Using smart cards to store signature keys and master key parts is more secure than using workstation files. When a signature key is stored on a smart card, it never appears in the clear outside the smart card. When a master key part is stored on a smart card, it never appears in the clear outside the smart card or a crypto unit. 

When a signature key or master key part is stored in a workstation file, the key or key part is decrypted and appears temporarily in the clear in workstation memory when it is used.

When recovery crypto units are used to generate a random master key value and hold the backup copy of the master key, the master key value never appears in the clear outside an IBM crypto unit.

## Considerations for defining the Management Utilities security policy
{: #smart-card-security-plan}

If you decide to use smart cards, you need to consider the following aspects:

- How many backup copies of your smart cards are you going to make? You should make at least one backup copy of all smart cards and store them in a secure place.
- Where are you going to store smart cards when they are not in use?
- Who need to know the smart card PINs?

Some organizations store their smart cards in a safe, and keep a log of when the smart cards are used for administrative actions and who used them.

## Considerations for defining the workstation file security policy
{: #file-security-plan}

If you decide to use workstation files, you also need to consider the following aspects:

- Where are you going to save backup copies of the workstation file?
- Who need to know the workstation file passwords?

Many security standards require dual control for administrative actions. Dual control means that more than one person must cooperate in order to perform the action. Dual control can be accomplished by setting the signature threshold to 2 or more, and having different people own each smart card and PIN or having different people know the workstation file passwords. Dual control when loading the master key register from smart cards can be accomplished by placing the master key parts on different smart cards and having different people own each smart card and PIN.
