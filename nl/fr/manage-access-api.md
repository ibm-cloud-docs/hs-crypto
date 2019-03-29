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

# Gestion de l'accès aux clés
{: #manage-access-api}

{{site.data.keyword.iamlong}} permet un contrôle d'accès granulaire à vos clés de chiffrement en créant et en modifiant des règles d'accès.
{: shortdesc}

Cette page vous guide à travers plusieurs scénarios de gestion de l'accès à vos clés de chiffrement à l'aide de l'[API Access Management ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://iampap.ng.bluemix.net/v1/docs/#/Policies/post_v1_policies){: new_window}.

## Avant de commencer
{: #prereqs}

Pour utiliser l'API, générez vos données d'authentification, par exemple, votre [jeton d'accès](/docs/services/hs-crypto/access-api.html#retrieve-token) et  votre [ID d'instance](/docs/services/hs-crypto/access-api.html#retrieve-instance-ID). Vous avez également besoin de l'ID de la clé {{site.data.keyword.hscrypto}} dont vous souhaitez gérer l'accès.

Pour savoir comment afficher les ID de clé, voir [Affichage des clés](/docs/services/hs-crypto/view-keys.html).
{: tip}

### Extraction de votre ID de compte
{: #retrieve-account-ID}

Après avoir extrait vos données d'identification, déterminez la portée de votre nouvelle règle d'accès en procédant à l'extraction de l'ID du compte qui contient votre instance de service {{site.data.keyword.hscrypto}}.

Pour extraire votre ID de compte, procédez comme suit :

1. Connectez-vous à l'interface de ligne de commande d'{{site.data.keyword.cloud_notm}}.
```sh
    ibmcloud login [--sso]
    ```
    {: codeblock}

    **Remarque** : le paramètre `--sso` est requis quand vous vous connectez avec un ID fédéré. Si cette option est utilisée, accédez au lien répertorié dans la sortie d'interface de ligne de commande pour générer un code d'accès unique.

    Le résultat affiche les informations d'identification pour votre compte.

    ```sh
    Authenticating...
    OK

    Select an account (or press enter to skip):

    1. sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    Enter a number> 1
    Targeted account sample-acount (b6hnh3560ehqjkf89s4ba06i367801e)

    API endpoint:   https://api.ng.bluemix.net (API version: 2.75.0)
    Region:         us-south
    User:           admin
    Account:        sample-account (b6hnh3560ehqjkf89s4ba06i367801e)
    ```
    {: screen}

2. Copiez la valeur de votre ID de compte.

    La valeur _b6hnh3560ehqjkf89s4ba06i367801e_ est un exemple d'ID de compte.

### Extraction de l'ID utilisateur
{: #retrieve-user-ID}

Extrayez l'ID de l'utilisateur dont vous souhaitez modifier l'accès.

Pour récupérer l'ID utilisateur, procédez comme suit :

1. [Demandez à l'utilisateur de fournir son jeton IAM](/docs/services/hs-crypto/access-api.html#retrieve-token).
    La structure du jeton IAM se présente comme suit :

    ```sh
    IAM token: Bearer <value>.<value>.<value>
    ```
    {: screen}

2. Copiez la valeur intermédiaire et exécutez la commande suivante :
    ```sh
    echo -n "<value>" | base64 --decode
    ```
    {: codeblock}

    Le résultat obtenu présente un objet JSON semblable au suivant :
   ```json
   {
        "iam_id":"...",
        "id":"...",
        "realmid":"...",
        "identifier":"...",
        "given_name":"...",
        "family_name":"...",
        "name":"...",
        "email":"...",
        "sub":"...",
        "account":{
            "bss":"..."},
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

4. Copiez la valeur de la propriété `id`.

## Création d'une règle d'accès
{: #create-policy}

Pour activer le contrôle d'accès pour une clé spécifique, vous pouvez envoyer une demande à {{site.data.keyword.iamshort}} en exécutant la commande ci-dessous. Répétez la commande pour chaque règle d'accès.

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
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

Si vous devez gérer l'accès aux clés dans une organisation et un espace Cloud Foundry spécifique, remplacez `serviceInstance` par `organizationId` et `spaceId`. Pour en savoir plus, consultez la [documentation de référence des API Access Management ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://iampap.ng.bluemix.net/v1/docs/#!/Access_Policies/){: new_window}.
{: tip}

Remplacez `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` et `<key_ID>` par les valeurs appropriées.

**Facultatif :** vérifiez que la règle a été créée.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}


## Mise à jour d'une règle d'accès
{: #update-policy}

Vous pouvez utiliser un identificateur de règle extrait pour modifier une règle existante pour un utilisateur. Envoyez une demande à {{site.data.keyword.iamshort}} en exécutant la commande suivante :

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
      "serviceName": "Hyper Protect Crypto Services",
      "accountId": "<account_ID>",
      "region": "<region>",
      "serviceInstance": "<instance_ID>",
      "resourceType": "key",
      "resource": "<key_ID>"
    }
  ]
}'
```
{: codeblock}

Remplacez `<user_ID>`, `<Admin_IAM_token>`, `<IAM_role>`, `<region>`, `<account_ID>`, `<instance_ID>` et `<key_ID>` par les valeurs appropriées.

**Facultatif :** vérifiez que la règle a été mise à jour.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

## Suppression d'une règle d'accès
{: #delete-policy}

Vous pouvez utiliser un identificateur de règle extrait pour supprimer une règle existante pour un utilisateur. Envoyez une demande à {{site.data.keyword.iamshort}} en exécutant la commande suivante :

```cURL
curl -X DELETE \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies/<policy_ID> \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}

Remplacez `<account_ID>`, `<user_ID>`, `<policy_ID>` et `<Admin_IAM_token>` par les valeurs appropriées.

**Facultatif :** vérifiez que la règle a été supprimée.

```cURL
curl -X GET \
  https://iam.bluemix.net/acms/v1/scopes/a%2F<account_ID>/users/<user_ID>/policies \
  -H 'Authorization: Bearer <Admin_IAM_token>' \
  -H 'Accept: application/json' \
```
{: codeblock}
