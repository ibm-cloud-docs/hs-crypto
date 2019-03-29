---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

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

# Rotation des clés
{: #rotating-keys}

Vous pouvez effectuer une rotation de vos clés racine à la demande à l'aide d'{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

La rotation des clés maîtresses n'est pas actuellement prise en charge.
{: important}

Lorsque vous effectuez une rotation de votre clé racine, vous raccourcissez sa durée de vie et limitez la quantité d'informations qu'elle protège.   

Pour savoir comment la rotation des clés vous aide à répondre aux normes de l'industrie et à respecter les meilleures pratiques en matière de cryptographie, voir [Rotation des clés](/docs/services/key-protect/concepts/key-rotation.html).

La rotation est disponible uniquement pour les clés racine.
{: tip}

## Rotation de clés racine à l'aide de l'interface graphique
{: #gui}

Si vous préférez effectuer une rotation de vos clés racine à l'aide d'une interface graphique, vous pouvez utiliser l'interface graphique utilisateur {{site.data.keyword.hscrypto}}.

[Après avoir créé ou importé vos clés racine existantes dans le service](/docs/services/hs-crypto/create-root-keys.html), procédez comme suit pour effectuer une rotation de clé :

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/){: new_window}.
2. Dans votre tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez l'instance {{site.data.keyword.hscrypto}} mise à disposition.
3. Utilisez le tableau **Clés** pour parcourir les clés du service.
4. Cliquez sur l'icône ⋮ pour ouvrir la liste des options de la clé à laquelle appliquer une rotation.
5. Dans le menu d'options, cliquez sur **Rotate key** et confirmez la rotation dans l'écran suivant.

Si vous avez initialement importé la clé racine, pour effectuer sa rotation, vous devez fournir une nouvelle matière de clé encodée en base64. Pour plus d'informations, voir [Importation de clés racine à l'aide de l'interface graphique utilisateur](/docs/services/hs-crypto/import-root-keys.html#gui).
{: tip}

## Rotation de clés racine à l'aide de l'API
{: #api}

[Après avoir désigné une clé racine dans le service](/docs/services/hs-crypto/create-root-keys.html), vous pouvez la faire tourner en envoyant un appel `POST` au point d'extrémité suivant.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service.](/docs/services/hs-crypto/access-api.html)

2. Copiez l'ID de la clé racine que vous voulez faire tourner.

4. Exécutez la commande cURL suivante pour remplacer la clé par une nouvelle matière de clé.

    ```cURL
    curl -X POST \
      'https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=rotate' \
      -H 'accept: application/vnd.ibm.kms.key_action+json' \
      -H 'authorization: Bearer <IAM_token>' \
      -H 'bluemix-instance: <instance_ID>' \
      -H 'content-type: application/vnd.ibm.kms.key_action+json' \
      -d '{
        'payload: <key_material>'
      }'
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
        <td>Abréviation de la région, comme <code>us-south</code> ou <code>eu-gb</code>, représentant la zone géographique dans laquelle votre instance de service {{site.data.keyword.hscrypto}} réside. Pour plus d'informations, consultez <a href="/docs/services/hs-crypto/regions.html#endpoints">Points d'extrémité de service régional</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>Identificateur unique de la clé racine à laquelle appliquer la rotation.</td>
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
        <td><varname>key_material</varname></td>
        <td>
          <p>Elément de clé codée en base64 que vous voulez stocker et gérer dans le service. Cette valeur est requise si vous avez initialement importé la matière de la clé lors de l'ajout de la clé au service.</p>
          <p>Pour procéder à la rotation d'une clé initialement générée dans {{site.data.keyword.hscrypto}}, omettez l'attribut <code>payload</code> et transmettez une demande entity-body vide. Pour procéder à la rotation d'une clé importée, fournissez une matière de clé répondant aux exigences suivantes :</p>
          <p>
            <ul>
              <li>La clé doit être une clé à 256, 384 ou 512 bits.</li>
              <li>Les octets de données, par exemple 32 octets pour 256 bits, doivent être encodés en base64.</li>
            </ul>
          </p>
        </td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des variables nécessaires pour la rotation d'une clé spécifiée dans {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Une demande de rotation réussie renvoie une réponse HTTP `204 No Content`, qui indique que votre clé racine a été remplacée par une nouvelle matière de clé.

4. Facultatif : vérifiez que la clé a fait l'objet d'une rotation en exécutant l'appel suivant pour parcourir les clés de votre instance de service {{site.data.keyword.hscrypto}}.

    ```cURL
    curl -X GET \
    https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys \
    -H 'accept: application/vnd.ibm.collection+json' \
    -H 'authorization: Bearer <IAM_token>' \
    -H 'bluemix-instance: <instance_ID>' \
    ```
    {: codeblock}

    Examinez la valeur `lastRotateDate` de la réponse entity-body pour connaître la date et l'heure de la dernière rotation de votre clé.
