---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: REST API, RESTful API, access token, instance ID

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Acessando a API
{: #access-api}

O {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} integra-se à API de REST do {{site.data.keyword.keymanagementserviceshort}}, que pode ser usada com qualquer linguagem de programação para armazenar, recuperar e gerar chaves.
{: shortdesc}

Para trabalhar com a API, é necessário gerar suas credenciais de serviço e autenticação.

## Recuperando um token de acesso
{: #retrieve-token}

É possível autenticar com o {{site.data.keyword.hscrypto}} ao recuperar um token de acesso do
{{site.data.keyword.iamshort}}. Com um [ID de serviço](/docs/iam/serviceid.html#serviceids), é possível trabalhar
com a API do {{site.data.keyword.hscrypto}} em nome do seu serviço ou aplicativo ou fora do
{{site.data.keyword.cloud_notm}}, sem precisar compartilhar suas credenciais do usuário pessoais.  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

Conclua as seguintes etapas para recuperar um token de acesso:

1. No console do {{site.data.keyword.cloud_notm}}, acesse **Gerenciar** &gt;
**Segurança** &gt; **Identidade e acesso** &gt; **IDs de serviço**. Siga o processo para [criar um ID do serviço](/docs/iam/serviceid.html#creating-a-service-id).
2. Use o menu **Ações** para [definir uma política de acesso para o seu novo ID do serviço](/docs/iam/serviceidaccess.html).

    Para obter mais informações sobre como gerenciar o acesso para seus recursos do
{{site.data.keyword.hscrypto}}, consulte [Funções e permissões](/docs/services/hs-crypto/manage-access.html#roles).
3. Use a seção **Chaves API** para [criar uma chave API para associar com o ID do serviço](/docs/iam/serviceid_keys.html#serviceidapikeys). Salve sua chave API por meio de seu download para um local seguro.
4. Chame a API do {{site.data.keyword.iamshort}} para recuperar seu token de acesso.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    Na solicitação, substitua `<API_KEY>` pela chave API que você criou na etapa 3. O exemplo truncado
a seguir mostra a saída de token:

    ```
    {
    "access_token": "eyJraWQiOiIyM...",
    "expiration": 1512161390,
    "expires_in": 3600,
    "refresh_token": "...",
    "token_type": "Bearer"
    }
    ```
    {: screen}

    Use o valor integral `access_token`, prefixado pelo tipo de token _Bearer_ para gerenciar chaves
programaticamente para seu serviço usando a API do {{site.data.keyword.hscrypto}}.

    Os tokens de acesso são válidos por 1 hora, mas é possível gerá-los novamente conforme necessário. Para manter o acesso ao serviço, atualize o token de acesso para a sua chave API em uma base regular chamando a API do {{site.data.keyword.iamshort}}.   
    {: tip }

## Recuperando o ID de sua instância
{: #retrieve-instance-ID}

É possível recuperar as informações de identificação para sua instância de serviço do {{site.data.keyword.hscrypto}} usando a [CLI do {{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview). Use um ID de instância para gerenciar suas chaves de criptografia dentro de uma instância especificada de
{{site.data.keyword.hscrypto}} em sua conta.

1. Efetue login no  {{site.data.keyword.cloud_notm}}  com a  [ {{site.data.keyword.cloud_notm}}  CLI ](/docs/cli/index.html#overview).

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Observação:** se o login falhar, execute o comando `ibmcloud login --sso` e tente novamente. O parâmetro `--sso` é necessário quando você efetua login com um ID federado. Se essa opção for usada, acesse o link listado na saída da CLI para gerar uma senha descartável.

2. Selecione a conta que contém sua instância provisionada.

    É possível executar `ibmcloud resource service-instances` para listar todas as instâncias de serviço que são fornecidas em sua conta.

3. Recupere o Cloud Resource Name (CRN) que identifica exclusivamente sua instância de serviço do {{site.data.keyword.hscrypto}}.

    ```sh
    ibmcloud resource service-instance < instance_name> -- id
    ```
    {: pre}

    Substitua `<instance_name>` com o alias exclusivo que você designou para sua instância do
{{site.data.keyword.hscrypto}}. O exemplo truncado a seguir mostra a saída da CLI. O valor _42454b3b-5b06-407b-a4b3-34d9ef323901_ é um ID da instância de exemplo.

    ```
    crn:v1 :bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea: 42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## Recuperando informações de conexão
{: #retrieve-connection-info}

Antes de chamar quaisquer APIs do {{site.data.keyword.keymanagementserviceshort}}, chame a API **Recuperar as informações de conexão** primeiro para recuperar as informações de conexão. Para obter mais informações, consulte [o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.

## Formando sua solicitação de API
{: #form-api-request}

Ao fazer uma chamada API para o serviço, estruture sua solicitação de API de acordo com a maneira como você inicialmente
provisionou sua instância do {{site.data.keyword.hscrypto}}.

Para construir sua solicitação, emparelhe um [terminal em serviço
regional](/docs/services/hs-crypto/regions.html) com as credenciais de autenticação apropriadas. Por exemplo, se você criou uma instância de serviço para a região us-south, use o terminal a seguir e os cabeçalhos de API para procurar chaves em seu serviço:

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### O que vem a seguir

- Para saber mais sobre como gerenciar programaticamente suas chaves, [verifique o doc de referência da API do {{site.data.keyword.hscrypto}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
- Para ver um exemplo de como chaves armazenadas no {{site.data.keyword.hscrypto}} podem funcionar para criptografar e decriptografar dados, [consulte o aplicativo de amostra no GitHub ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}.
