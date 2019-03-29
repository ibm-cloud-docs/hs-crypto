---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: standard keys, standard encryption key, creating standard keys, create standard keys

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Creazione delle chiavi standard
{: #create-standard-keys}

Puoi creare una chiave di crittografia standard con la GUI {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, o in modo programmatico con l'API {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Creazione delle chiavi standard con la GUI
{: #gui}

[Dopo aver creato un'istanza del servizio](/docs/services/hs-crypto/provision.html), completa la seguente procedura per creare una chiave standard con la GUI {{site.data.keyword.hscrypto}}.

1. [Accedi alla console {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/){: new_window}.
2. Dal tuo dashboard {{site.data.keyword.cloud_notm}}, seleziona l'istanza di {{site.data.keyword.hscrypto}} di cui è stato eseguito il provisioning.
3. Per creare una nuova chiave, fai clic su **Add key** e seleziona la finestra **Generate a new key**.

    Specifica i dettagli della chiave:

    <table>
      <tr>
        <th>Impostazione</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>
          <p>Un alias univoco e leggibile dall'utente per una facile identificazione della tua chiave.</p>
          <p>Per proteggere la tua privacy, assicurati che il nome della chiave non contenga informazioni d'identificazione personale, come il tuo nome o la tua posizione.</p>
        </td>
      </tr>
      <tr></tr>
        <td>Tipo di chiave</td>
        <td>Il <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo di chiave</a> che desideri gestire in {{site.data.keyword.hscrypto}}. Dall'elenco dei tipi di chiave, seleziona <b>Standard key</b>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrive le impostazioni di <b>Generate new key</b></caption>
    </table>

4. Una volta che hai finito di compilare i dettagli della chiave, fai clic su **Generate key** per confermare.

## Creazione delle chiavi standard con l'API
{: #api}

Crea una chiave standard effettuando una chiamata `POST` al seguente endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Richiama le tue credenziali del servizio e di autenticazione per utilizzare le chiavi nel servizio](/docs/services/hs-crypto/access-api.html).

2. Richiama l'[API {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} con il seguente comando cURL.

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
        "resources": [
        {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "extractable": <key_type>
       }
     ]
    }'
    ```
    {: codeblock}

    Per utilizzare le chiavi in un'organizzazione o uno spazio Cloud Foundry specifici nel tuo account, sostituisci `Bluemix-Instance` con le intestazioni `Bluemix-org` e `Bluemix-space` appropriate. [Per ulteriori informazioni, vedi la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
    {: tip}

    Sostituisci le variabili nella richiesta di esempio in base alla seguente tabella.
    <table>
      <tr>
        <th>Variabile</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>L'abbreviazione della regione, come <code>us-south</code> o <code>eu-gb</code>, che rappresenta l'area geografica in cui si trova la tua istanza del servizio {{site.data.keyword.hscrypto}}. Per ulteriori informazioni, vedi <a href="/docs/services/hs-crypto/regions.html#endpoints">Endpoint di servizio regionali</a>.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Il tuo token di accesso {{site.data.keyword.cloud_notm}}. Includi il contenuto completo del token <code>IAM</code>, compreso il valore Bearer, nella richiesta cURL. Per ulteriori informazioni, vedi <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Richiamo di un token di accesso</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>L'identificativo univoco che viene assegnato alla tua istanza del servizio {{site.data.keyword.hscrypto}}. Per ulteriori informazioni, vedi <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Richiamo di un'ID istanza</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>L'identificativo univoco utilizzato per tracciare e correlare le transazioni.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>Facoltativo: un'intestazione che modifica il comportamento del server per le operazioni <code>POST</code> e <code>DELETE</code>.</p><p>Quando imposti la variabile <em>return_preference</em> su <code>return=minimal</code>, il servizio restituisce solo i metadati della chiave, come il valore ID e il nome della chiave, nel corpo-entità della risposta. Quando imposti la variabile su <code>return=representation</code>, il servizio restituisce sia i metadati che il materiale della chiave.</p></td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>Un nome leggibile dall'utente e univoco per una facile identificazione della tua chiave.</p>
          <p>Importante: per proteggere la tua privacy, non memorizzare i tuoi dati personali come metadati per la tua chiave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>Facoltativo: una descrizione estesa della tua chiave.</p>
          <p>Importante: per proteggere la tua privacy, non memorizzare i tuoi dati personali come metadati per la tua chiave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>Facoltativo: la data e l'ora di scadenza della chiave nel sistema, nel formato RFC 3339. Se l'attributo <code>expirationDate</code> viene omesso, la chiave non avrà scadenza. </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>Un valore booleano che determina se il materiale della chiave può lasciare il servizio.</p>
          <p>Quando imposti l'attributo <code>extractable</code> su <code>true</code>, il servizio crea una chiave standard che puoi archiviare nelle tue applicazioni o nei tuoi servizi.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabella 2. Descrive le variabili necessarie per aggiungere una chiave standard con l'API {{site.data.keyword.hscrypto}}</caption>
    </table>

    Per proteggere la riservatezza dei tuoi dati personali, evita di immettere informazioni d'identificazione personale, come il tuo nome o la tua posizione, quando aggiungi le chiavi al servizio. Per ulteriori esempi di informazioni d'identificazione personale, vedi la sezione 2.2 di [NIST Special Publication 800-122 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    Una risposta `POST /v2/keys` corretta restituisce il valore dell'ID per la tua chiave, insieme ad altri metadati. L'ID è un identificativo univoco che viene assegnato alla tua chiave e utilizzato per le seguenti chiamate all'API {{site.data.keyword.hscrypto}}.

3. Facoltativo: verifica che la chiave sia stata creata eseguendo la seguente chiamata per ottenere le chiavi nella tua istanza del servizio {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
      https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### Operazioni successive

- Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, [consulta la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
- Per visualizzare un esempio di come è possibile utilizzare le chiavi archiviate in {{site.data.keyword.hscrypto}} per crittografare e decrittografare i dati, [controlla l'applicazione di esempio in GitHub ![Icona di link esterno](../../icons/launch-glyph.svg "Icona di link esterno")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
