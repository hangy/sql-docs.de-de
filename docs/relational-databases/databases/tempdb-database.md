---
title: tempdb-Datenbank | Microsoft-Dokumentation
description: Dieser Artikel enthält Details zur Konfiguration und Verwendung der tempdb-Datenbank in SQL Server und Azure SQL-Datenbank.
ms.custom: P360
ms.date: 08/21/2019
ms.prod: sql
ms.prod_service: database-engine
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
ms.reviewer: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a7a1f692abdb5f9ce1b9fd69c494f719b9027c22
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/25/2019
ms.locfileid: "72909548"
---
# <a name="tempdb-database"></a>TempDB-Datenbank

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Die **tempdb**-Systemdatenbank ist eine globale Ressource, die für alle Benutzer verfügbar ist, die mit der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oder mit der SQL-Datenbank verbunden sind. Tempdb wird verwendet, um Folgendes zu speichern:  
  
- Temporäre **Benutzerobjekte**, die explizit erstellt werden, z.B. globale oder lokale temporäre Tabellen und Indizes, temporäre gespeicherte Prozeduren, Tabellenvariablen, in Tabellenwertfunktionen zurückgegebene Tabellen oder Cursor.  
- **Interne Objekte**, die von der Datenbank-Engine erstellt werden. Dazu gehören:
  - Arbeitstabellen, in denen direkte Ergebnisse für Spools, Cursor, Sortierungen und temporäre große Objektspeicher (LOB) gespeichert werden.
  - Arbeitsdateien für Hashjoin- oder Hashaggregatvorgänge.
  - Zwischenergebnisse von Sortierungen für Vorgänge, wie z. B. das Erstellen oder Neuerstellen von Indizes (wenn SORT_IN_TEMPDB angegeben ist) oder bestimmte GROUP BY-, ORDER BY- oder UNION-Abfragen.

  > [!NOTE]
  > Jedes interne Objekt verwendet mindestens neun Seiten: eine IAM-Seite (Index Allocation Map) und eine achtseitige Erweiterung. Weitere Informationen zu Seiten und Blöcken finden Sie unter [Seiten und Blöcke](../../relational-databases/pages-and-extents-architecture-guide.md#pages-and-extents).
  > [!IMPORTANT]
  > In der Azure SQL-Datenbank unterstützen Singletons und Pools für elastische Datenbanken globale temporäre Tabellen und globale temporär gespeicherte Prozeduren, die in tempdb gespeichert werden und auf Datenbankebene gelten. Globale temporäre Tabellen und globale temporär gespeicherte Prozeduren werden für alle Benutzersitzungen innerhalb derselben Azure SQL-Datenbank freigegeben. Benutzersitzungen von anderen Azure SQL-Datenbanken können nicht auf globale temporäre Tabellen zugreifen. Weitere Informationen finden Sie unter [Database scoped global temporary tables (Azure SQL Database) (Globale temporäre Tabellen auf Datenbankebene (Azure SQL-Datenbank))](../../t-sql/statements/create-table-transact-sql.md#database-scoped-global-temporary-tables-azure-sql-database). [Verwaltete Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)) unterstützt die gleichen temporäre Objekte wie SQL Server.
  > Für Azure SQL-Datenbank Singletons und Pools für elastische Datenbanken gelten nur die Masterdatenbank und die tempdb-Datenbank. Weitere Informationen finden Sie unter [Was ist ein Azure SQL-Datenbank-Server](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases#what-is-an-azure-sql-database-server). Eine Erläuterung von tempdb im Kontext von Azure SQL-Datenbank Singletons und Pools für elastische Datenbanken finden Sie unter [tempdb-Datenbank in Azure SQL-Datenbank Singletons und Pools für elastische Datenbanken ](#tempdb-database-in-sql-database). Für die verwaltete Azure SQL-Datenbank-Instanz gelten alle Systemdatenbanken.

- **Versionsspeicher**, die aus einer Auflistung von Datenseiten bestehen, in denen die Datenzeilen enthalten sind, die zur Unterstützung der Funktionen, die die Zeilenversionsverwaltung verwenden, erforderlich ist. Es gibt zwei Versionsspeicher: ein allgemeiner Versionsspeicher und ein Onlineindexerstellungs-Versionsspeicher. Die Versionsspeicher beinhalten Folgendes:
  - Zeilenversionen, die von Datenänderungstransaktionen in einer Datenbank generiert werden, die READ COMMITTED mit Zeilenversionsverwaltung oder Transaktionen der Momentaufnahmeisolation verwendet.  
  - Zeilenversionen, die von Datenänderungstransaktionen für Funktionen, wie z. B. Onlineindexvorgänge, Multiple Active Result Sets (MARS) und AFTER-Trigger, generiert wurden.  
  
Vorgänge innerhalb von **tempdb** werden minimal protokolliert, sodass ein Rollback für Transaktionen ausgeführt werden kann. **tempdb** wird bei jedem Start von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu erstellt, sodass das System immer mit einer bereinigten Kopie der Datenbank startet. Temporäre Tabellen und gespeicherte Prozeduren werden beim Trennen der Verbindung automatisch gelöscht; es sind keine Verbindungen aktiv, wenn das System heruntergefahren wird. Daher wird zwischen den einzelnen Sitzungen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nichts in **tempdb** gespeichert. Sicherungs- und Wiederherstellungsvorgänge sind in **tempdb** nicht zulässig.  

## <a name="physical-properties-of-tempdb-in-sql-server"></a>Physische Eigenschaften von tempdb in SQL Server

In der folgenden Tabelle werden die anfänglichen Konfigurationswerte der **tempdb**-Daten- und Protokolldateien in SQL Server aufgeführt, die auf den Standardeinstellungen der Modelldatenbank basieren. Die Größe dieser Dateien kann sich in den verschiedenen Editionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geringfügig unterscheiden.  
  
|File|Logischer Name (logical name)|Physischer Name (physical name)|Anfangsgröße|Dateivergrößerung (file growth)|  
|----------|------------------|-------------------|------------------|-----------------|  
|Primäre Daten|tempdev|tempdb.mdf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Speicherplatz auf dem Datenträger erschöpft ist|  
|Sekundäre Datendateien*|temp#|tempdb_mssql_#.ndf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Speicherplatz auf dem Datenträger erschöpft ist|  
|Log|templog|templog.ldf|8 Megabytes|Automatische Vergrößerung um 64 MB, bis der Maximalwert von 2 TB erreicht wird|  
  
\* Die Anzahl der Dateien hängt von der Anzahl der (logischen) Prozessoren auf dem Computer ab. Als allgemeine Regel gilt: Verwenden Sie die Anzahl von Datendateien, die der Anzahl von logischen Prozessoren entspricht, falls die Anzahl von logischen Prozessoren acht oder weniger beträgt. Verwenden Sie acht Datendateien, wenn die Anzahl von logischen Prozessoren größer als acht ist. Falls weiterhin ein Konflikt besteht, erhöhen Sie die Anzahl von Datendateien um ein Vielfaches von vier, bis der Konflikt auf ein akzeptables Ausmaß reduziert ist, oder ändern Sie die Workload bzw. den Code.

> [!NOTE]
> Der Standardwert für die Anzahl der Datendateien basiert auf den allgemeinen Richtlinien in [KB 2154845](https://support.microsoft.com/kb/2154845/).  
  
### <a name="moving-the-tempdb-data-and-log-files-in-sql-server"></a>Verschieben der tempdb-Daten und -Protokolldateien in SQL Server

Weitere Informationen zum Verschieben der **tempdb**-Daten- und -Protokolldateien finden Sie unter [Verschieben von Systemdatenbanken](../../relational-databases/databases/move-system-databases.md).  
  
### <a name="database-options-for-tempdb-in-sql-server"></a>Datenbankoptionen für tempdb in SQL Server

Die folgende Tabelle nennt die Standardwerte für die einzelnen Datenbankoptionen in der **tempdb**-Datenbank und gibt an, ob die entsprechende Option geändert werden kann. Zum Anzeigen der aktuellen Einstellungen dieser Optionen verwenden Sie die Katalogsicht [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) .  
  
|Datenbankoption|Standardwert|Kann geändert werden.|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Ja|  
|ANSI_NULL_DEFAULT|OFF|Ja|  
|ANSI_NULLS|OFF|Ja|  
|ANSI_PADDING|OFF|Ja|  
|ANSI_WARNINGS|OFF|Ja|  
|ARITHABORT|OFF|Ja|  
|AUTO_CLOSE|OFF|Nein|  
|AUTO_CREATE_STATISTICS|ON|Ja|  
|AUTO_SHRINK|OFF|Nein|  
|AUTO_UPDATE_STATISTICS|ON|Ja|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Ja|  
|CHANGE_TRACKING|OFF|Nein|  
|CONCAT_NULL_YIELDS_NULL|OFF|Ja|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Ja|  
|CURSOR_DEFAULT|GLOBAL|Ja|  
|Datenbankverfügbarkeitsoptionen|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|Nein<br /><br /> Nein<br /><br /> Nein|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Ja|  
|DB_CHAINING|ON|Nein|  
|ENCRYPTION|OFF|Nein|  
|MIXED_PAGE_ALLOCATION|OFF|Nein|  
|NUMERIC_ROUNDABORT|OFF|Ja|  
|PAGE_VERIFY|CHECKSUM für neue Installationen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> NONE für Upgrades von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|Ja|  
|PARAMETERIZATION|SIMPLE|Ja|  
|QUOTED_IDENTIFIER|OFF|Ja|  
|READ_COMMITTED_SNAPSHOT|OFF|Nein|  
|RECOVERY|SIMPLE|Nein|  
|RECURSIVE_TRIGGERS|OFF|Ja|  
|Service Broker-Optionen|ENABLE_BROKER|Ja|  
|TRUSTWORTHY|OFF|Nein|  
  
Eine Beschreibung dieser Datenbankoptionen finden Sie unter [ALTER DATABASE SET-Optionen (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="tempdb-database-in-sql-database"></a>tempdb-Datenbank in SQL-Datenbank

### <a name="tempdb-sizes-for-dtu-based-service-tiers"></a>tempdb-Größen für DTU-basierte Diensttarife

|SLO|Maximale Dateigröße für tempdb-Daten (GB)|Anzahl von tempdb-Datendateien|Maximale Datengröße für tempdb (GB)|
|---|---:|---:|---:|
|Standard|13|1|13|
|S0|13|1|13|
|S1|13|1|13|
|S2|13|1|13|
|S3|32|1|32
|S4|32|2|64|
|S6|32|3|96|
|S7|32|6|192|
|S9|32|12|384|
|S12|32|12|384|
|P1|13|12|156|
|P2|13|12|156|
|P4|13|12|156|
|P6|13|12|156|
|P11|13|12|156|
|P15|13|12|156|
|Elastischer Premium-Pool (alle DTU-Konfigurationen)|13|12|156|
|Elastischer Standard-Pool (S0-S2)|13|12|156|
|Elastischer Standard-Pool (S3 und höher) |32|12|384|
|Elastischer Basic-Pool (alle DTU-Konfigurationen)|13|12|156|
||||

### <a name="tempdb-sizes-for-vcore-based-service-tiers"></a>tempdb-Größen für auf virtuellen Kern basierende Diensttarife

Weitere Informationen finden Sie unter [V-Kern-basierte Ressourceneinschränkungen](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits).

## <a name="restrictions"></a>Beschränkungen

Die folgenden Operationen können mit der **tempdb**-Datenbank nicht ausgeführt werden:  
  
- Hinzufügen von Dateigruppen
- Sichern und Wiederherstellen der Datenbank
- Ändern der Sortierung. Die Standardsortierung entspricht der Serversortierung.
- Ändern des Datenbankbesitzers Der Besitzer von**tempdb** ist **sa**.
- Erstellen einer Datenbankmomentaufnahme
- Löschen der Datenbank
- Löschen des **guest** -Benutzers aus der Datenbank
- Aktivieren von Change Data Capture
- Teilnehmen an der Datenbankspiegelung
- Entfernen der primären Dateigruppe, der primären Datendatei oder der Protokolldatei
- Umbenennen der Datenbank oder der primären Dateigruppe
- Ausführen von DBCC CHECKALLOC
- Ausführen von DBCC CHECKCATALOG
- Versetzen der Datenbank in den OFFLINE-Modus
- Versetzen der Datenbank oder der primären Dateigruppe in den READ_ONLY-Modus
  
## <a name="permissions"></a>Berechtigungen

Jeder Benutzer ist berechtigt, temporäre Objekte in tempdb zu erstellen. Benutzer haben nur Zugriff auf ihre eigenen Objekte, es sei denn, ihnen wurden zusätzliche Berechtigungen zugewiesen. Die CONNECT-Berechtigung für tempdb kann widerrufen werden, um Benutzer daran zu hindern, tempdb zu verwenden. Dies wird jedoch nicht empfohlen, da einige Routinevorgänge auf die Verwendung von tempdb angewiesen sind.  

## <a name="optimizing-tempdb-performance-in-sql-server"></a>Optimieren der tempdb-Leistung in SQL Server
Die Größe und die physische Platzierung der tempdb-Datenbank kann sich auf die Leistung eines Systems auswirken. Wurde für tempdb beispielsweise eine zu kleine Größe definiert, muss bei jedem Neustart der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz möglicherweise ein Teil der Verarbeitungslast des Systems dafür aufgewendet werden, die tempdb-Datenbank automatisch auf den Umfang zu vergrößern, der zum Unterstützen der anfallenden Arbeitsauslastung erforderlich ist.

Verwenden Sie nach Möglichkeit die [schnelle Dateiinitialisierung für Datenbank](../../relational-databases/databases/database-instant-file-initialization.md), um die Leistung von Datendateivergrößerungen zu verbessern.

Weisen Sie allen tempdb-Dateien im Voraus Speicherplatz zu, indem Sie die Dateigröße auf einen Wert festlegen, der hoch genug ist, um der typischen Arbeitsauslastung in der Umgebung gerecht zu werden. Durch die Vorabzuordnung wird verhindert, dass tempdb zu häufig vergrößert und die Leistung dadurch beeinträchtigt wird. Für die tempdb-Datenbank sollte die automatische Vergrößerung festgelegt werden, jedoch nur für den Fall eines zusätzlichen Speicherplatzbedarfs für nicht geplante Ausnahmen.

Datendateien sollten in jeder [Dateigruppe](../../relational-databases/databases/database-files-and-filegroups.md#filegroups) die gleiche Größe haben, da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] einen Algorithmus zum proportionalen Auffüllen verwendet, in dem Zuteilungen in Dateien mit mehr freiem Platz bevorzugt werden. Ein Aufteilen von tempdb in mehrere Datendateien gleicher Größe bietet einen hohen Grad an paralleler Effizienz in Vorgängen, in denen tempdb verwendet wird.

Legen Sie das Inkrement für die Dateivergrößerung auf eine sinnvolle Größe fest, sodass der Zuwachs der tempdb-Datenbank nicht zu gering ausfällt. Wenn der Dateizuwachs im Vergleich zur Anzahl der Daten, die in tempdb geschrieben werden, zu gering ist, muss tempdb möglicherweise ständig vergrößert werden und kann die Leistung beeinträchtigen.

Führen Sie die folgende Abfrage aus, um die aktuelle Größe von tempdb und die aktuellen Größenzuwachsparameter zu überprüfen:

```sql
 SELECT name AS FileName,
    size*1.0/128 AS FileSizeInMB,
    CASE max_size
        WHEN 0 THEN 'Autogrowth is off.'
        WHEN -1 THEN 'Autogrowth is on.'
        ELSE 'Log file grows to a maximum size of 2 TB.'
    END,
    growth AS 'GrowthValue',
    'GrowthIncrement' =
        CASE
            WHEN growth = 0 THEN 'Size is fixed.'
            WHEN growth > 0 AND is_percent_growth = 0
                THEN 'Growth value is in 8-KB pages.'
            ELSE 'Growth value is a percentage.'
        END
FROM tempdb.sys.database_files;
GO
```

Platzieren Sie die tempdb-Datenbank auf einem schnellen E/A-Subsystem. Verwenden Sie Datenträgerstriping, wenn viele Datenträger direkt angeschlossen sind. Einzelne oder Gruppen von tempdb-Datendateien müssen nicht unbedingt auf verschiedenen Datenträgern oder Spindeln gespeichert sein – es sei denn, Sie stoßen auf E/A-Engpässe.

Legen Sie die tempdb-Datenbank auf anderen Datenträgern ab als denen, die von den Benutzerdatenbanken verwendet werden.

## <a name="performance-improvements-in-tempdb-for-sql-server"></a>Leistungsverbesserungen in tempdb für SQL Server
Ab [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] wird die **tempdb**-Leistung auf folgende Weise weiter optimiert:  
  
- Temporäre Tabellen und Tabellenvariablen werden zwischengespeichert. Das Zwischenspeichern ermöglicht das sehr schnelle Ausführen von Vorgängen zum Löschen und Erstellen der temporären Objekte und reduziert das Auftreten von Seitenzuordnungskonflikten.  
- Das Latchprotokoll der Zuordnungsseite wurde verbessert, um die Anzahl der verwendeten Updatelatches zu verringern.  
- Der Protokollierungsaufwand für **tempdb** wurde verringert, um die E/A-Bandbreite des Datenträgers für die **tempdb**-Protokolldatei zu reduzieren.  
- Das Setup fügt während der Installation einer neuen Instanz mehrere tempdb-Datendateien hinzu. Diese Aufgabe kann mit der neuen Eingabesteuerung der Benutzeroberfläche im Bereich **Datenbank-Engine-Konfiguration** und einem Befehlszeilenparameter `/SQLTEMPDBFILECOUNT` durchgeführt werden. Standardmäßig fügt das Setup die Anzahl von tempdb-Datendateien hinzu, die der Anzahl von logischen Prozessoren entspricht, höchstens jedoch acht.  
- Wenn mehrere **tempdb**-Datendateien vorhanden sind, werden alle Dateien gleichzeitig und im selben Umfang je nach Wachstumseinstellungen automatisch vergrößert. [Ablaufverfolgungsflag 1117](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) ist nicht mehr erforderlich.  
- Alle Zuordnungen in **tempdb** verwenden gleichartige Blöcke. [Ablaufverfolgungsflag 1118](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) ist nicht mehr erforderlich.  
- Für die primäre Dateigruppe ist die AUTOGROW_ALL_FILES-Eigenschaft aktiviert und kann nicht geändert werden.

Weitere Informationen zu Verbesserungen der Leistung in tempdb finden Sie im folgenden Blogartikel:

[TEMPDB – Files and Trace Flags and Updates, Oh My! (TEMPDB: Dateien, Ablaufverfolgungsflags und Updates)](https://blogs.msdn.microsoft.com/sql_server_team/tempdb-files-and-trace-flags-and-updates-oh-my/)

## <a name="memory-optimized-tempdb-metadata"></a>Speicheroptimierte TempDB-Metadaten
Bislang stellten tempdb-Metadatenkonflikte einen Engpass für die Skalierbarkeit vieler Workloads auf [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar. Mit [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] wird eine neue Funktion eingeführt, die Teil der [In-Memory Database](../in-memory-database.md)-Featurefamilie ist. Hierbei handelt es sich um speicheroptimierte tempdb-Metadaten, durch die dieser Engpass effektiv behoben wird und sich eine neue Ebene der Skalierbarkeit für tempdb-intensive Workloads ergibt. In [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] können die Systemtabellen, die an der Verwaltung von Metadaten temporärer Tabellen beteiligt sind, in nicht dauerhafte speicheroptimierte Tabellen ohne Latches verschoben werden. Zur Verwendung dieser neuen Funktion führen Sie das folgende Skript aus:

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED TEMPDB_METADATA = ON 
```

Damit diese Konfigurationsänderung wirksam wird, muss der Dienst neu gestartet werden.

Bei dieser Implementierung sind einige Einschränkungen zu beachten:

1. Das Ein- und Ausschalten dieser Funktion ist nicht dynamisch. Aufgrund der systeminternen Änderungen, die an der Struktur von tempdb vorgenommen werden müssen, ist ein Neustart erforderlich, um die Funktion zu aktivieren oder zu deaktivieren.

2. Eine einzelne Transaktion kann nicht auf speicheroptimierte Tabellen in mehreren Datenbanken zugreifen.  Das bedeutet, dass Transaktionen, bei denen eine speicheroptimierte Tabelle in einer Benutzerdatenbank beteiligt ist, nicht innerhalb derselben Transaktion auf TempDB-Systemsichten zugreifen können.  Wenn Sie versuchen, in derselben Transaktion wie eine speicheroptimierte Tabelle in einer Benutzerdatenbank auf TempDB-Systemsichten zuzugreifen, wird die folgende Fehlermeldung angezeigt:
    
    ```
    A user transaction that accesses memory optimized tables or natively compiled modules cannot access more than one user database or databases model and msdb, and it cannot write to master.
    ```
    
    Beispiel:
    
    ```sql
    BEGIN TRAN
    SELECT *
    FROM tempdb.sys.tables  -----> Creates a user In-Memory OLTP Transaction on Tempdb
    INSERT INTO <user database>.<schema>.<mem-optimized table>
    VALUES (1)  ----> Attempts to create user In-Memory OLTP transaction but will fail
    COMMIT TRAN
    ```
    
3. Abfragen für speicheroptimierte Tabellen unterstützen keine Sperr- und Isolationshinweise, sodass bei Abfragen für speicheroptimierte TempDB-Katalogsichten Sperr- und Isolationshinweise nicht berücksichtigt werden. Wie bei anderen Systemkatalogsichten in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erfolgen alle Transaktionen für Systemsichten in READ COMMITTED-Isolation (oder in diesem Fall in READ COMMITTED SNAPSHOT-Isolation).

4. [Columnstore-Indizes](../indexes/columnstore-indexes-overview.md) können nicht für temporäre Tabellen erstellt werden, wenn speicheroptimierte TempDB-Metadaten aktiviert sind.

5. Aufgrund der Einschränkung für Columnstore-Indizes wird die Verwendung der gespeicherten Systemprozedur „sp_estimate_data_compression_savings“ mit den Datenkomprimierungsparametern „COLUMNSTORE“ oder „COLUMNSTORE_ARCHIVE“ nicht unterstützt, wenn speicheroptimierte TempDB-Metadaten aktiviert sind.

> [!NOTE] 
> Diese Einschränkungen gelten nur beim Verweisen auf TempDB-Systemsichten, und Sie können beim Zugriff auf eine speicheroptimierte Tabelle in einer Benutzerdatenbank bei Bedarf eine temporäre Tabelle in derselben Transaktion erstellen.

Mit dem folgenden T-SQL-Befehl können Sie überprüfen, ob TempDB speicheroptimiert ist:
```
SELECT SERVERPROPERTY('IsTempdbMetadataMemoryOptimized')
```

Wenn nach dem Aktivieren von speicheroptimierten TempDB-Metadaten aus irgendeinem Grund ein Fehler beim Starten des Servers auftritt, können Sie die Funktion umgehen, indem Sie SQL Server mithilfe der Startoption **-f** in der [Minimalkonfiguration](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md) starten. Dadurch können Sie die Funktion deaktivieren und SQL Server anschließend im normalen Modus neu starten.

## <a name="capacity-planning-for-tempdb-in-sql-server"></a>Kapazitätsplanung für tempdb in SQL Server
Das Festlegen der angemessenen Größe von tempdb in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produktionsumgebung hängt von vielen Faktoren ab. Wie bereits zuvor in diesem Artikel beschrieben, schließen diese Faktoren die vorhandene Workload und die verwendeten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Funktionen ein. Es wird empfohlen, die vorhandene Workload durch Ausführen folgender Aufgaben in einer SQL Server-Testumgebung zu analysieren:

- Festlegen der automatischen Vergrößerung für tempdb
- Ausführen einzelner Abfragen oder Ablaufverfolgungsdateien der Workload sowie Überwachen der Speicherplatzverwendung in tempdb
- Ausführen von Indexverwaltungsvorgängen wie das Neuerstellen von Indizes und die Überwachung des Speicherplatzes in tempdb
- Verwenden der Werte zur Speicherplatzverwendung aus den vorigen Schritten, um den Gesamtverbrauch der Workload vorherzusagen; Anpassen dieses Werts für prognostizierte gleichzeitige Aktivitäten und anschließend Festlegen der entsprechenden Größe von tempdb.

## <a name="how-to-monitor-tempdb-use"></a>Überwachen der Speicherplatzverwendung in tempdb
Wenn nicht mehr genügend Speicherplatz in tempdb vorhanden ist, kann das erhebliche Störungen in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Produktionsumgebung verursachen und dazu führen, dass ausgeführte Anwendungen Vorgänge nicht abschließen können. Sie können mit der dynamischen Verwaltungssicht [sys.dm_db_file_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) den in den tempdb-Dateien verwendeten Speicherplatz überwachen:

```sql
 -- Determining the Amount of Free Space in TempDB
SELECT SUM(unallocated_extent_page_count) AS [free pages],
  (SUM(unallocated_extent_page_count)*1.0/128) AS [free space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount Space Used by the Version Store
SELECT SUM(version_store_reserved_page_count) AS [version store pages used],
  (SUM(version_store_reserved_page_count)*1.0/128) AS [version store space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by Internal Objects
SELECT SUM(internal_object_reserved_page_count) AS [internal object pages used],
  (SUM(internal_object_reserved_page_count)*1.0/128) AS [internal object space in MB]
FROM sys.dm_db_file_space_usage;

-- Determining the Amount of Space Used by User Objects
SELECT SUM(user_object_reserved_page_count) AS [user object pages used],
  (SUM(user_object_reserved_page_count)*1.0/128) AS [user object space in MB]
FROM sys.dm_db_file_space_usage;
 ```

Um darüber hinaus die Aktivität für die Seitenzuordnung und die Zuordnungsaufhebung in tempdb auf der Sitzungs- oder Aufgabenebene zu überwachen, können Sie die dynamischen Verwaltungssichten [sys.dm_db_session_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md) und [sys.dm_db_task_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md) verwenden. Mithilfe dieser Sichten können große Abfragen, temporäre Tabellen oder Tabellenvariablen identifiziert werden, die große Mengen von Speicherplatz in tempdb belegen. Es gibt ebenfalls mehrere Leistungsindikatoren, die zum Überwachen des in tempdb verfügbaren freien Speicherplatzes verwendet werden können. Diese können auch verwendet werden, um die Ressourcen, die tempdb verwenden, zu überwachen. Weitere Informationen finden Sie im nächsten Abschnitt.

```sql
-- Obtaining the space consumed by internal objects in all currently running tasks in each session
SELECT session_id,
  SUM(internal_objects_alloc_page_count) AS task_internal_objects_alloc_page_count,
  SUM(internal_objects_dealloc_page_count) AS task_internal_objects_dealloc_page_count
FROM sys.dm_db_task_space_usage
GROUP BY session_id;

-- Obtaining the space consumed by internal objects in the current session for both running and completed tasks
SELECT R2.session_id,
  R1.internal_objects_alloc_page_count
  + SUM(R2.internal_objects_alloc_page_count) AS session_internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count
  + SUM(R2.internal_objects_dealloc_page_count) AS session_internal_objects_dealloc_page_count
FROM sys.dm_db_session_space_usage AS R1
INNER JOIN sys.dm_db_task_space_usage AS R2 ON R1.session_id = R2.session_id
GROUP BY R2.session_id, R1.internal_objects_alloc_page_count,
  R1.internal_objects_dealloc_page_count;;
```

## <a name="related-content"></a>Verwandte Inhalte
[SORT_IN_TEMPDB-Option für Indizes](../../relational-databases/indexes/sort-in-TempDB-option-for-indexes.md)    
[Systemdatenbanken](../../relational-databases/databases/system-databases.md)    
[sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)    
[sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)    
[Verschieben von Datenbankdateien](../../relational-databases/databases/move-database-files.md)    
  
