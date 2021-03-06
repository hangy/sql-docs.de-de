---
title: Sys.dm_pdw_component_health_active_alerts (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c53e4a36-b841-424a-b8e2-255b1878deb6
author: stevestein
ms.author: sstein
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7378b5f4f87c2511909aef6b75c412b6043e8c71
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67899548"
---
# <a name="sysdmpdwcomponenthealthactivealerts-transact-sql"></a>sys.dm_pdw_component_health_active_alerts (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Speichert der aktive Warnungen auf [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Komponenten.  
  
|Spaltenname|Datentyp|Beschreibung|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Der eindeutige Bezeichner des eine [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Knoten.<br /><br /> Pdw_node_id, Component_id, Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|component_id|**int**|Die ID der Komponente. Finden Sie unter [sys.pdw_health_components &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md).<br /><br /> Pdw_node_id, Component_id, Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|component_instance_id|**nvarchar(255)**|Pdw_node_id, Component_id, Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|alert_id|**int**|Die ID für den Warnungstyp aus. Finden Sie unter [sys.pdw_health_alerts &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md).<br /><br /> Pdw_node_id, Component_id, Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|alert_instance_id|**nvarchar(36)**|Identifiziert eine Instanz einer bestimmten Warnung.<br /><br /> Pdw_node_id, Component_id, Component_instance_id, Alert_id und Alert_instance_id bilden den Schlüssel für diese Ansicht ein.|NOT NULL|  
|current_value|**nvarchar(255)**|Verwendet, wenn die Warnung vom Typ StatusChange ist. Dies ist der aktuelle Komponentenstatus. Wert ist NULL für Warnungen vom Typ Schwellenwert. Finden Sie unter [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) eine Liste der Warnungstypen.|NULL|  
|previous_value|**nvarchar(255)**|Verwendet, wenn die Warnung vom Typ StatusChange ist. Dies ist der vorherige Komponentenstatus. Wert ist NULL für Warnungen vom Typ Schwellenwert. Finden Sie unter [sys.pdw_health_alerts &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-pdw-health-alerts-transact-sql.md) eine Liste der Warnungstypen.|NULL|  
|create_time|**datetime**|Uhrzeit und Datum, wenn die Warnung generiert wurde.|NOT NULL|  
  
 Informationen zu den maximalen Zeilen, die von dieser Sicht beibehalten, finden Sie unter "Minimum und Maximum Values" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Datawarehouse und Parallel Data Warehouse-dynamische Verwaltungssichten &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
