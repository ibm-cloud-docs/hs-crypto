---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# Risoluzione dei problemi
{: #troubleshooting}

I problemi generali con l'utilizzo di {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} potrebbero includere il fornire intestazioni o credenziali corrette quando interagisci con l'API. In molti casi, puoi risolvere questi problemi seguendo pochi semplici passi.
{: shortdesc}

## Si è verificato un errore durante l'eliminazione di un'istanza {{site.data.keyword.hscrypto}} inizializzata

Potresti ricevere un errore simile al seguente quando elimini un'istanza {{site.data.keyword.hscrypto}} inizializzata:

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

Non hai cancellato (azzerato) l'istanza {{site.data.keyword.hscrypto}} inizializzata prima di eliminarla.
{: tsCauses}

Immetti il seguente comando prima di eliminare l'istanza:
{: tsResolve}

```
ibmcloud tke domain-zeroize
```
{: codeblock}

## Token non autorizzato dopo l'esecuzione dei comandi relativi al plug-in Trusted Key Entry

Potresti ricevere messaggi simili ai seguenti dopo aver eseguito i comandi della CLI `tke`:

```
ibmcloud tke domains
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

Il token non viene aggiornato.
{: tsCauses}

Accedi di nuovo a {{site.data.keyword.cloud_notm}} con il comando `ibmcloud login` per aggiornare il token.
{: tsResolve}

## Ricevi `error CKR_IBM_WK_NOT_INITIALIZED` quando utilizzi la CLI o l'API

Quando utilizzi la CLI o l'API, potresti ricevere un messaggio di errore simile al seguente:

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

Quando hai eseguito il comando `ibmcloud tke domain-compare`, non hai ricevuto una conferma `Valid` sul REGISTRO CHIAVE MASTER CORRENTE.
{: tsCauses}

Assicurati che la chiave master HSM sia stata impostata correttamente.
{: tsResolve}

## Impossibile creare o eliminare chiavi
{: #unable-to-create-keys}

Quando accedi all'interfaccia utente {{site.data.keyword.hscrypto}}, non vedi le opzioni per aggiungere o eliminare le chiavi.

Dal dashboard {{site.data.keyword.cloud_notm}}, seleziona la tua istanza del servizio {{site.data.keyword.hscrypto}}.
{: tsSymptoms}

Puoi vedere un elenco di chiavi, ma non vedi le opzioni per aggiungere o eliminare le chiavi.

Non hai l'autorizzazione corretta per eseguire le azioni di {{site.data.keyword.hscrypto}}.
{: tsCauses}

Verifica con il tuo amministratore che ti sia stato assegnato il ruolo corretto nel gruppo di risorse o nell'istanza del servizio applicabile. Per ulteriori informazioni sui ruoli, vedi [Ruoli e autorizzazioni](/docs/services/key-protect/manage-access.html#roles).
{: tsResolve}

## Come ottenere aiuto e supporto
{: #getting-help}

Se hai dei problemi o delle domande quando utilizzi {{site.data.keyword.hscrypto}}, puoi controllare in {{site.data.keyword.cloud_notm}} oppure ottenere aiuto cercando informazioni o facendo domande attraverso un forum. Puoi inoltre aprire un ticket di supporto.
{: shortdesc}

Puoi controllare se {{site.data.keyword.cloud_notm}} è disponibile andando alla [pagina sugli stati ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/status?tags=platform,runtimes,services).

Puoi rivedere i forum per controllare se altri utenti hanno riscontrato lo stesso problema. Quando stai utilizzando i forum per fare una domanda, contrassegna con una tag la tua domanda in modo che sia visualizzabile dai team di sviluppo
{{site.data.keyword.cloud_notm}}.

- Se hai domande tecniche su {{site.data.keyword.hscrypto}}, inserisci la tua domanda in [Stack Overflow ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://stackoverflow.com/){: new_window} e contrassegnala con le tag  "ibm-cloud" e "hyperprotect-crypto".
- Per domande sul servizio e sulle istruzioni introduttive, utilizza il forum [IBM developerWorks dW Answers ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://developer.ibm.com/answers/index.html){: new_window}. Includi le tag "ibm-cloud" e "hyperprotect-crypto".

Per ulteriori dettagli sull'utilizzo dei forum, consulta il documento relativo a [come ottenere assistenza ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://cloud.ibm.com/docs/support/index.html#getting-help){: new_window}.

Per ulteriori informazioni sull'apertura di un ticket di supporto {{site.data.keyword.IBM_notm}} o sui livelli di supporto e sulla gravità dei ticket, vedi [Come contattare il supporto ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/docs/support/index.html#contacting-support){: new_window}.
