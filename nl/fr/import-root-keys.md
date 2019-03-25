---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: root keys, import keys, symmetric key, Hyper Protect Crypto Services GUI

subcollection: hs-crypto
---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Importation de clés racine
{: #import-root-keys}

Vous pouvez utiliser
{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} pour sécuriser des clés racine existantes à l'aide de l'interface graphique {{site.data.keyword.hscrypto}} ou à l'aide d'un programme via l'API {{site.data.keyword.hscrypto}}.
{: shortdesc}

Les clés racine sont des clés d'encapsulage de clés symétriques qui permettent d'assurer la sécurité des données chiffrées dans le cloud. Pour plus d'informations sur les clés racine, voir [Chiffrement d'enveloppe](/docs/services/key-protect/concepts/envelope-encryption.html).

## Importation de clés racine à l'aide de l'interface graphique
{: #gui}

[Après avoir créé une instance du service](/docs/services/
hs-crypto/provision.html), effectuez les étapes suivantes pour ajouter votre clé racine existante avec l'interface graphique de {{site.data.keyword.hscrypto}}.

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/){: new_window}.
2. Dans votre tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez l'instance {{site.data.keyword.hscrypto}} mise à disposition.
3. Pour importer une clé, cliquez sur **Add key** et sélectionnez la fenêtre **Enter existing key**.

    Indiquez les détails relatifs à la clé :

    <table>
      <tr>
        <th>Paramètre</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>Name</td>
        <td>
          <p>Alias unique et lisible permettant d'identifier facilement votre clé.</p>
          <p>Pour protéger votre vie privée, assurez-vous que le nom de clé ne contient pas d'informations identifiant la personne, comme votre nom ou votre emplacement.</p>
        </td>
      </tr>
      <tr>
        <td>Key type</td>
        <td><a href="/docs/services/key-protect/concepts/envelope-encryption.html#key-types">Type de clé</a> que vous souhaitez gérer dans {{site.data.keyword.hscrypto}}. Dans la liste des types de clés, sélectionnez <b>Root key</b>.</td>
      </tr>
      <tr>
        <td>Key material</td>
        <td>
          <p>Matière de clé encodée en base64, telle qu'une clé d'encapsulage de clé existante, que vous souhaitez stocker et gérer dans le service.</p>
          <p>Vérifiez que la matière de la clé remplit les conditions suivantes :</p>
          <p>
            <ul>
              <li>La clé doit être une clé à 256, 384 ou 512 bits.</li>
              <li>Les octets de données, par exemple 32 octets pour 256 bits, doivent être encodés en base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des paramètres <b>Enter existing key</b></caption>
    </table>

4. Une fois les détails de la clé indiqués, cliquez sur **Add new key** pour confirmer l'opération.

## Importation de clés racine avec l'API
{: #api}

Ajoutez votre clé racine existante en soumettant un appel `POST` au point d'extrémité suivant.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service](/docs/services/hs-crypto/access-api.html).

1. Appelez l'API [{{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window} à l'aide de la commande cURL suivante. 

    ```cURL
    curl -X POST \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key+json' \
      -H 'correlation-id: <correlation_ID>' \
      -d '{
     "metadata": {
       "collectionType": "application/vnd.ibm.kms.key+json",
       "collectionTotal": 1
     },
     "resources": [
       {
       "type": "application/vnd.ibm.kms.key+json",
       "name": "<key_alias>",
       "description": "<key_description>",
       "expirationDate": "<YYYY-MM-DDTHH:MM:SS.SSZ>",
       "payload": "<key_material>",
       "extractable": <key_type>
       }
     ]
    }'
    ```
    {: codeblock}

    Pour utiliser les clés dans une organisation et un espace Cloud Foundry de votre compte, remplacez `Bluemix-Instance` par les en-têtes `Bluemix-org` et `Bluemix-space` appropriés. [Pour plus d'informations, consultez la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/hs-crypto){: new_window}.
    {: tip}

    Remplacez les variables dans l'exemple de demande en fonction du tableau suivant :
    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>Abréviation de la région, comme <code>us-south</code> ou <code>eu-gb</code>, représentant la zone géographique dans laquelle votre instance de service {{site.data.keyword.hscrypto}} réside. Pour plus d'informations, consultez <a href="/docs/services/hs-crypto/regions.html#endpoints">Points d'extrémité de service régional</a>.</td>
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
        <td>Identificateur unique qui est utilisé pour suivre et corréler des transactions.</td>
      </tr>
      <tr>
        <td><varname>key_alias</varname></td>
        <td>
          <p>Nom lisible permettant d'identifier facilement votre clé.</p>
          <p>Important : pour protéger votre vie privée, ne stockez aucune donnée personnelle comme métadonnées pour votre clé.</p>
        </td>
      </tr>
      <tr>
        <td><varname>key_description</varname></td>
        <td>
          <p>Facultatif : description développée de votre clé.</p>
          <p>Important : pour protéger votre vie privée, ne stockez aucune donnée personnelle comme métadonnées pour votre clé.</p>
        </td>
      </tr>
      <tr>
        <td><varname>YYYY-MM-DD</varname><br><varname>HH:MM:SS.SS</varname></td>
        <td>Facultatif : date et heure d'expiration de la clé dans le système, au format RFC 3339. Si l'attribut <code>expirationDate</code> est omis, la clé n'expire pas.</td>
      </tr>
      <tr>
        <td><varname>key_material</varname></td>
        <td>
          <p>Matière de clé encodée en base64, telle qu'une clé d'encapsulage de clé existante, que vous souhaitez stocker et gérer dans le service.</p>
          <p>Vérifiez que la matière de la clé remplit les conditions suivantes :</p>
          <p>
            <ul>
              <li>La clé doit être une clé à 256, 384 ou 512 bits.</li>
              <li>Les octets de données, par exemple 32 octets pour 256 bits, doivent être encodés en base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <tr>
        <td><varname>key_type</varname></td>
        <td>
          <p>Valeur booléenne qui détermine si la matière de la clé peut quitter le service.</p>
          <p>Lorsque vous affectez la valeur <code>false</code> à l'attribut <code>extractable</code>, le service désigne la clé en tant que clé racine disponible pour les opérations <code>wrap</code> ou<code>unwrap</code>.</p>
        </td>
      </tr>
        <caption style="caption-side:bottom;">Tableau 1. Description des variables requises pour ajouter une clé racine à l'aide de l'API {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Pour protéger la confidentialité de vos données personnelles, évitez d'entrer des informations identifiant la personne, comme votre nom ou votre emplacement, lorsque vous ajoutez des clés au service. Pour visualiser d'autres exemples d'informations identifiant la personne, voir la section 2.2 du document [NIST Special Publication 800-122 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-122.pdf){: new_window}.
    {: tip}

    Une réponse `POST /v2/keys` qui aboutit renvoie la valeur de l'ID de la clé, ainsi que d'autres métadonnées. L'ID est un identificateur unique qui est affecté à la clé et qui est utilisé pour les appels adressés ultérieurement à {{site.data.keyword.hscrypto}}.

2. Facultatif : Vérifiez que la clé a été ajoutée en exécutant l'appel suivant pour parcourir les clés de l'instance de service {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
      https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
      -H 'accept: application/vnd.ibm.collection+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'correlation-id: <correlation_ID>' \
    ```
    {: codeblock}

**Remarque :** Lorsque vous ajoutez une clé racine existante au service, la clé reste dans les limites du service {{site.data.keyword.hscrypto}} et sa matière ne peut pas être extraite.

### Etapes suivantes

- Pour plus d'informations sur la protection de clés à l'aide du chiffrement d'enveloppe, voir [Encapsulage de clés](/docs/services/hs-crypto/wrap-keys.html).
- Pour plus d'informations sur la gestion de vos clés à l'aide d'un programme, [consultez la documentation de référence de l'API {{site.data.keyword.hscrypto}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/apidocs/
hs-crypto){: new_window}.

