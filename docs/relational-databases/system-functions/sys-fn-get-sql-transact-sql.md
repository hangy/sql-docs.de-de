---
title: Sys.fn_get_sql (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_get_sql
- sys.fn_get_sql_TSQL
- fn_get_sql_TSQL
- sys.fn_get_sql
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_sql function
- text [SQL Server], SQL handles
- sys.fn_get_sql function
- valid SQL handles [SQL Server]
- SQL handles
ms.assetid: d5fe49b5-0813-48f2-9efb-9187716b2fd4
author: rothja
ms.author: jroth
ms.openlocfilehash: 58cb9c4b35329a24db954460097dca5f7d87e4f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68120262"
---
# <a name="sysfngetsql-transact-sql"></a>sys.fn_get_sql (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt den Text der SQL-Anweisung für das angegebene SQL-Handle zurück.  
  
> [!IMPORTANT]  
>  Dieses Feature wird in einer künftigen Version von Microsoft SQL Server entfernt. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Verwenden Sie stattdessen sys.dm_exec_sql_text. Weitere Informationen finden Sie unter [Sys. dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.fn_get_sql ( SqlHandle )  
```  
  
## <a name="arguments"></a>Argumente  
 *SqlHandle*  
 Wert des Handles. *SqlHandle* ist **varbinary(64)** hat keinen Standardwert.  
  
## <a name="tables-returned"></a>Zurückgegebene Tabellen  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|dbid|**smallint**|Datenbank-ID Für Ad-hoc-Anweisungen und vorbereitete SQL-Anweisungen, die ID der Datenbank, in der die Anweisungen kompiliert wurden.|  
|objectid|**int**|ID des Datenbankobjekts. Dieser Wert ist für Ad-hoc-SQL-Anweisungen NULL.|  
|number|**smallint**|Gibt die Nummer der Gruppe an, wenn die Prozeduren gruppiert sind.<br /><br /> 0 = Einträge sind keine Prozeduren.<br /><br /> NULL = Ad-hoc-SQL-Anweisungen.|  
|encrypted|**bit**|Zeigt an, ob das Objekt verschlüsselt ist.<br /><br /> 0 = Nicht verschlüsselt<br /><br /> 1 = Verschlüsselt.|  
|text|**text**|Der Text der SQL-Anweisung. Der Wert ist für verschlüsselte Objekte NULL.|  
  
## <a name="remarks"></a>Hinweise  
 Sie erhalten ein gültiges SQL-Handle aus der Spalte sql_handle-Wert, der die [Sys. dm_exec_requests &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) dynamische verwaltungssicht.  
  
 Wenn Sie ein Handle, das nicht mehr übergeben vorhanden ist, im Cache, Fn_get_sq**l** wird ein leeres Resultset zurückgegeben. Wenn Sie ein ungültiges Handle übergeben, wird die Ausführung des Batches beendet und eine Fehlermeldung zurückgegeben.  
  
 Die [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] nicht zwischenspeichern einige [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungen, wie massenkopieranweisungen und Anweisungen mit Zeichenfolgenliteralen, die größer als 8 KB sind. Handles für diese Anweisungen können nicht mithilfe von fn_get_sql abgerufen werden.  
  
 Die **Text** -Spalte des Resultsets wird nach Text, der möglicherweise Kennwörter enthält gefiltert. Weitere Informationen zum Bezug gespeicherten-Prozeduren, die nicht überwacht werden, finden Sie unter [Filtern einer Ablaufverfolgung](../../relational-databases/sql-trace/filter-a-trace.md).  
  
 Die Fn_get_sql-Funktion gibt Informationen zurück, wie die [DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md) Befehl. Im Folgenden handelt es sich um Beispiele, in denen die fn_get_sql-Funktion verwendet werden kann, weil DBCC INPUTBUFFER nicht verwendet werden kann:  
  
-   Ereignisse umfassen mehr als 255 Zeichen.  
  
-   Sie möchten die höchste aktuelle Schachtelungsebene einer gespeicherten Prozedur zurückgeben. Es gibt z. B. zwei gespeicherte Prozeduren, die sp_1 und sp_2 benannt sind. Wenn sp_1 sp_2 ruft und Abrufen des Handles aus der dynamischen verwaltungssicht Sys. dm_exec_requests während sp_2 ausgeführt wird, gibt die Fn_get_sql-Funktion Informationen zu sp_2 zurück. Außerdem gibt die fn_get_sql-Funktion den gesamten Text der gespeicherten Prozedur auf der höchsten aktuellen Schachtelungsebene zurück.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Benutzer benötigt die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
 Datenbankadministratoren können die fn_get_sql-Funktion, wie im folgenden Beispiel gezeigt, für die Diagnose von Problemprozessen verwenden. Nachdem ein Administrator eine problematische Sitzungs-ID erkannt hat, kann der Administrator die SQL-Handle für diese Sitzung abrufen, fn_get_sql-Funktion mit dem Handle aufrufen und dann das Start- und Endoffsets verwenden, um zu bestimmen, die SQL-Text der problematischen Sitzungs-ID  
  
```  
DECLARE @Handle varbinary(64);  
SELECT @Handle = sql_handle   
FROM sys.dm_exec_requests   
WHERE session_id = 52 and request_id = 0;  
SELECT * FROM sys.fn_get_sql(@Handle);  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
