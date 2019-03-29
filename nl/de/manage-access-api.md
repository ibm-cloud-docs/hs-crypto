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

# Zugriff auf Schlüssel verwalten
{: #manage-access-api}

Mit {{site.data.keyword.iamlong}} können Sie eine differenzierte Zugriffssteuerung für Ihre Verschlüsselungsschlüssel ermöglichen, indem Sie Zugriffsrichtlinie erstellen und bearbeiten.
{: shortdesc}

Diese Seite führt Sie durch Szenarios für die Verwaltung des Zugriffs auf Ihre Chiffrierschlüssel mit der [API für die Zugriffsverwaltung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link") ](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window}.

## Vorbereitungen
{: #prereqs}

Für die Arbeit mit der API generieren Sie Ihre Authentifizierungsnachweise, z. B. [Zugriffstoken](/docs/services/hs-crypto/access-api.html#retrieve-token) und [Instanz-ID](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID). Darüber hinaus benötigen Sie die ID des {{site.data.keyword.hscrypto}}-Schlüssels, für den Sie den Zugriff verwalten möchten.

Weitere Informationen zum Anzeigen von Schlüssel-IDs finden Sie unter [Schlüssel anzeigen](/docs/services/hs-crypto/view-keys.html).
{: tip}

### Konto-ID abrufen
{: #retrieve-account-ID}

Nachdem Sie Ihre Berechtigungsnachweise abgerufen haben, bestimmen Sie den Zugriffsbereich für Ihre neue Zugriffsrichtlinie, indem Sie die ID des Kontos abrufen, das Ihre {{site.data.keyword.hscrypto}}-Serviceinstanz enthält.

Zum Abrufen Ihrer Konto-ID führen Sie die folgenden Schritte aus:

1. Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-CLI an.
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **Hinweis:** Der Parameter `--sso` ist erforderlich, wenn Sie sich mit einer eingebundenen ID anmelden. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

    Das Ergebnis zeigt die Identifikationsinformationen für Ihr Konto an.

    ```sh
    Authenticating...
    OK

    Wählen Sie ein Konto aus (oder drücken Sie zum Überspringen die Eingabetaste):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API-Endpunkt:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    Benutzer:           admin
    Konto:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. Kopieren Sie den Wert für Ihre Konto-ID.

    Der Wert _b6hnh3560ehqjkf89s4ba06i367801e_ ist eine Beispiel-Konto-ID.

### Benutzer-ID abrufen
{: #retrieve-user-ID}

Rufen Sie die Benutzer-ID des Benutzers ab, dessen Zugriff geändert werden soll.

Zum Abrufen der Benutzer-ID führen Sie die folgenden Schritte aus:

1. [Bitten Sie den Benutzer, ein IAM-Token anzugeben](/docs/services/hs-crypto/access-api.html#retrieve-token).
    Die Struktur des IAM-Tokens ist wie folgt:

    ```sh
    IAM-Token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Kopieren Sie den mittleren Wert und führen Sie den folgenden Befehl aus:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    Das Ergebnis zeigt ein JSON-Objekt ähnlich dem folgenden Beispiel:
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

4. Kopieren Sie den Wert der Eigenschaft `id`.

## Zugriffsrichtlinie erstellen
{: #create-policy}

Zum Aktivieren der Zugriffssteuerung für einen bestimmten Schlüssel können Sie eine Anforderung an {{site.data.keyword.iamshort}} senden, indem Sie den folgenden Befehl ausführen. Wiederholen Sie den Befehl für jede Zugriffsrichtlinie.

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

Wenn Sie den Zugriff auf Schlüssel innerhalb einer angegebenen Cloud Foundry-Organisation und eines festgelegten Cloud Foundry-Bereichs verwalten müssen, ersetzen Sie `serviceInstance` durch `organizationId` und `spaceId`. Weitere Informationen finden Sie in der [Referenzdokumentation zur API für die Zugriffsverwaltung ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.
{: tip}

Ersetzen Sie `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` und `<key_ID>` durch die entsprechenden Werte.

**Optional:** Überprüfen Sie, ob die Richtlinie erfolgreich erstellt wurde.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Zugriffsrichtlinie aktualisieren
{: #update-policy}

Sie können eine abgerufene Richtlinien-ID verwenden, um eine vorhandene Richtlinie für einen Benutzer zu ändern. Senden Sie dazu eine Anforderung an {{site.data.keyword.iamshort}}, indem Sie den folgenden Befehl ausführen:

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

Ersetzen Sie `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` und `<key_ID>` durch die entsprechenden Werte.

**Optional:** Überprüfen Sie, ob die Richtlinie erfolgreich aktualisiert wurde.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Zugriffsrichtlinie löschen
{: #delete-policy}

Sie können eine abgerufene Richtlinien-ID verwenden, um eine vorhandene Richtlinie für einen Benutzer zu löschen. Senden Sie dazu eine Anforderung an {{site.data.keyword.iamshort}}, indem Sie den folgenden Befehl ausführen:

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Ersetzen Sie `<account_ID>`, `<user_ID>`, `<policy_ID>` und `<Admin_IAM_token>` durch die entsprechenden Werte.

**Optional:** Überprüfen Sie, ob die Richtlinie erfolgreich gelöscht wurde.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
