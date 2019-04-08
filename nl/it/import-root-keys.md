---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root keys, import keys, symmetric key, Hyper Protect Crypto Services GUI

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Importazione delle chiavi root
{: #import-root-keys}

Puoi utilizzare {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} per proteggere le chiavi root utilizzando la GUI {{site.data.keyword.hscrypto}}, o in modo programmatico con l'API {{site.data.keyword.hscrypto}}.
{: shortdesc}

Le chiavi root sono chiavi simmetriche per l'impacchettamento della chiave che vengono utilizzate per proteggere la sicurezza dei dati crittografati nel cloud. Per ulteriori informazioni sulle chiavi root, consulta [Crittografia envelope](/docs/services/key-protect/concepts/envelope-encryption.html).

## Importazione delle chiavi root con la GUI
{: #import-root-key-gui}

[Dopo aver creato un'istanza del servizio](/docs/services/
hs-crypto/provision.html), completa la seguente procedura per aggiungere la tua chiave root esistente con la GUI {{site.data.keyword.hscrypto}}.

1. [Accedi alla console {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/){: new_window}.
2. Vai a **Menu** &gt; **Elenco risorse** per visualizzare un elenco delle tue risorse.
3. Dal tuo elenco risorse {{site.data.keyword.cloud_notm}}, seleziona la tua istanza di cui è stato eseguito il provisioning di {{site.data.keyword.hscrypto}}.
4. Per importare una chiave, fai clic su **Aggiungi chiave** e seleziona la finestra **Import your own key**.

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
      <tr>
        <td>Tipo di chiave</td>
        <td>Il <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo di chiave</a> che desideri gestire in {{site.data.keyword.hscrypto}}. Dall'elenco dei tipi di chiave, seleziona <b>Root key</b>.</td>
      </tr>
      <tr>
        <td>Materiale della chiave</td>
        <td>
          <p>Il materiale della chiave codificato con base64, come ad esempio una chiave di impacchettamento della chiave esistente, che desideri archiviare e gestire nel servizio.</p>
          <p>Assicurati che il materiale della chiave soddisfi i seguenti requisiti:</p>
          <p>
            <ul>
              <li>La chiave deve essere di 128, 192 o 256 bit.</li>
              <li>I byte di dati, ad esempio 32 byte per 256 bit, devo essere codificati utilizzando la codifica base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrive le impostazioni di <b>Enter existing key</b></caption>
    </table>

5. Una volta che hai finito di compilare i dettagli della chiave, fai clic su **Import key** per confermare.

## Importazione delle chiavi root con l'API
{: #import-root-key-api}

Aggiungi la tua chiave root esistente effettuando una chiamata `POST` al seguente endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Richiama le tue credenziali del servizio e di autenticazione per utilizzare le chiavi nel servizio](/docs/services/hs-crypto/access-api.html).

1. Richiama l'[API {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto){: new_window} con il seguente comando cURL.

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
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
       "payload": "<key_material>",
       "extractable": <key_type>
       }
     ]
    }'
    ```
    {: codeblock}
    <!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
        {: tip} -->

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
        <td>Facoltativo: la data e l'ora di scadenza della chiave nel sistema, nel formato RFC 3339. Se l'attributo <code>expirationDate</code> viene omesso, la chiave non avrà scadenza.</td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>Il materiale della chiave codificato con base64, come ad esempio una chiave di impacchettamento della chiave esistente, che desideri archiviare e gestire nel servizio.</p>
          <p>Assicurati che il materiale della chiave soddisfi i seguenti requisiti:</p>
          <p>
            <ul>
              <li>La chiave deve essere di 128, 192 o 256 bit.</li>
              <li>I byte di dati, ad esempio 32 byte per 256 bit, devo essere codificati utilizzando la codifica base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>Un valore booleano che determina se il materiale della chiave può lasciare il servizio.</p>
          <p>Quando imposti l'attributo <code>extractable</code> su <code>false</code>, il servizio designa una chiave root che puoi utilizzare per le operazioni <code>wrap</code> o <code>unwrap</code>.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabella 1. Descrive le variabili necessarie per aggiungere una chiave root con l'API {{site.data.keyword.hscrypto}}</caption>
    </table>

    Per proteggere la riservatezza dei tuoi dati personali, evita di immettere informazioni d'identificazione personale, come il tuo nome o la tua posizione, quando aggiungi le chiavi al servizio. Per ulteriori esempi di informazioni d'identificazione personale, vedi la sezione 2.2 di [NIST Special Publication 800-122 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    Una risposta `POST /v2/keys` corretta restituisce il valore dell'ID per la tua chiave, insieme ad altri metadati. L'ID è un identificativo univoco che viene assegnato alla tua chiave e utilizzato per le seguenti chiamate all'API {{site.data.keyword.hscrypto}}.

2. Facoltativo: verifica che la chiave sia stata aggiunta eseguendo la seguente chiamata per sfogliare le chiavi nella tua istanza del servizio {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**Nota:** dopo aver aggiunto una chiave root esistente al servizio, la chiave rimane nei limiti di {{site.data.keyword.hscrypto}} e il materiale della chiave non può essere richiamato.

### Operazioni successive
{: #import-root-key-next}

- Per ulteriori informazioni sulla protezione delle chiavi con la crittografia envelope, controlla [Impacchettamento delle chiavi](/docs/services/hs-crypto/wrap-keys.html).
- Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, [consulta la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
