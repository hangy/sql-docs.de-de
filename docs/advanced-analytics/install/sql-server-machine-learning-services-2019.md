---
title: Isolationsänderungen für Windows
description: In diesem Artikel werden die Änderungen am Isolationsmechanismus in Machine Learning Services in SQL Server 2019 unter Windows beschrieben. Diese Änderungen wirken sich auf SQLRUserGroup, Firewallregeln, Dateiberechtigungen und die implizite Authentifizierung aus.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4fae460e78682263c604d8e1e86ca40b7b62df97
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69531039"
---
# <a name="sql-server-2019-on-windows-isolation-changes-for-machine-learning-services"></a>SQL Server 2019 unter Windows: Isolationsänderungen für Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In diesem Artikel werden die Änderungen am Isolationsmechanismus in Machine Learning Services in SQL Server 2019 unter Windows beschrieben. Diese Änderungen wirken sich auf **SQLRUserGroup**, Firewallregeln, Dateiberechtigungen und die implizite Authentifizierung aus.

Weitere Informationen finden Sie unter [Installieren von SQL Server Machine Learning Services unter Windows](sql-machine-learning-services-windows-install.md).

## <a name="changes-to-isolation-mechanism"></a>Änderungen am Isolationsmechanismus

Bei SQL Server 2019-Setup wurde unter Windows der Isolationsmechanismus für externe Prozesse geändert. Im Rahmen dieser Änderung wurden lokale Workerkonten durch [AppContainer](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation) ersetzt. Hierbei handelt es sich um eine Isolationstechnologie für Clientanwendungen, die unter Windows ausgeführt werden. 

Aufgrund der Änderung sind für den Administrator keine bestimmten Aktionselemente vorhanden. Auf einem neuen oder aktualisierten Server gehorchen alle externen Skripts und Codes, die über [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) ausgeführt werden, automatisch dem neuen Isolationsmodell. 

Die wichtigsten Änderungen in diesem Release:

+ Lokale Benutzerkonten unter **SQL Restricted User Group (SQLRUserGroup)** (unter SQL eingeschränkte Benutzergruppe) werden nicht mehr erstellt oder zum Ausführen externer Prozesse verwendet. Diese werden durch AppContainer ersetzt.
+ Die Mitgliedschaft in **SQLRUserGroup** wurde geändert. Eine Mitgliedschaft besteht nun nicht mehr aus mehreren lokalen Benutzerkonten, sondern nur noch aus dem SQL Server-Launchpad-Dienstkonto. R- und Python-Prozesse werden nun isoliert durch AppContainer unter der Launchpad-Dienstidentität ausgeführt.

Obwohl sich das Isolationsmodell geändert hat, bleiben Installations-Assistent und Befehlszeilenparameter in SQL Server 2019 unverändert. Weitere Informationen zur Installation finden Sie unter [Installieren von SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Informationen zur AppContainer-Isolation

In früheren Releases enthielt **SQLRUserGroup** einen Pool mit lokalen Windows-Benutzerkonten (MSSQLSERVER00-MSSQLSERVER20), die zum Isolieren und Ausführen externer Prozesse verwendet wurden. Wenn ein externer Prozess ausgeführt werden musste, hat der SQL Server-Launchpad-Dienst dazu ein verfügbares Konto verwendet. 

In SQL Server 2019 werden von Setup keine lokalen Workerkonten mehr erstellt. Stattdessen wird die Isolation durch [AppContainer](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation) erreicht. Wenn zur Laufzeit in einer gespeicherten Prozedur oder Abfrage eingebettete Skripts oder Codes erkannt werden, ruft SQL Server Launchpad mit der Anforderung eines erweiterungsspezifischen Startprogramms auf. Launchpad ruft die entsprechende Laufzeitumgebung in einem Prozess unter seiner Identität auf und instanziiert einen AppContainer, um ihn aufzunehmen. Diese Änderung hat den Vorteil, dass keine lokalen Konten und Kennwörter mehr verwaltet werden müssen. Zudem kann dank dem Wegfall der Abhängigkeit von lokalen Benutzerkonten dieses Feature nun in Installationen verwendet werden, bei denen lokale Benutzerkonten nicht zulässig sind.

Gemäß der Implementierung durch SQL Server handelt es sich bei AppContainern um einen internen Mechanismus. Obwohl sich AppContainer im Prozessmonitor physisch nicht nachweisen lassen, sind sie dennoch in Firewallregeln für ausgehenden Datenverkehr zu finden, die von Setup erstellt werden, um zu verhindern, dass Prozesse Netzwerkaufrufe ausführen.

## <a name="firewall-rules-created-by-setup"></a>Von Setup erstellte Firewallregeln

Standardmäßig werden ausgehende Verbindungen von SQL Server durch Erstellen von Firewallregeln deaktiviert. Bisher haben diese Regeln auf lokalen Benutzerkonten basiert, bei denen im Rahmen des Setups eine Ausgangsregel für **SQLRUserGroup** erstellt wurde, die für die Mitglieder den Netzwerkzugriff verweigert hat (jedes Workerkonto wurde gemäß der Regel als lokales Prinzip aufgeführt). 

Aufgrund des Wechsels zu AppContainer gibt es nun neue Firewallregeln, die auf AppContainer-SIDs basieren: jeweils eine Regel für jede der 20 von SQL Server-Setup erstellten AppContainer. Die Namenskonvention für den Namen der Firewallregel lautet **Netzwerkzugriff für AppContainer-00 in SQL Server-Instanz MSSQLSERVER blockieren**, wobei 00 für die Nummer des AppContainers (standardmäßig 00-20) steht und MSSQLSERVER der Name der SQL Server-Instanz ist. 

> [!Note]
> Wenn Netzwerkaufrufe erforderlich sind, können Sie die Ausgangsregeln in der Windows-Firewall deaktivieren.

## <a name="program-file-permissions"></a>Berechtigungen für Programmdateien

Wie bei früheren Releases stellt **SQLRUserGroup** weiterhin die Berechtigungen zum Lesen und Ausführen von ausführbaren Dateien in den SQL Server-Verzeichnissen **Binn**, **R_SERVICES** und **PYTHON_SERVICES** bereit. In diesem Release enthält **SQLRUserGroup** als einziges Mitglied das SQL Server-Launchpad-Dienstkonto.  Wenn durch den Launchpad-Dienst eine R- oder Python-Ausführungsumgebung aufgerufen wird, wird der Prozess als LaunchPad-Dienst ausgeführt.

## <a name="implied-authentication"></a>Implizite Authentifizierung

Für die *implizite Authentifizierung* ist wie bisher eine zusätzliche Konfiguration erforderlich, wenn das Skript oder der Code zum Abrufen von Daten oder Ressourcen erneut eine Verbindung mit SQL Server über eine vertrauenswürdige Authentifizierung herstellen muss. Im Rahmen der zusätzlichen Konfiguration muss für **SQLRUserGroup** eine Datenbankanmeldung erstellt werden. Diese Gruppe enthält nun nicht mehr mehrere Workerkonten, sondern nur noch das SQL Server-Launchpad-Dienstkonto. Weitere Informationen zu diesem Task finden Sie unter [Hinzufügen von SQLRUserGroup als Datenbankbenutzer](../security/create-a-login-for-sqlrusergroup.md).


## <a name="symbolic-link-created-by-setup"></a>Symbolische Verknüpfung erstellt durch Setup

Im Rahmen des SQL Server-Setups wird für die aktuellen Standardverzeichnisse **R_SERVICES** und **PYTHON_SERVICES** eine symbolische Verknüpfung erstellt. Wenn Sie nicht möchten, dass diese Verknüpfung erstellt wird, können Sie „allen Anwendungspaketen“ eine Leseberechtigung für den Ordner in der Hierarchie weiter oben gewähren.


## <a name="see-also"></a>Siehe auch

+ [Installieren von SQL Server-Machine Learning Services unter Windows](sql-machine-learning-services-windows-install.md)
+ [Installieren von SQL Server-Machine Learning Services unter Linux](../../linux/sql-server-linux-setup-machine-learning.md)
