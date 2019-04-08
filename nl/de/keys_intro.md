---

copyright:
  years: 2018, 2019
lastupdated: "2019-01-15"

Keywords: root keys, master keys, standard keys

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}

# Einführung in Schlüssel
{: #introduce-keys}

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} unterstützt mehrere Schlüsseltypen, darunter Rootschlüssel, Standardschlüssel und Masterschlüssel.
{:shortdesc}

## Rootschlüssel
{: #introduce-root-keys}

*Rootschlüssel* sind symmetrische Key-Wrapping-Schlüssel, die in {{site.data.keyword.hscrypto}} vollständig verwaltet werden. Sie können einen Rootschlüssel verwenden, um andere Verschlüsselungsschlüssel mit einer erweiterten Verschlüsselung zu schützen. Weitere Informationen finden Sie in <a href="/docs/services/key-protect/concepts/envelope-encryption.html">Envelope-Verschlüsselung</a>.

Sie können Rootschlüssel anhand der Schritte in [Schlüssel verwalten](/docs/services/hs-crypto/index.html#manage-keys) verwalten.

## Standardschlüssel
{: #introduce-standard-keys}

*Standardschlüssel* sind symmetrische Schlüssel, die in der Kryptografie verwendet werden. Sie können einen Standardschlüssel verwenden, um Daten direkt zu verschlüsseln und zu entschlüsseln.

Sie können Standardschlüssel anhand der Schritte in [Schlüssel verwalten](/docs/services/hs-crypto/index.html#manage-keys) verwalten.

## Masterschlüssel
{: #introduce-master-keys}

*Masterschlüssel* werden verwendet, um die Serviceinstanz für den Schlüsselspeicher zu verschlüsseln. Mit dem Masterschlüssel besitzen Sie die Vertrauens-Root, die die gesamte Kette der Schlüssel verschlüsselt, einschließlich Rootschlüsseln und Standardschlüsseln.

Aufgrund des geschützten End-to-End-Kanals zu der Serviceinstanz, der eingerichtet wurde, können nur die Administratoren der Serviceinstanz den Masterschlüssel festlegen und verwalten. Beachten Sie, dass IBM den Masterschlüssel nicht sichern oder beeinflussen kann und keine Möglichkeit hat, diesen zu kopieren oder auf einer anderen Maschine oder in einem anderen Rechenzentrum wiederherzustellen.

Eine Serviceinstanz kann nur einen einzigen Masterschlüssel haben. Das Löschen des Masterschlüssels der Serviceinstanz ist ein wirksames Verfahren, um alle Daten unbrauchbar zu machen, die mit den in dem Service verwalteten Schlüsseln verschlüsselt wurden. 

Die Verwaltung der Masterschlüssel erfolgt beim [Initialisieren der Serviceinstanzen zum Schutz des Schlüsselspeichers](/docs/services/hs-crypto/initialize_hsm.html). 

Die Rotation des Masterschlüssels wird im aktuellen Stadium nicht unterstützt.
{:important}
