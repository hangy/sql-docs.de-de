---
title: Installieren und Konfigurieren der wideworldimporters-Beispieldatenbank
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: e1683adfa20851d279e8b8e18a3c767db9e5810d
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056275"
---
# <a name="installation-and-configuration"></a>Installation und Konfiguration
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Anweisungen zur Installation und Konfiguration der OLTP-Datenbank für Wide World.

## <a name="prerequisites"></a>Prerequisites

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (oder höher) oder [Azure SQL-Datenbank](https://azure.microsoft.com/services/sql-database/). Verwenden Sie für die vollständige Version des Beispiels SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Um die besten Ergebnisse zu erzielen, verwenden Sie die Version vom Juni 2016 oder höher.

## <a name="download"></a>Herunterladen

Die neueste Version des Beispiels:

[wide-world-importers-release](https://go.microsoft.com/fwlink/?LinkID=800630)

Laden Sie die Beispieldatenbank "wideworldimporters" und die BacPac-Datei herunter, die Ihrer Edition von SQL Server oder Azure SQL-Datenbank entspricht.

Der Quellcode zum erneuten Erstellen der Beispieldatenbank ist unter folgendem Speicherort verfügbar. Beachten Sie, dass das Neuerstellen des Beispiels zu geringfügigen Unterschieden in den Daten führt, da es einen zufälligen Faktor für die Datengenerierung gibt:

[weltweit Importierer](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-database-scripts)

## <a name="install"></a>Install


### <a name="sql-server"></a>SQL Server

Zum Wiederherstellen einer Sicherung in einer SQL Server Instanz können Sie Management Studio verwenden.

1. Öffnen Sie SQL Server Management Studio und stellen Sie eine Verbindung mit der Ziel SQL Server Instanz her.
2. Klicken Sie mit der rechten Maustaste auf den Knoten **Datenbanken** , und wählen Sie **Datenbank wiederherstellen**.
3. Wählen Sie **Gerät** aus, und klicken Sie auf die Schaltfläche **...**
4. Wählen Sie im Dialogfeld **Sicherungs**Medien aus, klicken Sie auf **Hinzufügen**, navigieren Sie im Dateisystem des Servers zu der Datenbanksicherung, und wählen Sie die Sicherung aus. Klicken Sie auf **OK**.
5. Ändern Sie ggf. den Zielort für die Daten-und Protokolldateien im Bereich " **Dateien** ". Beachten Sie, dass es eine bewährte Vorgehensweise ist, Daten-und Protokolldateien auf verschiedenen Laufwerken zu platzieren.
6. Klicken Sie auf **OK**. Dadurch wird die Daten Bank Wiederherstellung initiiert. Nachdem der Vorgang abgeschlossen ist, wird die Datenbank "wideworldimporters" auf der SQL Server-Instanz installiert.

### <a name="azure-sql-database"></a>Azure SQL Database

Zum Importieren einer BacPac-Datenbank in eine neue SQL-Datenbank können Sie Management Studio verwenden.

1. optionale Wenn Sie noch keine SQL Server in Azure haben, navigieren Sie zum [Azure-Portal](https://portal.azure.com/) , und erstellen Sie eine neue SQL-Datenbank. Beim Erstellen einer Datenbank erstellen Sie einen Server. Notieren Sie sich den Server.
   - In [diesem Tutorial](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) finden Sie Informationen zum Erstellen einer Datenbank in wenigen Minuten.
2. Öffnen Sie SQL Server Management Studio, und stellen Sie in Azure eine Verbindung mit Ihrem Server her
3. Klicken Sie mit der rechten Maustaste auf den Knoten **Datenbanken** , und wählen Sie **Datenebenenanwendung importieren**aus.
4. Wählen Sie unter **Import Einstellungen** die Option **aus lokalem Datenträger importieren aus** , und wählen Sie die BacPac-Datei der Beispieldatenbank aus dem Dateisystem aus.
5. Ändern Sie unter **Datenbankeinstellungen** den Datenbanknamen in *wideworldimporters* , und wählen Sie die zu verwendende Ziel Edition und das Dienst Ziel aus.
6. Klicken Sie auf **weiter** und **Beenden** , um die Bereitstellung zu starten. Es dauert einige Minuten, bis ein P1-Vorgang abgeschlossen ist. Wenn ein niedrigerer Tarif erwünscht ist, empfiehlt es sich, in eine neue P1-Datenbank zu importieren und dann den Tarif auf die gewünschte Stufe zu ändern.

## <a name="configuration"></a>Configuration

### <a name="full-text-indexing"></a>Volltextindizierung

In der-Beispieldatenbank kann die voll Text Indizierung verwendet werden. Dieses Feature wird jedoch nicht standardmäßig mit SQL Server installiert. Sie müssen es während SQL Server Setup auswählen (es ist standardmäßig in Azure SQL-Datenbank aktiviert). Daher ist ein Schritt nach der Installation erforderlich.

1. Stellen Sie in SQL Server Management Studio eine Verbindung mit der Datenbank wideworldimporters her, und öffnen Sie ein neues Abfragefenster.
2. Führen Sie den folgenden T-SQL-Befehl aus, um die Verwendung der voll Text Indizierung in der-Datenbank zu aktivieren: `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

Gilt für: SQL Server

Zum Aktivieren der Überwachung in SQL Server ist die Server Konfiguration erforderlich. Führen Sie die folgende Anweisung in der Datenbank aus, um SQL Server Überwachung für das wideworldimporters-Beispiel zu aktivieren:

    EXECUTE [Application].[Configuration_ApplyAuditing]

In Azure SQL-Datenbank wird Audit über den [Azure-Portal](https://portal.azure.com/)konfiguriert.

### <a name="row-level-security"></a>Sicherheit auf Zeilenebene

Gilt für: Azure SQL-Datenbank

Die Sicherheit auf Zeilenebene ist im BacPac-Download von wideworldimporters standardmäßig nicht aktiviert. Führen Sie die folgende gespeicherte Prozedur aus, um die Sicherheit auf Zeilenebene in der Datenbank zu aktivieren:

    EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]

