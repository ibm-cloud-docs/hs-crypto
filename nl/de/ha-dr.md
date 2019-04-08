---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-20"

Keywords: disaster recovery, High availability, HA, DR

subcollection: hs-crypto

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}

# Hochverfügbarkeit und Disaster-Recovery
{: #ha-dr}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} ist ein hoch verfügbarer regionaler Service mit automatischen Funktionen, die Ihnen helfen, Ihre Anwendungen sicher und betriebsfähig zu halten.
{: shortdesc}

Auf dieser Seite erfahren Sie mehr über Hochverfügbarkeit und Disaster-Recovery-Strategien von {{site.data.keyword.hscrypto}}.

## Standorte, Tenancy und Verfügbarkeit
{: #availability}

<!-- {{site.data.keyword.hscrypto}} is a multi-tenant, regional service. -->

Sie können {{site.data.keyword.hscrypto}}-Ressourcen in einer der unterstützten [{{site.data.keyword.cloud_notm}}-Regionen](/docs/services/hs-crypto/regions.html) erstellen, die den geografischen Bereich darstellen, in dem Ihre {{site.data.keyword.hscrypto}}-Anfragen abgewickelt und verarbeitet werden. Jede {{site.data.keyword.cloud_notm}}-Region enthält [mehrere Verfügbarkeitszonen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/blogs/bluemix/2018/06/expansion-availability-zones-global-regions/), um die Anforderungen an die Sicherheit, geringe Latenz und Sicherheit für die Region zu erfüllen.

Bei der Planung Ihrer Strategie der Verschlüsselung ruhender Daten mit {{site.data.keyword.cloud_notm}} beachten Sie, dass die Bereitstellung von {{site.data.keyword.hscrypto}} in einer geografisch nahegelegenen Region mit höherer Wahrscheinlichkeit zu schnelleren, zuverlässigeren Verbindungen führt, wenn Sie mit den {{site.data.keyword.hscrypto}}-APIs interagieren. Wählen Sie eine bestimmte Region aus, wenn die Benutzer, Apps oder Services, die von einer {{site.data.keyword.hscrypto}}-Ressource abhängig sind, geografisch konzentriert sind. Denken Sie daran, dass für Benutzer und Services, die weit von der Region entfernt sind, höhere Latenzzeiten entstehen könnten.

Ihre Verschlüsselungsschlüssel sind auf die Region beschränkt, in der Sie sie erstellt haben. {{site.data.keyword.hscrypto}} kopiert oder exportiert keine Verschlüsselungsschlüssel in andere Regionen.
{: note}

## Disaster-Recovery
{: #disaster-recovery}

{{site.data.keyword.hscrypto}} verfügt über ein regionales Disaster-Recovery mit einer RTO (Recovery Time Objective-RTO) von einer Stunde. Der Service folgt bei der Planung und bei Wiederherstellungen nach einem Katastrophenfall den {{site.data.keyword.cloud_notm}}-Anforderungen. Weitere Informationen finden Sie in [Disaster-Recovery](/docs/overview/zero_downtime.html#disaster-recovery).
