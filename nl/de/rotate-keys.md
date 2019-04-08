---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

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

# Schlüsselrotation
{: #rotating-keys}

Sie können Rootschlüssel mit {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} bedarfsgesteuert turnusmäßig wechseln (Schlüsselrotation).
{: shortdesc}

Durch die Rotation des Rootschlüssels wird die Laufzeit des Schlüssels verkürzt und die Menge der durch den betreffenden Schlüssel geschützten Informationen wird begrenzt.   

Die Schlüsselrotation unterstützt Sie bei der Einhaltung branchenspezifischer Vorgaben und dem Einsatz bewährter Verschlüsselungsverfahren. Informationen hierzu finden Sie in [Schlüsselrotation](/docs/services/key-protect/concepts/key-rotation.html).

Die Rotation ist nur für Rootschlüssel verfügbar.
{: tip}

## Schlüsselrotation für Rootschlüssel mit der GUI
{: #rotate-root-key-gui}

Wenn Sie die Rotation von Rootschlüsseln über eine grafische Oberfläche bevorzugen, können Sie hierzu die {{site.data.keyword.hscrypto}}-GUI verwenden.

[Nach dem Erstellen oder Importieren der vorhandenen Rootschlüssel in den Service](/docs/services/hs-crypto/create-root-keys.html) führen Sie die folgenden Schritte aus, um eine Schlüsselrotation durchzuführen:

1. [Melden Sie sich bei der {{site.data.keyword.cloud_notm}}-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/){: new_window} an.
2. Rufen Sie **Menü** &gt; **Ressourcenliste** auf, um eine Liste Ihrer Ressourcen anzuzeigen. 
3. Wählen Sie in Ihrer {{site.data.keyword.cloud_notm}}-Ressourcenliste die bereitgestellte Instanz von {{site.data.keyword.hscrypto}} aus. 
4. Verwenden Sie die Tabelle **Schlüssel** auf der Anwendungsdetailseite, um die Schlüssel in Ihrem Service zu durchsuchen. 
5. Klicken Sie auf das Symbol ⋮, um eine Liste der Optionen für den Schlüssel zu öffnen, für den Sie eine Rotation durchführen möchten.
6. Klicken Sie im Auswahlmenü auf **Schlüsselrotation** und bestätigen Sie die Rotation in der nächsten Anzeige.

Wenn Sie den Rootschlüssel zu Anfang importiert haben, müssen Sie neue, mit Base64-Codierung verschlüsselte Schlüsselinformationen für die Schlüsselrotation angeben. Weitere Informationen finden Sie in [Rootschlüssel über die GUI importieren](/docs/services/hs-crypto/import-root-keys.html#gui).
{: tip}

## Schlüsselrotation für Rootschlüssel mit der API
{: #rotate-root-kay-api}

[Nach der Angabe eines Rootschlüssels im Service](/docs/services/hs-crypto/create-root-keys.html) können Sie eine Rotation für den Schlüssel durchführen, indem Sie einen `POST`-Aufruf an den folgenden Endpunkt vornehmen.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [Rufen Sie Ihren Service- und Authentifizierungsnachweis ab, um mit den Schlüsseln im Service zu arbeiten.](/docs/services/hs-crypto/access-api.html)

2. Kopieren Sie die ID des Rootschlüssels, für den eine Rotation durchgeführt werden soll.

4. Führen Sie den folgenden cURL-Befehl aus, um den Schlüssel durch neue Schlüsselinformationen zu ersetzen.

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
        <td>Die eindeutige ID für den Rootschlüssel, für den eine Rotation durchgeführt werden soll.</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>Die mit einer Base64-Codierung verschlüsselten Schlüsselinformationen, die im Service gespeichert und verwaltet werden sollen. Dieser Wert ist erforderlich, wenn die Schlüsselinformationen ursprünglich beim Hinzufügen des Schlüssels zum Service importiert wurden.</p>
          <p>Geben Sie für die Rotation eines Schlüssels, der ursprünglich in {{site.data.keyword.hscrypto}} generiert wurde, das Attribut <code>payload</code> nicht an und übergeben Sie einen leeren Entitätshauptteil für die Anforderung. Geben Sie für die Rotation eines importierten Schlüssels Schlüsselinformationen an, die die folgenden Voraussetzungen erfüllen:</p>
          <p>
            <ul>
              <li>Der Schlüssel muss 128, 192 oder 256 Bit groß sein. </li>
              <li>Die Byte der Daten (z. B. 32 Byte oder 256 Bit) müssen mit der base64-Codierung verschlüsselt werden.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Variablen, die für die Rotation eines bestimmten Schlüssels in {{site.data.keyword.hscrypto}} erforderlich sind.</caption>
    </table>

    Eine erfolgreiche Rotationsanforderung gibt die HTTP-Antwort `204 No Content` zurück, die bedeutet, dass der Rootschlüssel durch neue Schlüsselinformationen ersetzt wurde.

4. Optional: Stellen Sie sicher, dass die Schlüsselrotation durchgeführt wurde, indem Sie den folgenden Aufruf ausführen, um die Schlüssel in der {{site.data.keyword.hscrypto}}-Serviceinstanz zu durchsuchen.

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    Überprüfen Sie den Wert für `lastRotateDate` im Entitätshauptteil der Antwort, um das Datum und die Uhrzeit der letzten Rotation des Schlüssels zu prüfen.
