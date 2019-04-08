---

copyright:
  years: 2018, 2019
lastupdated: "2019-33-22"

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
{: #HSM-certifications}

### Wie kann ich überprüfen, ob eine IBM Crypto Card (HSM) auf die Erfüllung von FIPS 140-2-Stufe 4 geprüft wurde?
{: #FIPS-L4}

FIPS 140-2 Stufe 4 ist eine sehr hohe Sicherungsstufe, die auf dem Markt nicht weit verbreitet ist. IBM ist der führende Anbieter für zertifizierte HSMs der höchsten Stufe und investiert sehr viel darin, diese Validierung für jede neue Kartengeneration zu erhalten. Die Anforderung dieser hohen Zusicherungsstufe wurde Regierungsanforderungen entnommen. Zur Validierung der Zertifizierung werden Sie auf die NIST-Homepage verwiesen, wo die Zertifizierung veröffentlicht wurde.

### Worin liegt der Unterschied zwischen FIPS 140-2 Stufe 2, 3 und 4?
{: #FIPS-levels}

* FIPS 140-2 Stufe 2: Anforderungen an Manipulationsschutz mittels Dichtungen und einbruchsicheren Schlössern an abnehmbaren Abdeckungen und Türen. An einem Verschlüsselungsmodul werden manipulationssichere Überzüge oder Dichtungen angebracht, die beschädigt werden müssten, um physischen Zugang zu den unverschlüsselten Verschlüsselungsschlüsseln und kritischen Sicherheitsparametern (CSPs) innerhalb des Moduls zu erhalten. Die Sicherheitsstufe 2 erfordert mindestens eine rollenbasierte Authentifizierung, bei der ein Verschlüsselungsmodul die Autorisierung eines Bedieners authentifiziert, eine bestimmte Rolle anzunehmen und ein entsprechendes Servicepaket auszuführen.
* FIPS 140-2 Stufe 3: Physische Sicherheitsmechanismen, die für Sicherheitsstufe 3 erforderlich sind, sollten über eine hohe Erkennungswahrscheinlichkeit verfügen und in der Lage sein, auf Versuche des physischen Zugriffs oder der Verwendung oder Änderung des Verschlüsselungsmoduls zu reagieren. Für Sicherheitsstufe 3 sind identitätsbasierte Authentifizierungsmechanismen erforderlich, die die von den rollenbasierten Authentifizierungsmechanismen bereitgestellte und für Sicherheitsstufe 3 erforderliche Sicherheit erhöhen.

* FIPS 140-2 Stufe 4: Auf dieser Sicherheitsstufe stellen die physischen Sicherheitsmechanismen eine vollständige Schutzhülle um das Verschlüsselungsmodul bereit, mit der alle unbefugten Versuche des physischen Zugriffs erkannt und beantwortet werden können. Der unbefugte Zugriff auf diese Umhüllung des Verschlüsselungsmoduls aus beliebiger Richtung wird mit sehr hoher Wahrscheinlichkeit erkannt und führt zur sofortigen Nullung aller Klartext-CSPs (Critical Security Parameters). Verschlüsselungsmodule der Sicherheitsstufe 4 sind für den Betrieb in physisch ungeschützten Umgebungen nützlich. Sicherheitsstufe 4 schützt ein Verschlüsselungsmodul auch vor Sicherheitsbeeinträchtigungen aufgrund von Umgebungsbedingungen oder Schwankungen außerhalb der normalen Betriebsbereiche des Moduls für Spannung und Temperatur. Beabsichtigte Abweichungen von den normalen Betriebsbereichen können von einem Angreifer verwendet werden, um die Abwehr eines Verschlüsselungsmoduls zu verhindern.

## Schlüsselverwaltung
{: #key-management}

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

<!-- ## Pricing
{: #pricing}

### Where can I find the detailed pricing information?
{: #pricing_info}

You can refer to the **Pricing** tab on the [{{site.data.keyword.hscrypto}} home page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/cloud/hyper-protect-crypto){: new_window} for details.

### Is there a pricing example I can refer to?
{: #pricing_example}

Here is one. If you have a requirement of 5000 keys to be crypto-processed, for high availability, you need to set up two crypto units. The amount is $3140 ($1570 per crypto unit) per month. The first 1,000,000 API calls are free of charge. However, if you perform 2,000,000 API calls per month, you will be charged additional $1 ($0.01 per 10,000 API calls over 1,000,000 API calls). In total, there will be a monthly charge of $3141 ($3140 for the crypto units and $1 for the additional API calls) for your service instance.

The following table contains the pricing details.

| Pricing components | Cost per month |
|-----|----------------|
| Crypto unit 1 | $1570 |
| Crypto unit 2 | $1570 |
| First 1,000,000 API calls | $0 |
| 1,000,000 additional API calls (10,000 API calls x 100) | $1 ($0.01 x 100) |
| End of month charge | $3141  |

*Table 1. Charge of two crypto units with a monthly API calls of 2,000,000* -->
