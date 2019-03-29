---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-05"

Keywords: dedicated key management service, IBM Key, Own Keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Einführung in {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

<!-- {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is in the BETA phase and is for tryout and test purpose only. To prevent data loss, use only test data in the current service. This restriction also applies to using {{site.data.keyword.hscrypto}} with other  {{site.data.keyword.cloud_notm}} services.
{:important} -->

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} (abgekürzt {{site.data.keyword.hscrypto}}) stellt ein Cloud-Hardwaresicherheitsmodul (HSM) für einen dedizierten Schlüsselverwaltungsservice bereit. {{site.data.keyword.hscrypto}} hilft Ihnen, Ihre Daten auf der Sicherheitsstufe der IBM Z-Kryptografie bequem und kostengünstig zu verschlüsseln.{:shortdesc}

{{site.data.keyword.hscrypto}} wird in {{site.data.keyword.keymanagementservicefull_notm}}-APIs integriert, um Schlüssel zu generieren und zu verschlüsseln. Die Funktion "Eigene Schlüssel behalten" (KYOK) wird auch von {{site.data.keyword.hscrypto}} aktiviert, um Zugriff auf Verschlüsselungshardware zu bieten, die für FIPS 140-2 Stufe 4 zertifizierte Technologie beinhaltet, die höchste erreichbare Sicherheitsstufe. {{site.data.keyword.hscrypto}} bietet Netz-adressierbare Hardwaresicherheitsmodule (HSMs)<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> Weitere Informationen über {{site.data.keyword.hscrypto}} finden Sie in der [Übersicht zu {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/overview.html). Weitere Informationen zu Sicherheitsanforderungen für Verschlüsselungsmodule finden Sie in der [NIST-Spezifikation für die FIPS 140-2-Stufe ![Symbol für externen Link](image/external_link.svg "Symbol für externen Link")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}.

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

In diesem Lernprogramm erfahren Sie, wie Sie Ihre Verschlüsselungsinstanz mithilfe von Masterschlüsseln verwalten und wie Sie über das {{site.data.keyword.hscrypto}}-Dashboard Verschlüsselungsschlüssel erstellen bzw. vorhandene hinzufügen.


## Schritt 1: Service bereitstellen
{: #provision}

Vor dem Beginn müssen Sie über die {{site.data.keyword.cloud_notm}}-Konsole eine Instanz von {{site.data.keyword.hscrypto}} erstellen. Eine genaue Beschreibung der Schritte finden Sie unter [Service bereitstellen](/docs/services/hs-crypto/provision.html).

## Schritt 2: Verschlüsselungsinstanz initialisieren

Um Ihre Schlüssel zu verwalten, müssen Sie zuerst Ihre Verschlüsselungsinstanz (HSM) initialisieren. Ein Lernprogramm für den Schnelleinstieg finden Sie unter [Einführung in die Initialisierung der Verschlüsselungsinstanz](/docs/services/hs-crypto/get_started_hsm.html). Eine ausführliche Beschreibung der Schritte sowie bewährte Verfahren finden Sie unter [Verschlüsselungsinstanzen zum Schutz des Schlüsselspeichers initialisieren](/docs/services/hs-crypto/initialize_hsm.html).

## Schritt 3: Schlüssel verwalten
{: #manage-keys}

Über das {{site.data.keyword.hscrypto}}-Dashboard können Sie neue Rootschlüssel oder Standardschlüssel für die Verschlüsselung erstellen oder vorhandene Schlüssel importieren. Weitere Informationen zu Rootschlüsseln und Standardschlüsseln finden Sie unter [Einführung in Schlüssel](/docs/services/hs-crypto/keys_intro.html).

### Neue Schlüssel erstellen
{: #create-keys}

Führen Sie die folgenden Schritte aus, um Ihren ersten Verschlüsselungsschlüssel zu erstellen.

1. Klicken Sie im {{site.data.keyword.hscrypto}}-Dashboard auf **Verwalten** &gt; **Schlüssel hinzufügen**.
2. Wenn Sie einen neuen Schlüssel erstellen möchten, wählen Sie das Fenster **Schlüssel erstellen** aus.

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
        <td>Der <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Schlüsseltyp</a>, den Sie in {{site.data.keyword.hscrypto}} verwalten möchten.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 1. Beschreibung der Einstellungen für <b>Schlüssel erstellen</b></caption>
    </table>

3. Geben Sie die Details zum Schlüssel ein und klicken Sie anschließend zum Bestätigen auf **Schlüssel erstellen**.

Die im Service generierten Schlüssel sind symmetrische 256-Bit-Schlüssel, die vom AES-GCM-Algorithmus unterstützt werden. Um eine höhere Sicherheit zu erhalten, werden die Schlüssel von FIPS 140-2 Stufe 4-zertifizierten Hardwaresicherheitsmodulen (HSMs) generiert, die sich in sicheren {{site.data.keyword.cloud_notm}}-Rechenzentren befinden.

### Eigene Schlüssel importieren
{: #import-keys}

Sicherheitsvorteile erhalten Sie auch mit einer KYOK-Unterstützung (Keep Your Own Key), wenn Sie dem Service vorhandene Schlüssel hinzufügen und vorhandene Schlüssel verwalten.

Führen Sie die folgenden Schritte aus, um einen vorhandenen Schlüssel hinzuzufügen.

1. Klicken Sie im {{site.data.keyword.hscrypto}}-Dashboard auf **Verwalten** &gt; **Schlüssel hinzufügen**.
2. Wenn Sie einen vorhandenen Schlüssel hochladen möchten, wählen Sie das Fenster **Eigenen Schlüssel importieren ** aus.

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
        <td>Der <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Schlüsseltyp</a>, den Sie in {{site.data.keyword.hscrypto}} verwalten möchten.</td>
      </tr>
      <tr>
        <td>Schlüsselinformationen</td>
        <td>Die Schlüsselinformationen, z. B. ein symmetrischer Schlüssel, die im {{site.data.keyword.hscrypto}}-Service gespeichert werden sollen. Der bereitgestellte Schlüssel muss base64-codiert sein.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabelle 2. Beschreibung der Einstellungen für <b>Eigenen Schlüssel importieren</b></caption>
    </table>

3. Geben Sie die Details zum Schlüssel ein und klicken Sie anschließend zum Bestätigen auf **Schlüssel importieren**.

Mit dem {{site.data.keyword.hscrypto}}-Dashboard können Sie die allgemeinen Merkmale Ihrer neuen Schlüssel überprüfen.

## Weitere Schritte

Sie können Ihre Schlüssel nun verwenden, um Ihre Apps und Services zu codieren. Wenn Sie einen Rootschlüssel zum Service hinzugefügt haben, können Sie weitere Informationen zur Verwendung des Rootschlüssels für den Schutz der Schlüssel, mit denen Ihre ruhenden Daten verschlüsselt werden, abrufen. Lesen die zum Einstieg [Wrapping für Schlüssel durchführen](/docs/services/hs-crypto/wrap-keys.html).

- Weitere Informationen zum Verwalten und Schützen der Verschlüsselungsschlüssel mithilfe eines Rootschlüssels finden Sie in [Envelope-Verschlüsselungg](/docs/services/key-protect/concepts/envelope-encryption.html).
- Weitere Informationen zur Integration des {{site.data.keyword.hscrypto}}-Service in andere Clouddaten-Lösungen, finden Sie [in der Integrationsdokumentation](/docs/services/key-protect/integrations/integrate-services.html).
- Weitere Informationen zur programmgesteuerten Verwaltung von Schlüsseln [finden Sie in der {{site.data.keyword.hscrypto}}-API-Referenzdokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.

<!-- Complete the following steps to provision {{site.data.keyword.hscrypto}}:
1. Log in to your [IBM Cloud account ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/){:new_window}.
2. Visit [{{site.data.keyword.cloud_notm}} Experimental Services ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/catalog/labs/){:new_window} to see the list of services in experimental phase.
3. From the **All Categories** navigation pane on the left, click the **Security** category under **Platform**.
4. From the list of services, click the **{{site.data.keyword.hscrypto}}** tile.
5. Select the **{{site.data.keyword.hscrypto}} Lite Plan**, and click **Create** to provision an instance of {{site.data.keyword.IBM_notm}} CloudCrypto in the account, region, and resource group where you log in.-->

<!-- ## Installing ACSP client libraries -->

<!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client. Complete the following steps to install the ACSP client libraries in your local environment. -->

<!-- 1. Download the installation package from the [GitHub repository ![External link icon](image/external_link.svg "External link icon")](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto){:new_window}. In the **packages** folder, choose the installation package file that is suitable for your operation system and CPU architecture. For example, for Ubuntu on x86, choose `acsp-pkcs11-client_1.5-3.5_amd64.deb`.
2. Install the package to install the ACSP client libraries with the `dpkg` command. For example, `dpkg -i acsp-pkcs11-client_1.5-3.5_amd64.deb`. -->



<!-- ## Configuring ACSP client -->

<!-- At the current stage, {{site.data.keyword.hscrypto}} provides only self-signed certificates.

You need to configure the ACSP client to enable a proper secure communication channel (mutual TLS) to your service instance in the cloud. -->

<!-- 1. In your {{site.data.keyword.hscrypto}} service instance in {{site.data.keyword.cloud_notm}}, select **Manage** from the left navigator.
2. On the "Manage" screen, click the **Download Config** button to download the `acsp_client_credentials.uue` file.
3. Copy the `acsp_client_credentials.uue` file to the `/opt/ibm/acsp-pkcs11-client/config` directory in your local environment.
4. In the `/opt/ibm/acsp-pkcs11-client/config` directory, decode the file with the following command:
       `base64 --decode acsp_client_credentials.uue > acsp_client_credentials.tar`
5. Extract the client credentials file with the following command:
       `tar xf acsp_client_credentials.tar`
6. Move the `server-config` files into the default place with the following command:
       `mv server-config/* ./`
7. Rename the client credentials file with the following command:
       `mv acsp.properties.client acsp.properties`
8. (Optional:) Change group ID of the files with the following command:
       `chown root.pkcs11 *`
9. Enable ACSP to use the proper config for the service instance in the cloud:
       `export ACSP_P11=/opt/ibm/acsp-pkcs11-client/config/acsp.properties` -->

<!-- Now your ACSP client is operational and your {{site.data.keyword.hscrypto}} is ready to use!

For more information about ACSP client installation and configuration, see [ACSP Client Installation and Configuration Guide ![External link icon](image/external_link.svg "External link icon")](https://github.com/ibm-developer/ibm-cloud-hyperprotectcrypto/blob/master/doc/ACSP-client-config-guide.pdf){:new_window}. -->
