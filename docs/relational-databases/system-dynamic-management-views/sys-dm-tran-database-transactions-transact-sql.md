---
title: sys. dm_tran_database_transactions (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/09/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_database_transactions
- sys.dm_tran_database_transactions_TSQL
- dm_tran_database_transactions_TSQL
- sys.dm_tran_database_transactions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_database_transactions dynamic management view
ms.assetid: 82a44295-4cbc-4a5b-891a-8ebaf307b8f5
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a01dc7df9a8269190ae1c1c3cf05de3adaecc662
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982313"
---
# <a name="sysdm_tran_database_transactions-transact-sql"></a>sys.dm_tran_database_transactions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Gibt Informationen zu Transaktionen auf Datenbankebene zurück.  
  
> [!NOTE]  
>  Um diese DMV aus [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]aufzurufen, verwenden Sie den Namen **sys. dm_pdw_nodes_tran_database_transactions**.  
  
|Spaltenname|Datentyp|und Beschreibung|  
|-----------------|---------------|-----------------|  
|transaction_id|**bigint**|ID der Transaktion auf Instanzebene, nicht auf Datenbankebene. Diese ist nur in allen Datenbanken innerhalb einer Instanz eindeutig, nicht jedoch innerhalb aller Serverinstanzen.|  
|database_id|**int**|ID der Datenbank, die der Transaktion zugeordnet ist.|  
|database_transaction_begin_time|**datetime**|Zeitpunkt, zu dem die Datenbank in die Transaktion aufgenommen wurde. Genauer gesagt: Dies ist die Zeit des ersten Protokolldatensatzes in der Datenbank für die Transaktion.|  
|database_transaction_type|**int**|1 = Lese-/Schreibtransaktion<br /><br /> 2 = Schreibgeschützte Transaktion<br /><br /> 3 = Systemtransaktion|  
|database_transaction_state|**int**|1 = Die Transaktion wurde nicht initialisiert.<br /><br /> 3 = Die Transaktion wurde initialisiert, hat jedoch keine Protokolldatensätze generiert.<br /><br /> 4 = Die Transaktion hat Protokolldatensätze generiert.<br /><br /> 5 = Die Transaktion wurde vorbereitet.<br /><br /> 10 = Für die Transaktion wurde ein Commit ausgeführt.<br /><br /> 11 = Für die Transaktion wurde ein Rollback ausgeführt.<br /><br /> 12 = Für die Transaktion wird ein Commit ausgeführt. (Der Protokolldaten Satz wird generiert, aber noch nicht materialisiert oder persistent gespeichert.)|  
|database_transaction_status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_status2|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|database_transaction_log_record_count|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> Anzahl der Protokolldatensätze, die in der Datenbank für die Transaktion generiert wurden.|  
|database_transaction_replicate_record_count|**int**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> Die Anzahl der Protokolldaten Sätze, die in der Datenbank für die replizierte Transaktion generiert wurden.|  
|database_transaction_log_bytes_used|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> Anzahl von Bytes, die bisher im Datenbankprotokoll für die Transaktion verwendet wurden.|  
|database_transaction_log_bytes_reserved|**bigint**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> Anzahl von Bytes, die zur Verwendung im Datenbankprotokoll für die Transaktion reserviert wurden.|  
|database_transaction_log_bytes_used_system|**int**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> Anzahl von Bytes, die im Datenbankprotokoll für Systemtransaktionen bisher für diese Transaktion verwendet wurden.|  
|database_transaction_log_bytes_reserved_system|**int**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> Anzahl von Bytes, die im Datenbankprotokoll für Systemtransaktionen zur Verwendung für diese Transaktion reserviert wurden.|  
|database_transaction_begin_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> Protokollfolgenummer (Log Sequence Number, LSN) des ersten Datensatzes für die Transaktion im Datenbankprotokoll.|  
|database_transaction_last_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> LSN des zuletzt protokollierten Datensatzes für die Transaktion im Datenbankprotokoll.|  
|database_transaction_most_recent_savepoint_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> LSN des letzten Sicherungspunktes für die Transaktion im Datenbankprotokoll.|  
|database_transaction_commit_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> LSN des Protokolldatensatzes für den Commit der Transaktion im Datenbankprotokoll.|  
|database_transaction_last_rollback_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> LSN, zu der das letzte Rollback ausgeführt wurde. Wenn kein Rollback durchgeführt wurde, ist der Wert MaxLSN.|  
|database_transaction_next_undo_lsn|**numeric(25,0)**|**Gilt für**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher.<br /><br /> LSN des nächsten Datensatzes, der rückgängig gemacht werden soll.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)][!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, auf dem sich diese Distribution befindet.|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]ist `VIEW SERVER STATE` Berechtigung erforderlich.   
Bei [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium-Tarifen ist die `VIEW DATABASE STATE`-Berechtigung in der Datenbank erforderlich. In [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard-und Basic-Tarifen ist der **Server Administrator** oder ein **Azure Active Directory Administrator** Konto erforderlich.   

## <a name="see-also"></a>Siehe auch  
 [sys.dm_tran_active_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-transactions-transact-sql.md)   
 [sys.dm_tran_session_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-session-transactions-transact-sql.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungssichten und Funktionen in Verbindung mit Transaktionen &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


