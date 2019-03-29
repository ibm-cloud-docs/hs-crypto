---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-21"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Domande frequenti (FAQ)
{: #faqs}

Puoi utilizzare le seguenti FAQ con {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.

## Certificazioni HSM
{: #HSM}

### Come posso verificare che una scheda di crittografia IBM (HSM) sia stata convalidata per soddisfare FIPS 140-2 Level 4?

FIPS 140-2 Level 4 è un livello di protezione molto elevato non ampiamente disponibile sul mercato. IBM è il principale fornitore di HSM certificati di altissimo livello e ha investito molto per mantenere questa convalida per ogni nuova generazione di schede. Il requisito per l'alto livello di garanzia è stato raccolto dai requisiti del governo. Per la convalida della certificazione, vieni indirizzato alla home page NIST perché la certificazione è stata pubblicata lì. 

### Qual è la differenza tra FIPS 140-2 Level 2, 3 e 4?

* FIPS 140-2 Level 2: requisiti per le prove di manomissione eseguite da sigilli, serrature resistenti agli urti su coperchi e porte rimovibili. I rivestimenti o i sigilli a prova di manomissione sono collocati su un modulo di crittografia in modo che il rivestimento o il sigillo debbano essere rotti per ottenere l'accesso fisico alle chiavi di crittografia e ai parametri di sicurezza critici (CSP) in testo normale all'interno del modulo. Il livello di sicurezza 2 richiede, come minimo, un'autenticazione basata sui ruoli in cui un modulo di crittografia autentica l'autorizzazione di un operatore per assumere un ruolo specifico ed eseguire una serie di servizi corrispondenti.
 
* FIPS 140-2 Level 3: i meccanismi di sicurezza fisica richiesti al livello di sicurezza 3 sono destinati ad avere un'alta probabilità di rilevare e rispondere ai tentativi di accesso fisico, uso o modifica del modulo di crittografia. Il livello di sicurezza 3 richiede meccanismi di autenticazione basati sull'identità, migliorando la sicurezza fornita dai meccanismi di autenticazione basati sui ruoli specificati per il livello di sicurezza 2.  

* FIPS 140-2 Level 4: a questo livello di sicurezza, i meccanismi di sicurezza fisica forniscono una protezione completa attorno al modulo di crittografia con l'intento di rilevare e rispondere a tutti i tentativi non autorizzati di accesso fisico. La penetrazione della recinzione del modulo di crittografia da qualsiasi direzione ha una probabilità molto elevata di essere rilevata, con conseguente azzeramento immediato di tutti i CSP (parametri di sicurezza critici) in testo normale. I moduli di crittografia con livello di sicurezza 4 sono utili per il funzionamento in ambienti fisicamente non protetti. Il livello di sicurezza 4 protegge inoltre un modulo di crittografia da un compromesso alla sicurezza dovuto a condizioni ambientali o fluttuazioni al di fuori dei normali intervalli operativi del modulo per la tensione e la temperatura. Le escursioni intenzionali oltre i normali intervalli operativi possono essere utilizzate da un utente malintenzionato per contrastare le difese di un modulo di crittografia.   

## Gestione delle chiavi

### È possibile utilizzare {{site.data.keyword.hscrypto}} in combinazione con il servizio {{site.data.keyword.keymanagementserviceshort}}?

 {{site.data.keyword.hscrypto}} è un servizio di crittografia gestito fornito con un'API {{site.data.keyword.keymanagementserviceshort}} completamente compatibile, che ha un'esperienza utente identica a quella di Key Protect. La principale differenza è che {{site.data.keyword.hscrypto}} si basa su un HSM che è stato certificato da FIPS 140-2 Level 4. Inoltre, fornisce il pieno controllo con la chiave master HSM gestita dal cliente (KYOK). Il servizio è dedicato per istanza rispetto alla configurazione a più tenant per {{site.data.keyword.keymanagementserviceshort}}. {{site.data.keyword.hscrypto}} offre anche funzionalità HSM per operazioni di crittografia come firma/verifica, generazione chiavi, hashing crittografico, crittografia/decrittografia e impacchettamento/spacchettamento. 

### Che lunghezza può avere un nome chiave?
{: #key_names}

Puoi utilizzare un nome chiave con una lunghezza massima di 50 caratteri.

### Posso utilizzare i caratteri della lingua come parte del nome della chiave?
{: #key_chars}

I caratteri della lingua, come i caratteri cinesi, non possono essere utilizzati come parte del nome della chiave.

### Cosa succede quando elimino una chiave?
{: #key_destruction}

Quando elimini una chiave, distruggi permanentemente il suo contenuto e i dati associati. I dati che sono stati crittografati con la chiave non saranno più accessibili.

Prima di eliminare una chiave, assicurati di non richiedere più l'accesso ai dati associati alla chiave.
