---
title: sys. DM _exec_compute_node_errors (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SYS.DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
- DM_EXEC_COMPUTE_NODE_ERRORS
- DM_EXEC_COMPUTE_NODE_ERRORS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PolyBase
- PolyBase, views
- dm_exec_compute_node_errors
- sys.dm_exec_compute_node_errors management view
ms.assetid: 9a03c039-70e4-4974-95d8-d3fa45984ffb
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b074da717a2c5deac9d576da938d1229dafeac77
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532791"
---
# <a name="sysdm_exec_compute_node_errors-transact-sql"></a>sys. DM _exec_compute_node_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Gibt Fehler zurück, die auf polybase-Computeknoten auftreten.  
  
|Spaltenname|Datentyp|Beschreibung|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|error_id|`nvarchar(36)`|Eindeutige numerische ID, die dem Fehler zugeordnet ist.|Eindeutig in allen Abfrage Fehlern im System|  
|Quelle|`nvarchar(255)`|Quellthread oder PROZESSBESCHREIBUNG||  
|type|`nvarchar(255)`|Fehlertyp.||  
|create_time|`datetime`|Der Zeitpunkt des Auftretens des Fehlers.||  
|compute_node_id|`int`|Bezeichner des spezifischen computeknotens|Siehe compute_node_id of [sys. DM _exec_compute_nodes &#40;Transact-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)|  
|rexecution_id|`nvarchar(36)`|Der Bezeichner der polybase-Abfrage, falls vorhanden.||  
|spid|`int`|Bezeichner der SQL Server Sitzung||  
|thread_id|`int`|Numerischer Bezeichner des Threads, in dem der Fehler aufgetreten ist.||  
|Details|nvarchar(4000)|Vollständige Beschreibung der Details des Fehlers.||
|compute_pool_id|`int`|Eindeutiger Bezeichner für den Pool.|

  
## <a name="see-also"></a>Siehe auch  
 [Problembehandlung bei polybase mit dynamischen Verwaltungs Sichten](https://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Dynamische Verwaltungs Sichten &#40;in Verbindung mit der Datenbank Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
