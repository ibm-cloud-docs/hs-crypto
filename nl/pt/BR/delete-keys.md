---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: details of the DELETE request, delete encryption key, deleting keys, Variable Description region

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Excluindo chaves
{: #deleting-keys}

É possível usar o {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} para excluir uma chave de criptografia e seus conteúdos, se você é um administrador para o espaço do {{site.data.keyword.cloud_notm}} ou instância de serviço {{site.data.keyword.hscrypto}}.
{: shortdesc}

**Importante:** ao excluir uma chave, você fragmenta permanentemente seus conteúdos e dados associados. A ação não pode ser invertida. A destruição de recursos não é recomendada para ambientes de produção, mas pode ser útil para ambientes temporários, como de teste ou QA.

## Excluindo chaves com a GUI
{: #delete-keys-gui}

Se você preferir excluir suas chaves de criptografia usando uma interface gráfica, será possível usar a GUI do {{site.data.keyword.hscrypto}}.

[Depois de criar ou importar as chaves existentes no serviço](/docs/services/hs-crypto/create-root-keys.html),conclua as etapas a seguir para excluir a chave:

1. [Efetue login no console do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/){: new_window}.
2. Acesse **Menu** &gt; **Lista de recursos** para visualizar uma lista de seus recursos.
3. Em sua lista de recursos do {{site.data.keyword.cloud_notm}}, selecione a sua instância provisionada do {{site.data.keyword.hscrypto}}.
4. Use a tabela de **Chaves** para procurar as chaves em seu serviço.
5. Clique no ícone ⋮ para abrir uma lista de opções para a chave que você deseja excluir.
6. No menu de opções, clique em **Excluir chave** e confirme a exclusão da chave na próxima tela.

Depois de excluir uma chave, a chave transita para o estado _Destruído_. As chaves nesse estado não são mais recuperáveis. Metadados que estão associados à chave, como a data de exclusão da chave, são mantidos no banco de dados do {{site.data.keyword.hscrypto}}.

## Excluindo chaves com a API
{: #api}

Para excluir uma chave e os seus conteúdos, faça uma chamada `DELETE` para o terminal a seguir.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

1. [Recupere suas credenciais de serviço e autenticação para trabalhar com chaves no serviço](/docs/services/hs-crypto/access-api.html).

2. Recupere o ID da chave que você gostaria de excluir.

    É possível recuperar o ID para uma chave especificada fazendo uma solicitação `GET /v2/keys/` ou visualizando suas chaves no painel do {{site.data.keyword.hscrypto}}.

3. Execute o comando cURL a seguir para excluir permanentemente a chave e seus conteúdos.

    ```cURL
    curl -X DELETE \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'prefer: <return_preference>'
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
        <td><varname>key_ID</varname></td>
        <td>O identificador exclusivo para a chave que você gostaria de excluir.</td>
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
        <td><varname>return_preference</varname></td>
        <td><p>Um cabeçalho que altera o comportamento do servidor para as operações <code>POST</code> e <code>DELETE</code>.</p><p>Ao configurar a variável <em>return_preference</em> para <code>return=minimal</code>, o serviço retorna uma resposta de exclusão bem-sucedida. Quando você configura a variável para <code>return=representation</code>, o serviço retorna tanto o material da chave quanto os metadados da chave.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis que são necessárias para excluir chaves com a API do {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Se a variável _return_preference_ estiver configurada como `return=representation`, os detalhes da solicitação `DELETE` serão retornados no corpo da entidade de resposta. O objeto JSON a seguir mostra um valor retornado de exemplo.
    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "...",
          "description": "...",
          "state": 5,
          "crn": "...",
          "deleted": true,
          "algorithmType": "AES",
          "createdBy": "...",
          "deletedBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "deletionDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SS.SSZ",
          "nonactiveStateReason": 2,
          "extractable": true
        }
      ]
    }
    ```
    {: screen}

    Para obter uma descrição detalhada dos parâmetros disponíveis, veja o {{site.data.keyword.hscrypto}} [documento de referência da API de REST ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
