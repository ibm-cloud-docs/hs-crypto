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

{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} unterstützt mehrere Schlüsseltypen, darunter Rootschlüssel, Standardschlüssel und Masterschlüssel.{:shortdesc}

## Rootschlüssel

*Rootschlüssel* sind symmetrische Key-Wrapping-Schlüssel, die in {{site.data.keyword.hscrypto}} vollständig verwaltet werden. Sie können einen Rootschlüssel verwenden, um andere Verschlüsselungsschlüssel mit einer erweiterten Verschlüsselung zu schützen. Weitere Informationen finden Sie in <a href="/docs/services/key-protect/concepts/envelope-encryption.html">Envelope-Verschlüsselung</a>.

Sie können Rootschlüssel anhand der Schritte in [Schlüssel verwalten](/docs/services/hs-crypto/index.html#manage-keys) verwalten.

## Standardschlüssel

*Standardschlüssel* sind symmetrische Schlüssel, die in der Kryptografie verwendet werden. Sie können einen Standardschlüssel verwenden, um Daten direkt zu verschlüsseln und zu entschlüsseln.

Sie können Standardschlüssel anhand der Schritte in [Schlüssel verwalten](/docs/services/hs-crypto/index.html#manage-keys) verwalten.

## Masterschlüssel

*Masterschlüssel* werden zur Verschlüsselung der Verschlüsselungsinstanz (HSM) verwendet, die die Rootschlüssel und Standardschlüssel ver- und entschlüsselt und verwaltet. Mit dem Masterschlüssel besitzen Sie die Vertrauens-Root, die die gesamte Kette der Schlüssel verschlüsselt, einschließlich Rootschlüsseln und Standardschlüsseln.

Aufgrund des eingerichteten End-to-End-Kanals zur Verschlüsselungsinstanz (HSM) können nur die Administratoren der {{site.data.keyword.hscrypto}}-Instanz den Masterschlüssel festlegen und verwalten. Beachten Sie, dass IBM den Masterschlüssel nicht sichern oder beeinflussen kann und keine Möglichkeit hat, diesen zu kopieren oder auf einer anderen Maschine oder in einem anderen Rechenzentrum wiederherzustellen.

Eine Verschlüsselungsinstanz (HSM) kann nur einen Masterschlüssel besitzen. Wenn Sie den Masterschlüssel der {{site.data.keyword.hscrypto}}-Instanz löschen, können Sie alle Daten, die mit den im Service verwalteten Schlüsseln verschlüsselt wurden, wirksam verschlüsseln.

Die Verwaltung der Masterschlüssel erfolgt beim [Initialisieren der Verschlüsselungsinstanzen zum Schutz des Schlüsselspeichers](/docs/services/hs-crypto/initialize_hsm.html).

Die Rotation des Masterschlüssels wird in diesem Stadium nicht unterstützt.
{:important}
