# FAQs for {{site.data.keyword.uko_short}}

Read to get answers for questions about {{site.data.keyword.uko_short}}.


## How many Agents do I need to install to make {{site.data.keyword.uko_short}} work? How many for high availability / fail over?

There must be one {{site.data.keyword.uko_short}} Agent per keystore (CKDS). When keystores are shared in a sysplex, it is sufficient to have one {{site.data.keyword.uko_short}} Agent per sysplex.

## Why do I need TKE and what for?

TKE is required to create the {{site.data.keyword.uko_short}} Disaster Recovery Key in a form that enables an organization to restore the key in the CKDS. All keys in the {{site.data.keyword.uko_short}} repository database are encrypted with the Recovery Key (directly or indirectly) and without it no new keys can be created and existing keys cannot be distributed to keystores. In addition, the use of TKE makes it easier to properly manage the crypto cards and to initialize the HSM master keys.

## Can't I just use ICSF for Pervasive Encryption keys?

With ICSF, you can manage keys in a single keystore. If keys must be in multiple keystores, the keys must be manually transferred in a separate manual process. With {{site.data.keyword.uko_short}} you manage keys in multiple keystores as easily as managing keys in a single keystore. (I consider keystores in a CKDS-sharing group a single keystore). The manual transfer process may be non-compliant with regulations due to how Data keys are protected. This will be relevant for some customers but not all. For any customer who must live up to regulations such as PCI, IBM recommends the use of Cipher keys because of their stronger protection. However, ICSF does not provide the means to create AES Cipher keys for PE out-of-the-box. It would require a custom program that uses the ICSF API. {{site.data.keyword.uko_short}} can create these AES Cipher keys out-of-the-box.

## What about tape encryption?

Tape encryption is out of scope for {{site.data.keyword.uko_short}}. Please refer the general documentation for Pervasive Encryption.

## Will the {{site.data.keyword.uko_short}} Liberty instance count as 1 simultaneously instance? What about scanner job - does that count as SI as well?

The [announcement letter](https://www.ibm.com/common/ssi/cgi-bin/ssialias?infotype=AN&subtype=CA&htmlfid=897/ENUS220-108) exclusively names the Agent as counting as simultaneous instance: "EKMF Web includes a pricing metric that enables flexibility in the way clients choose to implement production, test, and development environments. Pricing is determined by the number of simultaneous EKMF Web agent instances in use aggregated across an enterprise."

## Can I control access via RACF groups?

It's generally considered a best practice to permit users' access to RACF resources through their group privileges, and this is extended to the EJBROLE class as well. So when giving users a certain capability in {{site.data.keyword.uko_short}} through EJBROLE roles, what you're really doing is giving a particular RACF group READ access to the EJBROLE profile they need access to - i.e. READ access to "templates:write" EJBROLE profile to give a key Admin group the ability to create key templates.

## Why is disaster recovery not good enough for key management?

The data keys are stored in the CKDS. If the CKDS is backed up frequently, what value would {{site.data.keyword.uko_short}} provide, other than an easier to use GUI if a key needs to be recovered for whatever reason?

A benefit of {{site.data.keyword.uko_short}} is the master key independent backup of all keys and the ability to determine missing keys and the 1-click-recovery of individual keys. This is much faster than the corresponding process for extracting individual keys out of a CKDS backup (With added complexity if the CKDS backup was under an old master key). The {{site.data.keyword.uko_short}} backup of keys also means that the keys in the CKDS are not the only copy of the key, making them less vulnerable to accidental deletion and/or corruption of the CKDS dataset.

## Can I rotate keys? Can I rotate them automatically?

Key rotation consists of creating a new key and then updating the DFP data segment for datasets. {{site.data.keyword.uko_short}} can generate new keys and put them in the CKDS. However, the changes to RACF/DFP must be done separately. {{site.data.keyword.uko_short}} will by design, not do anything without being started by a user, but does provide an API that will allow external automation to trigger key generation.

## How would key rotation be easier with {{site.data.keyword.uko_short}} as opposed to just using ICSF?

{{site.data.keyword.uko_short}} has a function that will create a new key based on the properties of an existing key. This ensures that the key label for the new key is the same as the old key with an incremented sequence number.

## When will a customer need a key manager vs doing the work manually?

It is true that for a small number of keys, a key management system could be too much. However, any reasonable setup of PE, will use many more keys and will therefore need a key management system. You might use ICSF for the initial trials on a sandbox system, but for testing and especially production, they really should use a key management system from the start. There is also an aspect of planning in it. You need a key label naming convention and {{site.data.keyword.uko_short}} can help you structure and enforce such a naming convention. In our experience, this naming convention is typically missing when we introduce {{site.data.keyword.uko_short}} to existing systems with existing keys. This complicates the import of existing keys. 
