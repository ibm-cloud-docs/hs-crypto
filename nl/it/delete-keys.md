---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: details of the DELETE request, delete encryption key, deleting keys, Variable Description region

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Eliminazione delle chiavi
{: #deleting-keys}

Puoi utilizzare {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} per eliminare una chiave crittografata e il suo contenuto, se sei un amministratore del tuo spazio {{site.data.keyword.cloud_notm}} o dell'istanza del servizio {{site.data.keyword.hscrypto}}.
{: shortdesc}

**Importante:** quando elimini una chiave, distruggi permanentemente il suo contenuto e i dati associati. L'azione è irreversibile. Distruggere le risorse non è consigliato negli ambienti di produzione, ma può essere utile negli ambienti temporanei come test o QA.

## Eliminazione delle chiavi con la GUI
{: #gui}

Se preferisci eliminare le tue chiavi di crittografia con un'interfaccia grafica, puoi utilizzare la GUI {{site.data.keyword.hscrypto}}.

[Dopo aver creato o importato le tue chiavi esistenti nel servizio](/docs/services/hs-crypto/create-root-keys.html), completa la seguente procedura per eliminare una chiave:

1. [Accedi alla console {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/){: new_window}.
2. Dal dashboard {{site.data.keyword.cloud_notm}}, seleziona l'istanza di {{site.data.keyword.hscrypto}} di cui è stato eseguito il provisioning.
3. Utilizza la tabella **Keys** per sfogliare le chiavi nel tuo servizio.
4. Fai clic sull'icona con tre punti per aprire un elenco di opzioni per la chiave che desideri eliminare.
5. Dal menu di opzioni, fai clic su **Delete key** e conferma l'eliminazione della chiave nella schermata successiva.

Dopo aver eliminato una chiave, la chiave passa allo stato _Destroyed_. Le chiavi in questo stato non sono più ripristinabili. I metadati associati alla chiave, come la data di eliminazione della chiave, vengono conservati nel database {{site.data.keyword.hscrypto}}.

## Eliminazione delle chiavi con l'API
{: #api}

Per eliminare una chiave e il suo contenuto, effettua una chiamata `DELETE` al seguente endpoint.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

1. [Richiama le tue credenziali del servizio e di autenticazione per utilizzare le chiavi nel servizio](/docs/services/hs-crypto/access-api.html).

2. Richiama l'ID della chiave che desideri eliminare.

    Puoi richiamare l'ID di una chiave specificata effettuando una richiesta `GET /v2/keys/` o visualizzando le tue chiavi nel dashboard {{site.data.keyword.hscrypto}}.

3. Esegui il seguente comando cURL per eliminare permanentemente la chiave e il suo contenuto.

    ```cURL
    curl -X DELETE \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
    ```
    {: codeblock}

    Per utilizzare le chiavi in un'organizzazione o uno spazio Cloud Foundry nel tuo account, sostituisci `Bluemix-Instance` con le intestazioni `Bluemix-org` e `Bluemix-space` appropriate. [Per ulteriori informazioni, vedi la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
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
        <td><varname>key_ID</varname></td>
        <td>L'identificativo univoco della chiave che desideri eliminare.</td>
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
        <td><varname>return_preference</varname></td>
        <td><p>Un'intestazione che modifica il comportamento del server per le operazioni <code>POST</code> e <code>DELETE</code>.</p><p>Quando imposti la variabile <em>return_preference</em> su <code>return=minimal</code>, il servizio restituisce una risposta di eliminazione positiva. Quando imposti la variabile su <code>return=representation</code>, il servizio restituisce sia i metadati che il materiale della chiave.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrive le variabili necessarie per eliminare le chiavi con l'API {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Se la variabile _return_preference_ è impostata su `return=representation`, i dettagli della richiesta `DELETE` vengono restituiti nel corpo-entità della risposta. Il seguente oggetto JSON mostra un valore restituito di esempio.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
      },
        "resources": [
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    Per una descrizione dettagliata dei parametri disponibili, consulta la [documentazione di riferimento API REST ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} di {{site.data.keyword.hscrypto}}.
