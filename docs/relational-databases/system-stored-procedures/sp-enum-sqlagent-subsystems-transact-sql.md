---
title: Sp_enum_sqlagent_subsystems (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_sqlagent_subsystems
- sp_enum_sqlagent_subsystems_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_sqlagent_subsystems
ms.assetid: 019a3c9d-bac3-495b-a70a-2c19f1d2e20e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 963cbcea93091eb48b8c73214ee3bc509f118e67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124671"
---
# <a name="spenumsqlagentsubsystems-transact-sql"></a>sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Führt die Subsysteme des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents in einer Liste auf.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## <a name="arguments"></a>Argumente  
 None  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**subsystem**|**nvarchar(40)**|Der Name des Subsystems.|  
|**description**|**nvarchar(512)**|Beschreibung des Subsystems.|  
|**subsystem_dll**|**nvarchar(510)**|DLL-Modul, das das Subsystem enthält.|  
|**agent_exe**|**nvarchar(510)**|Ausführbares Modul, das vom Subsystem verwendet wird.|  
|**start_entry_point**|**nvarchar(30)**|Prozedur, die der SQL Server-Agent während der Ausführung der Auftragsschritte aufruft.|  
|**event_entry_point**|**nvarchar(30)**|Prozedur, die der SQL Server-Agent während der Ausführung der Auftragsschritte aufruft.|  
|**stop_entry_point**|**nvarchar(30)**|Prozedur, die der SQL Server-Agent während der Ausführung der Auftragsschritte aufruft.|  
|**max_worker_threads**|**int**|Maximale Anzahl von Threads, die der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent für dieses Subsystem startet.|  
|**subsystem_id**|**int**|Bezeichner für das Subsystem.|  
  
## <a name="remarks"></a>Hinweise  
 Diese Prozedur listet die in der Instanz verfügbaren Subsysteme auf.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** diese gespeicherte Prozedur ausführen. Andere Benutzer müssen Mitglieder der festen Datenbankrolle **SQLAgentOperatorRole** in der **msdb** -Datenbank sein.  
  
 Weitere Informationen zu **SQLAgentOperatorRole**, finden Sie unter [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Implementieren von SQL Server-Agent-Sicherheit](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
