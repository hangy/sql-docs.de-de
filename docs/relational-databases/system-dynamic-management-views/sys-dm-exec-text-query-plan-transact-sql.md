---
title: sys. dm_exec_text_query_plan (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_text_query_plan
- sys.dm_exec_text_query_plan_TSQL
- dm_exec_text_query_plan_TSQL
- sys.dm_exec_text_query_plan
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_text_query_plan dynamic management function
ms.assetid: 9d5e5f59-6973-4df9-9eb2-9372f354ca57
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d23813078c2a90b18af0a1df48079b571e77a13
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2019
ms.locfileid: "73983143"
---
# <a name="sysdm_exec_text_query_plan-transact-sql"></a>sys.dm_exec_text_query_plan (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Gibt den Showplan im Textformat für einen [!INCLUDE[tsql](../../includes/tsql-md.md)]-Batch oder für eine bestimmte Anweisung innerhalb des Batches zurück. Der vom Plan handle angegebene Abfrageplan kann entweder zwischengespeichert oder derzeit ausgeführt werden. Diese Tabellenwert Funktion ähnelt [sys. dm_exec_query_plan &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md), weist jedoch die folgenden Unterschiede auf:  
  
-   Die Ausgabe des Abfrageplans wird im Textformat zurückgegeben.  
-   Die Größe der Ausgabe des Abfrageplans ist nicht beschränkt.  
-   Im Batch können einzelne Anweisungen angegeben werden.  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlink (Symbol)") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_exec_text_query_plan   
(   
    plan_handle   
    , { statement_start_offset | 0 | DEFAULT }  
        , { statement_end_offset | -1 | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>Argumente  
*plan_handle*  
Ein Token, das einen Abfrage Ausführungsplan für einen Batch eindeutig identifiziert, der ausgeführt wurde und dessen Plan sich im Plancache befindet oder gerade ausgeführt wird. *plan_handle* ist vom Datentyp **varbinary(64)** .   

*plan_handle* kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden: 
  
-   [sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
-   [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-   [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  

-   [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  

-   [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
*statement_start_offset* | 0 | Vorgegebene  
Gibt die Startposition der Abfrage an (in Bytes), die von der Zeile im Text des zugehörigen Batches oder persistenten Objekts beschrieben wird. *statement_start_offset* ist vom Datentyp **int**. Der Wert 0 gibt den Anfang des Batches an. Der Standardwert ist 0.  
  
Der Startoffset der Anweisung kann aus den folgenden dynamischen Verwaltungsobjekten abgerufen werden:  
  
-  [sys.dm_exec_query_stats](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
  
-  [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
*statement_end_offset* | -1 | Vorgegebene  
Gibt (in Bytes) die Endposition der Abfrage an, die die Zeile innerhalb des Texts des Batches oder des persistenten Objekts beschreibt.  
  
*statement_start_offset* ist vom Datentyp **int**.  
  
Der Wert -1 gibt das Ende des Batches an. Der Standardwert ist -1.  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|und Beschreibung|  
|-----------------|---------------|-----------------|  
|**dbid**|**smallint**|ID der Kontextdatenbank, die gültig war, als die diesem Plan entsprechende [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisung kompiliert wurde. Für Ad-hoc-Anweisungen und vorbereitete SQL-Anweisungen, die ID der Datenbank, in der die Anweisungen kompiliert wurden.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
|**objectid**|**int**|ID des Objekts (z. B. gespeicherte Prozedur oder benutzerdefinierte Funktion) für diesen Abfrageplan. Für Ad-hoc- und vorbereitete Batches entspricht diese Spalte dem Wert **NULL**.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
|**number**|**smallint**|Gespeicherte Prozedur mit ganzer Zahl. Eine Gruppe von Prozeduren für die **orders** -Anwendung kann z. B. die Namen **orderproc;1**, **orderproc;2**usw. haben. Für Ad-hoc- und vorbereitete Batches entspricht diese Spalte dem Wert **NULL**.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
|**encrypted**|**bit**|Zeigt an, ob die entsprechende Prozedur verschlüsselt ist.<br /><br /> 0 = nicht verschlüsselt<br /><br /> 1 = verschlüsselt<br /><br /> NULL-Werte sind in der Spalte nicht zulässig.|  
|**query_plan**|**nvarchar(max)**|Enthält eine zur Kompilierzeit erstellte Showplandarstellung des Abfrageausführungsplans, der mit *plan_handle*angegeben ist. Der Showplan liegt im Textformat vor. Für jeden Batch, der z. B. Ad-hoc- [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, Aufrufe von gespeicherten Prozeduren und benutzerdefinierten Funktionen enthält, wird jeweils ein Plan generiert.<br /><br /> Die Spalte lässt NULL-Werte zu.|  
  
## <a name="remarks"></a>Remarks  
 Unter den folgenden Bedingungen wird keine Show Plan Ausgabe in der **Plan** -Spalte der zurückgegebenen Tabelle für **sys. dm_exec_text_query_plan**zurückgegeben:  
  
-   Falls der mit *plan_handle* angegebene Abfrageplan aus dem Plancache entfernt wurde, enthält die **query_plan** -Spalte der zurückgegebenen Tabelle den Wert NULL. Diese Bedingung kann z. b. auftreten, wenn eine Zeitverzögerung zwischen dem Erfassen des Plan Handles und dem Verwenden von **sys. dm_exec_text_query_plan**auftritt.  
  
-   Einige [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen werden nicht zwischengespeichert. Beispiele hierfür sind Anweisungen für Massenvorgänge oder Anweisungen mit Zeichenfolgenliteralen, die größer als 8 KB sind. Showplans für solche Anweisungen können nicht mithilfe von **sys. dm_exec_text_query_plan** abgerufen werden, da Sie nicht im Cache vorhanden sind.  
  
-   Wenn ein [!INCLUDE[tsql](../../includes/tsql-md.md)] Batch oder eine gespeicherte Prozedur einen aufzurufenden benutzerdefinierten Funktion oder einen aufzurufenden dynamischen SQL-Code (z. b. mit exec (*String*)) enthält, ist der kompilierte XML-Showplan für die benutzerdefinierte Funktion nicht in der Tabelle enthalten, die von **sys. dm_exec_text_query_plan** für den Batch oder die gespeicherte Prozedur zurückgegeben wird. Stattdessen müssen Sie einen **dm_exec_text_query_plan** separaten-Befehl für den *plan_handle* ausführen, der der benutzerdefinierten Funktion entspricht.  
  
Wenn eine Ad-hoc-Abfrage eine [einfache](../../relational-databases/query-processing-architecture-guide.md#SimpleParam) oder [erzwungene Parametrisierung](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)verwendet, enthält die **query_plan** Spalte nur den Anweisungs Text und nicht den tatsächlichen Abfrageplan. Um den Abfrageplan zurückzugeben, nennen Sie **sys. dm_exec_text_query_plan** für das Plan Handle der vorbereiteten parametrisierten Abfrage. Sie können anhand der **sql** -Spalte der [sys.syscacheobjects](../../relational-databases/system-compatibility-views/sys-syscacheobjects-transact-sql.md) -Sicht oder anhand der Textspalte der dynamischen [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) -Verwaltungssicht ermitteln, ob die Abfrage parametrisiert wurde.  
  
## <a name="permissions"></a>Berechtigungen  
 Zum Ausführen von **sys. dm_exec_text_query_plan**muss ein Benutzer Mitglied der festen Server Rolle **sysadmin** sein oder über die View Server State-Berechtigung auf dem Server verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-retrieving-the-cached-query-plan-for-a-slow-running-transact-sql-query-or-batch"></a>A. Abrufen des zwischengespeicherten Abfrageplans für eine langsam ausgeführte Transact-SQL-Abfrage oder einen langsam ausgeführten Transact-SQL-Batch  
 Wenn eine [!INCLUDE[tsql](../../includes/tsql-md.md)] -Abfrage oder ein -Batch für lange Zeit mit einer bestimmten Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ausgeführt wird, können Sie den Ausführungsplan für diese Abfrage oder diesen Batch abrufen, um die Ursache der Verzögerung zu ermitteln. Im folgenden Beispiel wird das Abrufen des Showplans für eine langsam ausgeführte Abfrage oder einen Batch gezeigt.  
  
> [!NOTE]  
> Ersetzen Sie zum Ausführen dieses Beispiels die Werte für *session_id* und *plan_handle* mit den Werten Ihres Servers.  
  
 Rufen Sie zunächst die Serverprozess-ID (SPID) für den Prozess ab, der die Abfrage oder den Batch ausführt, indem Sie die gespeicherte Prozedur `sp_who` verwenden:  
  
```sql  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
 Das von `sp_who` zurückgegebene Resultset gibt die SPID `54`an. Verwenden Sie die SPID nun mit der dynamischen Verwaltungssicht `sys.dm_exec_requests` , um das Planhandle mithilfe der folgenden Abfrage abzurufen:  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_requests  
WHERE session_id = 54;  
GO  
```  
  
 Die von **sys. dm_exec_requests** zurückgegebene Tabelle gibt an, dass das Plan Handle für die Abfrage oder den Batch mit langsamer Ausführung `0x06000100A27E7C1FA821B10600`ist. Im folgenden Beispiel wird der Abfrageplan für das angegebene Planhandle zurückgegeben, und die Standardwerte 0 und -1 werden verwendet, um alle Anweisungen in der Abfrage oder im Batch zurückzugeben.  
  
```sql  
USE master;  
GO  
SELECT query_plan   
FROM sys.dm_exec_text_query_plan (0x06000100A27E7C1FA821B10600,0,-1);  
GO  
```  
  
### <a name="b-retrieving-every-query-plan-from-the-plan-cache"></a>B. Abrufen aller Abfrage Pläne aus dem Plancache  
 Wenn Sie eine Momentaufnahme aller im Plancache gespeicherten Abfragen abrufen möchten, rufen Sie die Planhandles aller Abfragepläne im Cache ab, indem Sie die dynamische Verwaltungssicht `sys.dm_exec_cached_plans` abfragen. Die Planhandles sind in der `plan_handle` -Spalte von `sys.dm_exec_cached_plans`gespeichert. Verwenden Sie dann den CROSS APPLY-Operator, um die Planhandles wie folgt an `sys.dm_exec_text_query_plan` zu übergeben. Die Show Plan Ausgabe für jeden aktuell im Plancache gespeicherten Plan wird in der `query_plan`-Spalte der zurückgegebenen Tabelle angezeigt.  
  
```sql  
USE master;  
GO  
SELECT *   
FROM sys.dm_exec_cached_plans AS cp   
CROSS APPLY sys.dm_exec_text_query_plan(cp.plan_handle, DEFAULT, DEFAULT);  
GO  
```  
  
### <a name="c-retrieving-every-query-plan-for-which-the-server-has-gathered-query-statistics-from-the-plan-cache"></a>C. Abrufen von jedem Abfrageplan, für den der Server eine Abfrage Statistik aus dem Plancache erfasst hat  
 Wenn Sie eine Momentaufnahme aller im Plancache gespeicherten Abfragen abrufen möchten, für die der Server eine Statistik erfasst hat, rufen Sie die Planhandles dieser Pläne im Cache ab, indem Sie die dynamische Verwaltungssicht `sys.dm_exec_query_stats` abfragen. Die Planhandles sind in der `plan_handle` -Spalte von `sys.dm_exec_query_stats`gespeichert. Verwenden Sie dann den CROSS APPLY-Operator, um die Planhandles wie folgt an `sys.dm_exec_text_query_plan` zu übergeben. Die Showplanausgabe für die einzelnen Pläne befindet sich in der `query_plan`-Spalte der zurückgegebenen Tabelle.  
  
```sql  
USE master;  
GO  
SELECT * FROM sys.dm_exec_query_stats AS qs   
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, qs.statement_start_offset, qs.statement_end_offset);  
GO  
```  
  
### <a name="d-retrieving-information-about-the-top-five-queries-by-average-cpu-time"></a>D. Abrufen von Informationen zu den fünf Abfragen mit der höchsten durchschnittlichen CPU-Zeit  
 Im folgenden Beispiel werden die Abfragepläne und die durchschnittliche CPU-Zeit für die fünf Abfragen mit der höchsten durchschnittlichen CPU-Zeit zurückgegeben. Die **sys. dm_exec_text_query_plan** -Funktion gibt die Standardwerte 0 und-1 an, um alle Anweisungen im Batch im Abfrageplan zurückzugeben.  
  
```sql  
SELECT TOP 5 total_worker_time/execution_count AS [Avg CPU Time],  
Plan_handle, query_plan   
FROM sys.dm_exec_query_stats AS qs  
CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, 0, -1)  
ORDER BY total_worker_time/execution_count DESC;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)  
