---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: instance ID, account ID, Access Management

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gerenciando o acesso às chaves
{: #manage-access-api}

Com o {{site.data.keyword.iamlong}}, é possível ativar o controle de acesso granular para suas chaves de
criptografia criando e modificando políticas de acesso.
{: shortdesc}

Esta página apresenta os cenários para gerenciar o acesso às suas chaves de criptografia com a [API de Gerenciamento de acesso ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window}.

## Antes de Começar
{: #prereqs-manage-api}

Para trabalhar com a API, gere as suas credenciais de autenticação, como o [token de acesso](/docs/services/hs-crypto/access-api.html#retrieve-token) e o [ID da instância](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID). É necessário o ID da chave do {{site.data.keyword.hscrypto}} cujo acesso você deseja gerenciar.

Para aprender sobre como visualizar IDs de chave, veja [Visualizando chaves](/docs/services/hs-crypto/view-keys.html).
{: tip}

### Recuperando seu ID da conta
{: #retrieve-account-ID}

Após você ter recuperado as suas credenciais, determine o escopo de acesso para a sua nova política de acesso recuperando o ID da conta que contém a sua instância do {{site.data.keyword.hscrypto}} (instância de serviço para abreviação).

Para recuperar o seu ID da conta, conclua as etapas a seguir:

1. Efetue login na CLI do {{site.data.keyword.cloud_notm}}.
    ```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **Nota**: o parâmetro `--sso` é necessário ao efetuar login com um ID federado. Se essa opção for usada, acesse o link listado na saída da CLI para gerar uma senha descartável.

    O resultado exibe as informações de identificação para sua conta.

    ```sh
    Autenticando ...     OK

    Selecionar uma conta (ou pressionar Enter para ignorar):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Insira um número> 1
    Conta de amostra de conta direcionada (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. Copie o valor para seu ID da conta.

    O valor _b6hnh3560ehqjkf89s4ba06i367801e_ é um ID da conta de exemplo.

### Recuperando o ID do usuário
{: #retrieve-user-ID}

Recupere o ID do usuário cujo acesso você gostaria de modificar.

Para recuperar o ID do usuário, conclua as etapas a seguir:

1. [Solicite ao usuário que forneça um token do IAM](/docs/services/hs-crypto/access-api.html#retrieve-token).
    A estrutura de token do IAM é a seguinte:

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copie o valor médio e execute o comando a seguir:
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    O resultado mostra um objeto JSON semelhante ao exemplo a seguir:
   ```json
   {
        "iam_id": "...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss": "..."},
            "iat":...,
            "exp":...,
            "iss":"...",
            "grant_type":"...",
            "scope":"...",
            "client_id":"..."
        }
   }
   ```
   {: screen}

4. Copie o valor da propriedade `id`.

## Criando uma política de acesso
{: #create-policy}

Para ativar o controle de acesso para uma chave específica, é possível enviar uma solicitação para {{site.data.keyword.iamshort}} executando o comando a seguir. Repita o comando para cada política de acesso.

```cURL
curl -X POST \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services", "accountId": "<account_ID>", "region": "<region>", "serviceInstance": "<instance_ID>", "resourceType": "key", "resource": "<key_ID>" }
  ]
}'
```
{: codeblock}

<!-- If you need to manage access to keys within a specified Cloud Foundry org and space, replace `serviceInstance` with `organizationId` and `spaceId`. To learn more, see the [Access Management API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.
{: tip}

Replace `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>`, and `<key_ID>` with the appropriate values. -->

**Opcional:** verifique se a política foi criada com êxito.

```cURL
curl -X GET \ https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \ -H 'Authorization: Bearer <Admin_IAM_token>' \ -H 'Accept: application/json' \
```
{: codeblock}


## Atualizando uma Política de Acesso
{: #update-policy}

É possível usar um ID de política recuperado para modificar uma política existente para um usuário. Envie uma solicitação para {{site.data.keyword.iamshort}} executando o comando a seguir:

```cURL
curl -X PUT \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'If-Match': <ETag_ID> \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -d '{
  "roles": [
    {
      "id": "crn:v1:bluemix:public:iam::::role:<IAM_role>"
    }
  ],
  "resources": [
    {
      "serviceName": "Hyper Protect Crypto Services", "accountId": "<account_ID>", "region": "<region>", "serviceInstance": "<instance_ID>", "resourceType": "key", "resource": "<key_ID>" }
  ]
}'
```
{: codeblock}

Substitua `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` e `<key_ID>`  com os valores apropriados.

**Opcional:** verifique se a política foi atualizada com êxito.

```cURL
curl -X GET \ https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \ -H 'Authorization: Bearer <Admin_IAM_token>' \ -H 'Accept: application/json' \
```
{: codeblock}

## Excluindo uma política de acesso
{: #delete-policy}

É possível usar um ID de política recuperado para excluir uma política existente para um usuário. Envie uma solicitação para {{site.data.keyword.iamshort}} executando o comando a seguir:

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Substitua `<account_ID>`, `<user_ID>`, `<policy_ID>` e `<Admin_IAM_token>`  com os valores apropriados.

**Opcional:** verifique se a política foi excluída com êxito.

```cURL
curl -X GET \ https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \ -H 'Authorization: Bearer <Admin_IAM_token>' \ -H 'Accept: application/json' \
```
{: codeblock}
