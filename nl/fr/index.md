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

# Initiation à {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

<!-- {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is in the BETA phase and is for tryout and test purpose only. To prevent data loss, use only test data in the current service. This restriction also applies to using {{site.data.keyword.hscrypto}} with other  {{site.data.keyword.cloud_notm}} services.
{:important} -->

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} en abrégé) fournit un module matériel de sécurité (HSM) cloud pour un service de gestion de clés dédié. {{site.data.keyword.hscrypto}} vous aide à chiffrer vos données aux niveaux de sûreté et de sécurité caractéristiques de la cryptographie d'IBM Z d'une manière qui soit à la fois pratique et économique.
{:shortdesc}

{{site.data.keyword.hscrypto}} fonctionne en intégration avec les API de {{site.data.keyword.keymanagementservicefull_notm}} pour générer et chiffrer les clés. Le mécanisme KYKO (Keep Your Own Keys) est également rendu possible par {{site.data.keyword.hscrypto}} afin de fournir l'accès aux matériels cryptographiques à technologie certifiée FIPS 140-2 Level 4, le plus haut niveau de sécurité qui soit. {{site.data.keyword.hscrypto}} offre des modules matériels de sécurité (HSM) adressables sur le réseau<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> Pour plus d'informations sur {{site.data.keyword.hscrypto}}, consultez [Présentation de {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/overview.html). Pour plus d'informations sur les exigences de sécurité pour les modules cryptographiques, consultez la [spécification (en anglais) du NIST for FIPS 140-2 Level ![Icône de lien externe](image/external_link.svg "Icône de lien externe")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}.

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

Ce tutoriel vous montre comment configurer votre instance crypto en gérant vos clés maîtresses, en créant de nouvelles clés cryptographiques et en ajoutant des clés cryptographiques existantes à l'aide du tableau de bord {{site.data.keyword.hscrypto}}.


## Etape 1 : Mettez à disposition le service
{: #provision}

Avant de commencer, vous devez créer une instance de {{site.data.keyword.hscrypto}} à partir de la console {{site.data.keyword.cloud_notm}}. Pour les étapes détaillées, consultez [Mise à disposition du service](/docs/services/hs-crypto/provision.html).

## Etape 2 : Initialisez votre instance crypto

Pour gérer vos clés, vous devez d'abord initialiser votre instance crypto (HSM). Pour une initiation rapide, consultez [Démarrer avec l'initialisation de l'instance crypto](/docs/services/hs-crypto/get_started_hsm.html). Pour les étapes détaillées et les bonnes pratiques, consultez [Initialisation des instances crypto pour protéger le stockage des clés](/docs/services/hs-crypto/initialize_hsm.html).

## Etape 3 : Gérez vos clés
{: #manage-keys}

Dans le tableau de bord {{site.data.keyword.hscrypto}}, vous pouvez créer de nouvelles clés racine ou clés standard pour la cryptographie ou importer vos clés existantes. Pour plus d'informations sur les clés racine et les clés standard, consultez [Introduction aux clés](/docs/services/hs-crypto/keys_intro.html).

### Création de nouvelles clés
{: #create-keys}

Pour créer votre première clé cryptographique, procédez comme suit :

1. Dans le tableau de bord {{site.data.keyword.hscrypto}}, cliquez sur **Manage** &gt; **Add key**.
2. Pour créer une clé, sélectionnez la fenêtre **Create key**.

    Indiquez les détails relatifs à la clé :

    <table>
      <tr>
        <th>Paramètre</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>
          <p>Alias unique et lisible permettant d'identifier facilement votre clé.</p>
          <p>Pour protéger votre vie privée, assurez-vous que le nom de clé ne contient pas d'informations identifiant la personne, comme votre nom ou votre emplacement.</p>
        </td>
      </tr>
      <tr>
        <td>Key type</td>
        <td><a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Type de clé</a> que vous souhaitez gérer dans {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des paramètres de la fenêtre <b>Créer une clé</b></caption>
    </table>

3. Une fois les détails de la clé indiqués, cliquez sur **Create key** pour confirmer l'opération.

Les clés qui sont créées dans le service sont des clés symétriques de 256 bits prises en charge par l'algorithme AES-GCM. Pour renforcer la sécurité, elles sont générées par des modules HSM (Hardware Security Module) certifiés FIPS 140-2 niveau 4 résidant dans des centres de données {{site.data.keyword.cloud_notm}} sécurisés.

### Importation de vos propres clés
{: #import-keys}

Vous pouvez bénéficier des avantages du mécanisme KYOK (Keep Your Own Key, conservez votre propre clé) en introduisant et en gérant vos clés existantes dans le service.

Pour ajouter une clé existante, procédez comme suit :

1. Dans le tableau de bord {{site.data.keyword.hscrypto}}, cliquez sur **Manage** &gt; **Add key**.
2. Pour télécharger une clé existante, sélectionnez la fenêtre **Import your own key**.

    Indiquez les détails relatifs à la clé :

    <table>
      <tr>
        <th>Paramètre</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>
          <p>Alias unique et lisible permettant d'identifier facilement votre clé.</p>
          <p>Pour protéger votre vie privée, assurez-vous que le nom de clé ne contient pas d'informations identifiant la personne, comme votre nom ou votre emplacement.</p>
        </td>
      </tr>
      <tr>
        <td>Key type</td>
        <td><a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Type de clé</a> que vous souhaitez gérer dans {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>Matière de la clé, comme une clé symétrique, que vous voulez stocker dans le service {{site.data.keyword.hscrypto}}. La clé que vous fournissez doit être encodée en base64.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 2. Description des paramètres de la fenêtre <b>Import your own key</b></caption>
    </table>

3. Une fois les détails de la clé indiqués, cliquez sur **Import key** pour confirmer l'opération.

Dans le tableau de bord {{site.data.keyword.hscrypto}}, vous pouvez examiner les caractéristiques générales des nouvelles clés.

## Etapes suivantes

Vous pouvez désormais utiliser vos clés pour coder vos applications et services. Si vous avez ajouté une clé racine au service, vous voudrez peut-être en savoir plus sur l'utilisation de la clé racine pour protéger les clés qui chiffrent vos données au repos. Reportez-vous à [Encapsulage de clés](/docs/services/hs-crypto/wrap-keys.html) pour commencer.

- Pour plus d'informations sur la gestion et la protection de vos clés de chiffrement avec une clé racine, voir [Chiffrement d'enveloppe](/docs/services/key-protect/concepts/envelope-encryption.html).
- Pour plus d'informations sur l'intégration du service {{site.data.keyword.hscrypto}} à d'autres solutions de données de cloud, [voir la documentation relative aux intégrations](/docs/services/key-protect/integrations/integrate-services.html).
- Pour plus d'informations sur la gestion de vos clés à l'aide d'un programme, [consultez la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.

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
