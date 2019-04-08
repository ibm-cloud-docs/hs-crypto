---

copyright:
  years: 2018, 2019
lastupdated: "2019-03-21"

Keywords: release note, new

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Neuerungen
{: #what-new}

Bleiben Sie auf dem Laufenden mit den neuen Features, die für {{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} verfügbar sind.
{: shortdesc}

## März 2019
{: #March-2019}

### {{site.data.keyword.hscrypto}} ist allgemein verfügbar
{: #ga-201903}
Neuerungen mit Stand vom 29.03.2019

Weitere Informationen zum {{site.data.keyword.hscrypto}}-Produktangebot finden Sie auf der [{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}}-Homepage ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud/hyper-protect-crypto){:new_window}.

Ab 31. März 2019 ist die Bereitstellung neuer Hyper Protect Crypto Services-Betainstanzen nicht mehr möglich. Vorhandene Instanzen werden bis zum Enddatum des Betasupports (30. April 2019) unterstützt. 

Informationen zum Migrieren von Schlüsseln in eine Produktionsserviceinstanz finden Sie unter [Schlüssel aus einer Betaserviceinstanz migrieren](/docs/services/hs-crypto/transition-keys.html). 

### Hochverfügbarkeit und Disaster-Recovery
{: #ha-dr-new}
Neuerungen mit Stand vom 29.03.2019

{{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}} unterstützt jetzt drei Verfügbarkeitszonen in einer ausgewählten Region und ist ein hoch verfügbarer Service mit automatischen Funktionen, die Ihnen helfen, Ihre Anwendungen sicher und betriebsfähig zu halten. 

Sie können {{site.data.keyword.hscrypto}}-Ressourcen in den unterstützten [{{site.data.keyword.cloud_notm}}-Regionen](/docs/services/hs-crypto/regions.html) erstellen, die den geografischen Bereich darstellen, in dem Ihre {{site.data.keyword.hscrypto}}-Anfragen abgewickelt und verarbeitet werden. Jede {{site.data.keyword.cloud_notm}}-Region enthält [mehrere Verfügbarkeitszonen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/), um die Anforderungen an die Sicherheit, geringe Latenz und Sicherheit für die Region zu erfüllen.

Weitere Informationen finden Sie unter [Hochverfügbarkeit und Disaster-Recovery](/docs/services/hs-crypto/ha-dr.html).

### Skalierbarkeit
{: #scalability-new}
Neuerungen mit Stand vom 29.03.2019

Die Serviceinstanz kann auf bis zu maximal sechs Verschlüsselungseinheiten skaliert werden, um Ihre Leistungsanforderungen zu erfüllen. Jede Verschlüsselungseinheit kann bis zu 5000 Verschlüsselungsschlüssel verarbeiten. In einer Produktionsumgebung wird empfohlen, mindestens zwei Verschlüsselungseinheiten auszuwählen, um eine hohe Verfügbarkeit zu ermöglichen. Bei der Auswahl von drei oder mehr Verschlüsselungseinheiten werden diese Verschlüsselungseinheiten auf drei Verfügbarkeitszonen in der ausgewählten Region verteilt. 

Weitere Informationen finden Sie in [Service bereitstellen](/docs/services/hs-crypto/provision.html). 

## Februar 2019
{: #Feb-2019}

### {{site.data.keyword.hscrypto}} Beta ist verfügbar
{: #beta-201902}
Neuerungen mit Stand vom 05.02.2019

Die {{site.data.keyword.hscrypto}}-Betaversion wird freigegeben. Sie können jetzt über **Katalog** > **Sicherheit und Identität** direkt auf den {{site.data.keyword.hscrypto}}-Service zugreifen.

Mit Stand vom 5. Februar 2019 ist die Bereitstellung neuer Hyper Protect Crypto Services Experimental-Instanzen nicht mehr möglich. Vorhandene Instanzen werden bis zum Ende des Experimental-Unterstützungsdatums (5. März 2019) unterstützt.

## Dezember 2018
{: #Dec-2018}

### Hinzugefügt: Unterstützung für HSM-Verwaltung mit KYOK
{: #hsm-kyok}
Neuerungen mit Stand vom 19.12.2019

{{site.data.keyword.hscrypto}} unterstützt jetzt Keep Your Own Keys (KYOK), sodass Sie mithilfe von Verschlüsselungsschlüsseln, die Sie beibehalten, steuern und verwalten können, mehr Kontrolle und Berechtigungen für Ihre Daten behalten. Sie können Ihre Serviceinstanz über die {{site.data.keyword.cloud}}-Befehlszeilenschnittstelle (Command-Line Interface, CLI) initialisieren und verwalten. 

Weitere Informationen finden Sie unter [Serviceinstanzen zum Schutz des Schlüsselspeichers initialisieren](/docs/services/hs-crypto/initialize_hsm.html). 

### Hinzugefügt: Integration der {{site.data.keyword.keymanagementserviceshort}}-API
{: #kp-api}
Neuerungen mit Stand vom 19.12.2019

Die {{site.data.keyword.keymanagementserviceshort}}-API ist jetzt in Hyper Protect Crypto Services integriert, um Ihre Schlüssel zu generieren und zu schützen. Sie können die {{site.data.keyword.keymanagementserviceshort}}-API direkt über {{site.data.keyword.hscrypto}} aufrufen.

Weitere Informationen finden Sie in [Auf die API zugreifen](/docs/services/hs-crypto/access-api.html) und [{{site.data.keyword.hscrypto}}-API ![Symbol für externen Link](image/external_link.svg "Symbol für externen Link")](https://{DomainName}/apidocs/hs-crypto){:new_window}.

### Nicht mehr verwendet: Funktion für den Zugriff auf {{site.data.keyword.hscrypto}} über ACSP
{: #deprecated-acsp}
Neuerungen mit Stand vom 19.12.2019

Im aktuellen Stadium wird der Zugriff auf {{site.data.keyword.hscrypto}} über einen ACSP-Client (Advanced Cryptography Service Provider) nicht weiter unterstützt. Wenn Sie eine frühere Serviceinstanz verwenden, können Sie immer noch ACSP verwenden, um {{site.data.keyword.hscrypto}} zu durchsuchen.
