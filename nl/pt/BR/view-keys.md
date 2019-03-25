---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: view keys, key configuration, key type

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Visualizando chaves
{: #view-keys}

O {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} fornece um sistema centralizado para visualizar, gerenciar e auditar suas chaves de criptografia. Audite as suas chaves e as restrições de acesso às chaves para garantir a segurança de seus recursos.
{: shortdesc}

Audite a configuração de chaves com regularidade:

- Examine quando as chaves foram criadas e determine se é hora de girar a chave.
- [ Monitore chamadas API para  {{site.data.keyword.hscrypto}}  com o  {{site.data.keyword.cloudaccesstrailshort}} ](/docs/services/cloud-activity-tracker/tutorials/manage_events_cli.html).
- Inspecione quais usuários têm acesso a chaves e se o nível de acesso é apropriado.

Para obter mais informações sobre o acesso de auditoria a seus recursos, consulte [Gerenciando acesso de usuário com o Cloud IAM](/docs/services/hs-crypto/manage-access.html).

## Visualizando chaves com a GUI
{: #gui}

Se você preferir inspecionar as chaves em seu serviço usando uma interface gráfica, será possível usar o painel {{site.data.keyword.hscrypto}}.

[Depois de criar ou importar suas chaves existentes para o serviço](/docs/services/hs-crypto/create-root-keys.html), conclua as etapas a seguir para visualizar suas chaves.

1. [Efetue login no console do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/).
2. No painel do {{site.data.keyword.cloud_notm}}, selecione sua instância provisionada do {{site.data.keyword.hscrypto}}.
3. Procure as características gerais das suas chaves no painel do {{site.data.keyword.hscrypto}}:

    <table>
      <tr>
        <th>Coluna</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td>Nome</td>
        <td>O alias único, legível para o ser humano que foi designado à sua chave.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>Um ID de chave exclusiva que foi designado à sua chave pelo serviço do {{site.data.keyword.hscrypto}}. É possível usar o valor ID para fazer chamadas para o serviço com a [API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto).</td>
      </tr>
      <tr>
        <td>Estado</td>
        <td>O [estado de chave](/docs/services/key-protect/concepts/key-states.html) baseado em [NIST Special Publication 800-57, Recomendação para gerenciamento de chave ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf). Esses estados incluem <i>Pré-ativo</i>, <i>Ativo</i>, <i>Desativado</i> e <i>Destruído</i>.</td>
      </tr>
      <tr>
        <td>Tipo</td>
        <td>O [Tipo de chave](/docs/services/key-protect/concepts/envelope-encryption.html#key-types) que descreve o propósito designado de sua chave dentro do serviço.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve o <b>Chaves</b> tabela</caption>
    </table>

## Visualizando chaves com a API
{: #api}

É possível recuperar os conteúdos de suas chaves usando a API do {{site.data.keyword.hscrypto}}.

### Recuperando uma lista de suas chaves
{: #retrieve-keys-api}

Para uma visualização de alto nível, é possível procurar chaves que são gerenciadas em sua instância provisionada do {{site.data.keyword.hscrypto}} fazendo uma chamada `GET` para o terminal a seguir.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/hs-crypto/access-api.html).

2. Execute o comando cURL a seguir para visualizar características gerais sobre suas chaves.

    ```cURL
    curl -X GET \ https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \ -H 'accept: application/vnd.ibm.collection+json' \ -H 'authorization: Bearer <IAM_token>' \ -H 'bluemix-instance: <instance_ID>' \ -H 'correlation-id: <correlation_ID>' \
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
        <td>Opcional: o identificador exclusivo que é usado para rastrear e correlacionar transações.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 2. Descreve as variáveis que são necessárias para visualizar chaves com a API do {{site.data.keyword.hscrypto}}</caption>
    </table>

    Uma solicitação `GET /v2/keys` bem-sucedida retorna uma coleção de chaves que estão disponíveis em sua instância de serviço do {{site.data.keyword.hscrypto}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...", "type": "application/vnd.ibm.kms.key+json", "name": "Standard key", "description": "...", "state": 1, "crn": "...", "algorithmType": "AES", "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256", "mode": "GCM"
          },
          "extractable": true,
          "imported": false
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...", "state": 1, "crn": "...", "algorithmType": "AES", "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256", "mode": "GCM"
          },
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {:screen}

    Por padrão, `GET /keys` retorna as suas primeiras 2000 chaves, mas é possível ajustar esse limite usando o parâmetro `limit` no tempo de consulta. Para saber mais sobre o `limit` e o `offset`, veja [Recuperando um subconjunto de chaves](#retrieve_subset_keys_api).
    {: tip}

### Recuperando um subconjunto de chaves
{: #retrieve-subset-keys-api}

Especificando os parâmetros `limit` e `offset` no tempo de consulta, é possível recuperar um subconjunto de suas chaves, começando com o valor `offset` que você especifica.

Por exemplo, você pode ter um total de 3000 chaves que são armazenadas em sua instância de serviço do {{site.data.keyword.hscrypto}}, mas você deseja recuperar de 200 a 300 chaves quando faz uma solicitação `GET /keys`.

É possível usar a solicitação de exemplo a seguir para recuperar um conjunto diferente de chaves.

  ```cURL
  curl -X GET \
  https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys?offset=<offset>&limit=<limit> \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'correlation-id: <correlation_ID>' \
  ```
  {: codeblock}

  Substitua as variáveis `limit` e `offset` em sua solicitação de acordo com a tabela a seguir.
  <table>
    <tr>
      <th>Variável</th>
      <th>Descrição</th>
    </tr>
    <tr>
      <td><p><varname>offset</varname></p></td>
      <td>
        <p>Opcional: o número de chaves a serem ignoradas.</p>
        <p>Por exemplo, se você tiver 50 chaves em sua instância e desejar listar 26 a 50 chaves, use
            <code>../keys?offset=25</code>. Também é possível fazer par de <code>offset</code> com <code>limit</code> para percorrer os seus recursos disponíveis.</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>limit</varname></p></td>
      <td>
        <p>Opcional: o número de chaves a serem recuperadas.</p>
        <p>Por exemplo, se você tiver 100 chaves em sua instância e desejar listar apenas 10 chaves, use
            <code>../keys?limit=10</code>. O valor máximo para <code>limit</code> é 5000.</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">Tabela 2. Descreve as variáveis <code>limit</code> e <code>offset</code></caption>
  </table>

Para obter notas de uso, verifique os exemplos a seguir para configurar os seus parâmetros de consulta `limit` e `offset`.

<table>
  <tr>
    <th>URL</th>
    <th>Descrição</th>
  </tr>
  <tr>
    <td><code>.../keys</code></td>
    <td>Lista todos os recursos disponíveis, até as primeiras 2000 chaves.</td>
  </tr>
  <tr>
    <td><code>.../keys?limit=10</code></td>
    <td>Lista os primeiros 10 chaves.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=25 & limit=50</code></td>
    <td>Lista chaves 26-50.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=30 00 & limit=50</code></td>
    <td>Lista chaves 3001-3050.</td>
  </tr>
  <caption style="caption-side:bottom;">Tabela 3. Fornece notas de uso para os parâmetros de consulta limit e offset</caption>
</table>

Deslocamento é o local de uma determinada chave em um conjunto de dados. O valor `offset` é baseado em zero, o que significa que a décima chave de criptografia em um conjunto de dados está no deslocamento 9.
{: tip}

### Recuperando uma chave por ID
{: #retrieve-key-api}

Para visualizar informações detalhadas sobre uma chave específica, é possível fazer uma chamada `GET` para o terminal a seguir.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/hs-crypto/access-api.html).

2. Recupere o ID da chave que você gostaria de acessar ou gerenciar.

    O valor do ID é usado para acessar informações detalhadas sobre a chave, como o próprio material da chave. É possível recuperar o ID para uma chave especificada fazendo uma solicitação `GET /v2/keys` ou acessando a GUI do {{site.data.keyword.hscrypto}}.

3. Execute o comando cURL a seguir para obter detalhes sobre a chave e o material da chave.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Substitua as variáveis na solicitação de exemplo de acordo com a tabela a seguir.

    <table>
      <tr>
        <th>Variável</th>
        <th>Descrição</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>A abreviação da região, como <code>us-south</code> ou <code>eu-gb</code>, que representa a área geográfica na qual reside sua instância de serviço do {{site.data.keyword.hscrypto}}. Veja <a href="/docs/services/hs-crypto/regions.html#endpoints">Terminais em serviço regionais</a> para obter mais informações.</td>
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
        <td>Opcional: o identificador exclusivo que é usado para rastrear e correlacionar transações.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>O identificador para a chave que você recuperou na [etapa 1](#retrieve-keys-api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 4. Descreve as variáveis que são necessárias para visualizar uma chave especificada com a API do {{site.data.keyword.hscrypto}}</caption>
    </table>

    Um  ` GET v2/keys/ bem-sucedido<key_ID>` bem-sucedida retorna detalhes sobre a sua chave e o material da chave. O objeto JSON a seguir mostra um valor retornado de exemplo para uma chave padrão.

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...", "type": "application/vnd.ibm.kms.key+json", "name": "Standard key", "description": "...", "state": 1, "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256", "mode": "GCM"
            },
            "extractable": true,
            "imported": false
        }
      ]
    }
    ```
    {:screen}

    Para obter uma descrição detalhada dos parâmetros disponíveis, veja o {{site.data.keyword.hscrypto}} [documento de referência da API de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
