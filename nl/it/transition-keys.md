---

copyright:
years: 2018, 2019
lastupdated: "2019-03-26"

Keywords: root keys, standard keys, migration, transition, beta

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Migrazione delle chiavi dall'istanza del servizio beta
{: #migrate-keys}

Se stai utilizzando un'istanza del servizio beta e vuoi migrare le chiavi root e standard che gestisci a un'istanza del servizio di produzione {{site.data.keyword.hscrypto}}, questa è la procedura che devi seguire.
{: shortdesc}

Gli amministratori di IBM Cloud non possono migrare le chiavi master perché non sono estraibili dall'unità di crittografia. Devi inizializzare l'istanza del servizio di produzione con la tua chiave master.
{:important}  

## Prima di cominciare
{: #migrate-prerequisites}

1. [Crea un'istanza del servizio](/docs/services/hs-crypto/provision.html) con il piano Hyper Protect Crypto Services.

2. [Inizializza l'istanza del servizio](/docs/services/hs-crypto/initialize_hsm.html) con il plugin Trusted Key Entry.

## Migrazione delle chiavi
{: #migrate-keys-steps}  

Completa la seguente procedura per migrare le chiavi root e standard all'ambiente di produzione.

1. [Importa le chiavi root](/docs/services/hs-crypto/import-root-keys.html) tramite la GUI o l'API.

  Puoi migrare le chiavi root importate dall'istanza del servizio beta a quella di produzione.
  {:tip}

2. Spacchetta le chiavi di crittografia dei dati (DEK) dall'istanza del servizio beta e impacchetta le DEK nell'istanza del servizio di produzione:

  1. [Spacchetta le chiavi di crittografia dei dati (DEK)](/docs/services/hs-crypto/unwrap-keys.html) dall'istanza del servizio beta con l'[API invoke-an-action-on-a-key ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key){: new_window}.

  2. [Impacchetta le DEK](/docs/services/hs-crypto/wrap-keys.html) nell'istanza del servizio di produzione con l'[API invoke-an-action-on-a-key ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto#invoke-an-action-on-a-key{: new_window}).

3. Ricrea le chiavi standard seguendo questa procedura:

  1. [Richiama le chiavi standard](/docs/services/hs-crypto?topic=hs-crypto-view-keys#retrieve-key-api) con l'[API retrieve-key-by-id ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto#retrieve-a-key-by-id){: new_window}. Viene restituito il payload utilizzato per creare la chiave nell'istanza beta.

  2. [Crea le chiavi standard](/docs/services/hs-crypto/create-standard-keys.html) nella nuova istanza del servizio con le informazioni richiamate nel passo precedente tramite la GUI o l'[API create-a-new-key ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto#create-a-new-key){: new_window}.

## Operazioni successive
{: #migration-next}

Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, [consulta la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
