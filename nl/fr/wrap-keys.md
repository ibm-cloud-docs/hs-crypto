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

# Encapsulage de clés
{: #wrap-keys}

Si vous êtes un utilisateur privilégié, vous pouvez gérer et protéger vos clés de chiffrement avec une clé racine à l'aide de l'API {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.
{: shortdesc}

Lorsque vous encapsulez une clé DEK (Data Encryption Key) avec une clé racine, {{site.data.keyword.hscrypto}}
associe la puissance de plusieurs algorithmes pour protéger la confidentialité et l'intégrité des données chiffrées.  

Pour découvrir comment l'encapsulage de clés peut vous aider à contrôler la sécurité des données au repos dans le cloud, reportez-vous à la rubrique [Chiffrement d'enveloppe](/docs/services/key-protect/concepts/envelope-encryption.html).

## Encapsulage de clés à l'aide de l'API
{: #wrap-keys-api}

Vous pouvez protéger la clé DEK indiquée avec une clé racine que vous gérez dans {{site.data.keyword.hscrypto}}.

Quand vous fournissez une clé racine pour l'encapsulage, vérifiez qu'il s'agit d'une clé racine de 128, 192 ou 256 bits pour que l'opération aboutisse. Si vous créez une clé racine dans le service, {{site.data.keyword.hscrypto}} génère, à partir de son module HSM, une clé de 256 bits, prise en charge par l'algorithme AES-GCM.

[Après avoir désigné une clé racine dans le service](/docs/services/hs-crypto/create-root-keys.html), vous pouvez encapsuler une clé DEK avec un chiffrement avancé en soumettant un appel `POST` au point d'extrémité suivant.

```
https://<region>.hs-crypto.cloud.ibm.com:<port>/api/v2/keys/<key_ID>?action=wrap
```
{: codeblock}

1. [Extrayez vos données d'authentification et de service afin d'utiliser les clés dans le service.](/docs/services/hs-crypto/access-api.html)

2. Copiez la matière (octets) de la clé DEK que vous voulez gérer et protéger.

    Si vous avez des privilèges de responsable ou d'auteur pour l'instance de service {{site.data.keyword.hscrypto}}, [vous pouvez extraire
la matière de la clé en soumettant une demande GET /v2/keys/<key_ID>](/docs/services/hs-crypto/view-keys.html#api).

3. Copiez l'ID de la clé racine que vous voulez utiliser pour l'encapsulage.

4. Exécutez la commande cURL suivante pour protéger la clé avec une opération d'encapsulage :

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

    Remplacez les variables dans l'exemple de demande en fonction du tableau suivant :

    <table>
      <tr>
        <th>Variable</th>
        <th>Description</th>
      </tr>
      <tr>
        <td><varname>region</varname></td>
        <td>Abréviation de la région, comme <code>us-south</code> ou <code>eu-gb</code>, représentant la zone géographique dans laquelle votre instance de service {{site.data.keyword.hscrypto}}
réside. Pour plus d'informations, voir <a href="/docs/services/hs-crypto/regions.html#endpoints">Points d'extrémité de service régional</a>.</td>
      </tr>
      <tr>
        <td><varname>key_ID</varname></td>
        <td>ID unique de la clé racine que vous souhaitez utiliser pour l'encapsulage.</td>
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
        <td><varname>return_preference</varname></td>
        <td><p>En-tête qui modifie le comportement du serveur pour les opérations <code>POST</code> et <code>DELETE</code>.</p><p>Lorsque vous affectez la valeur <code>return=minimal</code> à la variable <em>return_preference</em>, le service renvoie uniquement les métadonnées de la clé, comme le nom et l'ID de la clé, dans la section entity-body de la réponse. Si cette variable a pour valeur <code>return=representation</code>, le service renvoie à la fois la matière de la clé et ses métadonnées.</p></td>
      </tr>
      <tr>
        <td><varname>data_key</varname></td>
        <td>Optionnel : Matière (octets) de la clé DEK que vous souhaitez gérer et protéger. La valeur <code>plaintext</code> doit être codée en base64. Pour générer une clé DEK, omettez l'attribut <code>plaintext</code>. Le service génère un texte brut aléatoire (32 octets) et l'encapsule.</td>
      </tr>
      <tr>
        <td><varname>additional_data</varname></td>
        <td>Optionnel : Données d'authentification additionnelles (AAD) utilisées pour renforcer la sécurité de la clé. Chaque chaîne peut inclure jusqu'à 255 caractères. Si vous indiquez des données d'authentification supplémentaires lorsque vous soumettez un appel d'encapsulage au service, vous devez indiquer les mêmes données d'authentification supplémentaires lors de l'appel de désencapsulage ultérieur.<br></br>Important : le service {{site.data.keyword.hscrypto}}
ne sauvegarde pas les données d'authentification supplémentaires. Si vous indiquez des données d'authentification supplémentaires, sauvegardez ces données dans un emplacement sécurisé afin de pouvoir y accéder et fournir les mêmes données lors des demandes de désencapsulage ultérieures.</td>
      </tr>
      <caption style="caption-side:bottom;">Tableau 1. Description des variables nécessaires pour encapsuler une clé spécifiée dans {{site.data.keyword.hscrypto}}.</caption>
    </table>

    La clé encapsulée, qui contient la matière de la clé encodée en base64, est renvoyée dans la section entity-body de la réponse. L'objet JSON suivant présente un exemple de valeur renvoyée.

    ```
    {
      "plaintext": "VGhpcyBpcyBhIHNlY3JldCBtZXNzYWdlLg==",
      "ciphertext": "eyJjaXBoZXJ0ZXh0Ijoic3VLSDNRcmdEZjdOZUw4Rkc4L2FKYjFPTWcyd3A2eDFvZlA4MEc0Z1B2RmNrV2g3cUlidHphYXU0eHpKWWoxZyIsImhhc2giOiJiMmUyODdkZDBhZTAwZGZlY2Q3OGJmMDUxYmNmZGEyNWJkNGUzMjBkYjBhN2FjNzVhMWYzZmNkMDZlMjAzZWYxNWM5MTY4N2JhODg2ZWRjZGE2YWVlMzFjYzk2MjNkNjA5YTRkZWNkN2E5Y2U3ZDc5ZTRhZGY1MWUyNWFhYWM5MjhhNzg3NmZjYjM2NDFjNTQzMTZjMjMwOGY2MThlZGM2OTE3MjAyYjA5YTdjMjA2YzkxNTBhOTk1NmUxYzcxMTZhYjZmNmQyYTQ4MzZiZTM0NTk0Y2IwNzJmY2RmYTk2ZSJ9"
      "aad": ["data1", "data2"]
    }
    ```
    {:screen}
