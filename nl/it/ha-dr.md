---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: disaster recovery, High availability, HA, DR

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Alta disponibilità e ripristino di emergenza
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} è un servizio regionale altamente disponibile con funzionalità automatiche che aiutano a mantenere le tue applicazioni sicure e operative.
{: shortdesc}

Utilizza questa pagina per ulteriori informazioni sulla disponibilità e sulle strategie di ripristino di emergenza di {{site.data.keyword.hscrypto}}.

## Ubicazioni, locazione e disponibilità
{: #availability}

<!-- {{site.data.keyword.hscrypto}} is a multi-tenant, regional service. -->

Puoi creare risorse {{site.data.keyword.hscrypto}} in una delle [regioni {{site.data.keyword.cloud_notm}}](/docs/services/hs-crypto/regions.html) supportate, che rappresentano l'area geografica in cui vengono gestite ed elaborate le tue richieste {{site.data.keyword.hscrypto}}. Ogni regione {{site.data.keyword.cloud_notm}} contiene [più zone di disponibilità ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/) per soddisfare i requisiti di accesso locale, bassa latenza e sicurezza per la regione.

Mentre pianifichi la tua strategia di crittografia dei dati inattivi con {{site.data.keyword.cloud_notm}}, tieni presente che il provisioning di {{site.data.keyword.hscrypto}} in una regione più vicina a te ha maggiori probabilità di generare connessioni più veloci e affidabili quando interagisci con le API {{site.data.keyword.hscrypto}}. Scegli una regione specifica se gli utenti, le applicazioni o i servizi che dipendono da una risorsa {{site.data.keyword.hscrypto}} sono geograficamente concentrati. Ricorda che utenti e servizi lontani dalla regione potrebbero riscontrare una maggiore latenza.

Le tue chiavi di crittografia sono confinate nella regione in cui le hai create. {{site.data.keyword.hscrypto}} non copia o esporta le chiavi di crittografia in altre regioni.
{: note}

## Ripristino di emergenza
{: #disaster-recovery}

{{site.data.keyword.hscrypto}} dispone di un ripristino di emergenza regionale con un obiettivo del tempo di risposta (RTO) di un'ora. Il servizio segue i requisiti di {{site.data.keyword.cloud_notm}} per la pianificazione e il ripristino in seguito a eventi di emergenza. Per ulteriori informazioni, vedi [Ripristino di emergenza](/docs/overview/zero_downtime.html#disaster-recovery).
