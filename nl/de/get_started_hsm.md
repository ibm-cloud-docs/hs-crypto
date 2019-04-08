---

copyright:
  years: 2018, 2019
lastupdated: "2019-02-15"

Keywords: key storage, service instance, HSM, hardware security module

subcollection: hs-crypto

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}  
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:important: .important}
{:tip: .tip}

# Einführung in die Initialisierung der Serviceinstanz
{: #get-started-hsm}

<!-- Master keys protect the contents of key storage in a host logical partition.--> In diesem Lernprogramm erfahren Sie, wie Sie die Serviceinstanz initialisieren, indem Sie die Masterschlüssel zum Schutz Ihres Schlüsselspeichers mit dem Plug-in "Trusted Key Entry" laden. Nachdem Sie die Serviceinstanz initialisiert haben, können Sie mit der Verwaltung der Rootschlüssel beginnen.    
{:shortdesc}

## Voraussetzungen
{: #get-started-hsm-prerequisite}

Führen Sie die folgenden Schritte aus, bevor Sie beginnen:

1. Stellen Sie die {{site.data.keyword.cloud_notm}} {{site.data.keyword.hscrypto}}-Instanz (kurz: Serviceinstanz) bereit. Eine genaue Beschreibung der Schritte finden Sie unter [{{site.data.keyword.hscrypto}} bereitstellen](/docs/services/hs-crypto/provision.html).

2. Führen Sie den folgenden Befehl aus, um sicherzustellen, dass Sie beim richtigen API-Endpunkt angemeldet sind: 

  ```
  ibmcloud api https://api.ng.bluemix.net
  ```
  {: pre}

3. Installieren Sie das aktuelle "Trusted Key Entry"-Plug-in über die {{site.data.keyword.cloud_notm}}-CLI (Befehlszeilenschnittstelle) mit dem folgenden Befehl:

  ```
  ibmcloud plugin install tke
  ```
  {: pre}

  Informationen zur Installation des CLI-Plug-ins finden Sie unter [Einführung in die {{site.data.keyword.cloud_notm}}-CLI](/docs/cli/index.html).
  {: tip}

4. Umgebungsvariable CLOUDTKEFILES so festlegen, dass sie das Unterverzeichnis angibt, in dem die Schlüsselteile und Signaturschlüssel gespeichert werden sollen

##  Schritt 1: Masterschlüsselteile und Signaturschlüsseldateien erstellen
{: #hsm-step1}

1. Erstellen Sie einen beliebigen Masterschlüsselteil oder einen Masterschlüsselteil mit einem bekannten Wert.

  * Für die Erstellung eines beliebigen Masterschlüsselteils verwenden Sie folgenden Befehl:

    ```
    ibmcloud tke mk-add --random
    ```
    {: pre}

    Geben Sie bei entsprechender Aufforderung eine Beschreibung für den Schlüsselteil und ein Kennwort für die Schlüsselteildatei ein.

  * Für die Erstellung eines Masterschlüsselteils mit bekanntem Wert verwenden Sie folgenden Befehl:

    ```
    ibmcloud tke mk-add --value
    ```
    {: pre}

    Geben Sie bei entsprechender Aufforderung den bekannten Wert für den Schlüsselteil als hexadezimale Zeichenfolge und anschließend eine Beschreibung und ein Kennwort für die Schlüsselteildatei ein.

  Wiederholen Sie den Befehl, um weitere Schlüsselteile zu erstellen.

2. Erstellen Sie einen Signaturschlüssel mit dem folgenden Befehl:
  ```
  ibmcloud tke sigkey-add
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung einen Administratornamen und ein Kennwort für die Signaturschlüsseldatei ein.

## Schritt 2: Verschlüsselungseinheiten auswählen, mit denen Sie arbeiten wollen
{: #hsm-step2}

Alle Verschlüsselungseinheiten in einer Serviceinstanz müssen gleich konfiguriert sein. 

1. Mit dem folgenden Befehl können Sie die Serviceinstanzen und Verschlüsselungseinheiten anzeigen, die Ihrem IBM Cloud-Konto zugeordnet sind: 

  ```
  ibmcloud tke cryptounits
  ```
  {: pre}

2. Verwenden Sie den folgenden Befehl, um zusätzliche Verschlüsselungseinheiten auszuwählen, mit denen Sie arbeiten möchten: 

  ```
  ibmcloud tke cryptounit-add
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung die zusätzlichen Verschlüsselungseinheiten ein, mit denen Sie arbeiten möchten. 

3. Verwenden Sie den folgenden Befehl, um Verschlüsselungseinheiten aus der Gruppe zu entfernen, mit der Sie arbeiten möchten: 

  ```
  ibmcloud tke cryptounit-rm
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung die Verschlüsselungseinheiten ein, die Sie entfernen möchten. 

## Schritt 3: Administratoren für Verschlüsselungseinheiten hinzufügen und Modus 'imprint' verlassen
{: #hsm-step3}

Bevor Sie die Masterschlüssel in einer Verschlüsselungseinheit laden können, müssen Sie mindestens einen Administrator für Verschlüsselungseinheiten erstellen und den Modus 'imprint' verlassen. 

1. Laden Sie einen Administrator für Verschlüsselungseinheiten. Verwenden Sie den folgenden Befehl, um einen Administrator für Verschlüsselungseinheiten zu erstellen: 
  ```
  ibmcloud tke cryptounit-admin-add
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung die "KEYNUM" (Schlüsselnummer) des Signaturschlüssels für den Administrator und das Kennwort für die Signaturschlüsseldatei ein.

2. Wählen Sie den Signaturschlüssel aus, der zum Signieren von Befehlen verwendet werden soll, indem Sie folgenden Befehl verwenden:

  ```
  ibmcloud tke sigkey-sel
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung die "KEYNUM" (Schlüsselnummer) des Signaturschlüssels zum Signieren von Befehlen ein.

  Diese muss mit einem der Signaturschlüssel identisch sein, die zum Laden eines Administrators für Verschlüsselungseinheiten in Schritt 3.1 verwendet werden.
  {: tip}

3. Verlassen Sie den Modus 'imprint' mit dem folgenden Befehl:

  ```
   ibmcloud tke cryptounit-exit-impr
  ```
  {: pre}

Nachdem Sie einen Administrator für Verschlüsselungseinheiten geladen und den Modus 'imprint' verlassen haben, können Sie den Status Ihrer Verschlüsselungseinheiten mit dem folgenden Befehl überprüfen:
{: tip}

```
 ibmcloud tke cryptounit-compare
```
{: pre}

## Schritt 4: Masterschlüsselregister laden
{: #hsm-step4}

Um das Masterschlüsselregister zu laden, muss mindestens ein Administrator für Verschlüsselungseinheiten definiert sein und die Verschlüsselungseinheit muss den Modus 'imprint' verlassen haben. 

1. Laden Sie das neue Masterschlüsselregister mit dem folgenden Befehl:

  ```
  ibmcloud tke cryptounit-mk-load
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung die "KEYNUM" (Schlüsselnummer) der zu ladenden Schlüsselteile, das Kennwort für die Signaturschlüsseldatei und die Kennwörter für jeden ausgewählten Schlüsselteil ein.

2. Schreiben Sie das neue Masterschlüsselregister mit dem folgenden Befehl fest:

  ```
  ibmcloud tke cryptounit-mk-commit
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung das Kennwort für die Signaturschlüsseldatei ein.

3. Verschieben Sie den Masterschlüssel mit dem folgenden Befehl in das aktuelle Masterschlüsselregister: 

  ```
  ibmcloud tke cryptounit-mk-setimm
  ```
  {: pre}

  Geben Sie bei entsprechender Aufforderung das Kennwort für die Signaturschlüsseldatei ein.

## Weitere Schritte
{: #hsm-next}

Jetzt können Sie mit der Verwendung Ihrer Serviceinstanz beginnen. Details zur Implementierung der Prozedur in einer Produktionsumgebung finden Sie unter [Serviceinstanzen zum Schutz des Schlüsselspeichers initialisieren](/docs/services/hs-crypto/initialize_hsm.html). 
