---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-13"

Keywords: view keys, key configuration, key type

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Affichage des clés
{: #view-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} fournit un système centralisé pour afficher et gérer vos clés de chiffrement et en effectuer un audit. Cette dernière opération ainsi que les restrictions d'accès aux clés vous permettent d'assurer la sécurité de vos ressources.
{: shortdesc}

Effectuez un audit régulier de la configuration de vos clés :

- Voyez quand les clés ont été créées et déterminez s'il n'est pas temps d'effectuer une rotation.
- Surveillez les appels API dans {{site.data.keyword.hscrypto}} avec {{site.data.keyword.cloudaccesstrailshort}}.
- Vérifiez quels sont les utilisateurs qui ont accès aux clés et assurez-vous que leur niveau d'accès est approprié.

Pour plus d'informations sur l'audit d'accès à vos ressources, voir la [gestion de l'accès utilisateur avec Cloud IAM](/docs/services/hs-crypto/manage-access.html).

## Affichage des clés avec l'interface graphique utilisateur
{: #view-key-gui}

Si vous préférez examiner les clés de votre service à l'aide d'une interface graphique, vous pouvez utiliser le tableau de bord {{site.data.keyword.hscrypto}}.

[Après avoir créé ou importé les clés existantes dans le service](/docs/services/hs-crypto/create-root-keys.html), vous pouvez les afficher en procédant comme suit :

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/).
2. Accédez à **Menu** &gt; **Liste de ressources** pour afficher la liste de vos ressources.
3. Dans la liste de ressources {{site.data.keyword.cloud_notm}}, sélectionnez votre instance {{site.data.keyword.hscrypto}} mise à disposition.
3. Parcourez les caractéristiques générales de vos clés dans la page Détails de l'application :

    <table>
      <tr>
        <th>Colonne</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Nom</td>
        <td>Alias unique et lisible qui est affecté à votre clé.</td>
      </tr>
      <tr>
        <td>ID</td>
        <td>ID de clé unique affecté à votre clé par {{site.data.keyword.hscrypto}}. Vous pouvez utiliser la valeur de l'ID pour appeler le service avec l'API [{{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/hs-crypto).</td>
      </tr>
      <tr>
        <td>Etat</td>
        <td>[Etat des clés](/docs/services/key-protect/concepts/key-states.html) basé sur le document [NIST Special Publication 800-57, Recommendation for Key Management ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-57pt1r4.pdf). Ces états sont <i>Pré-actif</i>, <i>Actif</i>, <i>Désactivé</i> et <i>Détruit</i>.</td>
      </tr>
      <tr>
        <td>Type</td>
        <td>[Type de clé](/docs/services/key-protect/concepts/envelope-encryption.html#key-types) qui décrit la fonction définie de la clé dans le service.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description du tableau <b>Clés</b></caption>
    </table>

## Affichage des clés avec l'API
{: #view-key-api}

Vous pouvez extraire le contenu de vos clés à l'aide de l'API {{site.data.keyword.hscrypto}}.

### Extraction d'une liste de clés
{: #retrieve-keys-api}

Pour obtenir une vue globale, vous pouvez parcourir les clés qui sont gérées dans votre instance {{site.data.keyword.hscrypto}} mise à disposition en soumettant une demande `GET` au point d'extrémité suivant.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service](/docs/services/hs-crypto/access-api.html).

2. Exécutez la commande cURL suivante pour afficher les caractéristiques générales de vos clés :

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}
    <!--    To work with keys within a Cloud Foundry org and space in your account, replace `Bluemix-Instance` with the appropriate `Bluemix-org` and `Bluemix-space` headers. [For more information, see the {{site.data.keyword.hscrypto}} API reference doc ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
        {: tip} -->

    Remplacez les variables dans l'exemple de demande en fonction du tableau suivant :
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>Abréviation de la région, comme <code>us-south</code> ou <code>eu-gb</code>, représentant la zone géographique dans laquelle votre instance de service {{site.data.keyword.hscrypto}} réside. Pour plus d'informations, voir <a href="/docs/services/hs-crypto/regions.html#endpoints">Points d'extrémité de service régional</a>.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Votre jeton d'accès {{site.data.keyword.cloud_notm}}. Incluez l'ensemble du contenu du jeton <code>IAM</code>, y compris la valeur Bearer, dans la demande cURL. Pour plus d'informations, voir <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Extraction d'un jeton d'accès</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>Identificateur unique affecté à votre instance de service {{site.data.keyword.hscrypto}}. Pour plus d'informations, voir <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Extraction d'un ID d'instance</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>Facultatif: identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 2. Description des variables requises pour afficher des clés via l'API {{site.data.keyword.hscrypto}}</caption>
    </table>

    Une demande `GET /v2/keys` qui aboutit renvoie une collection des clés qui sont disponibles dans votre instance de service {{site.data.keyword.hscrypto}}.

    ```
    {
      "metadata": {
        "collectionType": "application/vnd.ibm.collection+json",
        "collectionTotal": 2
      },
    "resources": [
      {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Standard key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": true,
          "imported": false
        },
        {
          "id": "...",
          "type": "application/vnd.ibm.kms.key+json",
          "name": "Root key",
          "description": "...",
          "state": 1,
          "crn": "...",
          "algorithmType": "AES",
          "createdBy": "...",
          "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastUpdateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "lastRotateDate": "YYYY-MM-DDTHH:MM:SSZ",
          "algorithmMetadata": {
            "bitLength": "256",
            "mode": "GCM"
          },
          "extractable": false,
          "imported": true
        }
      ]
    }
    ```
    {:screen}

    Par défaut, `GET /keys` renvoie vos 2000 premières clés, mais vous pouvez ajuster cette limite à l'aide du paramètre `limit` lors de l'interrogation. Pour en savoir plus sur `limit` et `offset`, voir [Extraction d'un sous-ensemble de clés](#retrieve_subset_keys_api).
    {: tip}

### Extraction d'un sous-ensemble de clés
{: #retrieve-subset-keys-api}

En spécifiant les paramètres `limit` et `offset` lors de l'interrogation, vous pouvez extraire un sous-ensemble de vos clés, à partir de la valeur `offset` que vous spécifiez.

Par exemple, vous pouvez avoir un total de 3000 clés stockées dans votre instance de service {{site.data.keyword.hscrypto}}, mais vous souhaitez extraire les clés 200 à 300 lorsque vous effectuez une demande `GET /keys`.

Vous pouvez utiliser l'exemple de demande suivant pour extraire un autre ensemble de clés :

  ```cURL
  curl -X GET \
  https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys?offset=<offset>&limit=<limit> \
  -H 'accept: application/vnd.ibm.collection+json' \
  -H 'authorization: Bearer <IAM_token>' \
  -H 'bluemix-instance: <instance_ID>' \
  -H 'correlation-id: <correlation_ID>' \
  ```
  {: codeblock}

  Remplacez les variables `limit` et `offset` dans votre demande conformément au tableau suivant :
  <table>
    <tr>
      <th>Variable</th>
      <th>Description</th>
    </tr>
    <tr>
      <td><p><varname>offset</varname></p></td>
      <td>
        <p>Optionnel : nombre de clés à sauter.</p>
        <p>Par exemple, si vous avez 50 clés dans votre instance et que vous souhaitez répertorier les clés 26 à 50, utilisez <code>../keys?offset=25</code>. Vous pouvez également apparier <code>offset</code> avec <code>limit</code> afin de parcourir vos ressources disponibles.</p>
      </td>
    </tr>
    <tr>
      <td><p><varname>limit</varname></p></td>
      <td>
        <p>Optionnel : nombre de clés à extraire.</p>
        <p>Par exemple, si vous avez 100 clés dans votre instance et que vous souhaitez répertorier 10 clés seulement, utilisez <code>../keys?limit=10</code>. La valeur maximale pour <code>limit</code> est 5000.</p>
      </td>
    </tr>
    <caption style="caption-side:bottom;">Tableau 2. Description des variables <code>limit</code> et <code>offset</code></caption>
  </table>

Pour les remarques d'utilisation, reportez-vous aux exemples suivants relatifs à la configuration de vos paramètres de requête `limit` et `offset`.

<table>
  <tr>
    <th>URL</th>
    <th>Description</th>
  </tr>
  <tr>
    <td><code>.../keys</code></td>
    <td>Répertorie toutes vos ressources disponibles, jusqu'au 2000 premières clés.</td>
  </tr>
  <tr>
    <td><code>.../keys?limit=10</code></td>
    <td>Répertorie les 10 premières clés.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=25&limit=50</code></td>
    <td>Répertorie les clés 26 à 50.</td>
  </tr>
  <tr>
    <td><code>.../keys?offset=3000&limit=50</code></td>
    <td>Répertorie les clés 3001 à 3050.</td>
  </tr>
  <caption style="caption-side:bottom;">Tableau 3. Remarques d'utilisation relatives aux paramètres de requête limit et offset</caption>
</table>

Le paramètre offset correspond à l'emplacement d'une clé spécifique dans un jeu de données. La valeur `offset` est basée sur zéro, ce qui signifie que la 10ème clé de chiffrement dans un jeu de données se situe à l'emplacement 9.
{: tip}

### Extraction d'une clé via son ID
{: #retrieve-key-api}

Pour afficher des informations détaillées sur une clé spécifique, vous pouvez envoyer un appel `GET` au point d'extrémité suivant.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service](/docs/services/hs-crypto/access-api.html).

2. Extrayez l'ID de la clé que vous souhaitez gérer ou à laquelle vous souhaitez accéder.

    La valeur d'ID permet d'accéder à des informations détaillées sur la clé, telles que sa matière (octets composant la clé proprement dite). Vous pouvez extraire l'ID d'une clé spécifique en soumettant une demande `GET /v2/keys` ou en accédant à l'interface graphique utilisateur {{site.data.keyword.hscrypto}}.

3. Exécutez la commande cURL suivante pour obtenir des détails sur votre clé et sa matière.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID> \
      -H 'accept: application/vnd.ibm.kms.key+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

    Remplacez les variables dans l'exemple de demande en fonction du tableau suivant :

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>Abréviation de la région, comme <code>us-south</code> ou <code>eu-gb</code>, représentant la zone géographique dans laquelle votre instance de service {{site.data.keyword.hscrypto}} réside. Pour plus d'informations, voir <a href="/docs/services/hs-crypto/regions.html#endpoints">Points d'extrémité de service régional</a>.</td>
      </tr>
      <tr>
        <td><varname>IAM_token</varname></td>
        <td>Votre jeton d'accès {{site.data.keyword.cloud_notm}}. Incluez l'ensemble du contenu du jeton <code>IAM</code>, y compris la valeur Bearer, dans la demande cURL. Pour plus d'informations, voir <a href="/docs/services/hs-crypto/access-api.html#retrieve-token">Extraction d'un jeton d'accès</a>.</td>
      </tr>
      <tr>
        <td><varname>instance_ID</varname></td>
        <td>Identificateur unique affecté à votre instance de service {{site.data.keyword.hscrypto}}. Pour plus d'informations, voir <a href="/docs/services/hs-crypto/access-api.html#retrieve-instance-ID">Extraction d'un ID d'instance</a>.</td>
      </tr>
      <tr>
        <td><varname>correlation_ID</varname></td>
        <td>Facultatif: identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>Identificateur de la clé que vous avez extraite à l'[étape 1](#retrieve-keys-api).</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 4. Description des variables requises pour afficher une clé spécifiée à l'aide de l'API {{site.data.keyword.hscrypto}}</caption>
    </table>

    Une réponse `GET v2/keys/<key_ID>` qui aboutit renvoie des détails sur votre clé et sa matière (octets). L'objet JSON suivant présente un exemple de valeur renvoyée pour une clé standard :

    ```
    {
        "metadata": {
            "collectionTotal": 1,
            "collectionType": "application/vnd.ibm.kms.key+json"
        },
    "resources": [
      {
            "id": "...",
            "type": "application/vnd.ibm.kms.key+json",
            "name": "Standard key",
            "description": "...",
            "state": 1,
            "crn": "...",
            "algorithmType": "AES",
            "payload": "...",
            "createdBy": "...",
            "creationDate": "YYYY-MM-DDTHH:MM:SSZ",
            "algorithmMetadata": {
                "bitLength": "256",
                "mode": "GCM"
            },
            "extractable": true,
            "imported": false
        }
      ]
    }
    ```
    {:screen}

    Pour obtenir une description détaillée des paramètres disponibles, voir la {{site.data.keyword.hscrypto}} [documentation de référence de l'API REST ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
