---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-21"

Keywords: frequently asked questions, critical security parameters, cryptographic module, Security Level

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}

# Häufig gestellte Fragen
{: #faqs}

Mit den folgenden häufig gestellten Fragen erhalten Sie Unterstützung bei der Arbeit mit {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}.

## HSM-Zertifizierungen
{: #HSM}

### Wie kann ich überprüfen, ob eine IBM Crypto Card (HSM) auf die Erfüllung von FIPS 140-2-Stufe 4 geprüft wurde?

FIPS 140-2 Stufe 4 ist eine sehr hohe Sicherungsstufe, die auf dem Markt nicht weit verbreitet ist. IBM ist der führende Anbieter für zertifizierte HSMs der höchsten Stufe und investiert sehr viel darin, diese Validierung für jede neue Kartengeneration zu erhalten. Die Anforderung dieser hohen Zusicherungsstufe wurde Regierungsanforderungen entnommen. Zur Validierung der Zertifizierung werden Sie auf die NIST-Homepage verwiesen, wo die Zertifizierung veröffentlicht wurde.

### Worin liegt der Unterschied zwischen FIPS 140-2 Stufe 2, 3 und 4?

* FIPS 140-2 Stufe 2: Anforderungen an Manipulationsschutz mittels Dichtungen und einbruchsicheren Schlössern an abnehmbaren Abdeckungen und Türen. An einem Verschlüsselungsmodul werden manipulationssichere Überzüge oder Dichtungen angebracht, die beschädigt werden müssten, um physischen Zugang zu den unverschlüsselten Verschlüsselungsschlüsseln und kritischen Sicherheitsparametern (CSPs) innerhalb des Moduls zu erhalten. Die Sicherheitsstufe 2 erfordert mindestens eine rollenbasierte Authentifizierung, bei der ein Verschlüsselungsmodul die Autorisierung eines Bedieners authentifiziert, eine bestimmte Rolle anzunehmen und ein entsprechendes Servicepaket auszuführen.
* FIPS 140-2 Stufe 3: Physische Sicherheitsmechanismen, die für Sicherheitsstufe 3 erforderlich sind, sollten über eine hohe Erkennungswahrscheinlichkeit verfügen und in der Lage sein, auf Versuche des physischen Zugriffs oder der Verwendung oder Änderung des Verschlüsselungsmoduls zu reagieren. Für Sicherheitsstufe 3 sind identitätsbasierte Authentifizierungsmechanismen erforderlich, die die von den rollenbasierten Authentifizierungsmechanismen bereitgestellte und für Sicherheitsstufe 3 erforderliche Sicherheit erhöhen.

* FIPS 140-2 Stufe 4: Auf dieser Sicherheitsstufe stellen die physischen Sicherheitsmechanismen eine vollständige Schutzhülle um das Verschlüsselungsmodul bereit, mit der alle unbefugten Versuche des physischen Zugriffs erkannt und beantwortet werden können. Der unbefugte Zugriff auf diese Umhüllung des Verschlüsselungsmoduls aus beliebiger Richtung wird mit sehr hoher Wahrscheinlichkeit erkannt und führt zur sofortigen Nullung aller Klartext-CSPs (Critical Security Parameters). Verschlüsselungsmodule der Sicherheitsstufe 4 sind für den Betrieb in physisch ungeschützten Umgebungen nützlich. Sicherheitsstufe 4 schützt ein Verschlüsselungsmodul auch vor Sicherheitsbeeinträchtigungen aufgrund von Umgebungsbedingungen oder Schwankungen außerhalb der normalen Betriebsbereiche des Moduls für Spannung und Temperatur. Beabsichtigte Abweichungen von den normalen Betriebsbereichen können von einem Angreifer verwendet werden, um die Abwehr eines Verschlüsselungsmoduls zu verhindern.

## Schlüsselverwaltung

### Kann {{site.data.keyword.hscrypto}} in Kombination mit dem {{site.data.keyword.keymanagementserviceshort}}-Service verwendet werden?

 {{site.data.keyword.hscrypto}} ist ein verwalteter Verschlüsselungsservice und wird mit einer vollständig kompatiblen {{site.data.keyword.keymanagementserviceshort}}-API geliefert, die dieselbe Benutzererfahrung wie Key Protect bietet. Der Hauptunterschied besteht darin, dass {{site.data.keyword.hscrypto}} auf einem HSM mit FIPS 140-2 Stufe 4-Zertifizierung basiert. Außerdem bietet es uneingeschränkten Zugriff auf den HSM-Masterschlüssel, der vom Kunden verwaltet wird (KYOK). Der Service ist im Gegensatz zur Multi-Tenant-Konfiguration für {{site.data.keyword.keymanagementserviceshort}} für jede einzelne Instanz dediziert. {{site.data.keyword.hscrypto}} bietet auch HSM-Funktionalität für Verschlüsselungsoperationen wie z. B. Signieren/Prüfen, Schlüsselgenerierung, verschlüsseltes Hashing, Verschlüsseln/Entschlüsseln und Wrappping/Aufhebung des Wrappings.

### Wie lang darf ein Schlüsselname sein?
{: #key_names}

Es kann ein Schlüsselname mit einer Länge von maximal 50 Zeichen verwendet werden.

### Kann ich im Schlüsselnamen landessprachliche Zeichen verwenden?
{: #key_chars}

Landessprachliche Zeichen, z. B. chinesische Zeichen, können nicht als Teil des Schlüsselnamens verwendet werden.

### Was passiert, wenn ich einen Schlüssel lösche?
{: #key_destruction}

Wenn Sie einen Schlüssel löschen, werden der Schlüsselinhalt und die zugehörigen Daten permanent zerstört. Auf die Daten, die mit diesem Schlüssel verschlüsselt wurden, kann nicht mehr zugegriffen werden.

Stellen Sie vor dem Löschen eines Schlüssels sicher, dass Sie keinen Zugriff auf Daten mehr benötigen, die dem betreffenden Schlüssel zugeordnet sind.
