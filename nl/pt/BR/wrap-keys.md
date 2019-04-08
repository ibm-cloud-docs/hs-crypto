---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root key, data encryption key, Hyper Protect Crypto Services

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Chaves de quebra
{: #wrap-keys}

É possível gerenciar e proteger suas chaves de criptografia com uma chave raiz usando a API do {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, se você for um usuário privilegiado.
{: shortdesc}

Ao agrupar uma chave de criptografia de dados (DEK) com uma chave raiz, o {{site.data.keyword.hscrypto}} combina a força de múltiplos algoritmos para proteger a privacidade e a integridade de seus dados criptografados.  

Para saber como a quebra de chave ajuda a controlar a segurança de dados em descanso na nuvem, consulte [Criptografia de envelope](/docs/services/key-protect/concepts/envelope-encryption.html).

## Agrupando chaves usando a API
{: #wrap-keys-api}

É possível proteger uma chave de criptografia de dados especificada (DEK) com uma chave raiz que você gerencia em {{site.data.keyword.hscrypto}}.

Ao fornecer uma chave raiz para agrupamento, assegure-se de que a chave raiz seja de 128, 192 ou 256 bits para que a chamada de agrupamento possa ser bem-sucedida. Se você criar uma chave raiz no serviço, o {{site.data.keyword.hscrypto}}
gerará uma chave de 256 bits por meio de seus HSMs, suportada pelo algoritmo AES-CBC.

[Após você designar uma chave raiz no serviço](/docs/services/hs-crypto/create-root-keys.html), poderá agrupar uma DEK com criptografia avançada fazendo uma chamada `POST` para o terminal a seguir.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [Recuperar suas credenciais de autenticação e serviço para que funcionem com chaves no serviço.](/docs/services/hs-crypto/access-api.html)

2. Copie o material de chave do DEK que você deseja gerenciar e proteger.

    Se você tiver privilégios de gerenciador ou de gravador para sua instância de serviço do {{site.data.keyword.hscrypto}}, [será possível recuperar o material da chave para uma chave específica fazendo uma solicitação `GET /v2/keys/<key_ID>`](/docs/services/hs-crypto/view-keys.html#api).

3. Copie o ID da chave raiz que você deseja usar para agrupamento.

4. Execute o comando cURL a seguir para proteger a chave com uma operação de agrupamento.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -H 'correlation-id: <correlation_ID>' \
      -H 'prefer: <return_preference>' \
      -d '{
      "plaintext": "<data_key>",
      "aad": ["<additional_data>", "<additional_data>"]
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
        <td>A abreviação da região, como <code>us-south</code> ou <code>eu-gb</code>, que representa a área geográfica na qual reside sua instância de serviço
 do {{site.data.keyword.hscrypto}}. Para obter mais informações, consulte <a href="/docs/services/hs-crypto/regions.html#endpoints">Terminais regionais em serviço</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>O identificador exclusivo para a chave raiz que você deseja usar para agrupamento.</td>
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
        <td><varname>return_preference</varname></td>
        <td><p>Um cabeçalho que altera o comportamento do servidor para as operações <code>POST</code> e <code>DELETE</code>.</p><p>Quando você configurar a variável <em>return_preference</em> para <code>return=minimal</code>, o serviço retornará somente os metadados da chave, como o nome da chave e o valor de ID, no corpo da entidade de resposta. Quando você configura a variável para <code>return=representation</code>, o serviço retorna tanto o material da chave quanto os metadados da chave.</p></td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td>Opcional: o material da chave do DEK que você deseja gerenciar e proteger. O valor <code>plaintext</code> deve ser codificado em base64. Para gerar um novo DEK, omita o atributo <code>plaintext</code>. O serviço gera um texto sem formatação aleatório (32 bytes) e agrupa esse valor.</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>Opcional: os dados de autenticação adicionais (AAD) usados para tornar a chave mais segura. Cada sequência pode ter até 255 caracteres. Se você fornecer AAD quando fizer uma chamada de agrupamento para o serviço, deverá especificar o mesmo AAD durante a chamada de desagrupamento subsequente.<br></br>Importante: o serviço do {{site.data.keyword.hscrypto}} não salva dados de autenticação adicionais. Se você fornecer um AAD, salve os dados em um local seguro para assegurar que você possa acessar e fornecer o mesmo AAD durante as solicitações de desagrupamento subsequentes.</td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis que são necessárias para agrupar uma chave especificada em {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Sua chave agrupada, contendo o material de chave com codificação Base64, é retornada no corpo da entidade de resposta. O objeto JSON a seguir mostra um valor retornado de exemplo.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
