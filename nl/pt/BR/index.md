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

# Introdução ao {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}
{: #get-started}

<!-- {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} is in the BETA phase and is for tryout and test purpose only. To prevent data loss, use only test data in the current service. This restriction also applies to using {{site.data.keyword.hscrypto}} with other  {{site.data.keyword.cloud_notm}} services.
{:important} -->

O {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} ({{site.data.keyword.hscrypto}} abreviadamente) fornece um módulo de segurança de hardware (HSM) em nuvem para um serviço dedicado de gerenciamento de chave. O {{site.data.keyword.hscrypto}} ajuda a criptografar seus dados no nível de segurança de criptografia do IBM Z de uma maneira conveniente e de custo competitivo.
{:shortdesc}

O {{site.data.keyword.hscrypto}} integra-se às APIs do {{site.data.keyword.keymanagementservicefull_notm}} para gerar e criptografar chaves. A função Keep Your Own Keys (KYOK) também é ativada pelo {{site.data.keyword.hscrypto}} para fornecer acesso ao hardware criptográfico que é a tecnologia certificada FIPS 140-2 Nível 4, o mais alto nível atingível de segurança. O {{site.data.keyword.hscrypto}} oferece módulos de segurança de hardware (HSMs) endereçáveis de rede<!-- and is accessible via PKCS#11 application programming interfaces (APIs) with several popular programming languages such as Java, JavaScript, Swift, and so on-->.  <!-- You can access {{site.data.keyword.hscrypto}} via an Advanced Cryptography Service Provider (ACSP) client, which communicates with the ACSP server to enable you to access the backend cryptographic resources.--> Para obter mais informações sobre o  {{site.data.keyword.hscrypto}}, veja  [ {{site.data.keyword.hscrypto}}  visão geral ](/docs/services/hs-crypto/overview.html). Para obter mais informações sobre os requisitos de segurança para módulos de criptografia, consulte [a especificação do NIST for FIPS 140-2 Level ![Ícone de link externo](image/external_link.svg "Ícone de link externo")](https://csrc.nist.gov/publications/detail/fips/140/2/final){:new_window}.

<!-- {{site.data.keyword.hscrypto}} is the cryptography that {{site.data.keyword.blockchainfull_notm}} Platform is built with. It is also a member of the {{site.data.keyword.cloud_notm}} Hyper Protect Family, including [{{site.data.keyword.cloud_notm}} Hyper Protect DBaaS ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-dbaas/index.html){:new_window}, {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}, [{{site.data.keyword.cloud_notm}} Container Service ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/containers/container_index.html){:new_window}, and [{{site.data.keyword.cloud_notm}} {{site.data.keyword.hsplatform}} ![External link icon](image/external_link.svg "External link icon")](https://cloud.ibm.com/docs/services/hypersecure-platform/index.html){:new_window}. -->

Este tutorial orienta como configurar sua instância de criptografia gerenciando suas chaves mestras, além de criar e incluir chaves criptográficas existentes usando o painel do {{site.data.keyword.hscrypto}}.


## Etapa 1: Fornecer o Serviço
{: #provision}

Antes de iniciar, deve-se criar uma instância do {{site.data.keyword.hscrypto}} por meio do console do {{site.data.keyword.cloud_notm}}. Para obter as etapas detalhadas, consulte [Fornecendo o serviço](/docs/services/hs-crypto/provision.html).

## Etapa 2: Inicializar sua Instância de Criptografia

Para gerenciar suas chaves, é necessário inicializar a instância de criptografia (HSM) primeiro. Para obter um tutorial de introdução rápida, consulte [Introdução à inicialização da instância de criptografia](/docs/services/hs-crypto/get_started_hsm.html). Para obter etapas detalhadas e as melhores práticas, consulte [Inicializando instâncias de criptografia para proteger o armazenamento de chave](/docs/services/hs-crypto/initialize_hsm.html).

## Etapa 3: Gerenciar suas chaves
{: #manage-keys}

No painel do {{site.data.keyword.hscrypto}}, é possível criar novas chaves raiz ou chaves padrão para criptografia ou importar suas chaves existentes. Para obter mais informações sobre chaves raiz e chaves padrão, consulte [Introdução às chaves](/docs/services/hs-crypto/keys_intro.html).

### Criando novas chaves
{: #create-keys}

Conclua as etapas a seguir para criar sua primeira chave criptográfica.

1. No painel {{site.data.keyword.hscrypto}}, clique em **Gerenciar** &gt; **Incluir chave**.
2. Para criar uma nova chave, selecione a janela **Criar uma chave**.

    Especifique os detalhes da chave:

    <table>
      <tr>
        <th>Configuração</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>
          <p>Um alias exclusivo, legível para fácil identificação de sua chave.</p>
          <p>Para proteger sua privacidade, assegure-se de que o nome da chave não contenha informações pessoalmente identificáveis (PII), como seu nome ou local.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo de chave</td>
        <td>O <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo de chave</a> que você gostaria de gerenciar no {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descrição das configurações de <b>Criar uma chave</b></caption>
    </table>

3. Quando você tiver concluído o preenchimento dos detalhes da chave, clique em **Criar chave** para confirmar.

Chaves que são criadas no serviço são chaves simétricas de 256 bits, suportadas pelo algoritmo AES-GCM. Para obter segurança adicional, as chaves são geradas pelos módulos de segurança de hardware (HSMs) certificados pelo FIPS 140-2 Nível 4 que estão localizados em data centers seguros do {{site.data.keyword.cloud_notm}}.

### Importando suas próprias chaves
{: #import-keys}

É possível ativar os benefícios de segurança de Keep Your Own Key (KYOK) introduzindo suas chaves existentes no serviço e gerenciando-as.

Conclua as etapas a seguir para incluir uma chave existente.

1. No painel {{site.data.keyword.hscrypto}}, clique em **Gerenciar** &gt; **Incluir chave**.
2. Para fazer upload de uma chave existente, selecione a janela **Importar sua própria chave**.

    Especifique os detalhes da chave:

    <table>
      <tr>
        <th>Configuração</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>
          <p>Um alias exclusivo, legível para fácil identificação de sua chave.</p>
          <p>Para proteger sua privacidade, assegure-se de que o nome da chave não contenha informações pessoalmente identificáveis (PII), como seu nome ou local.</p>
        </td>
      </tr>
      <tr>
        <td>Tipo de chave</td>
        <td>O <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo de chave</a> que você gostaria de gerenciar no {{site.data.keyword.hscrypto}}.</td>
      </tr>
      <tr>
        <td>Material de chave</td>
        <td>O material da chave, como uma chave simétrica, que você deseja armazenar no serviço {{site.data.keyword.hscrypto}}. A chave fornecida deve ser codificada em Base64.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 2. Descrição das configurações de <b>Importar sua própria chave</b></caption>
    </table>

3. Quando você tiver concluído o preenchimento dos detalhes da chave, clique em **Importar chave** para confirmar.

No painel {{site.data.keyword.hscrypto}}, é possível inspecionar as características gerais de suas novas chaves.

## O que vem a seguir

Agora é possível usar suas chaves para codificar seus apps e serviços. Se você incluiu uma chave raiz no serviço, talvez deseje aprender mais sobre o uso da chave raiz para proteger as chaves que criptografam seus dados em repouso. Veja [Agrupando chaves](/docs/services/hs-crypto/wrap-keys.html) para começar.

- Para saber mais sobre o gerenciamento e a proteção de suas chaves de criptografia com uma chave raiz, veja [Criptografia de envelope](/docs/services/key-protect/concepts/envelope-encryption.html).
- Para saber mais sobre como integrar o serviço do {{site.data.keyword.hscrypto}} com outras soluções de dados da nuvem, o [ consulte o doc Integrações](/docs/services/key-protect/integrations/integrate-services.html).
- Para saber mais sobre como gerenciar programaticamente suas chaves, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.

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
