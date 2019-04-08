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

# Suppression de clés
{: #deleting-keys}

Vous pouvez utiliser {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} pour supprimer une clé de chiffrement et son contenu, si vous êtes administrateur de l'espace {{site.data.keyword.cloud_notm}} ou de l'instance de service {{site.data.keyword.hscrypto}}.
{: shortdesc}

**Important :** : lorsque vous supprimez une clé, vous détruisez définitivement son contenu et les données associées. L'action est irréversible. La destruction de ressources n'est pas recommandée dans les environnements de production, mais peut être utile dans les environnements temporaires tels que les environnements de test ou d'assurance qualité.

## Suppression de clés avec l'interface graphique utilisateur
{: #delete-keys-gui}

Si vous préférez supprimer vos clés de chiffrement à l'aide d'une interface graphique, vous pouvez utiliser l'interface graphique utilisateur {{site.data.keyword.hscrypto}}.

[Après avoir créé ou importé vos clés existantes dans le service](/docs/services/hs-crypto/create-root-keys.html), procédez comme suit pour supprimer une clé :

1. [Connectez-vous à la console {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/){: new_window}.
2. Accédez à **Menu** &gt; **Liste de ressources** pour afficher la liste de vos ressources.
3. Dans la liste de ressources {{site.data.keyword.cloud_notm}}, sélectionnez votre instance {{site.data.keyword.hscrypto}} mise à disposition.
4. Utilisez le tableau **Clés** pour parcourir les clés du service.
5. Cliquez sur l'icône pour ouvrir la liste des options de la clé à supprimer..
6. Dans le menu d'options, cliquez sur **Supprimer la clé** et confirmez la suppression dans l'écran suivant.

Une fois supprimée, la clé passe à l'état _Détruit_. Les clés qui se trouvent dans cet état sont irrécupérables. Les métadonnées associées à la clé, comme la date de suppression de la clé, sont conservées dans la base de données {{site.data.keyword.hscrypto}}.

## Suppression de clés avec l'API
{: #api}

Pour supprimer une clé et son contenu, envoyez un appel `DELETE` au point d'extrémité suivant.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>
```

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service](/docs/services/hs-crypto/access-api.html).

2. Extrayez l'ID de la clé à supprimer.

    Vous pouvez extraire l'ID d'une clé spécifique en soumettant une demande `GET /v2/keys/` ou en affichant vos clés dans le tableau de bord {{site.data.keyword.hscrypto}}.

3. Exécutez la commande cURL suivante pour supprimer définitivement la clé et son contenu :

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
        <td><varname>key_ID</varname></td>
        <td>Identificateur unique de la clé à supprimer.</td>
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
        <td><varname>return_preference</varname></td>
        <td><p>En-tête qui modifie le comportement du serveur pour les opérations <code>POST</code> et <code>DELETE</code>.</p><p>Lorsque vous affectez la valeur <code>return=minimal</code> à la variable <em>return_preference</em>, le service renvoie une réponse indiquant que la suppression a abouti. Si cette variable a pour valeur <code>return=representation</code>, le service renvoie à la fois la matière de la clé et ses métadonnées.</p></td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des variables requises pour supprimer des clés via l'API {{site.data.keyword.hscrypto}}.</caption>
    </table>

    Si la variable _return_preference_ a pour valeur `return=representation`, les détails de la demande `DELETE` sont renvoyés dans la section entity-body de la réponse. L'objet JSON suivant présente un exemple de valeur renvoyée.
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

    Pour obtenir une description détaillée des paramètres disponibles, voir la {{site.data.keyword.hscrypto}} [documentation de référence de l'API REST ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/hs-crypto){: new_window}.
