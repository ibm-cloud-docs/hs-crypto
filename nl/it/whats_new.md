---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Novità
{: #what-new}

Rimani aggiornato con le nuove funzioni disponibili per {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Marzo 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} è generalmente disponibile
{: #ga-201903}
Novità a partire dal 29-03-2019

Per ulteriori informazioni sull'offerta {{site.data.keyword.hscrypto}}, visita l'[home page di {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}.

A partire dal 31 marzo 2019, non sarà più possibile eseguire il provisioning di nuove istanze beta di Hyper Protect Crypto Services. Le istanze esistenti avranno supporto fino alla fine della data di supporto beta (30 aprile 2019).

Vedi [Migrazione delle chiavi da un'istanza del servizio beta](/docs/services/hs-crypto/transition-keys.html) per informazioni sulla migrazione delle chiavi a un'istanza del servizio di produzione.

### Alta disponibilità e ripristino di emergenza
{: #ha-dr-new}
Novità a partire dal 29-03-2019

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, che ora supporta tre zone di disponibilità in una regione selezionata, è un servizio altamente disponibile con funzioni automatiche che aiutano a mantenere le tue applicazioni sicure e operative.

Puoi creare risorse {{site.data.keyword.hscrypto}} nelle [regioni {{site.data.keyword.cloud_notm}}](/docs/services/hs-crypto/regions.html) supportate, che rappresentano l'area geografica in cui vengono gestite ed elaborate le tue richieste {{site.data.keyword.hscrypto}}. Ogni regione {{site.data.keyword.cloud_notm}} contiene [più zone di disponibilità ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) per soddisfare i requisiti di accesso locale, bassa latenza e sicurezza per la regione.

Per ulteriori informazioni, vedi [Alta disponibilità e ripristino di emergenza](/docs/services/hs-crypto/ha-dr.html).

### Scalabilità
{: #scalability-new}
Novità a partire dal 29-03-2019

L'istanza del servizio può essere ridimensionata in modo incrementale fino a un massimo di sei unità di crittografia per soddisfare i tuoi requisiti di prestazioni. Ogni unità di crittografia può crittografare 5000 chiavi. In un ambiente di produzione, ti consigliamo di selezionare almeno due unità di crittografia per abilitare l'elevata disponibilità. Selezionando tre o più unità di crittografia, vengono distribuite insieme a tre zone di disponibilità nella regione selezionata.
  

Per ulteriori informazioni, leggi [Provisioning del servizio](/docs/services/hs-crypto/provision.html).

## Febbraio 2019
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} Beta è disponibile
{: #beta-201902}
Novità a partire dal 05-02-2019

È stata rilasciata la versione Beta di {{site.data.keyword.hscrypto}}. Puoi ora accedere al servizio {{site.data.keyword.hscrypto}} direttamente tramite **Catalogo** > **Sicurezza e identità**.

A partire dal 5 febbraio 2019, non sarà più possibile eseguire il provisioning di nuove istanze sperimentali di Hyper Protect Crypto Services. Le istanze esistenti avranno supporto fino alla fine della data di supporto sperimentale (5 marzo 2019).

## Dicembre 2018
{: #Dec-2018}

### Aggiunto: supporto per la gestione HSM con KYOK
{: #hsm-kyok}
Novità a partire dal 19-12-2018

{{site.data.keyword.hscrypto}} supporta ora la funzione KYOK (Keep Your Own Keys) che ti permette di avere più controllo e autorità sui dati con le chiavi di crittografia che puoi conservare, controllare e gestire. Puoi inizializzare e gestire la tua istanza del servizio con la CLI (command-line interface) {{site.data.keyword.cloud}}.

Per ulteriori informazioni, vedi [Inizializzazione delle istanze del servizio per proteggere l'archiviazione chiavi](/docs/services/hs-crypto/initialize_hsm.html).

### Aggiunto: integrazione dell'API {{site.data.keyword.keymanagementserviceshort}}
{: #kp-api}
Novità a partire dal 19-12-2018

L'API {{site.data.keyword.keymanagementserviceshort}} è ora integrata con Hyper Protect Crypto Services per generare e proteggere le tue chiavi. Puoi richiamare l'API {{site.data.keyword.keymanagementserviceshort}} direttamente tramite {{site.data.keyword.hscrypto}}.

Per ulteriori informazioni, vedi [Accesso all'API](/docs/services/hs-crypto/access-api.html) e [API {{site.data.keyword.hscrypto}} ![Icona link esterno](image/external_link.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto){:new_window}.

### Obsoleto: funzione di accesso a {{site.data.keyword.hscrypto}} tramite ACSP
{: #deprecated-acsp}
Novità a partire dal 19-12-2018

Allo stato attuale, l'accesso a {{site.data.keyword.hscrypto}} tramite un client ACSP (Advanced Cryptography Service Provider) è obsoleto. Se utilizzi un'istanza del servizio precedente, puoi ancora utilizzare ACSP per esplorare {{site.data.keyword.hscrypto}}.
