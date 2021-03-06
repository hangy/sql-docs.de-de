---
title: index_columns (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_columns
- sys.index_columns_TSQL
- index_columns
- index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.index_columns catalog view
ms.assetid: 211471aa-558a-475c-9b94-5913c143ed12
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e20bd7ecc783e0449a1deaa21c9f3db6e07abbc7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122668"
---
# <a name="sysindexcolumns-transact-sql"></a>sys.index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Enthält eine Zeile pro Spalte, die Teil einer **sys.indexes** Index oder einer unsortierten Tabelle (Heap).  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID des Objekts, für das der Index definiert wird|  
|**index_id**|**int**|ID des Indexes, in dem die Spalte definiert wird|  
|**index_column_id**|**int**|Die ID der Indexspalte. **Index_column_id** ist nur innerhalb eindeutig **Index_id**.|  
|**column_id**|**int**|ID der Spalte in **object_id**.<br /><br /> 0 = Zeilenbezeichner (RID, Row Identifier) in einem nicht gruppierten Index.<br /><br /> **column_id** ist nur innerhalb von **object_id**eindeutig.|  
|**key_ordinal**|**tinyint**|Ordinalzahl (auf 1 basierend) innerhalb einer Gruppe von Schlüsselspalten.<br /><br /> 0 = Keine Schlüsselspalte oder ein XML-Index, columnstore-Index oder räumlicher Index.<br /><br /> Hinweis: Ein XML-Index oder räumlichen Index kann nicht kein Schlüssel sein, da die zugrunde liegenden Spalten nicht vergleichbar sind, was bedeutet, dass ihre Werte nicht sortiert werden können.|  
|**partition_ordinal**|**tinyint**|Ordinalzahl (1-basiert) innerhalb einer Gruppe von Partitionierungsspalten. Ein gruppierter columnstore-Index kann maximal 1 Partitionierungsspalte aufweisen.<br /><br /> 0 = Keine Partitionierungsspalte.|  
|**is_descending_key**|**bit**|1 = Indexschlüsselspalte hat eine absteigende Sortierreihenfolge.<br /><br /> 0 = Indexschlüsselspalte hat eine aufsteigende Sortierreihenfolge, oder die Spalte ist Teil eines columnstore-Indexes oder Hashindexes.|  
|**is_included_column**|**bit**|1 = Spalte ist eine Nichtschlüsselspalte, die dem Index mit der CREATE INDEX INCLUDE-Klausel hinzugefügt wurde, oder die Spalte ist Teil eines columnstore-Indexes.<br /><br /> 0 = Spalte ist keine eingeschlossene Spalte.<br /><br /> Spalten, die implizit hinzugefügt werden, da sie Teil der Gruppierungsschlüssel sind nicht in aufgeführt werden **index_columns**.<br /><br /> Spalten, die implizit hinzugefügt wurden, da sie eine Partitionierungsspalte sind, werden als 0 zurückgegeben.| 
|**column_store_order_ordinal**</br> Betrifft: Azure SQL Data Warehouse (Vorschau)|**tinyint**|Ordinalzahl (1-basiert) in der Reihenfolge der Spalten in einem geordneten gruppierten columnstore-Index fest|
  
## <a name="permissions"></a>Berechtigungen

 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Beispiele

 Im folgenden Beispiel werden alle Indizes und Indexspalten für die Tabelle `Production.BillOfMaterials` zurückgegeben.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT i.name AS index_name  
    ,COL_NAME(ic.object_id,ic.column_id) AS column_name  
    ,ic.index_column_id  
    ,ic.key_ordinal  
,ic.is_included_column  
FROM sys.indexes AS i  
INNER JOIN sys.index_columns AS ic
    ON i.object_id = ic.object_id AND i.index_id = ic.index_id  
WHERE i.object_id = OBJECT_ID('Production.BillOfMaterials');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```
  
index_name                                                 column_name        index_column_id key_ordinal is_included_column  
---------------------------------------------------------- -----------------  --------------- ----------- -------------  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ProductAssemblyID  1               1           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate ComponentID        2               2           0  
AK_BillOfMaterials_ProductAssemblyID_ComponentID_StartDate StartDate          3               3           0  
PK_BillOfMaterials_BillOfMaterialsID                       BillOfMaterialsID  1               1           0  
IX_BillOfMaterials_UnitMeasureCode                         UnitMeasureCode    1               1           0  
  
(5 row(s) affected)  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Katalogsichten für Objekte &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Katalogsichten &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Häufig gestellte Fragen zu Abfragen des SQL Server-Systemkatalogs](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
