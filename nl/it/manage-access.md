---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-18"

Keywords: user access, Cloud IAM roles, encryption keys

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Gestione dell'accesso utente
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} supporta un sistema di controllo dell'accesso centralizzato, controllato da
{{site.data.keyword.iamlong}}, per aiutarti a gestire gli utenti e l'accesso alle tue chiavi crittografate.
{: shortdesc}

Ti raccomandiamo di concedere le autorizzazioni di accesso quando inviti nuovi utenti nel tuo servizio o account. Ad esempio, considera le seguenti linee guida:

- **Abilita l'accesso utente alle risorse nel tuo account assegnando i ruoli Cloud IAM.**
    Anziché condividere le tue credenziali ammin, crea nuove politiche per gli utenti che devono accedere alle chiavi crittografate nel tuo account. Se sei l'amministratore del tuo account, ti viene automaticamente assegnata una politica _Gestore_ con l'accesso a tutte le risorse nell'account.
- **Concedi i ruoli e le autorizzazioni solo per gli scopi necessari.**
    Ad esempio, se un utente deve accedere solo a una vista di alto livello delle chiavi all'interno di uno spazio specificato, concedi all'utente il ruolo _Lettore_ per tale spazio.
- **Controlla regolarmente chi può gestire il controllo degli accessi ed eliminare le risorse della chiave.**
    Ricorda che concedendo un ruolo _Gestore_ a un utente lo rendi capace di modificare le politiche del servizio per altri utenti, in aggiunta a distruggere le risorse.

## Ruoli e autorizzazioni
{: #roles}

Con {{site.data.keyword.iamshort}} (IAM), puoi gestire e definire l'accesso per gli utenti e le risorse nel tuo account.

Per semplificare l'accesso, {{site.data.keyword.hscrypto}} allinea i ruoli Cloud IAM in modo che ogni utente disponga di una vista differente del servizio, in base al ruolo assegnato. Se sei un amministratore della sicurezza del tuo servizio, puoi assegnare i ruoli Cloud IAM che corrispondono alle autorizzazioni {{site.data.keyword.hscrypto}} specifiche che vuoi concedere ai membri del tuo team.

La seguente tabella mostra come i ruoli di identità e accesso vengono associati alle autorizzazioni {{site.data.keyword.hscrypto}}:
<table>
  <tr>
    <th>Ruolo di accesso al servizio</th>
    <th>Descrizione</th>
    <th>Azioni</th>
  </tr>
  <tr>
    <td><p>Lettore</p></td>
    <td><p>Un lettore può esplorare una vista di alto livello delle chiavi e eseguire le azioni di impacchettamento e spacchettamento. I lettori non possono accedere o modificare il materiale della chiave.</p></td>
    <td>
      <p>
        <ul>
          <li>Visualizza le chiavi</li>
          <li>Impacchetta le chiavi</li>
          <li>Spacchetta le chiavi</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Scrittore</p></td>
    <td><p>Uno scrittore può creare e modificare le chiavi e accedere al materiale della chiave.</p></td>
    <td>
      <p>
        <ul>
          <li>Crea le chiavi</li>
          <li>Visualizza le chiavi</li>
          <li>Impacchetta le chiavi</li>
          <li>Spacchetta le chiavi</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Gestore</p></td>
    <td><p>Un gestore può eseguire tutte le azioni di un lettore e di uno scrittore, inclusa la possibilità di eliminare le chiavi, invitare nuovi utenti e assegnare le politiche di accesso ad altri utenti.</p></td>
    <td>
      <p>
        <ul>
          <li>Tutte le azioni che un lettore o uno scrittore possono eseguire</li>
          <li>Elimina le chiavi</li>
          <li>Assegna le politiche di accesso</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabella 1. Descrive come i ruoli di identità e accesso vengono associati alle autorizzazioni {{site.data.keyword.hscrypto}}</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

Per ulteriori informazioni su {{site.data.keyword.iamshort}}, consulta [Ruoli utente e autorizzazioni](/docs/iam/users_roles.html#userroles).

### Operazioni successive
{: #manage-access-next}

Gli amministratori e i proprietari dell'account possono invitare gli utenti e configurare le politiche del servizio che corrispondono alle azioni {{site.data.keyword.hscrypto}} che possono eseguire gli utenti.

- Per ulteriori informazioni sull'assegnazione dei ruoli utente nella IU {{site.data.keyword.cloud_notm}}, vedi [Gestione dell'accesso IAM](/docs/iam/mngiam.html).
- Per informazioni su come concedere autorizzazioni avanzate per accedere a chiavi di crittografia specifiche, vedi [Gestione dell'accesso alle chiavi](/docs/services/hs-crypto/manage-access-api.html).
