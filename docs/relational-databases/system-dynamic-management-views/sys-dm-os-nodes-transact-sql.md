---
title: dm_os_nodes (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 02/13/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_nodes
- dm_os_nodes_TSQL
- dm_os_nodes
- sys.dm_os_nodes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_nodes dynamic management view
ms.assetid: c768b67c-82a4-47f5-850b-0ea282358d50
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b2b6f88e857ab7fc6300698174914126fb0881f6
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265727"
---
# <a name="sysdmosnodes-transact-sql"></a>sys.dm_os_nodes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Eine interne Komponente mit der Bezeichnung SQLOS erstellt Knotenstrukturen, die die Lage des Hardwareprozessors imitieren. Diese Strukturen können geändert werden, mithilfe von [Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) um benutzerdefinierte knotenlayouts zu erstellen.  

> [!NOTE]
> Beginnend mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] Soft-NUMA automatisch bestimmte Hardwarekonfigurationen verwenden. Weitere Informationen finden Sie unter [automatischen Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md#automatic-soft-numa).
  
Die folgende Tabelle enthält Informationen zu diesen Knoten.  
  
> [!NOTE]
> Diese DMV aus aufrufen [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_nodes**.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|node_id|**smallint**|ID des Knotens.|  
|node_state_desc|**nvarchar(256)**|Beschreibung des Knotenzustands. Die Werte werden zuerst mit den sich gegenseitig ausschließenden Werten angezeigt, gefolgt von den kombinierbaren Werten. Zum Beispiel:<br /> Online, Thread Resources Low, Lazy Preemptive<br /><br />Es gibt vier sich gegenseitig ausschließende Node_state_desc-Werte. Sie können mit ihren Beschreibungen sind unten aufgeführt.<br /><ul><li>ONLINE: Knoten ist online<li>OFFLINE: Knoten ist offline<li>IDLE: Knoten verfügt über keine ausstehenden arbeitsanforderungen und hat einen Leerlaufzustand angenommen.<li>IDLE_READY: Knoten verfügt über keine ausstehenden arbeitsanforderungen und ist bereit für den Leerlauf wechselt.</li></ul><br />Es gibt drei kombinierbare Node_state_desc-Werte, die unten aufgeführten, mit ihren Beschreibungen aufgeführt.<br /><ul><li>DAC: Dieser Knoten ist reserviert für die [dedizierte Verwaltungsverbindung](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md).<li>THREAD_RESOURCES_LOW: Keine neuen Threads können aufgrund einer Bedingung für geringen Arbeitsspeicher auf diesem Knoten erstellt werden.<li>IM LAUFENDEN SYSTEMBETRIEB HINZUGEFÜGT: Gibt an, die Knoten hinzugefügt wurden, als Reaktion auf ein Hinzufügen von CPUS.</li></ul>|  
|memory_object_address|**varbinary(8)**|Adresse des Speicherobjekts ist diesem Knoten zugeordnet. 1: 1-Beziehung zu [Sys. dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md).memory_object_address.|  
|memory_clerk_address|**varbinary(8)**|Adresse des Speicherclerks ist diesem Knoten zugeordnet. 1: 1-Beziehung zu [Sys. dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md).memory_clerk_address.|  
|io_completion_worker_address|**varbinary(8)**|Adresse des Arbeitsthreads ist dem E/A-Abschluss für diesen Knoten zugewiesen. 1: 1-Beziehung zu [dm_os_workers](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md).worker_address.|  
|memory_node_id|**smallint**|ID des Arbeitsspeicherknotens, zu dem dieser Knoten gehört. Zu viele-zu-eins-Beziehung [dm_os_memory_nodes](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-nodes-transact-sql.md).memory_node_id.|  
|cpu_affinity_mask|**bigint**|Bitmap, das die CPUs identifiziert, die diesem Knoten zugeordnet sind.|  
|online_scheduler_count|**smallint**|Die Anzahl der onlinescheduler, die von diesem Knoten verwaltet werden.|  
|idle_scheduler_count|**smallint**|Anzahl der Onlinescheduler, die über keinen aktiven Arbeitsthread verfügen.|  
|active_worker_count|**int**|Anzahl der Arbeitsthreads, die auf allen von diesem Knoten verwalteten Zeitplanungsmodulen aktiv sind.|  
|avg_load_balance|**int**|Durchschnittliche Anzahl von Tasks pro Zeitplanungsmodul auf diesem Knoten.|  
|timer_task_affinity_mask|**bigint**|Bitmap, das die Zeitplanungsmodule identifiziert, denen Zeitgebertasks zugewiesen sein können.|  
|permanent_task_affinity_mask|**bigint**|Bitmap, das die Zeitplanungsmodule identifiziert, denen permanente Zeitgebertasks zugewiesen sein können.|  
|resource_monitor_state|**bit**|Jeder Knoten verfügt über einen zugewiesenen Ressourcenmonitor. Der Ressourcenmonitor kann ausgeführt werden oder sich im Leerlauf befinden. Der Wert 1 gibt an, dass der Monitor ausgeführt wird, der Wert 0 gibt an, dass er sich im Leerlauf befindet.|  
|online_scheduler_mask|**bigint**|Identifiziert die Prozessaffinitätsmaske für diesen Knoten.|  
|processor_group|**smallint**|Identifiziert die Gruppe von Prozessoren für diesen Knoten.|  
|cpu_count |**int** |Anzahl der CPUs, die für diesen Knoten verfügbar. |
|pdw_node_id|**int**|Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.<br /><br /> **Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]|  
  
## <a name="permissions"></a>Berechtigungen

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium-Tarife, erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank. Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Standard und Basic-Version, erfordert die **Serveradministrator** oder **Azure Active Directory-Administrator** Konto.   

## <a name="see-also"></a>Siehe auch    
 [Dynamische Verwaltungssichten in Verbindung mit SQL Server-Betriebssystem &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
