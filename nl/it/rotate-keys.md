---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root keys, Rotate key, key rotation

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Rotazione delle chiavi
{: #rotating-keys}

Puoi eseguire la rotazione delle tue chiavi root su richiesta utilizzando {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

La rotazione delle chiavi master non è attualmente supportata.
{: important}

Quando esegui la rotazione della tua chiave root, ne abbrevi la durata e limiti la quantità di informazioni da essa protetta.   

Per saperne di più sul modo in cui la rotazione delle chiavi ti aiuta a soddisfare gli standard del settore e le prassi ottimali crittografiche, vedi [Rotazione delle chiavi](/docs/services/key-protect/concepts/key-rotation.html).

La rotazione è disponibile solo per le chiavi root.
{: tip}

## Rotazione delle chiavi root con la GUI
{: #gui}

Se preferisci eseguire la rotazione delle tue chiavi root utilizzando un'interfaccia grafica, puoi utilizzare la GUI {{site.data.keyword.hscrypto}}.

[Dopo aver creato o importato le tue chiavi root esistenti nel servizio](/docs/services/hs-crypto/create-root-keys.html), completa la seguente procedura per eseguire la rotazione di una chiave:

1. [Accedi alla console {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/){: new_window}.
2. Dal tuo dashboard {{site.data.keyword.cloud_notm}}, seleziona l'istanza di {{site.data.keyword.hscrypto}} di cui è stato eseguito il provisioning.
3. Utilizza la tabella **Keys** per sfogliare le chiavi nel tuo servizio.
4. Fai clic sull'icona ⋮ per aprire un elenco di opzioni per la chiave di cui desideri eseguire la rotazione.
5. Dal menu di opzioni, fai clic su **Rotate key** e conferma la rotazione nella schermata successiva.

Se inizialmente hai importato la chiave root, devi fornire un nuovo materiale della chiave con codifica base64 per eseguire la rotazione della chiave. Per ulteriori informazioni, vedi [Importazione delle chiavi root con la GUI](/docs/services/hs-crypto/import-root-keys.html#gui).
{: tip}

## Rotazione delle chiavi root utilizzando l'API
{: #api}

[Dopo aver designato una chiave root nel servizio](/docs/services/hs-crypto/create-root-keys.html), puoi eseguire la rotazione della tua chiave effettuando una chiamata `POST` al seguente endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [Richiama le tue credenziali del servizio e di autenticazione per utilizzare le chiavi nel servizio.](/docs/services/hs-crypto/access-api.html)

2. Copia l'ID della chiave root di cui desideri eseguire la rotazione.

4. Esegui il seguente comando cURL per sostituire la chiave con il nuovo materiale della chiave.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <key_material>'
      }'
    ```
    {: codeblock}

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
        <td><varname>key_ID</varname></td>
        <td>L'identificativo univoco per la chiave root di cui desideri eseguire la rotazione.</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>Il materiale della chiave con codifica base64 che vuoi archiviare e gestire nel servizio. Il valore è obbligatorio se hai inizialmente importato il materiale della chiave quando hai aggiunto la chiave al servizio.</p>
          <p>Per eseguire la rotazione di una chiave che era stata inizialmente generata da {{site.data.keyword.hscrypto}}, ometti l'attributo <code>payload</code> e passa un corpo-entità della richiesta vuoto. Per eseguire la rotazione di una chiave importata, fornisci un materiale della chiave che soddisfa i seguenti requisiti:</p>
          <p>
            <ul>
              <li>La chiave deve essere di 256, 384 o 512 bit.</li>
              <li>I byte di dati, ad esempio 32 byte per 256 bit, devo essere codificati utilizzando la codifica base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrive le variabili necessarie per eseguire la rotazione di una specifica chiave in {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Una richiesta di rotazione eseguita correttamente restituisce una risposta HTTP `204 No Content`, che indica che la tua chiave root è stata sostituita da nuovo materiale della chiave.

4. Facoltativo: verifica che sia stata eseguita la rotazione della chiave eseguendo la seguente chiamata per sfogliare le chiavi nella tua istanza del servizio {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    Riesamina il valore `lastRotateDate` nel corpo-entità della risposta per ispezionare la data e l'ora dell'ultima rotazione della tua chiave.
