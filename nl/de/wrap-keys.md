---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root key, data encryption key, Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Wrapping für Schlüssel durchführen
{: #wrap-keys}

Sie als privilegierter Benutzer können Ihre Verschlüsselungsschlüssel mit dem Rootschlüssel mithilfe der {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}-API verwalten und schützen.
{: shortdesc}

Wenn Sie für einen Datenverschlüsselungsschlüssel (DEK) Wrapping anhand eines Rootschlüssels durchführen, kombiniert {{site.data.keyword.hscrypto}} die Stärke mehrerer Algorithmen, um den Datenschutz und die Integrität Ihrer verschlüsselten Daten zu gewährleisten.  

Informationen darüber, wie Key-Wrapping Sie unterstützt, die Sicherheit ruhender Daten in der Cloud zu gewährleisten, finden Sie in [Envelope-Verschlüsselung](/docs/services/key-protect/concepts/envelope-encryption.html).

## Wrapping für Schlüssel über die API durchführen
{: #api}

Sie können einen bestimmten Datenverschlüsselungsschlüssel (DEK) mit einem Rootschlüssel schützen, den Sie in {{site.data.keyword.hscrypto}} verwalten.

**Wichtig:** Wenn Sie einen Rootschlüssel für das Wrapping angeben, stellen Sie sicher, dass der Rootschlüssel 256, 384 oder 512 Bit groß ist, damit der Wrapping-Aufruf erfolgreich ist. Wenn Sie einen Rootschlüssel im Service erstellen, generiert {{site.data.keyword.hscrypto}} einen 256-Bit-Schlüssel aus den HSMs, der vom AES-GCM-Algorithmus unterstützt wird.

[Nach der Angabe eines Rootschlüssels im Service](/docs/services/hs-crypto/create-root-keys.html) können Sie einen DEK mit der erweiterten Verschlüsselung mithilfe eines `POST`-Aufrufs zum folgenden Endpunkt einschließen.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/hs-crypto/access-api.html)

2. Kopieren Sie die Schlüsselinformationen, die Sie verwalten und schützen möchten.

    Wenn Sie über Manager- oder Schreibzugriffsberechtigungen für Ihre {{site.data.keyword.hscrypto}}-Serviceinstanz verfügen, [können Sie die Schlüsselinformationen für einen bestimmten Schlüssel mit der Anforderung `GET /v2/keys/<key_ID>` abrufen](/docs/services/hs-crypto/view-keys.html#api).

3. Kopieren Sie die ID des Rootschlüssels, den Sie für das Wrapping verwenden möchten.

4. Führen Sie den folgenden cURL-Befehl aus, um den Schlüssel mit einer Wrapping-Operation zu schützen.

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

    Um mit Schlüsseln in Cloud Foundry-Organisationen und -Bereichen zu arbeiten, ersetzen Sie `Bluemix-Instance` durch die entsprechenden Header `Bluemix-org` und `Bluemix-space`. [Weitere Informationen finden Sie in der {{site.data.keyword.hscrypto}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
    {: tip}

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
        <td><varname>key_ID</varname></td>
        <td>Die eindeutige ID für den Rootschlüssel, der für das Wrapping verwendet werden soll.</td>
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
        <td>Optional: Die eindeutige ID, die zum Überwachen und Korrelieren von Transaktionen verwendet wird.</td>
      </tr>
      <tr>
        <td><varname>return_preference</varname></td>
        <td><p>Ein Header, der das Serververhalten für <code>POST</code>- und <code>DELETE</code>-Operationen ändert.</p><p>Wenn Sie die Variable <em>return_preference</em> auf <code>return=minimal</code> setzen, werden im Entitätshauptteil der Antwort nur die Metadaten des Schlüssels zurückgegeben, wie zum Beispiel Schlüsselname und ID-Wert. Wenn Sie für die Variable <code>return=representation</code> festlegen, werden sowohl die Schlüsselinformationen als auch die Metadaten des Schlüssels zurückgegeben.</p></td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td>Optional: Die Schlüsselinformationen des DEK, den Sie verwalten und schützen möchten. Der Wert <code>plaintext</code> muss base64-codiert sein. Um einen neuen DEK zu generieren, lassen Sie das Attribut <code>plaintext</code> weg. Der Service generiert einen zufälligen Klartext (32 Byte) und führt Wrapping für diesen Wert durch.</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>Optional: Die zusätzlichen Authentifizierungsdaten (AAD), die für die weitere Sicherung des Schlüssels verwendet werden. Jede Zeichenfolge kann bis zu 255 Zeichen enthalten. Wenn AAD bei einer Wrapping-Aufruf für den Service angegeben werden, müssen Sie dieselben AAD während des nachfolgenden Unwrap-Aufrufs verwenden.<br></br>Wichtig: Der {{site.data.keyword.hscrypto}}-Service speichert keine zusätzlichen Authentifizierungsdaten. Wenn AAD angegeben werden, speichern Sie die Daten an einer sicheren Position, um sicherzustellen, dass Sie bei nachfolgenden Anforderungen zum Aufheben des Wrappings auf dieselben AAD zugreifen und diese angeben können.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Variablen, die für das Wrapping eines bestimmten Schlüssels in {{site.data.keyword.hscrypto}} erforderlich sind.</caption>
    </table>

    Ihr Schlüssel mit Wrapping, der die mit Base64-Codierung verschlüsselten Schlüsselinformationen enthält, wird im Entitätshauptteil der Antwort zurückgegeben. Das folgende JSON-Objekt zeigt ein Beispiel für einen zurückgegebenen Wert.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
