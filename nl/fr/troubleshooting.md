---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: troubleshoot, problems, known issues

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:codeblock: .codeblock}

# Traitement des incidents
{: #troubleshooting}

Parmi les problèmes généraux liés à l'utilisation de {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}, citons notamment l'indication d'en-têtes ou de données d'identification valides lorsque vous interagissez avec l'API. Dans de nombreux cas, ces problèmes peuvent être résolus en quelques opérations simples.
{: shortdesc}

## Une erreur se produit lors de la suppression d'une instance initialisée de {{site.data.keyword.hscrypto}}

Il est possible que vous receviez une erreur similaire à la suivante lorsque vous supprimez une instance initialisée de {{site.data.keyword.hscrypto}} :

```
FAILED
Error response from server. Status code: 400; description: 400 DELETE https://zCryptoBroker.mybluemix.net/v2/service_instances/ failed with error status 409. Conflict.
```
{: codeblock}
{: tsSymptoms}

Vous n'avez pas effacé (mis à zéro) l'instance initialisée de {{site.data.keyword.hscrypto}} avant de la supprimer.
{: tsCauses}

Exécutez la commande suivante avant de supprimer l'instance :
{: tsResolve}

```
ibmcloud tke domain-zeroize
```
{: codeblock}

## Jeton non autorisé après exécution de commandes en lien avec le plug-in Trusted Key Entry

Après l'exécution de commandes `tke` dans l'interface de ligne de commande, il est possible que vous receviez des messages similaires aux suivants :

```
ibmcloud tke domains
FAILED
Error querying crypto instances.
Status code: 401
Message: Unauthorized
Your access token is invalid, expired, or does not have the necessary permissions to access this instance.`
```
{: codeblock}
{: tsSymptoms}

Le jeton n'est pas régénéré.
{: tsCauses}

Connectez-vous à nouveau à {{site.data.keyword.cloud_notm}} avec la commande `ibmcloud login` pour régénérer le jeton.
{: tsResolve}

## Erreur `CKR_IBM_WK_NOT_INITIALIZED` lors de l'utilisation de l'interface de ligne de commande ou de l'API

Lorsque vous utilisez l'interface de ligne de commande ou l'API, il est possible que vous receviez un message similaire au suivant :

```
ibmcloud kp -i <service_instance_id> wrap <key_id>
Wrapping key...
FAILED
Bad Request: rpc error: code = Unknown desc = GRPC Return Code: [0X434B525F484F53545F4D454D4F5259]  GRPC Message: [Got error CKR_IBM_WK_NOT_INITIALIZED, from libep11.so in m_UnwrapKey]
```
{: codeblock}
{: tsSymptoms}

Lors de l'exécution de la commande `ibmcloud tke domain-compare`, vous n'avez pas reçu de confirmation de validité (`Valid`) du registre de la clé maîtresse en vigueur (CURRENT MASTER KEY REGISTER).
{: tsCauses}

Assurez-vous que la clé maîtresse du HSM a été correctement définie.
{: tsResolve}

## Impossible de créer ou de supprimer des clés
{: #unable-to-create-keys}

Lorsque vous accédez à l'interface utilisateur {{site.data.keyword.hscrypto}}, les options d'ajout ou de suppression des clés ne s'affichent pas.

Dans le tableau de bord {{site.data.keyword.cloud_notm}}, sélectionnez votre instance du service {{site.data.keyword.hscrypto}}.
{: tsSymptoms}

Une liste de clés est visible, mais les options d'ajout ou de suppression des clés ne s'affichent pas.

Vous ne disposez pas des droits appropriés pour exécuter des actions {{site.data.keyword.hscrypto}}.
{: tsCauses}

Vérifiez auprès de votre administrateur qu'il vous a attribué le rôle adéquat dans le groupe de ressources ou l'instance de service applicable. Pour plus d'informations sur les rôles, voir [Rôles et droits](/docs/services/key-protect/manage-access.html#roles).
{: tsResolve}

## Aide et support
{: #getting-help}

Si vous rencontrez des problèmes ou si vous avez des questions lors de l'utilisation d'{{site.data.keyword.hscrypto}}, vous pouvez consulter {{site.data.keyword.cloud_notm}} ou rechercher des informations ou poser des questions via un forum. Vous pouvez également ouvrir un ticket de demande de service.
{: shortdesc}

Vous pouvez vérifier si {{site.data.keyword.cloud_notm}} est disponible en accédant à la [page de statut ![icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/status?tags=platform,runtimes,services).

Vous pouvez consulter les forums pour voir si d'autres utilisateurs ont rencontré le
même problème. Quand vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de façon à ce qu'elle soit vue par les équipes de développement {{site.data.keyword.cloud_notm}}.

- Si vous avez des questions d'ordre technique sur {{site.data.keyword.hscrypto}}, postez-les (en anglais) sur le forum [Stack Overflow ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://stackoverflow.com/){: new_window} en les accompagnant des étiquettes "ibm-cloud" et "hyperprotect-crypto".
- Pour des questions relatives au service et aux instructions de mise en route, utilisez le forum [IBM developerWorks dW Answers ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/answers/index.html){: new_window} forum. Incluez les étiquettes "ibm-cloud" et "hyperprotect-crypto".

Pour plus d'informations sur l'utilisation des forums, voir la rubrique expliquant [comment obtenir de l'aide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/docs/support/index.html#getting-help){: new_window}.

Pour plus d'informations sur l'ouverture d'un ticket de demande de service {{site.data.keyword.IBM_notm}}, sur les niveaux de support disponibles ou les niveaux de gravité des tickets, voir la rubrique expliquant [comment contacter le support![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://cloud.ibm.com/docs/support/index.html#contacting-support){: new_window}.
