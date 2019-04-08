---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: REST API, RESTful API, access token, instance ID

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Accesso all'API
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} si integra con l'API REST {{site.data.keyword.keymanagementserviceshort}}, che può essere utilizzata con qualsiasi linguaggio di programmazione per archiviare, richiamare e generare chiavi.
{: shortdesc}

Per utilizzare l'API, devi generare le tue credenziali del servizio e di autenticazione.

## Richiamo di un token di accesso
{: #retrieve-token}

Puoi eseguire l'autenticazione con {{site.data.keyword.hscrypto}} richiamando un token di accesso da {{site.data.keyword.iamshort}}. Con un [ID del servizio](/docs/iam/serviceid.html#serviceids), puoi utilizzare l'API {{site.data.keyword.hscrypto}} al posto del tuo servizio o applicazione all'interno o all'esterno di {{site.data.keyword.cloud_notm}}, senza il bisogno di condividere le tue credenziali utente personali.  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

Completa la seguente procedura per richiamare un token di accesso:

1. Nella console {{site.data.keyword.cloud_notm}}, vai a **Manage** &gt; **Security** &gt; **Identity and Access** &gt; **Service IDs**. Segui il processo per [creare un ID del servizio](/docs/iam/serviceid.html#creating-a-service-id).
2. Utilizza il menu **Actions** per [definire una politica di accesso per il tuo nuovo ID servizio](/docs/iam/serviceidaccess.html).

    Per ulteriori informazioni sulla gestione dell'accesso alle tue risorse {{site.data.keyword.hscrypto}}, consulta [Ruoli e autorizzazioni](/docs/services/hs-crypto/manage-access.html#roles).
3. Utilizza la sezione **API keys** per [creare una chiave API da associare all'ID servizio](/docs/iam/serviceid_keys.html#serviceidapikeys). Salva la tua chiave API scaricandola in un luogo sicuro.
4. Richiama l'API {{site.data.keyword.iamshort}} per richiamare il tuo token di accesso.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    Nella richiesta, sostituisci `<API_KEY>` con la chiave API che hai creato nel passo 3. Il seguente esempio troncato mostra l'output del token:

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Utilizza il valore `access_token` completo, preceduto dal tipo di token _Bearer_, per gestire in modo programmatico le chiavi per il tuo servizio utilizzando l'API {{site.data.keyword.hscrypto}}.

    I token di accesso sono validi per 1 ora, ma puoi rigenerarli quando necessario. Per mantenere l'accesso al servizio, aggiorna regolarmente il token di accesso per la tua chiave API richiamando l'API {{site.data.keyword.iamshort}}.   
    {: tip }

## Richiamo del tuo ID dell'istanza
{: #retrieve-instance-ID}

Puoi richiamare le informazioni di identificazione per la tua istanza del servizio {{site.data.keyword.hscrypto}} utilizzando la [CLI {{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview). Utilizza un ID dell'istanza per gestire le tue chiavi di crittografia in un'istanza specificata di {{site.data.keyword.hscrypto}} nel tuo account.

1. Accedi a {{site.data.keyword.cloud_notm}} con la [CLI {{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview).

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Nota:** se l'accesso non riesce, esegui il comando `ibmcloud login --sso` e prova di nuovo. Il parametro `--sso` è obbligatorio quando
accedi con un ID federato. Se viene utilizzata questa opzione, vai al link elencato nell'output della CLI
per generare una passcode monouso.

2. Seleziona l'account che contiene l'istanza di cui è stato eseguito il provisioning.

    Puoi eseguire `ibmcloud resource service-instances` per elencare tutte le istanze del servizio che sono state fornite nel tuo account.

3. Richiama il CRN (Cloud Resource Name) che identifica in modo univoco la tua istanza del servizio {{site.data.keyword.hscrypto}}.

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    Sostituisci `<instance_name>` con l'alias univoco che hai assegnato alla tua istanza di {{site.data.keyword.hscrypto}}. Il seguente esempio troncato mostra l'output della CLI. Il valore _42454b3b-5b06-407b-a4b3-34d9ef323901_ è un ID dell'istanza di esempio.

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## Richiamo delle informazioni sulla connessione
{: #retrieve-connection-info}

Prima di chiamare qualsiasi API {{site.data.keyword.keymanagementserviceshort}}, richiama prima l'API **Retrieve the connection info** per recuperare le informazioni sulla connessione. Per ulteriori informazioni, vedi [la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

## Creazione della tua richiesta API
{: #form-api-request}

Quando effettui una chiamata API al servizio, struttura la tua richiesta API in base a come hai inizialmente eseguito il provisioning della tua istanza di {{site.data.keyword.hscrypto}}.

Per creare la tua richiesta, accoppia un [endpoint del servizio regionale](/docs/services/hs-crypto/regions.html) con le credenziali di autenticazione appropriate. Ad esempio, se hai creato un'istanza del servizio per la regione `us-south`, utilizza il seguente endpoint e le intestazioni API per sfogliare le chiavi nel tuo servizio:

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### Operazioni successive
{: #api-next}

Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, [consulta la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}. -->
