---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# Introduzione alle chiavi
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} supporta diversi tipi di chiavi, tra cui le chiavi root, le chiavi standard e le chiavi master.
{:shortdesc}

## Chiavi root

Le *chiavi root* sono chiavi di impacchettamento della chiave simmetriche che gestisci completamente in {{site.data.keyword.hscrypto}}. Puoi utilizzare una chiave root per proteggere altre chiavi di crittografia con la codifica avanzata. Per ulteriori informazioni, consulta <a href="/docs/services/key-protect/concepts/envelope-encryption.html">Crittografia envelope</a>.

Puoi gestire le chiavi root seguendo la procedura descritta in [Gestisci le tue chiavi](/docs/services/hs-crypto/index.html#manage-keys).

## Chiavi standard

Le *chiavi standard* sono le chiavi simmetriche utilizzate per la crittografia. Puoi utilizzare una chiave standard per crittografare e decrittografare direttamente i dati.

Puoi gestire le chiavi standard seguendo la procedura descritta in [Gestisci le tue chiavi](/docs/services/hs-crypto/index.html#manage-keys).

## Chiavi master

Le *chiavi master* vengono utilizzate per crittografare l'istanza di crittografia (HSM) che elabora a livello crittografico e gestisce le chiave root e le chiavi standard. Con la chiave master, possiedi la radice di attendibilità che crittografa l'intera catena di chiavi, comprese le chiavi root e le chiavi standard.

A causa del canale protetto end-to-end stabilito per l'istanza di crittografia (HSM), solo gli amministratori dell'istanza {{site.data.keyword.hscrypto}} possono impostare e gestire la chiave master. Nota che IBM non esegue il backup o manipola la chiave master e non ha modo di copiarla o ripristinarla su un altro computer o data center.

Un'istanza di crittografia (HSM) può avere una sola chiave master. Se elimini la chiave master dell'istanza {{site.data.keyword.hscrypto}}, puoi effettivamente eliminare a livello crittografico tutti i dati che erano stati crittografati con le chiavi gestite nel servizio.

Puoi gestire le chiavi master durante l'[inizializzazione delle istanze di crittografia per proteggere l'archiviazione chiavi](/docs/services/hs-crypto/initialize_hsm.html).

La rotazione della chiave master non è supportata nella fase corrente.
{:important}
