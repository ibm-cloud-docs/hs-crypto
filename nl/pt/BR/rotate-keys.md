---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: root keys, Rotate key, key rotation

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:important: .important}

# Girando chaves
{: #rotating-keys}

É possível girar suas chaves raiz sob demanda usando o {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

Ao girar sua chave raiz, você encurta o tempo de vida da chave e limita a quantia de informações que são protegidas por
essa chave.   

Para saber como a rotação de chave ajuda a atender os padrões de mercado e as melhores práticas criptográficas, consulte
[Rotação de chave](/docs/services/key-protect/concepts/key-rotation.html).

A rotação está disponível apenas para chaves raízes.
{: tip}

## Girando chaves raiz com a GUI
{: #rotate-root-key-gui}

Se você preferir girar suas chaves raiz usando uma interface gráfica, será possível usar a GUI do {{site.data.keyword.hscrypto}}.

[Depois de criar ou importar suas chaves raiz existentes
para o serviço](/docs/services/hs-crypto/create-root-keys.html), conclua as etapas a seguir para girar uma chave:

1. [Efetue login no console do {{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/){: new_window}.
2. Acesse **Menu** &gt; **Lista de recursos** para visualizar uma lista de seus recursos.
3. Em sua lista de recursos do {{site.data.keyword.cloud_notm}}, selecione a sua instância provisionada do {{site.data.keyword.hscrypto}}.
4. Na página de detalhes do aplicativo, use a tabela de **Chaves** para procurar as chaves em seu serviço.
5. Clique no ícone de ? para abrir uma lista de opções para a chave que você deseja girar.
6. No menu de opções, clique em **Girar chave** e confirme a rotação na próxima tela.

No caso de se importar a chave raiz inicialmente, será necessário fornecer um novo material de chave codificada base64 para girar a chave. Para obter mais informações, consulte [Importando chaves raiz com a GUI](/docs/services/hs-crypto/import-root-keys.html#gui).
{: tip}

## Girando chaves raiz usando a API
{: #rotate-root-kay-api}

[Depois de designar uma chave raiz no serviço](/docs/services/hs-crypto/create-root-keys.html), é
possível girar sua chave fazendo uma chamada de `POST` para o terminal a seguir.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [Recuperar suas credenciais de autenticação e serviço para que funcionem com chaves no serviço.](/docs/services/hs-crypto/access-api.html)

2. Copie o ID da chave raiz que deseja girar.

4. Execute o comando cURL a seguir para substituir a chave pelo novo material de chave.

    ```cURL
    curl -X POST \ 'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <key_material>'
      }'
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
        <td>A abreviação da região, como <code>us-south</code> ou <code>eu-gb</code>, que representa a área geográfica na qual reside sua instância de serviço do {{site.data.keyword.hscrypto}}. Para obter mais informações, consulte <a href="/docs/services/hs-crypto/regions.html#endpoints">Terminais regionais em serviço</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>O identificador exclusivo para a chave raiz que você deseja girar.</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>O material de chave codificado base64 que você deseja armazenar e gerenciar no serviço. Esse valor será necessário se você importar inicialmente o material de chave quando incluir a chave no serviço.</p>
          <p>Para girar uma chave que foi gerada inicialmente pelo {{site.data.keyword.hscrypto}}, omita o atributo <code>payload</code> e transmita um corpo da entidade de solicitação vazio. Para girar uma chave importada, forneça um material de chave que atenda aos requisitos a seguir:</p>
          <p>
            <ul>
              <li>A chave deve ser de 128, 192 ou 256 bits.</li>
              <li>Os bytes de dados, por exemplo, 32 bytes para 256 bits, devem ser codificados usando codificação base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tabela 1. Descreve as variáveis que são necessárias para girar uma chave especificada no {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Uma solicitação de rotação bem-sucedida retorna uma resposta HTTP `204 No Content`, que indica que sua chave raiz foi substituída por um novo material de chave.

4. Opcional: verifique se a chave foi girada ao executar a chamada a seguir para procurar as chaves na instância de serviço do {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    Revise o valor `lastRotateDate` no corpo da entidade de resposta para inspecionar a data e hora em que sua chave foi girada pela última vez.
