---
title: Sys.pdw_table_mappings (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/01/2018
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1af14fe0-e562-4f48-a7f0-783f300a88ac
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1e8a4b17ad9f37546697714af9611b7e8dbf20c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068122"
---
# <a name="syspdwtablemappings-transact-sql"></a>sys.pdw_table_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Bindet Benutzertabellen nach internen Objektnamen durch **Object_id**.  
  
|Spaltenname|Datentyp|Beschreibung|Bereich|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar(36)**|Der physische Name für die Tabelle.<br /><br /> **Physical_name** und **Object_id** bilden den Schlüssel für diese Sicht.||  
|object_id|**int**|Die Objekt-ID für die Tabelle. Finden Sie unter [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).<br /><br /> **Physical_name** und **Object_id** bilden den Schlüssel für diese Sicht.||  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Data Warehouse- und Parallel Data Warehouse-Katalogsichten](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_index_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [sys.pdw_database_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-database-mappings-transact-sql.md)  
  
  
