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

# Auf die API zugreifen
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} wird in die {{site.data.keyword.keymanagementserviceshort}}-REST-API integriert, die mit jeder Programmiersprache verwendet werden kann, um Schlüssel zu speichern, abzurufen und zu generieren.
{: shortdesc}

Um mit der API zu arbeiten, müssen Sie eigene Service- und Authentifizierungsnachweise generieren.

## Ein Zugriffstoken abrufen
{: #retrieve-token}

Die Authentifizierung mit {{site.data.keyword.hscrypto}} erfolgt durch das Abrufen eines Zugriffstokens aus {{site.data.keyword.iamshort}}. Sie können mit einer [Service-ID](/docs/iam/serviceid.html#serviceids) mit der {{site.data.keyword.hscrypto}}-API für Ihren Service oder für Ihre Anwendung sowie außerhalb von {{site.data.keyword.cloud_notm}} arbeiten, ohne Ihren persönlichen Benutzerberechtigungsnachweis freizugeben.  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

Führen Sie die folgenden Schritte aus, um ein Zugriffstoken abzurufen:

1. Rufen Sie in der {{site.data.keyword.cloud_notm}}-Konsole die Optionen **Verwalten** &gt; **Sicherheit** &gt; **Identität und Zugriff** &gt; **Service-IDs**. Führen Sie die Schritte zum [Erstellen eines Service](/docs/iam/serviceid.html#creating-a-service-id) aus.
2. Verwenden Sie das Menü **Aktionen**, um [eine Zugriffsrichtlinie für die neue Service-ID zu definieren](/docs/iam/serviceidaccess.html).

    Weitere Informationen zum Verwalten des Zugriffs für Ihre {{site.data.keyword.hscrypto}}-Ressourcen finden Sie in [Rollen und Berechtigungen](/docs/services/hs-crypto/manage-access.html#roles).
3. Verwenden Sie den Abschnitt **API-Schlüssel**, um [einen API-Schlüssel zu erstellen, der der Service-ID zugeordnet wird](/docs/iam/serviceid_keys.html#serviceidapikeys). Speichern Sie Ihren API-Schlüssel, indem Sie ihn an eine sichere Position herunterladen.
4. Rufen Sie die {{site.data.keyword.iamshort}}-API auf, um Ihr Zugriffstoken abzurufen.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    Ersetzen Sie in der Anforderung `<API_KEY>` durch den API-Schlüssel, den Sie in Schritt 3 erstellt haben. Das folgende abgeschnittene Beispiel zeigt die Token-Ausgabe:

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

    Verwenden Sie den vollständigen Wert `access_token` mit dem Präfixtyp _Trägertoken_, um die Schlüssel für Ihren Service programmgesteuert mit der {{site.data.keyword.hscrypto}}-API zu verwalten.

    Zugriffstokens sind für einen Zeitraum von 1 Stunde gültig, können jedoch bei Bedarf neu generiert werden. Aktualisieren Sie das Zugriffstoken für Ihren API-Schlüssel regelmäßig, indem Sie die {{site.data.keyword.iamshort}}-API aufrufen, damit Ihr Zugriff auf den Service erhalten bleibt.   
    {: tip }

## Instanz-ID abrufen
{: #retrieve-instance-ID}

Sie können die Identifikationsinformationen für Ihre {{site.data.keyword.hscrypto}}-Serviceinstanz abrufen, indem Sie die [{{site.data.keyword.cloud_notm}}-CLI](/docs/cli/index.html#overview) verwenden. Verwenden Sie eine Instanz-ID, um Ihre Verschlüsselungsschlüssel in einer bestimmten Instanz von {{site.data.keyword.hscrypto}} in Ihrem Konto zu verwalten.

1. Melden Sie sich über die [{{site.data.keyword.cloud_notm}}-CLI](/docs/cli/index.html#overview) bei {{site.data.keyword.cloud_notm}} an.

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Hinweis:** Wenn die Anmeldung fehlschlägt, führen Sie den Befehl `ibmcloud login --sso` aus, um es erneut zu versuchen. Der Parameter `--sso` ist für die Anmeldung mit einer eingebundenen ID erforderlich. Rufen Sie bei Verwendung dieser Option den in der CLI-Ausgabe aufgeführten Link auf, um einen einmaligen Kenncode zu generieren.

2. Wählen Sie das Konto aus, das Ihre bereitgestellte Instanz enthält.

    Sie können `ibmcloud resource service-instances` ausführen, um alle Serviceinstanzen aufzulisten, die in Ihrem Konto bereitgestellt sind.

3. Rufen Sie den Cloudressourcennamen (CRN) ab, der Ihre {{site.data.keyword.hscrypto}}-Serviceinstanz eindeutig identifiziert.

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    Ersetzen Sie `<instance_name>` mit dem eindeutigen Alias, den Sie Ihrer Instanz von {{site.data.keyword.hscrypto}} zugeordnet haben. Im folgenden gekürzten Beispiel sehen Sie die CLI-Ausgabe. Der Wert _42454b3b-5b06-407b-a4b3-34d9ef323901_ ist eine Beispielinstanz-ID.

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## Verbindungsinformationen abrufen
{: #retrieve-connection-info}

Bevor Sie {{site.data.keyword.keymanagementserviceshort}}-APIs aufrufen, rufen Sie zuerst die API **Verbindungsinformationen abrufen** auf, um die Verbindungsinformationen abzurufen. Weitere Informationen finden Sie in [der {{site.data.keyword.hscrypto}}-API-Referenz ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto){: new_window}. 

## API-Anforderung formulieren
{: #form-api-request}

Wenn Sie einen API-Aufruf für den Service absetzen, strukturieren Sie Ihre API-Anforderung auf dieselbe Weise, wie Sie Ihre ursprüngliche Instanz von {{site.data.keyword.hscrypto}} bereitgestellt haben.

Um Ihre Anforderung zu erstellen, kombinieren Sie einen [regionalen Serviceendpunkt](/docs/services/hs-crypto/regions.html) mit dem entsprechenden Authentifizierungsnachweis. Beispiel: Wenn Sie eine Serviceinstanz für die Region `us-south` erstellen, verwenden Sie den folgenden Endpunkt und diese API-Header, um die Schlüssel in Ihrem Service zu durchsuchen:

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### Weitere Schritte
{: #api-next}

Weitere Informationen zur programmgesteuerten Verwaltung von Schlüsseln [finden Sie in der {{site.data.keyword.hscrypto}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}. -->
