---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: standard keys, standard encryption key, creating standard keys, create standard keys

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Criando chaves padrão
{: #create-standard-keys}

É possível criar uma chave de criptografia padrão com a GUI do {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ou programaticamente com a API do {{site.data.keyword.hscrypto}}.
{: shortdesc}

## Criando chaves padrão com a GUI
{: #standard-key-gui}

[Depois de criar uma instância do serviço](/docs/services/hs-crypto/provision.html), conclua as etapas a seguir para criar uma chave padrão com a GUI do {{site.data.keyword.hscrypto}}.

1. [Efetue login no console do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/){: new_window}.
2. Acesse **Menu** &gt; **Lista de recursos** para visualizar uma lista de seus recursos.
3. Em sua lista de recursos do {{site.data.keyword.cloud_notm}}, selecione a sua instância provisionada do {{site.data.keyword.hscrypto}}.
4. Para criar uma nova chave, clique em **Incluir chave** e selecione a janela **Criar uma chave**.

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
      <tr></tr>
        <td>Tipo de chave</td>
        <td>O <a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">tipo de chave</a> que você gostaria de gerenciar no {{site.data.keyword.hscrypto}}. Na lista de tipos de chave, selecione <b>Chave padrão</b>.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as configurações de <b>Gerar nova chave</b></caption>
    </table>

5. Quando você tiver concluído o preenchimento dos detalhes da chave, clique em **Criar chave** para confirmar.

## Criando chaves padrão com a API

Crie uma chave padrão fazendo uma chamada `POST` para o terminal a seguir.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/hs-crypto/access-api.html).

2. Chame a API do [{{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto){: new_window} com o comando cURL a seguir.

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json", "name": "<key_alias>", "description": "<key_description>", "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>", "extractable": <key_type> }
     ]
    }'
    ```
    {: codeblock}
<!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
    {: tip} -->

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
        <td><varname>return_preference</varname></td>
        <td><p>Opcional: um cabeçalho que altera o comportamento do servidor para operações <code>POST</code> e <code>DELETE</code>.</p><p>Quando você configurar a variável <em>return_preference</em> para <code>return=minimal</code>, o serviço retornará somente os metadados da chave, como o nome da chave e o valor de ID, no corpo da entidade de resposta. Quando você configura a variável para <code>return=representation</code>, o serviço retorna tanto o material da chave quanto os metadados da chave.</p></td>
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
        <td>Opcional: a data e hora em que a chave expira no sistema, no formato RFC 3339. Se o atributo <code>expirationDate</code> for omitido, a chave não expirará. </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>Um valor booleano determina se o material de chave pode sair do serviço.</p>
          <p>Ao configurar o atributo <code>extractable</code> para <code>true</code>, o serviço cria uma chave padrão que pode ser armazenada em seus aplicativos ou serviços.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tabela 2. Descreve as variáveis que são necessárias para incluir uma chave padrão com a API do {{site.data.keyword.hscrypto}}</caption>
    </table>

    Para proteger a confidencialidade de seus dados pessoais, evite inserir informações pessoalmente identificáveis (PII), como seu nome ou local, ao incluir chaves no serviço. Para obter mais exemplos de PII, consulte a seção 2.2 do [NIST Special Publication 800-122 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    Uma resposta `POST /v2/keys` bem-sucedida retorna o valor de ID para a sua chave, junto a outros metadados. O ID é um identificador exclusivo que é designado para sua chave e é usado para chamadas subsequentes para a API do {{site.data.keyword.hscrypto}}.

3. Opcional: verifique se a chave foi criada executando a chamada a seguir para obter as chaves em sua instância de serviço do {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
      https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}


### O que vem a seguir
{: #standard-key-next}

Para descobrir mais sobre como gerenciar programaticamente as suas chaves, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.-->
