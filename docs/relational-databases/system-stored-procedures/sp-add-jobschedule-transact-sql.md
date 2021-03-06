---
title: sp_add_jobschedule (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_jobschedule
- sp_add_jobschedule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_jobschedule
ms.assetid: ffce19d9-d1d6-45b4-89fd-ad0f60822ba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 06dbee74cfb3e2d5e697ea9594d46c98557de8ef
ms.sourcegitcommit: df1f71231f8edbdfe76e8851acf653c25449075e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2019
ms.locfileid: "70810495"
---
# <a name="sp_add_jobschedule-transact-sql"></a>sp_add_jobschedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Erstellt einen Zeitplan für einen SQL Agent-Auftrag.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
  > [!IMPORTANT]  
  > In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_jobschedule [ @job_id = ] job_id, | [ @job_name = ] 'job_name', [ @name = ] 'name'  
     [ , [ @enabled = ] enabled_flag ]  
     [ , [ @freq_type = ] frequency_type ]  
     [ , [ @freq_interval = ] frequency_interval ]  
     [ , [ @freq_subday_type = ] frequency_subday_type ]  
     [ , [ @freq_subday_interval = ] frequency_subday_interval ]  
     [ , [ @freq_relative_interval = ] frequency_relative_interval ]  
     [ , [ @freq_recurrence_factor = ] frequency_recurrence_factor ]  
     [ , [ @active_start_date = ] active_start_date ]  
     [ , [ @active_end_date = ] active_end_date ]  
     [ , [ @active_start_time = ] active_start_time ]  
     [ , [ @active_end_time = ] active_end_time ]  
     [ , [ @schedule_id = ] schedule_id OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @job_id = ] job_id`Die ID des Auftrags, dem der Zeitplan hinzugefügt wird. *job_id* ist vom Datentyp **uniqueidentifier**und hat keinen Standardwert.  
  
`[ @job_name = ] 'job_name'`Der Name des Auftrags, dem der Zeitplan hinzugefügt wird. *job_name* ist vom Datentyp **nvarchar (128)** und hat keinen Standardwert.  
  
> [!NOTE]  
>  Es muss entweder *job_id* oder *job_name* angegeben werden, aber beide können nicht angegeben werden.  
  
`[ @name = ] 'name'`Der Name des Zeitplans. *Name ist vom Datentyp* **nvarchar (128)** und hat keinen Standardwert.  
  
`[ @enabled = ] enabled_flag`Gibt den aktuellen Status des Zeitplans an. *enabled_flag* ist vom Datentyp **tinyint**. der Standardwert ist **1** (aktiviert). Wenn der Wert **0**ist, ist der Zeitplan nicht aktiviert. Wenn der Zeitplan deaktiviert ist, wird der Auftrag nicht ausgeführt.  
  
`[ @freq_type = ] frequency_type`Ein Wert, der angibt, wann der Auftrag ausgeführt werden soll. *frequency_type* ist vom Datentyp **int**und hat den Standardwert **0**. die folgenden Werte sind möglich:  
  
|Wert|Description|  
|-----------|-----------------|  
|**1**|Einmal|  
|**4**|Täglich|  
|**8**|Wöchentlicher Zeitplan|  
|**16**|Monatlicher Zeitplan|  
|**32**|Monatlich, relativ zu *frequency_interval.*|  
|**64**|Ausführen, wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent-Dienst gestartet wird.|  
|**128**|Ausführen, wenn sich der Computer im Leerlauf befindet.|  
  
`[ @freq_interval = ] frequency_interval`Der Tag, an dem der Auftrag ausgeführt wird. *frequency_interval* ist vom Datentyp **int**und hat den Standardwert 0. der Wert hängt vom Wert von *frequency_type* ab, wie in der folgenden Tabelle angegeben:  
  
|Wert|Wirkung|  
|-----------|------------|  
|**1** (einmal)|*frequency_interval* wird nicht verwendet.|  
|**4** (täglich)|Alle *frequency_interval* Tage.|  
|**8** (wöchentlich)|*frequency_interval* ist eine oder mehrere der folgenden (kombiniert mit einem logischen OR-Operator):<br /><br /> 1 = Sonntag<br /><br /> 2 = Montag<br /><br /> 4 = Dienstag<br /><br /> 8 = Mittwoch<br /><br /> 16 = Donnerstag<br /><br /> 32 = Freitag<br /><br /> 64 = Samstag|  
|**16** (monatlich)|Am *frequency_interval* Tag des Monats.|  
|**32** (monatlich, relativ)|*frequency_interval* ist einer der folgenden:<br /><br /> 1 = Sonntag<br /><br /> 2 = Montag<br /><br /> 3 = Dienstag<br /><br /> 4 = Mittwoch<br /><br /> 5 = Donnerstag<br /><br /> 6 = Freitag<br /><br /> 7 = Samstag<br /><br /> 8 = Tag<br /><br /> 9 = Arbeitstag<br /><br /> 10 = Wochenendtag|  
|**64** (beim Starten [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] des-Agent-Dienstanbieter)|*frequency_interval* wird nicht verwendet.|  
|**128**|*frequency_interval* wird nicht verwendet.|  
  
`[ @freq_subday_type = ] frequency_subday_type`Gibt die Einheiten für *frequency_subday_interval*an. *frequency_subday_type* ist vom Datentyp **int**und hat keinen Standardwert. die folgenden Werte sind möglich:  
  
|Wert|Beschreibung (Einheit)|  
|-----------|--------------------------|  
|**0x1**|Zum angegebenen Zeitpunkt|  
|**0x4**|Minuten|  
|**0x8**|Stunden|  
  
`[ @freq_subday_interval = ] frequency_subday_interval`Anzahl der *frequency_subday_type* Zeiträume zwischen den einzelnen Ausführungen des Auftrags. *frequency_subday_interval* ist vom Datentyp **int**und hat den Standardwert 0.  
  
`[ @freq_relative_interval = ] frequency_relative_interval`Definiert das *frequency_interval* , wenn *frequency_type* auf **32** (monatlich, relativ) festgelegt ist.  
  
 *frequency_relative_interval* ist vom Datentyp **int**und hat keinen Standardwert. die folgenden Werte sind möglich:  
  
|Wert|Beschreibung (Einheit)|  
|-----------|--------------------------|  
|**1**|Erster|  
|**2**|Zweimal|  
|**4**|Dritter|  
|**8**|Vierter|  
|**16**|Letzter|  
  
 *frequency_relative_interval* gibt das Vorkommen des Intervalls an. Wenn *frequency_relative_interval* beispielsweise auf **2**festgelegt ist, *frequency_type* auf **32**und *frequency_interval* auf **3**festgelegt ist, erfolgt der geplante Auftrag am zweiten Dienstag jedes Monats.  
  
`[ @freq_recurrence_factor = ] frequency_recurrence_factor`Anzahl der Wochen oder Monate zwischen der geplanten Ausführung des Auftrags. *frequency_recurrence_factor* wird nur verwendet, wenn *frequency_type* auf **8**, **16**oder **32**festgelegt ist. *frequency_recurrence_factor* ist vom Datentyp **int**und hat den Standardwert 0.  
  
`[ @active_start_date = ] active_start_date`Das Datum, an dem die Ausführung des Auftrags beginnen kann. *active_start_date* ist vom Datentyp **int**und hat keinen Standardwert. Das Datum wird als YYYYMMDD formatiert. Wenn *active_start_date* festgelegt ist, muss das Datum größer oder gleich 19900101 sein.  
  
 Überprüfen Sie nach dem Erstellen des Zeitplans, ob das Startdatum korrekt ist. Weitere Informationen finden Sie im Abschnitt "Planen des Start Datums" unter [Erstellen und Anfügen von Zeitplänen an Aufträge](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
`[ @active_end_date = ] active_end_date`Datum, an dem die Ausführung des Auftrags beendet werden kann. *active_end_date* ist vom Datentyp **int**und hat keinen Standardwert. Das Datum wird als YYYYMMDD formatiert.  
  
`[ @active_start_time = ] active_start_time`Uhrzeit an einem beliebigen Tag zwischen *active_start_date* und *active_end_date* , um die Auftragsausführung zu beginnen. *active_start_time* ist vom Datentyp **int**und hat keinen Standardwert. Die Uhrzeit wird in einem 24-Stunden-Format als HHMMSS formatiert.  
  
`[ @active_end_time = active_end_time_`Uhrzeit an einem beliebigen Tag zwischen *active_start_date* und *active_end_date* zum Beenden der Auftragsausführung. *active_end_time* ist vom Datentyp **int**und hat keinen Standardwert. Die Uhrzeit wird in einem 24-Stunden-Format als HHMMSS formatiert.  
  
`[ @schedule_id = schedule_idOUTPUT`Die Zeitplan-ID, die dem Zeitplan zugewiesen wird, wenn Sie erfolgreich erstellt wurde. *schedule_id* ist eine Ausgabevariable vom Typ **int**und hat keinen Standardwert.  
  
`[ @schedule_uid = ] _schedule_uidOUTPUT`Ein eindeutiger Bezeichner für den Zeitplan. *schedule_uid* ist eine Variable vom Typ **uniqueidentifier**.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 None  
  
## <a name="remarks"></a>Hinweise  
 Auftragszeitpläne können jetzt unabhängig von Aufträgen verwaltet werden. Wenn Sie einem Auftrag einen Zeitplan hinzufügen möchten, verwenden Sie **sp_add_schedule** , um den Zeitplan zu erstellen, und **sp_attach_schedule** , um den Zeitplan an einen Auftrag anzufügen.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Datenbankrollen in der **msdb** -Datenbank sein:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 Weitere Informationen zu den Berechtigungen dieser Rollen finden Sie unter [Feste Datenbankrollen des SQL Server-Agents](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
 
 ## <a name="example"></a>Beispiel
 Im folgenden Beispiel wird ein Auftrags Zeitplan zugewiesen `SaturdayReports` , der jeden Samstag um 2:00 Uhr ausgeführt wird.
```sql  
EXEC msdb.dbo.sp_add_jobschedule 
        @job_name = N'SaturdayReports', -- Job name
        @name = N'Weekly_Sat_2AM',  -- Schedule name
        @freq_type = 8, -- Weekly
        @freq_interval = 64, -- Saturday
        @freq_recurrence_factor = 1, -- every week
        @active_start_time = 20000 -- 2:00 AM
```
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anfügen von Zeitplänen an Aufträge](../../ssms/agent/create-and-attach-schedules-to-jobs.md)   
 [Planen eines Auftrags](../../ssms/agent/schedule-a-job.md)   
 [Erstellen eines Zeitplans](../../ssms/agent/create-a-schedule.md)   
 [SQL Server-Agent gespeicherter &#40;Prozeduren (Transact-SQL)&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-schedule-transact-sql.md)   
 [sp_update_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-schedule-transact-sql.md)   
 [sp_delete_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-schedule-transact-sql.md)   
 [sp_help_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-schedule-transact-sql.md)   
 [sp_attach_schedule &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-schedule-transact-sql.md)  
  
  
