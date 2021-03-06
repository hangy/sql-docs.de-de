---
title: sp_purge_jobhistory (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_jobhistory_TSQL
- sp_purge_jobhistory
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_jobhistory
ms.assetid: 237f9bad-636d-4262-9bfb-66c034a43e88
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ad5e7a1d03dde408da52ca2b5ebe6b40f10c06c9
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313756"
---
# <a name="sp_purge_jobhistory-transact-sql"></a>sp_purge_jobhistory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Entfernt die Verlaufsdatensätze für einen Auftrag.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_purge_jobhistory   
   {   [ @job_name = ] 'job_name' |   
     | [ @job_id = ] job_id }  
   [ , [ @oldest_date = ] oldest_date ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @job_name = ] 'job_name'` den Namen des Auftrags, für den die Verlaufs Datensätze gelöscht werden sollen. *job_name*ist vom **Datentyp vom Datentyp sysname**und hat den Standardwert NULL. Es muss entweder *job_id* oder *job_name* angegeben werden, aber beide können nicht angegeben werden.  
  
> [!NOTE]  
>  Mitglieder der festen Server Rolle **sysadmin** oder Mitglieder der festen Daten Bank Rolle **SQLAgentOperatorRole** können **sp_purge_jobhistory** ohne Angabe eines *job_name* oder *job_id*ausführen. Wenn **sysadmin** -Benutzer diese Argumente nicht angeben, wird der Auftrags Verlauf für alle lokalen und Multiserveraufträge innerhalb der durch *oldest_date*angegebenen Zeit gelöscht. Wenn **SQLAgentOperatorRole** -Benutzer diese Argumente nicht angeben, wird der Auftrags Verlauf für alle lokalen Aufträge innerhalb der durch *oldest_date*angegebenen Zeit gelöscht.  
  
`[ @job_id = ] job_id` die Auftrags-ID des Auftrags für die zu löschenden Datensätze. *job_id* ist vom Datentyp **uniqueidentifier**. der Standardwert ist NULL. Es muss entweder *job_id* oder *job_name* angegeben werden, aber beide können nicht angegeben werden. Informationen dazu, wie **sysadmin** -oder **SQLAgentOperatorRole** -Benutzer dieses Argument verwenden können, finden Sie in der Beschreibung **\@job_name** .  
  
`[ @oldest_date = ] oldest_date` der älteste Datensatz, der im Verlauf beibehalten werden soll. *oldest_date* ist vom **Datentyp DateTime**und hat den Standardwert NULL. Wenn *oldest_date* angegeben wird, entfernt **sp_purge_jobhistory** nur Datensätze, die älter sind als der angegebene Wert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 None  
  
## <a name="remarks"></a>Hinweise  
 Wenn **sp_purge_jobhistory** erfolgreich abgeschlossen wird, wird eine Meldung zurückgegeben.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig können diese gespeicherte Prozedur nur von Mitgliedern der festen Server Rolle **sysadmin** oder der festen Daten Bank Rolle **SQLAgentOperatorRole** ausgeführt werden. Mitglieder von **sysadmin** können den Auftrags Verlauf für alle lokalen und Multiserveraufträge bereinigen. Mitglieder von **SQLAgentOperatorRole** können den Auftrags Verlauf nur für alle lokalen Aufträge löschen.  
  
 Anderen Benutzern, einschließlich der Mitglieder von **SQLAgentUserRole** und den Mitgliedern von **SQLAgentReaderRole**, muss explizit die EXECUTE-Berechtigung für **sp_purge_jobhistory**erteilt werden. Nachdem die EXECUTE-Berechtigung für diese gespeicherte Prozedur erteilt wurde, können dieses Benutzer nur den Verlauf für Aufträge leeren, deren Besitzer sie sind.  
  
 Die SQL Server-Daten bankrollen **SQLAgentUserRole**, **SQLAgentReaderRole**und **SQLAgentOperatorRole** befinden sich in der **msdb** -Datenbank. Ausführliche Informationen zu ihren Berechtigungen finden Sie unter [SQL Server-Agent fester Daten bankrollen](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-remove-history-for-a-specific-job"></a>A. Entfernen des Verlaufs für einen bestimmten Auftrag  
 Im folgenden Beispiel wird der Verlauf eines Auftrags mit dem Namen `NightlyBackups` entfernt.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory  
    @job_name = N'NightlyBackups' ;  
GO  
```  
  
### <a name="b-remove-history-for-all-jobs"></a>B. Entfernen des Verlaufs für alle Aufträge  
  
> [!NOTE]  
>  Nur Mitglieder der festen Server Rolle **sysadmin** und die Mitglieder der **SQLAgentOperatorRole** können den Verlauf für alle Aufträge entfernen. Wenn **sysadmin** -Benutzer diese gespeicherte Prozedur ohne Parameter ausführen, wird der Auftrags Verlauf für alle lokalen und Multiserveraufträge bereinigt. Wenn **SQLAgentOperatorRole** -Benutzer diese gespeicherte Prozedur ohne Parameter ausführen, wird nur der Auftrags Verlauf für alle lokalen Aufträge gelöscht.  
  
 Im folgenden Beispiel wird die Prozedur ohne Parameter ausgeführt, um alle Verlaufsdatensätze zu entfernen.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_purge_jobhistory ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_help_job &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-job-transact-sql.md)   
 [sp_help_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-jobhistory-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [GRANT (Objektberechtigungen) &#40;Transact-SQL&#41;](../../t-sql/statements/grant-object-permissions-transact-sql.md)  
  
  
