---
title: Sicherungsdateien und Dateigruppen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/03/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backing up filegroups [SQL Server]
- file backups [SQL Server], how-to topics
- backing up files [SQL Server]
- backups [SQL Server], creating
- filegroups [SQL Server], backing up
ms.assetid: a0d3a567-7d8b-4cfe-a505-d197b9a51f70
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cf87d09eed5b955c1773c46270f25cb0a2d57eaa
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708685"
---
# <a name="back-up-files-and-filegroups"></a>Sichern von Dateien und Dateigruppen
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Sie Dateien und Dateigruppen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder PowerShell sichern. Wenn eine vollständige Datenbanksicherung wegen der Größe der Datenbank und aufgrund von Leistungsanforderungen nicht möglich ist, können Sie stattdessen eine Dateisicherung ausführen. Eine *Dateisicherung* enthält alle Daten in einer oder mehreren Dateien (oder Dateigruppen).
  
Weitere Informationen finden Sie unter [Vollständige Dateisicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md) und [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md).  

##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
- Die BACKUP-Anweisung ist nicht in einer expliziten oder implizierten Transaktion zulässig.  
  
- Im einfachen Wiederherstellungsmodell müssen alle Dateien mit Lese-/Schreibzugriff zusammen gesichert werden. Dies hilft Ihnen, die Datenbank bis zu einem bestimmten Zeitpunkt wiederherzustellen. Verwenden Sie die Option READ_WRITE_FILEGROUPS, statt die Dateien bzw. Dateigruppen mit Lese-/Schreibzugriff einzeln anzugeben. Mit dieser Option werden alle Dateigruppen mit Lese-/Schreibzugriff in der Datenbank gesichert. Eine Sicherung, die durch die Angabe von READ_WRITE_FILEGROUPS erstellt wird, wird als *Teilsicherung* bezeichnet. Weitere Informationen dazu finden Sie unter [Teilsicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md).  
  
Weitere Informationen zu Einschränkungen finden Sie unter [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
###  <a name="Recommendations"></a> Empfehlungen
  
Standardmäßig wird bei jedem erfolgreichen Sicherungsvorgang dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Fehlerprotokoll und dem Systemereignisprotokoll ein Eintrag hinzugefügt. Wenn Sie das Protokoll regelmäßig sichern, kann die Anzahl dieser Erfolgsmeldungen schnell ansteigen, d. h., es entstehen sehr große Fehlerprotokolle, die das Suchen nach anderen Meldungen erschweren können. In solchen Fällen können Sie diese Protokolleinträge mithilfe des Ablaufverfolgungsflags 3226 ausblenden, wenn keines der Skripts von diesen Einträgen abhängig ist. Weitere Informationen hierzu finden Sie unter [Ablaufverfolgungsflags &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  

###  <a name="Permissions"></a> Berechtigungen

Mitglieder der festen Serverrolle **sysadmin** und der festen Datenbankrollen **db_owner** und **db_backupoperator** verfügen standardmäßig über `BACKUP DATABASE`- und `BACKUP LOG`-Berechtigungen.  
  
 Besitz- und Berechtigungsprobleme im Zusammenhang mit der physischen Datei des Sicherungsmediums können den Sicherungsvorgang beeinträchtigen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muss über Lese- und Schreibberechtigungen für das Medium verfügen. Das Konto, unter dem der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienst ausgeführt wird, muss Schreibberechtigungen haben. Allerdings prüft die gespeicherte Prozedur [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md), die den Systemtabellen einen Eintrag für ein Sicherungsmedium hinzufügt, nicht die Dateizugriffsberechtigungen. Solche Probleme mit der physischen Datei des Sicherungsmediums treten möglicherweise erst auf, wenn auf die physische Ressource zugegriffen wird, um einen Sicherungs- oder Wiederherstellungsvorgang auszuführen.

## <a name="using-sql-server-management-studio"></a>Verwendung von SQL Server Management Studio   
  
1. Stellen Sie eine Verbindung mit der entsprechenden Instanz von [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]her, und klicken Sie danach im Objekt-Explorer auf den Servernamen, um die Serverstruktur zu erweitern.  
  
1. Erweitern Sie **Datenbanken**, und wählen Sie je nach Datenbank eine Benutzerdatenbank aus, oder erweitern Sie **Systemdatenbanken** , und wählen Sie eine Systemdatenbank aus.  
  
1. Klicken Sie mit der rechten Maustaste auf die Datenbank, zeigen Sie auf **Tasks**, und klicken Sie anschließend auf **Sichern**. Das Dialogfeld **Datenbank sichern** wird angezeigt.  
  
1. Überprüfen Sie im Listenfeld **Datenbank** den Datenbanknamen. Sie können optional eine andere Datenbank aus der Liste auswählen.  
  
1. Wählen Sie im Listenfeld **Sicherungstyp** die Option **Vollständig** oder **Differenziell**aus.  
  
1. Klicken Sie bei der Option **Sicherungskomponente** auf **Datei und Dateigruppen**.  
  
1. Wählen Sie im Dialogfeld **Dateien und Dateigruppen auswählen** die zu sichernden Dateien und Dateigruppen aus. Sie können eine oder mehrere einzelne Dateien auswählen oder das Kontrollkästchen für eine Dateigruppe aktivieren, um automatisch alle Dateien dieser Dateigruppe auszuwählen.  
  
1. Akzeptieren Sie entweder den im Textfeld **Name** vorgeschlagenen Standardnamen für den Sicherungssatz, oder geben Sie einen anderen Namen für den Sicherungssatz ein.  
  
1. Geben Sie (optional) in das Textfeld **Beschreibung** eine Beschreibung des Sicherungssatzes ein.  
  
1. Geben Sie an, wann der Sicherungssatz ablaufen soll:  
  
    - Wenn der Sicherungssatz nach einer bestimmten Anzahl von Tagen ablaufen soll, klicken Sie auf **Nach** (Standardoption), und geben Sie an, nach wie vielen Tagen der Sicherungssatz abläuft. Dieser Wert kann zwischen 0 und 99999 Tagen liegen. Ein Wert von 0 Tagen bedeutet, dass der Sicherungssatz nicht abläuft.  
  
         Der Standardwert wird im Dialogfeld **Servereigenschaften** (Seite **Datenbankeinstellungen** ) über die Option**Standardbeibehaltung für Sicherungsmedien (in Tagen)** festgelegt. Um auf diese Option zuzugreifen, klicken Sie mit der rechten Maustaste auf den Servernamen im Objekt-Explorer, und wählen Sie die Eigenschaften aus. Wählen Sie anschließend die Seite **Datenbankeinstellungen** aus.  
  
    - Zum Speichern des Sicherungssatzes an einem bestimmten Datum klicken Sie auf **Am**. Geben Sie das Datum ein, an dem der Sicherungssatz abläuft.  
  
1. Wählen Sie den Sicherungszieltyp aus, indem Sie auf **Datenträger** oder **Band**klicken. Zum Auswählen der Pfade von bis zu 64 Datenträgern oder Bandlaufwerken, die einen einzelnen Mediensatz enthalten, klicken Sie auf **Hinzufügen**. Die ausgewählten Pfade werden im Listenfeld **Sichern auf** angezeigt.  
  
    > [!NOTE]
    > Um einen Sicherungsziel zu entfernen, wählen Sie ihn aus, und klicken Sie auf **Entfernen**. Zum Anzeigen des Inhalts eines Sicherungsziels wählen Sie es aus, und klicken Sie auf **Inhalt**.  
  
1. Zum Anzeigen oder Auswählen der erweiterten Optionen klicken Sie auf **Optionen** im Bereich **Seite auswählen** .  
  
1. Wählen Sie eine Option von **Medium überschreiben** aus, indem Sie auf eine der folgenden Optionen klicken:  
  
    - **Auf vorhandenen Mediensatz sichern**  
  
         Klicken Sie bei dieser Option entweder auf **An vorhandenen Sicherungssatz anfügen** oder auf **Alle vorhandenen Sicherungssätze überschreiben**. 
         
         Informationen über das Sichern in einem vorhandenen Mediensatz finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
         - Aktivieren Sie (optional) das Kontrollkästchen für **Mediensatznamen und Ablaufzeit des Sicherungssatzes überprüfen**, damit beim Sicherungsvorgang das Datum und die Uhrzeit überprüft werden, zu der der Mediensatz und der Sicherungssatz ablaufen.  
  
         - Geben Sie (optional) einen Namen in das Textfeld **Mediensatzname** ein. Wenn kein Name angegeben wurde, wird ein Mediensatz mit leerem Namen erstellt. Wenn Sie einen Mediensatznamen angeben, wird das Medium (Band oder Datenträger) überprüft, um festzustellen, ob der tatsächliche Name mit dem von Ihnen hier eingegebenen Namen übereinstimmt.  
  
         Wenn Sie den Mediennamen leer lassen und das Kontrollkästchen aktivieren, um ihn anhand des Mediums zu überprüfen, ist die Prüfung erfolgreich, wenn der Medienname auf dem Medium ebenfalls leer ist.  
  
    - **Auf neuen Mediensatz sichern und alle vorhandenen Sicherungssätze löschen**  
  
         Geben Sie bei dieser Option einen Namen in das Textfeld **Name für neuen Mediensatz** und optional eine Beschreibung des Mediensatzes in das Textfeld **Beschreibung für neuen Mediensatz** ein.
         
         Weitere Informationen zum Erstellen eines neuen Mediensatzes finden Sie unter [Mediensätze, Medienfamilien und Sicherungssätze &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md).  
  
1. Aktivieren Sie (optional) im Abschnitt **Zuverlässigkeit** folgende Kontrollkästchen:  
  
    - **Sicherung nach dem Abschluss überprüfen**.  
  
    - **Vor dem Schreiben auf die Medien Prüfsumme bilden**, und optional **Continue on checksum error** (Bei Prüfsummenfehler fortfahren).
    
         Weitere Informationen zu Prüfsummen finden Sie unter [Mögliche Medienfehler während der Sicherung und Wiederherstellung &#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md).  
  
1. Wenn Sie auf ein Bandlaufwerk sichern (gemäß der Konfiguration im Abschnitt **Ziel** der Seite **Allgemein** ), ist die Option **Band nach dem Sichern entladen** aktiviert. Durch Klicken auf diese Option wird die Option **Band vor dem Entladen zurückspulen** aktiviert.  
  
    > [!NOTE]
    > Die Optionen im Abschnitt **Transaktionsprotokoll** sind inaktiv, es sei denn, Sie sichern ein Transaktionsprotokoll (wie im Abschnitt **Sicherungstyp** der Seite **Allgemein** angegeben).  
  
1. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] und höheren Versionen wird die [Sicherungskomprimierung](../../relational-databases/backup-restore/backup-compression-sql-server.md). Ob eine Sicherung standardmäßig komprimiert wird, ist abhängig vom Wert der Serverkonfigurationsoption **backup-compression default** . Sie können jedoch unabhängig von der aktuellen Standardeinstellung auf Serverebene eine Sicherung komprimieren, indem Sie die Option **Sicherung komprimieren**aktivieren, oder die Komprimierung verhindern, indem Sie die Option **Sicherung nicht komprimieren**aktivieren.  
  
     Informationen dazu, wie Sie Standardeinstellung für die Sicherungskomprimierung abrufen, finden Sie unter [Anzeigen oder Konfigurieren der Standardserverkonfigurationsoption für die Sicherungskomprimierung](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md).  

## <a name="using-transact-sql"></a>Verwenden von Transact-SQL
  
Verwenden Sie zum Erstellen einer Datei- oder Dateigruppensicherung eine [BACKUP DATABASE <Datei_oder_Dateigruppe>](../../t-sql/statements/backup-transact-sql.md)-Anweisung. Für diese Anweisung muss mindestens Folgendes angegeben werden:  
  
  - Der Datenbankname.  
  
  - Eine FILE- oder FILEGROUP-Klausel für jede Datei bzw. Dateigruppe.  
  
  - Das Sicherungsmedium, auf das die vollständige Sicherung geschrieben wird.  
  
Die grundlegende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Syntax für eine Dateisicherung lautet:  
  
  BACKUP DATABASE *database*  
  
  { FILE _=_ *logischer_Dateiname* | FILEGROUP _=_ *logischer_Dateigruppenname* } [ **,** ...*f* ]  
  
  TO *Sicherungsmedium* [ **,** ...*n* ]  
  
  [ WITH *mit_Optionen* [ **,** ...*o* ] ] ;  
  
|Option|und Beschreibung|  
|------------|-----------------|  
|*database*|Die Datenbank, für die ein Transaktionsprotokoll, eine Teildatenbank oder die vollständige Datenbank gesichert wird.|  
|FILE _=_ *logischer_Dateiname*|Gibt den logischen Namen einer Datei an, die in die Dateisicherung eingeschlossen werden soll.|  
|FILEGROUP _=_ *logischer_Dateigruppenname*|Gibt den logischen Namen einer Dateigruppe an, die in die Dateisicherung eingeschlossen werden soll. Beim einfachen Wiederherstellungsmodell wird die Dateigruppensicherung nur für eine schreibgeschützte Dateigruppe unterstützt.|  
|[ **,** ...*f* ]|Stellt einen Platzhalter dar, der anzeigt, dass mehrere Dateien und Dateigruppen angegeben werden können. Für die Anzahl der Dateien oder Dateigruppen gibt es keine Einschränkungen.|  
|*Sicherungsmedium* [ **,** ...*n* ]|Gibt eine Liste an, die zwischen 1 und 64 Sicherungsmedien für den Sicherungsvorgang enthalten kann. Sie können ein physisches Sicherungsmedium angeben oder ein entsprechendes logisches Sicherungsmedium, sofern es bereits definiert wurde. Geben Sie das physische Sicherungsmedium mithilfe der Option DISK oder TAPE an:<br /><br /> { DISK &#124; TAPE } _=_ *physischer_Sicherungsmediumname*<br /><br /> Weitere Informationen finden Sie unter [Sicherungsmedien &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)aufgezeichnet wurde.|  
|WITH *mit_Optionen* [ **,** ...*o* ]|Optional können eine oder mehrere zusätzliche Optionen (z. B. DIFFERENTIAL) angegeben werden. Für eine differenzielle Dateisicherung ist eine vollständige Dateisicherung als Basis erforderlich. <br /><br />Weitere Informationen finden Sie unter [Erstellen einer differenziellen Datenbanksicherung &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md).|  
  
Bei Verwendung des vollständigen Wiederherstellungsmodells müssen Sie auch das Transaktionsprotokoll sichern. Es müssen ausreichend Protokollsicherungen vorhanden sein, die alle Dateisicherungen umfassen, ausgehend von der ersten Dateisicherung, damit ein vollständiger Dateisicherungssatz für die Wiederherstellung der Datenbank verwendet werden kann.

Weitere Informationen finden Sie unter [Sichern eines Transaktionsprotokolls &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)bezeichnet) gesichert werden.  
  
###  <a name="TsqlExample"></a> Beispiele
In den folgenden Beispielen werden eine oder mehrere Dateien der sekundären Dateigruppen der `Sales` -Datenbank gesichert. Für diese Datenbank wird das vollständige Wiederherstellungsmodell verwendet, und es sind die folgenden sekundären Dateigruppen vorhanden:  
  
- Eine Dateigruppe namens `SalesGroup1` mit den Dateien `SGrp1Fi1` und `SGrp1Fi2`.  
  
- Eine Dateigruppe namens `SalesGroup2` mit den Dateien `SGrp2Fi1` und `SGrp2Fi2`.  
  
#### <a name="a-create-a-file-backup-of-two-files"></a>A. Erstellen einer Dateisicherung für zwei Dateien  
Im folgenden Beispiel wird eine differenzielle Dateisicherung für die `SGrp1Fi2` -Datei der Dateigruppe `SalesGroup1` und die `SGrp2Fi2` -Datei der Dateigruppe `SalesGroup2` erstellt.  
  
```sql  
--Backup the files in the SalesGroup1 secondary filegroup.  
BACKUP DATABASE Sales  
   FILE = 'SGrp1Fi2',   
   FILE = 'SGrp2Fi2'   
   TO DISK = 'G:\SQL Server Backups\Sales\SalesGroup1.bck';  
GO  
```  
  
#### <a name="b-create-a-full-file-backup-of-the-secondary-filegroups"></a>B. Erstellen einer vollständigen Dateisicherung der sekundären Dateigruppen  
Im folgenden Beispiel wird eine vollständige Dateisicherung von jeder Datei der beiden sekundären Dateigruppen erstellt.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck';  
GO  
```  
  
#### <a name="c-create-a-differential-file-backup-of-the-secondary-filegroups"></a>C. Erstellen einer differenziellen Dateisicherung der sekundären Dateigruppen  
Im folgenden Beispiel wird eine differenzielle Dateisicherung von jeder Datei der beiden sekundären Dateigruppen erstellt.  
  
```sql  
--Back up the files in SalesGroup1.  
BACKUP DATABASE Sales  
   FILEGROUP = 'SalesGroup1',  
   FILEGROUP = 'SalesGroup2'  
   TO DISK = 'C:\MySQLServer\Backups\Sales\SalesFiles.bck'  
   WITH   
      DIFFERENTIAL;  
GO  
```  
  
## <a name="PowerShellProcedure"></a> PowerShell

Richten Sie den [SQL Server PowerShell-Anbieter ein](../../relational-databases/scripting/sql-server-powershell-provider.md), und verwenden Sie ihn.
  
Verwenden Sie das Cmdlet **Backup-SqlDatabase** und geben Sie **Files** als Wert für den **-BackupAction** -Parameter an. Geben Sie zusätzlich einen der folgenden Parameter an:  
  
- Um eine bestimmte Datei zu sichern, geben Sie den Parameter _DatabaseFile_*Zeichenfolge* an, wobei *Zeichenfolge* mindestens einer zu sichernden Datenbankdatei entspricht.  
  
- Um alle Dateien in einer bestimmten Dateigruppe zu sichern, geben Sie den Parameter _-DatabaseFileGroup_*Zeichenfolge* an, wobei *Zeichenfolge* mindestens einer zu sichernden Datenbankdateigruppe entspricht.  
  
Im folgenden Beispiel wird eine vollständige Dateisicherung von jeder Datei in der sekundären Dateigruppe "FileGroup1" und "FileGroup2" in der `<myDatabase>` -Datenbank erstellt. Die Sicherungen werden am standardmäßigen Sicherungsspeicherort der Serverinstanz `Computer\Instance`erstellt.  

```powershell
Backup-SqlDatabase -ServerInstance Computer\Instance -Database <myDatabase> -BackupAction Files -DatabaseFileGroup "FileGroup1","FileGroup2" 
```
  
## <a name="see-also"></a>Weitere Informationen  
 [Übersicht über Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Sicherungsverlauf und Headerinformationen &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-history-and-header-information-sql-server.md)   
 [Datenbank sichern &#40;Seite „Allgemein“&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [Datenbank sichern &#40;Seite „Sicherungsoptionen“&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [Vollständige Dateisicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)   
 [Differenzielle Sicherungen &#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [Dateiwiederherstellungen &#40;vollständiges Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [Dateiwiederherstellungen &#40;einfaches Wiederherstellungsmodell&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)  
