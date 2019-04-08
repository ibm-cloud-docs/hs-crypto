---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: instance ID, account ID, Access Management

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestione dell'accesso alle chiavi
{: #manage-access-api}

Con {{site.data.keyword.iamlong}}, puoi abilitare il controllo dell'accesso granulare per le tue chiavi di crittografia creando e modificando le politiche di accesso.
{: shortdesc}

Questa pagina ti guida attraverso gli scenari per la gestione dell'accesso alle tue chiavi di crittografia con [Access Management API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window}.

## Prima di cominciare
{: #prereqs-manage-api}

Per lavorare con l'API, genera le tue credenziali di autenticazione, come il [token di accesso](/docs/services/hs-crypto/access-api.html#retrieve-token) e l'[ID istanza](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID). Ti serve anche l'ID della chiave {{site.data.keyword.hscrypto}} per cui vuoi gestire l'accesso.

Per informazioni sulla visualizzazione degli ID chiave, vedi [Visualizzazione delle chiavi](/docs/services/hs-crypto/view-keys.html).
{: tip}

### Richiamo del tuo ID account
{: #retrieve-account-ID}

Dopo aver richiamato le tue credenziali, determina l'ambito di accesso per la tua nuova politica di accesso richiamando l'ID dell'account che contiene la tua istanza {{site.data.keyword.hscrypto}} (istanza del servizio in breve).

Per richiamare il tuo ID account, completa la seguente procedura:

1. Accedi alla CLI {{site.data.keyword.cloud_notm}}.
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **Nota**: il parametro `--sso` è obbligatorio quando accedi con un ID federato. Se viene utilizzata questa opzione, vai al link elencato nell'output della CLI
per generare una passcode monouso.

    Il risultato visualizza le informazioni di identificazione del tuo account.

    ```sh
    Authenticating...
    OK

    Seleziona un account (o premi Invio per ignorare):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Immetti un numero> 1
    Account di destinazione sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    Endpoint API:   https://api.ng.bluemix.net (API version: 2.75.0)
    Regione:         us-south
    Utente:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. Copia il valore per il tuo ID account.

    Il valore _b6hnh3560ehqjkf89s4ba06i367801e_ è un ID account di esempio.

### Richiamo dell'ID utente
{: #retrieve-user-ID}

Richiama l'ID dell'utente per cui desideri modificare l'accesso.

Per richiamare l'ID utente, completa la seguente procedura:

1. [Chiedi all'utente di fornire un token IAM](/docs/services/hs-crypto/access-api.html#retrieve-token).
    La struttura del token IAM è la seguente:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copia il valore intermedio e immetti il seguente comando:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    Il risultato mostra un oggetto JSON simile al seguente esempio:
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copia il valore della proprietà `id`.

## Creazione di una politica di accesso
{: #create-policy}

Per abilitare il controllo dell'accesso per una chiave specifica, puoi inviare una richiesta a {{site.data.keyword.iamshort}} immettendo il seguente comando. Ripeti il comando per ogni politica di accesso.

```cURL
curl -X POST \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

<!-- If you need to manage access to keys within a specified Cloud Foundry org and space, replace `serviceInstance` with `organizationId` and `spaceId`. To learn more, see the [Access Management API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.
{: tip}

Replace `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>`, and `<key_ID>` with the appropriate values. -->

**Facoltativo:** verifica che la politica sia stata creata correttamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Aggiornamento di una politica di accesso
{: #update-policy}

Puoi utilizzare un ID politica richiamato per modificare una politica esistente di un utente. Invia una richiesta a {{site.data.keyword.iamshort}} immettendo il seguente comando:

```cURL
curl -X PUT \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

Sostituisci `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` e `<key_ID>` con i valori appropriati.

**Facoltativo:** verifica che la politica sia stata aggiornata correttamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Eliminazione di una politica di accesso
{: #delete-policy}

Puoi utilizzare un ID politica richiamato per eliminare una politica esistente di un utente. Invia una richiesta a {{site.data.keyword.iamshort}} immettendo il seguente comando:

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Sostituisci `<account_ID>`, `<user_ID>`, `<policy_ID>` e `<Admin_IAM_token>` con i valori appropriati.

**Facoltativo:** verifica che la politica sia stata eliminata correttamente.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
