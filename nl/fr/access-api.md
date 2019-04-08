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

# Accès à l'API
{: #access-api}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} s'intègre avec l'API REST de {{site.data.keyword.keymanagementserviceshort}}, qui peut être utilisée avec n'importe quel langage de programmation pour stocker, extraire et générer des clés.
{: shortdesc}

Pour utiliser l'API, vous devez générer vos données d'authentification et de service.

## Extraction d'un jeton d'accès
{: #retrieve-token}

Vous pouvez vous authentifier auprès de {{site.data.keyword.hscrypto}} en extrayant un jeton d'accès de {{site.data.keyword.iamshort}}. Avec un [ID de service](/docs/iam/serviceid.html#serviceids), vous pouvez utiliser l'API {{site.data.keyword.hscrypto}} au nom du service ou de l'application au sein ou en dehors de l'environnement {{site.data.keyword.cloud_notm}} sans avoir à partager vos données d'identification utilisateur personnelles.  

<!-- If you want to authenticate with your user credentials, you can retrieve your token by running `ibmcloud iam oauth-tokens` in the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli/index.html#overview).
{: tip} -->

Pour extraire un jeton d'accès, procédez comme suit :

1. Dans la console {{site.data.keyword.cloud_notm}}, accédez à **Gérer** &gt; **Sécurité** &gt; **Identity and Access** &gt; **ID de service**. Suivez la procédure indiquée pour [créer un ID de service](/docs/iam/serviceid.html#creating-a-service-id).
2. Utilisez le menu **Actions** afin de [définir une règle d'accès pour votre nouvel ID de service](/docs/iam/serviceidaccess.html).

    Pour plus d'informations sur la gestion des accès pour les ressources {{site.data.keyword.hscrypto}}, voir [Rôles et droits](/docs/services/hs-crypto/manage-access.html#roles).
3. Utilisez la section **Clés d'API** pour [créer une clé d'API à associer à l'ID de service](/docs/iam/serviceid_keys.html#serviceidapikeys). Sauvegardez la clé d'API en la téléchargeant dans un emplacement sécurisé.
4. Appelez l'API {{site.data.keyword.iamshort}} pour extraire votre jeton d'accès.

    ```cURL
    curl -X POST \
      "https://iam.bluemix.net/identity/token" \
      -H "Content-Type: application/x-www-form-urlencoded" \
      -H "Accept: application/json" \
      -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<API_KEY>" \
    ```
    {: codeblock}

    Dans la demande, remplacez `<API_KEY>` par la clé d'API que vous avez créée à l'étape 3. L'exemple partiel suivant présente la sortie du jeton :

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

    Utilisez l'ensemble de la valeur `access_token` avec le préfixe du type de jeton _Bearer_ pour gérer les clés de votre service à l'aide d'un programme via l'API {{site.data.keyword.hscrypto}}.

    Les jetons d'accès sont valides pendant 1 heure, mais vous pouvez les régénérer si besoin. Pour maintenir l'accès au service, actualisez régulièrement le jeton d'accès pour votre clé d'API en appelant l'API {{site.data.keyword.iamshort}}.   
    {: tip }

## Extraction de l'ID d'instance
{: #retrieve-instance-ID}

Vous pouvez extraire les informations d'identification de votre instance de service {{site.data.keyword.hscrypto}} à l'aide de l'[interface de ligne de commande d'{{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview). Utilisez un ID d'instance pour gérer vos clés de chiffrement au sein d'une instance {{site.data.keyword.hscrypto}} spécifique dans votre compte.

1. Connectez-vous à {{site.data.keyword.cloud_notm}} avec l'[interface de ligne de commande d'{{site.data.keyword.cloud_notm}}](/docs/cli/index.html#overview).

    ```sh
    ibmcloud login
    ```
    {: pre}

    **Remarque :** si la connexion échoue, exécutez la commande `ibmcloud login --sso` pour effectuer une nouvelle tentative. Le paramètre `--sso` est requis quand vous vous connectez avec un ID fédéré. Si cette option est utilisée, accédez au lien répertorié dans la sortie d'interface de ligne de commande pour générer un code d'accès unique.

2. Sélectionnez le compte qui inclut l'instance mise à disposition.

    Vous pouvez exécuter `ibmcloud resource service-instances` pour répertorier toutes les instances mises à disposition dans votre compte.

3. Extrayez le nom CRN (Cloud Resource Name) qui identifie de manière unique l'instance de service {{site.data.keyword.hscrypto}}.

    ```sh
    ibmcloud resource service-instance <instance_name> --id
    ```
    {: pre}

    Remplacez `<instance_name>` par l'alias unique que vous avez affecté à votre instance {{site.data.keyword.hscrypto}}. L'exemple partiel suivant présente la sortie de l'interface de ligne de commande. La valeur _42454b3b-5b06-407b-a4b3-34d9ef323901_ est un exemple d'ID d'instance.

    ```
    crn:v1:bluemix:public:kms:us-south:a/f047b55a3362ac06afad8a3f2f5586ea:42454b3b-5b06-407b-a4b3-34d9ef323901::
    ```
    {: screen}

## Extraction des informations de connexion
{: #retrieve-connection-info}

Avant d'appeler une API {{site.data.keyword.keymanagementserviceshort}} quelle qu'elle soit, appelez l'API **Retrieve the connection info** afin de récupérer les informations de connexion. Pour plus d'informations, voir [ la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

## Mise en forme de la demande d'API
{: #form-api-request}

Lorsque vous soumettez un appel d'API au service, structurez votre demande d'API en fonction de la manière dont votre instance {{site.data.keyword.hscrypto}} a été initialement mise à disposition.

Pour générer une demande, associez un [point d'extrémité de service régional](/docs/services/hs-crypto/regions.html) aux données d'authentification appropriées. Par exemple, si vous avez créé une instance de service pour la région `us-south`, utilisez le point d'extrémité et les en-têtes API ci-dessous pour parcourir les clés du service :

```cURL
curl -X GET \
    https://us-south.hs-crypto.cloud.ibm.com:<port>/api/v2/key \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <access_token>' \
    -H 'bluemix-instance: <instance_ID>' \
```
{: codeblock}

### Etapes suivantes
{: #api-next}

Pour plus d'informations sur la gestion de vos clés à l'aide d'un programme, [voir la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto){: new_window}.

<!-- To see an example of how keys stored in {{site.data.keyword.hscrypto}} can work to encrypt and decrypt data, [check out the sample app in GitHub ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Bluemix/key-protect-helloworld-python){: new_window}. -->
