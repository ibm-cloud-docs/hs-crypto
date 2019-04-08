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

# Benutzerzugriff verwalten
{: #manage-access}

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} unterstützt ein zentralisiertes Zugriffssteuerungssystem, das mit {{site.data.keyword.iamlong}} reguliert wird, um Sie bei der Verwaltung von Benutzern und beim Zugriff auf Ihre Verschlüsselungsschlüssel zu unterstützen.
{: shortdesc}

Es hat sich bewährt, Zugriffsberechtigungen zu erteilen, während Sie neue Benutzer zur Nutzung Ihres Kontos oder Service einladen. Beachten Sie hierbei z. B. die folgenden Leitlinien:

- **Aktivieren Sie den Benutzerzugriff auf die Ressourcen in Ihrem Konto, indem Sie Cloud IAM-Rollen zuweisen.**
    Anstatt Ihre Administratorberechtigungsnachweise gemeinsam zu nutzen, sollten Sie neue Richtlinien für die Benutzer erstellen, die Zugriff auf die Verschlüsselungsschlüssel in Ihrem Konto benötigen. Wenn Sie der Administrator Ihres Kontos sind, dann wird Ihnen automatisch eine _Manager_-Richtlinie mit Zugriff auf alle Ressourcen zugewiesen, die sich unter Ihrem Konto befinden.
- **Erteilen Sie Rollen und Berechtigungen für den kleinsten erforderlichen Geltungsbereich.**
    Wenn ein Benutzer beispielsweise nur Zugriff auf eine übergeordnete Ansicht der Schlüssel in einem bestimmten Bereich benötigt, dann ordnen Sie ihm die Rolle _Leseberechtigter_ für diesen Bereich zu.
- **Überprüfen Sie in regelmäßigen Zeitabständen, wer zur Verwaltung der Zugriffssteuerung und zum Löschen von Schlüsselressourcen berechtigt ist.**
    Beachten Sie dabei, dass die Erteilung einer Rolle als _Manager_ für einen Benutzer bedeutet, dass dieser Benutzer Servicerichtlinien für andere Benutzer ändern und außerdem Ressourcen löschen kann.

## Rollen und Berechtigungen
{: #roles}

Mit {{site.data.keyword.iamshort}} (IAM) können Sie den Zugriff für Benutzer und Ressourcen in Ihrem Konto verwalten und definieren.

Zur Vereinfachung des Zugriffs orientiert sich {{site.data.keyword.hscrypto}} an den Cloud IAM-Rollen, sodass jeder Benutzer über eine andere Ansicht des Service verfügt, und zwar abhängig von der Rolle, die diesem Benutzer zugewiesen wurde. Wenn Sie der Sicherheitsadministrator für Ihren Service sind, dann können Sie Cloud IAM-Rollen zuweisen, die den speziellen {{site.data.keyword.hscrypto}}-Berechtigungen entsprechen, die Sie Mitgliedern Ihres Teams erteilen wollen.

In der folgenden Tabelle erhalten Sie Informationen dazu, wie die Identitäts- und Zugriffsrollen den {{site.data.keyword.hscrypto}}-Berechtigungen zugeordnet werden:
<table>
  <tr>
    <th>Servicezugriffsrolle</th>
    <th>Beschreibung</th>
    <th>Aktionen</th>
  </tr>
  <tr>
    <td><p>Leseberechtigter</p></td>
    <td><p>Ein Leseberechtigter kann die übergeordnete Ansicht von Schlüsseln durchsuchen und Wrapping- und Unwrapping-Aktionen durchführen. Leseberechtigte können nicht auf Schlüsselinformationen zugreifen und nicht bearbeiten.</p></td>
    <td>
      <p>
        <ul>
          <li>Schlüssel anzeigen</li>
          <li>Wrapping für Schlüssel durchführen</li>
          <li>Wrapping für Schlüssel aufheben</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Schreibberechtigter</p></td>
    <td><p>Ein Schreibberechtigter kann Schlüssel erstellen und bearbeiten und auf die Schlüsselinformationen zugreifen.</p></td>
    <td>
      <p>
        <ul>
          <li>Schlüssel erstellen</li>
          <li>Schlüssel anzeigen</li>
          <li>Wrapping für Schlüssel durchführen</li>
          <li>Wrapping für Schlüssel aufheben</li>
        </ul>
      </p>
    </td>
  </tr>
  <tr>
    <td><p>Manager</p></td>
    <td><p>Ein Manager kann alle Aktionen ausführen, die ein Lese- und ein Schreibberechtigter ausführen können. Dies umfasst auch die Berechtigung zum Löschen von Schlüsseln, zum Einladen neuer Benutzer und zum Zuordnen von Zugriffsrichtlinien für andere Benutzer.</p></td>
    <td>
      <p>
        <ul>
          <li>Alle Aktionen, die ein Lese- oder ein Schreibberechtigter ausführen kann</li>
          <li>Schlüssel löschen</li>
          <li>Zugriffsrichtlinie zuweisen</li>
        </ul>
      </p>
    </td>
  </tr>
  <caption style="caption-side:bottom;">Tabelle 1. Informationen zur Zuordnung von Identitäts- und Zugriffsrollen zu {{site.data.keyword.hscrypto}}-Berechtigungen</caption>
</table>

<!-- **Note**: Cloud IAM user roles provide access at the service or service instance level. [Cloud Foundry roles](/docs/iam/cfaccess.html) are separate and define access at the organization or the space level. -->

Weitere Informationen zu {{site.data.keyword.iamshort}} finden Sie in [Benutzerrollen und -berechtigungen](/docs/iam/users_roles.html#userroles).

### Weitere Schritte
{: #manage-access-next}

Kontoeigner und Administratoren können Benutzer einladen und Servicerichtlinien festlegen, die den {{site.data.keyword.hscrypto}}-Aktionen entsprechen, die die Benutzer ausführen können.

- Weitere Informationen zur Zuweisung von Benutzerrollen in der {{site.data.keyword.cloud_notm}}-Benutzerschnittstelle finden Sie in [IAM-Zugriff verwalten](/docs/iam/mngiam.html).
- Weitere Informationen zum Erteilen erweiterter Berechtigungen für den Zugriff auf bestimmte Verschlüsselungsschlüssel finden Sie im Abschnitt [Zugriff auf Schlüssel verwalten](/docs/services/hs-crypto/manage-access-api.html).
