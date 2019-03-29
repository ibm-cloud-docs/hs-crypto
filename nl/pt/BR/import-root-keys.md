---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root keys, import keys, symmetric key, Hyper Protect Crypto Services GUI

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Importando chaves raiz
{: #import-root-keys}

É possível usar
{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} para proteger suas chaves raiz existentes usando a GUI do {{site.data.keyword.hscrypto}} ou programaticamente com a {{site.data.keyword.hscrypto}} do API.
{: shortdesc}

Chaves raiz são chaves simétricas de quebra de chaves usadas para proteger a segurança dos dados criptografados na nuvem. Para obter mais informações sobre chaves raiz, consulte [Criptografia de envelope](/docs/services/key-protect/concepts/envelope-encryption.html).

## Importando chaves raiz com a GUI
{: #gui}

[Depois de criar uma instância do serviço](/docs/services/
hs-crypto/provision.html), conclua as etapas a seguir para incluir sua chave raiz existente com a GUI do {{site.data.keyword.hscrypto}}.

1. [Efetue login no console do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/){: new_window}.
2. No painel do {{site.data.keyword.cloud_notm}}, selecione sua instância provisionada do {{site.data.keyword.hscrypto}}.
3. Para importar uma chave, clique em **Incluir chave** e selecione a janela **Inserir chave existente**.

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
        <td>O <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo de chave</a> que você gostaria de gerenciar no {{site.data.keyword.hscrypto}}. Na lista de tipos de chave, selecione <b>Chave raiz</b>.</td>
      </tr>
      <tr>
        <td>Material de chave</td>
        <td>
          <p>O material de chave com codificação base64, como uma chave de quebra de chave, que você deseja armazenar e gerenciar no serviço.</p>
          <p>Certifique-se de que o material da chave atenda aos seguintes requisitos:</p>
          <p>
            <ul>
              <li>A chave de ser de 256, 384 ou 512 bits.</li>
              <li>Os bytes de dados, por exemplo, 32 bytes para 256 bits, devem ser codificados usando codificação base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as configurações <b>Inserir chave existente</b></caption>
    </table>

4. Quando você tiver concluído o preenchimento dos detalhes da chave, clique em **Incluir nova chave** para confirmar.

## Importando chaves raiz com a API
{: #api}

Inclua a sua chave raiz existente fazendo uma chamada `POST` para o terminal a seguir.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/hs-crypto/access-api.html).

1. Chame a [API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} com o comando cURL a seguir.

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

    Para trabalhar com chaves dentro de uma organização e um espaço do Cloud Foundry em sua conta, substitua `Bluemix-Instance` pelos cabeçalhos `Bluemix-org` e `Bluemix-space` apropriados. [Para obter mais informações, consulte o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
    {: tip}

    Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.
    <table>
      <tr>
        <th>Variável</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>A abreviação da região, como <code>us-south</code> ou <code>eu-gb</code>, que representa a área geográfica na qual reside sua instância de serviço do {{site.data.keyword.hscrypto}}. Para obter mais informações, consulte <a href="/docs/services/hs-crypto/regions.html#endpoints">Terminais regionais em serviço</a>.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Seu token de acesso do {{site.data.keyword.cloud_notm}}. Inclua o conteúdo integral do token <code>IAM</code>, incluindo valor Bearer, na solicitação cURL. Para obter mais informações, veja <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Recuperando um token de acesso</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>O identificador exclusivo que é designado para sua instância de serviço {{site.data.keyword.hscrypto}}. Para obter mais informações, veja <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Recuperando um ID da instância</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>O identificador exclusivo que é usado para rastrear e correlacionar transações.</td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>Um nome exclusivo legível para fácil identificação da sua chave.</p>
          <p>Importante: para proteger sua privacidade, não armazene seus dados pessoais como metadados para sua chave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>Opcional: uma descrição estendida de sua chave.</p>
          <p>Importante: para proteger sua privacidade, não armazene seus dados pessoais como metadados para sua chave.</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>Opcional: a data e hora em que a chave expira no sistema, no formato RFC 3339. Se o atributo <code>expirationDate</code> for omitido, a chave não expirará.</td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>O material de chave com codificação base64, como uma chave de quebra de chave, que você deseja armazenar e gerenciar no serviço.</p>
          <p>Certifique-se de que o material da chave atenda aos seguintes requisitos:</p>
          <p>
            <ul>
              <li>A chave de ser de 256, 384 ou 512 bits.</li>
              <li>Os bytes de dados, por exemplo, 32 bytes para 256 bits, devem ser codificados usando codificação base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>Um valor booleano determina se o material de chave pode sair do serviço.</p>
          <p>Ao configurar o atributo <code>extractable</code> para <code>false</code>, o serviço designa a chave como uma chave raiz que pode ser usada para operações de <code>wrap</code> ou <code>unwrap</code>.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis que são necessárias para incluir uma chave raiz com a API do {{site.data.keyword.hscrypto}}</caption>
    </table>

    Para proteger a confidencialidade de seus dados pessoais, evite inserir informações pessoalmente identificáveis (PII), como seu nome ou local, ao incluir chaves no serviço. Para obter mais exemplos de PII, consulte a seção 2.2 do [NIST Special Publication 800-122 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    Uma resposta `POST /v2/keys` bem-sucedida retorna o valor de ID para a sua chave, junto a outros metadados. O ID é um identificador exclusivo que é designado para sua chave e é usado para chamadas subsequentes para a API do {{site.data.keyword.hscrypto}}.

2. Opcional: verifique se a chave foi incluída executando a chamada a seguir para procurar as chaves na instância de serviço do {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**Nota:** ao incluir uma chave raiz existente no serviço, a chave permanece dentro dos limites de {{site.data.keyword.hscrypto}} e seu material da chave não pode ser recuperado.

### O que vem a seguir

- Para descobrir mais sobre como proteger chaves com criptografia de envelope, consulte [Chaves de quebra](/docs/services/hs-crypto/wrap-keys.html).
- Para saber mais sobre como gerenciar programaticamente suas chaves, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/
hs-crypto){: new_window}.
