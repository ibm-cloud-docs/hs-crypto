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

# Iniciación a {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

<!-- {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is in the BETA phase and is for tryout and test purpose only. To prevent data loss, use only test data in the current service. This restriction also applies to using {{site.data.keyword.hscrypto}} with other  {{site.data.keyword.cloud_notm}} services.
{:important} -->

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} para abreviar) proporciona un módulo de seguridad de hardware (HSM) en la nube para un servicio de gestión de claves dedicado. {{site.data.keyword.hscrypto}} le ayuda a cifrar los datos con el nivel de seguridad y confianza de la criptografía de IBM Z de una manera cómoda y competitiva en costes.
{:shortdesc}

{{site.data.keyword.hscrypto}} se integra con las API de {{site.data.keyword.keymanagementservicefull_notm}} para generar y cifrar las claves. La función Keep Your Own Keys (KYOK) también está habilitada por {{site.data.keyword.hscrypto}} para proporcionar acceso a hardware criptográfico con tecnología certificada por FIPS 140-2 Level 4, el nivel más alto posible de seguridad. {{site.data.keyword.hscrypto}} ofrece módulos de seguridad de hardware (HSM) direccionables en la red<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> Para obtener más información acerca de {{site.data.keyword.hscrypto}}, consulte [Visión general de {{site.data.keyword.hscrypto}}](/docs/services/hs-crypto/overview.html). Para obtener más información sobre los requisitos de seguridad de los módulos criptográficos, consulte [la especificación de NIST para FIPS 140-2 Nivel 4 ![Icono de enlace externo](image/external_link.svg "Icono de enlace externo")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}.

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

Esta guía de aprendizaje le indica cómo configurar la instancia criptográfica gestionando sus claves maestras, así como crear y añadir claves criptográficas existentes utilizando el panel de control de {{site.data.keyword.hscrypto}}.


## Paso 1: Suministro del servicio
{: #provision}

Antes de empezar, debe crear una instancia de {{site.data.keyword.hscrypto}} desde la consola de {{site.data.keyword.cloud_notm}}. Para ver los pasos detallados, consulte [Suministro del servicio](/docs/services/hs-crypto/provision.html).

## Paso 2: Inicializar la instancia criptográfica

Para gestionar las claves, necesita inicializar la instancia criptográfica (HSM) en primer lugar. Para ver una guía de aprendizaje de inicio rápido, consulte [Guía de inicio de la inicialización de instancias criptográficas](/docs/services/hs-crypto/get_started_hsm.html). Para ver los pasos detallados y métodos recomendados, consulte [Inicialización de instancias criptográficas para proteger el almacén de claves](/docs/services/hs-crypto/initialize_hsm.html).

## Paso 3: Gestionar las claves
{: #manage-keys}

Desde el panel de control de {{site.data.keyword.hscrypto}}, puede crear nuevas claves raíz o claves estándar para el cifrado o importar sus claves existentes. Para obtener más información sobre las claves raíz y claves estándar, consulte [Introducción a las claves](/docs/services/hs-crypto/keys_intro.html).

### Creación de nuevas claves
{: #create-keys}

Siga estos pasos para crear su primera clave criptográfica.

1. En el panel de control de {{site.data.keyword.hscrypto}}, pulse **Gestionar** &gt; **Añadir clave**.
2. Para crear una nueva clave, seleccione la ventana **Crear una clave**.

    Especifique los detalles de la clave:

    <table>
      <tr>
        <th>Valor</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>
          <p>Un alias descriptivo exclusivo para identificar con facilidad su clave.</p>
          <p>Para proteger su privacidad, asegúrese de que el nombre de clave no contiene información de identificación personal (PII), como el nombre o la ubicación.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo de clave</td>
        <td><a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Tipo de clave</a> que desea gestionar en {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 1. Descripción de los valores de <b>Crear una clave</b></caption>
    </table>

3. Cuando haya terminado de cumplimentar los detalles de la clave, pulse **Crear una clave** para confirmar.

Las claves creadas en el servicio son claves simétricas de 256 bits, soportadas por el algoritmo AES-GCM. Para una mayor seguridad, las claves se generan con módulos de seguridad de hardware (HSM) con certificación FIPS 140-2 Nivel 4 que se ubican en centros de datos seguros de {{site.data.keyword.cloud_notm}}.

### Importación de sus propias claves
{: #import-keys}

Puede obtener las ventajas en seguridad que ofrece Keep Your Own Key (KYOK) introduciendo sus claves existentes en el servicio y gestionando las claves existentes.

Siga estos pasos para añadir una clave existente.

1. En el panel de control de {{site.data.keyword.hscrypto}}, pulse **Gestionar** &gt; **Añadir clave**.
2. Para subir una clave existente, seleccione la ventana **Importar su propia clave**.

    Especifique los detalles de la clave:

    <table>
      <tr>
        <th>Valor</th>
        <th>Descripción</th>
      </tr>
      <tr>
        <td>Nombre</td>
        <td>
          <p>Un alias descriptivo exclusivo para identificar con facilidad su clave.</p>
          <p>Para proteger su privacidad, asegúrese de que el nombre de clave no contiene información de identificación personal (PII), como el nombre o la ubicación.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo de clave</td>
        <td><a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Tipo de clave</a> que desea gestionar en {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <tr>
        <td>Material de la clave</td>
        <td>El material de la clave, como por ejemplo una clave simétrica, que desea almacenar en el servicio de {{site.data.keyword.hscrypto}}. La clave que proporcione debe estar codificada en base64.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabla 2. Descripción de los valores de <b>Importar su propia clave</b></caption>
    </table>

3. Cuando haya terminado de cumplimentar los detalles de la clave, pulse **Importar clave** para confirmar.

Desde el panel de control {{site.data.keyword.hscrypto}}, puede inspeccionar las características generales de sus nuevas claves.

## Qué hacer a continuación

Ahora puede utilizar sus claves para codificar las apps y servicios. Si ha añadido una clave raíz al servicio, es posible que desee obtener más información sobre el uso de la clave raíz para proteger las claves que cifran los datos en reposo. Consulte [Envolvimiento de claves](/docs/services/hs-crypto/wrap-keys.html) para empezar.

- Para encontrar más información sobre la gestión y la protección de las claves de cifrado con una clave raíz, consulte [Cifrado de sobre](/docs/services/key-protect/concepts/envelope-encryption.html).
- Para obtener más información sobre la integración del servicio {{site.data.keyword.hscrypto}} con otras soluciones de datos en la nube, [consulte el documento de Integraciones](/docs/services/key-protect/integrations/integrate-services.html).
- Para obtener más información sobre cómo gestionar las claves mediante programación, [consulte el documento de referencia de la API de {{site.data.keyword.hscrypto}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.

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
