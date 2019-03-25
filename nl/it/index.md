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

# Introduzione a {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

<!-- {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is in the BETA phase and is for tryout and test purpose only. To prevent data loss, use only test data in the current service. This restriction also applies to using {{site.data.keyword.hscrypto}} with other  {{site.data.keyword.cloud_notm}} services.
{:important} -->

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} (abbreviato {{site.data.keyword.hscrypto}}) fornisce un HSM (Hardware Security Module) su cloud per un servizio di gestione delle chiavi dedicato. {{site.data.keyword.hscrypto}} ti aiuta a crittografare i tuoi dati al livello di sicurezza e protezione della crittografia IBM Z in modo conveniente e competitivo.
{:shortdesc}

{{site.data.keyword.hscrypto}} si integra con le API {{site.data.keyword.keymanagementservicefull_notm}} per generare e crittografare le chiavi. {{site.data.keyword.hscrypto}} abilita inoltre la funzione KYOK (Keep Your Own Keys) per fornire accesso all'hardware di crittografia che è la tecnologia certificata da FIPS 140-2 Level 4, il massimo livello di sicurezza raggiungibile. {{site.data.keyword.hscrypto}} offre degli HSM (Hardware Security Module) indirizzabili di rete <!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> Per ulteriori informazioni su {{site.data.keyword.hscrypto}}, vedi [Panoramica di {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/overview.html). Per ulteriori informazioni sui requisiti di sicurezza per i moduli di crittografia, consulta [la specifica di NIST per FIPS 140-2 Level ![Icona link esterno](image/external_link.svg "Icona link esterno")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}.

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

Questa esercitazione ti guida su come configurare la tua istanza di crittografia gestendo le tue chiavi master e su come creare e aggiungere le chiavi di crittografia esistenti utilizzando il dashboard {{site.data.keyword.hscrypto}}.


## Passo 1: esegui il provisioning del servizio
{: #provision}

Prima di cominciare, devi creare un'istanza di {{site.data.keyword.hscrypto}} dalla console {{site.data.keyword.cloud_notm}}. Per la procedura dettagliata, vedi [Provisioning del servizio](/docs/services/hs-crypto/provision.html).

## Passo 2: inizializza la tua istanza di crittografia

Per gestire le tue chiavi, devi prima inizializzare l'istanza di crittografia (HSM). Per una rapida esercitazione introduttiva, vedi [Introduzione all'inizializzazione dell'istanza di crittografia](/docs/services/hs-crypto/get_started_hsm.html). Per i passi dettagliati e le prassi ottimali, vedi [Inizializzazione delle istanze di crittografia per proteggere l'archiviazione chiavi](/docs/services/hs-crypto/initialize_hsm.html).

## Passo 3: gestisci le tue chiavi
{: #manage-keys}

Dal dashboard {{site.data.keyword.hscrypto}}, puoi creare nuove chiavi root o chiavi standard per la crittografia oppure puoi importare le tue chiavi esistenti. Per ulteriori informazioni sulle chiavi root e sulle chiavi standard, vedi [Introduzione alla chiavi](/docs/services/hs-crypto/keys_intro.html).

### Creazione di nuove chiavi
{: #create-keys}

Completa la seguente procedura per creare la tua prima chiave crittografica.

1. Dal dashboard {{site.data.keyword.hscrypto}}, fai clic su **Manage** &gt; **Add key**.
2. Per creare una nuova chiave, seleziona la finestra **Create a key**.

    Specifica i dettagli della chiave:

    <table>
      <tr>
        <th>Impostazione</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>
          <p>Un alias univoco e leggibile dall'utente per una facile identificazione della tua chiave.</p>
          <p>Per proteggere la tua privacy, assicurati che il nome della chiave non contenga informazioni d'identificazione personale, come il tuo nome o la tua posizione.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo di chiave</td>
        <td>Il <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo di chiave</a> che desideri gestire in {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 1. Descrizione delle impostazioni <b>Create a key</b></caption>
    </table>

3. Una volta che hai finito di compilare i dettagli della chiave, fai clic su **Create key** per confermare.

Le chiavi create nel servizio sono chiavi simmetriche a 256 bit, supportate dall'algoritmo AES-GCM. Per una maggiore sicurezza, le chiavi sono generate dagli HSM (Hardware Security Module) certificati da FIPS 140-2 Level 4 che si trovano in data center {{site.data.keyword.cloud_notm}} sicuri.

### Importazione delle tue chiavi
{: #import-keys}

Puoi abilitare i vantaggi di sicurezza di KYOK (Keep Your Own Key) introducendo le tue chiavi esistenti nel servizio e gestendo le tue chiavi correnti.

Completa la seguente procedura per aggiungere una chiave esistente.

1. Dal dashboard {{site.data.keyword.hscrypto}}, fai clic su **Manage** &gt; **Add key**.
2. Per caricare una chiave esistente, seleziona la finestra **Import your own key**.

    Specifica i dettagli della chiave:

    <table>
      <tr>
        <th>Impostazione</th>
        <th>Descrizione</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>
          <p>Un alias univoco e leggibile dall'utente per una facile identificazione della tua chiave.</p>
          <p>Per proteggere la tua privacy, assicurati che il nome della chiave non contenga informazioni d'identificazione personale, come il tuo nome o la tua posizione.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo di chiave</td>
        <td>Il <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo di chiave</a> che desideri gestire in {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <tr>
        <td>Materiale della chiave</td>
        <td>Il materiale della chiave, come ad esempio la chiave simmetrica, che vuoi archiviare nel servizio {{site.data.keyword.hscrypto}}. La chiave che fornisci deve essere codificata con base64.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabella 2. Descrizione delle impostazioni <b>Import your own key</b></caption>
    </table>

3. Una volta che hai finito di compilare i dettagli della chiave, fai clic su **Import key** per confermare.

Dal dashboard {{site.data.keyword.hscrypto}} , puoi controllare le caratteristiche generali delle tue nuove chiavi.

## Operazioni successive

Ora puoi utilizzare le chiavi per crittografare i tuoi servizi e le tue applicazioni. Se hai aggiunto una chiave root al servizio, potresti volere ulteriori informazioni sul suo utilizzo per proteggere le chiavi che crittografano i tuoi dati inattivi. Per iniziare, consulta l'[Impacchettamento delle chiavi](/docs/services/hs-crypto/wrap-keys.html).

- Per trovare ulteriori informazioni sulla gestione e protezione delle tue chiavi crittografate con una chiave root, consulta [Crittografia envelope](/docs/services/key-protect/concepts/envelope-encryption.html).
- Per ulteriori informazioni sull'integrazione del servizio {{site.data.keyword.hscrypto}} con altre soluzioni di dati cloud, [controlla la documentazione di Integrations](/docs/services/key-protect/integrations/integrate-services.html).
- Per ulteriori informazioni sulla gestione a livello programmatico delle tue chiavi, [consulta la documentazione di riferimento API di {{site.data.keyword.hscrypto}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.

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
