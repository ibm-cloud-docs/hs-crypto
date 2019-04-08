---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root key, data encryption key, Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Impacchettamento delle chiavi
{: #wrap-keys}

Puoi gestire e proteggere le tue chiavi di crittografia con una chiave root utilizzando l'API {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, se sei un utente privilegiato.
{: shortdesc}

Quando impacchetti una chiave di crittografia dei dati (o DEK, data encryption key) con una chiave root, {{site.data.keyword.hscrypto}} combina la forza di più algoritmi per proteggere la riservatezza e l'integrità dei tuoi dati crittografati.  

Per ulteriori informazioni su come l'impacchettamento ti aiuta a controllare la sicurezza dei dati inattivi nel cloud, consulta [Crittografia envelope](/docs/services/key-protect/concepts/envelope-encryption.html).

## Impacchettamento delle chiavi utilizzando l'API
{: #wrap-keys-api}

Puoi proteggere una chiave di crittografia dei dati (o DEK, data encryption key) specificata con una chiave root che gestisci in {{site.data.keyword.hscrypto}}.

Quando fornisci una chiave root per l'impacchettamento, assicurati che la chiave root sia di 128, 192 o 256 bit in modo che la chiamata di impacchettamento possa avere esito positivo. Se crei una chiave root nel servizio, {{site.data.keyword.hscrypto}} genera una chiave di 256-bit dai suoi HSM, supportata dall'algoritmo AES-CBC.


[Dopo aver designato una chiave root nel servizio](/docs/services/hs-crypto/create-root-keys.html), puoi impacchettare una DEK con la crittografia avanzata effettuando una chiamata `POST` al seguente endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [Richiama le tue credenziali del servizio e di autenticazione per utilizzare le chiavi nel servizio.](/docs/services/hs-crypto/access-api.html)

2. Copia il materiale della chiave della DEK che vuoi gestire e proteggere.

    Se disponi dei privilegi da scrittore o gestore per la tua istanza del servizio {{site.data.keyword.hscrypto}}, [puoi richiamare il materiale della chiave per una chiave specifica effettuando una richiesta `GET /v2/keys/<key_ID>`](/docs/services/hs-crypto/view-keys.html#api).

3. Copia l'ID della chiave root che vuoi utilizzare per l'impacchettamento.

4. Esegui il seguente comando cURL per proteggere la chiave con un'operazione di impacchettamento.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
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
        <td><varname>key_ID</varname></td>
        <td>L'identificativo univoco della chiave root che vuoi utilizzare per l'impacchettamento.</td>
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
        <td>Facoltativo: l'identificativo univoco utilizzato per tracciare e correlare le transazioni.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>Un'intestazione che modifica il comportamento del server per le operazioni <code>POST</code> e <code>DELETE</code>.</p><p>Quando imposti la variabile <em>return_preference</em> su <code>return=minimal</code>, il servizio restituisce solo i metadati della chiave, come il valore ID e il nome della chiave, nel corpo-entità della risposta. Quando imposti la variabile su <code>return=representation</code>, il servizio restituisce sia i metadati che il materiale della chiave.</p></td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td>Facoltativo: il materiale della chiave della DEK che vuoi gestire e proteggere. Il valore <code>plaintext</code> deve essere codificato con base64. Per generare una nuova DEK, ometti l'attributo <code>plaintext</code>. Il servizio genera un testo non crittografato casuale (32 byte) e impacchetta il valore.</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>Facoltativo: gli ulteriori dati di autenticazione (AAD) che vengono utilizzati per proteggere ulteriormente la chiave. Ogni stringa può contenere fino a 255 caratteri. Se fornisci AAD quando effettui una chiamata di impacchettamento, devi specificare lo stesso AAD durante la seguente chiamata di spacchettamento.<br></br>Importante: il servizio {{site.data.keyword.hscrypto}} non salva i dati di autenticazione aggiuntivi. Se fornisci un AAD, salva i dati in un luogo sicuro per assicurarti di poter accedere e fornire lo stesso AAD durante le seguenti richieste di spacchettamento.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrive le variabili necessarie per impacchettare una chiave specificata in {{site.data.keyword.hscrypto}}.</caption>
    </table>

    La tua chiave impacchettata, contenente il materiale codificato con base64, viene restituita nel corpo-entità della risposta. Il seguente oggetto JSON mostra un valore restituito di esempio.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
