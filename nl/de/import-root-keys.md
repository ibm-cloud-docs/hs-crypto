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

# Rootschlüssel importieren
{: #import-root-keys}

Sie können mit {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} Rootschlüssel mithilfe der {{site.data.keyword.hscrypto}}-GUI oder programmgesteuert mit der {{site.data.keyword.hscrypto}}-API schützen.
{: shortdesc}

Rootschlüssel sind symmetrische Key-Wrapping-Schlüssel, die die Sicherheit verschlüsselter Daten in der Cloud gewährleisten. Weitere Informationen zu Rootschlüsseln finden Sie in [Envelope-Verschlüsselung](/docs/services/key-protect/concepts/envelope-encryption.html).

## Rootschlüssel mit der GUI importieren
{: #import-root-key-gui}

[Nach dem Erstellen einer Instanz des Service](/docs/services/hs-crypto/provision.html) führen Sie die folgenden Schritte aus, um einen vorhandenen Rootschlüssel mit der {{site.data.keyword.hscrypto}}-GUI hinzuzufügen.

1. [Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/){: new_window} an.
2. Rufen Sie **Menü** &gt; **Ressourcenliste** auf, um eine Liste Ihrer Ressourcen anzuzeigen. 
3. Wählen Sie in Ihrer {{site.data.keyword.cloud_notm}}-Ressourcenliste die bereitgestellte Instanz von {{site.data.keyword.hscrypto}} aus. 
4. Zum Importieren eines Schlüssels klicken Sie auf **Schlüssel hinzufügen** und wählen Sie das Fenster **Eigenen Schlüssel importieren** aus. 

    Geben Sie die Schlüsseldetails an:

    <table>
      <tr>
        <th>Einstellung</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>
          <p>Ein eindeutiger, lesbarer Alias zur einfachen Identifikation Ihres Schlüssels.</p>
          <p>Stellen Sie aus Datenschutzgründen sicher, dass der Schlüsselname keine personenbezogenen Daten (PII) wie den Namen oder den Standort enthält.</p>
        </td>
      </tr>
      <tr>
        <td>Schlüsseltyp</td>
        <td>Der <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Schlüsseltyp</a>, den Sie in {{site.data.keyword.hscrypto}} verwalten möchten. Wählen Sie aus der Liste der Schlüsseltypen <b>Rootschlüssel</b> aus.</td>
      </tr>
      <tr>
        <td>Schlüsselinformationen</td>
        <td>
          <p>Die base64-codierten Schlüsselinformationen (z. B. der vorhandene Key-Wrapping-Schlüssel), den Sie im Service speichern und verwalten möchten.</p>
          <p>Stellen Sie sicher, dass die Schlüsselinformationen die folgenden Anforderungen erfüllen:</p>
          <p>
            <ul>
              <li>Der Schlüssel muss 128, 192 oder 256 Bit groß sein. </li>
              <li>Die Byte der Daten (z. B. 32 Byte oder 256 Bit) müssen mit der base64-Codierung verschlüsselt werden.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Einstellungen für <b>Vorhandenen Schlüssel eingeben</b></caption>
    </table>

5. Geben Sie die Details zum Schlüssel ein und klicken Sie anschließend zum Bestätigen auf **Schlüssel importieren**.

## Rootschlüssel mit der API importieren
{: #import-root-key-api}

Fügen Sie Ihren vorhandenen Rootschlüssel hinzu, indem Sie einen `POST`-Aufruf zum folgenden Endpunkt absetzen.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/hs-crypto/access-api.html)

1. Rufen Sie die [{{site.data.keyword.hscrypto}}-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto){: new_window} mit dem folgenden cURL-Befehl auf.

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

    Ersetzen Sie die Variablen in der Beispielanforderung anhand der Angaben in der folgenden Tabelle.
    <table>
      <tr>
        <th>Variable</th>
        <th>Beschreibung</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>Die Regionsabkürzung, z. B. <code>us-south</code> oder <code>eu-gb</code>, die den geografischen Bereich darstellt, in dem sich Ihre {{site.data.keyword.hscrypto}}-Serviceinstanz befindet. Weitere Informationen finden Sie in <a href="/docs/services/hs-crypto/regions.html#endpoints">Regionale Serviceendpunkte</a>.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Ihr {{site.data.keyword.cloud_notm}}-Zugriffstoken. Nehmen Sie den vollständigen Inhalt des <code>IAM</code>-Tokens einschließlich des Werts für Bearer in die cURL-Anforderung auf. Weitere Informationen finden Sie in <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Zugriffstoken abrufen</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>Die eindeutige ID, die Ihrer {{site.data.keyword.hscrypto}}-Serviceinstanz zugewiesen ist. Weitere Informationen finden Sie in <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Instanz-ID abrufen</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>Die eindeutige ID, die zum Überwachen und Korrelieren von Transaktionen verwendet wird.</td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>Ein eindeutiger, lesbarer Name zur einfachen Identifikation Ihres Schlüssels.</p>
          <p>Wichtig: Aus Datenschutzgründen dürfen keine personenbezogenen Daten als Metadaten für den Schlüssel gespeichert werden.</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>Optional: Eine erweiterte Beschreibung des Schlüssels.</p>
          <p>Wichtig: Aus Datenschutzgründen dürfen keine personenbezogenen Daten als Metadaten für den Schlüssel gespeichert werden.</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>Optional: Der Zeitpunkt (Datum und Uhrzeit), zu dem der Schlüssel im System abläuft, im RFC-3339-Format. Wenn das Attribut <code>expirationDate</code> fehlt, bleibt der Schlüssel unbegrenzt gültig.</td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>Die base64-codierten Schlüsselinformationen (z. B. der vorhandene Key-Wrapping-Schlüssel), den Sie im Service speichern und verwalten möchten.</p>
          <p>Stellen Sie sicher, dass die Schlüsselinformationen die folgenden Anforderungen erfüllen:</p>
          <p>
            <ul>
              <li>Der Schlüssel muss 128, 192 oder 256 Bit groß sein. </li>
              <li>Die Byte der Daten (z. B. 32 Byte oder 256 Bit) müssen mit der base64-Codierung verschlüsselt werden.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>Ein boolescher Wert, der bestimmt, ob die Schlüsselinformationen den Service verlassen dürfen.</p>
          <p>Wenn das Attribut <code>extractable</code> auf <code>false</code> festgelegt wird, bezeichnet der Service einen Rootschlüssel, der für die Operationen <code>wrap</code> oder <code>unwrap</code> verwendet werden kann.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Variablen, die zum Hinzufügen eines Rootschlüssels mit der {{site.data.keyword.hscrypto}}-API erforderlich sind.</caption>
    </table>

    Vermeiden Sie zum Schutz der Vertraulichkeit Ihrer persönlichen Daten die Eingabe von personenbezogenen Informationen (PII) beim Hinzufügen von Schlüsseln zum Service. Hierzu gehören beispielsweise Namen oder Standortangaben. Weitere Beispiele für personenbezogene Daten finden Sie in Abschnitt 2.2 des Dokuments [NIST Special Publication 800-122 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    Mit der erfolgreichen Antwort `POST /v2/keys` werden der ID-Wert für Ihren Schlüssel sowie andere Metadaten zurückgegeben. Die ID ist eine eindeutige Kennung, die Ihrem Schlüssel zugeordnet ist und die für alle nachfolgenden Aufrufe für die {{site.data.keyword.hscrypto}}-API verwendet wird.

2. Optional: Stellen Sie sicher, dass der Schlüssel hinzugefügt wurde, indem Sie den folgenden Aufruf ausführen, um die Schlüssel in Ihrer {{site.data.keyword.hscrypto}}-Serviceinstanz zu durchsuchen.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**Hinweis:** Wenn Sie einem Service einen Rootschlüssel hinzufügen, ist der Schlüssel an {{site.data.keyword.hscrypto}} gebunden und seine Schlüsselinformationen können nicht abgerufen werden.

### Weitere Schritte
{: #import-root-key-next}

- Weitere Informationen zum Schutz von Schlüsseln mit der Envelope-Verschlüsselung finden Sie in [Schlüssel einschließen](/docs/services/hs-crypto/wrap-keys.html).
- Weitere Informationen zur programmgesteuerten Verwaltung von Schlüsseln [finden Sie in der {{site.data.keyword.hscrypto}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
