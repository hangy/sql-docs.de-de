---
title: sys. dm_sql_referencing_entities (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_sql_referencing_entities
- dm_sql_referencing_entities_TSQL
- sys.dm_sql_referencing_entities_TSQL
- dm_sql_referencing_entities
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_sql_referencing_entities dynamic management function
ms.assetid: c16f8f0a-483f-4feb-842e-da90426045ae
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bd09706d1b3de9ebe4a5b333f79be9644c433e7c
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982344"
---
# <a name="sysdm_sql_referencing_entities-transact-sql"></a>sys.dm_sql_referencing_entities (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede Entität in der aktuellen Datenbank zurück, die anhand des Namens auf eine andere benutzerdefinierte Entität verweist. Eine Abhängigkeit zwischen zwei Entitäten wird erstellt, wenn eine Entität, die als *Referenzierte Entität*bezeichnet wird, in einem permanenten SQL-Ausdruck einer anderen Entität, die als *verweisende Entität*bezeichnet wird, nach Namen Wird z. B. ein benutzerdefinierter Typ (User-Defined Type; UDT) als Entität angegeben, auf die verwiesen wird, gibt diese Funktion jede benutzerdefinierte Entität zurück, die anhand des Namens in der zugehörigen Definition auf diesen Typ verweist. Die Funktion gibt keine Entitäten in anderen Datenbanken zurück, die möglicherweise auf die angegebene Entität verweisen. Diese Funktion muss zusammen mit der master-Datenbank ausgeführt werden, um einen DDL-Trigger auf Serverebene als verweisende Entität zurückzugeben.  
  
 Verwenden Sie diese dynamische Verwaltungsfunktion, um zu folgenden Entitätstypen in der aktuellen Datenbank, die auf die angegebene Entität verweisen, einen Bericht zu erstellen:  
  
-   Schemagebundene oder nicht schemagebundene Entitäten  
  
-   DDL-Trigger auf Datenbankebene  
  
-   DDL-Trigger auf Server Ebene  
  
**Gilt für**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] und höher), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlink (Symbol)") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
sys.dm_sql_referencing_entities (  
    ' schema_name.referenced_entity_name ' , ' <referenced_class> ' )  
  
<referenced_class> ::=  
{  
    OBJECT  
  | TYPE  
  | XML_SCHEMA_COLLECTION  
  | PARTITION_FUNCTION  
}  
```  
  
## <a name="arguments"></a>Argumente  
 *schema_name.referenced*_*entity_name*  
 Der Name der Entität, auf die verwiesen wird.  
  
 *schema_name* ist erforderlich, außer wenn die referenzierte Klasse PARTITION_FUNCTION ist.  
  
 *schema_name. referenced_entity_name* ist vom Datentyp **nvarchar (517)** .  
  
 *< referenced_class >* :: = {Object | Typ | XML_SCHEMA_COLLECTION | PARTITION_FUNCTION}  
 Die Klasse der Entität, auf die verwiesen wird. Pro Anweisung kann nur eine Klasse angegeben werden.  
  
 *< referenced_class >* ist vom Datentyp **nvarchar**(60).  
  
## <a name="table-returned"></a>Zurückgegebene Tabelle  
  
|Spaltenname|Datentyp|und Beschreibung|  
|-----------------|---------------|-----------------|  
|referencing_schema_name|**sysname**|Schema, in das die verweisende Entität gehört. Lässt NULL-Werte zu.<br /><br /> NULL für DDL-Trigger auf Datenbankebene und Serverebene.|  
|referencing_entity_name|**sysname**|Name der verweisenden Entität. Lässt keine NULL-Werte zu.|  
|referencing_id|**int**|ID der verweisenden Entität. Lässt keine NULL-Werte zu.|  
|referencing_class|**tinyint**|Klasse der verweisenden Entität. Lässt keine NULL-Werte zu.<br /><br /> 1 = Objekt<br /><br /> 12 = DDL-Auslösung auf Datenbankebene<br /><br /> 13 = DDL-Auslösung auf Server Ebene|  
|referencing_class_desc|**nvarchar(60)**|Die Beschreibung der Klasse der verweisenden Entität.<br /><br /> OBJECT<br /><br /> DATABASE_DDL_TRIGGER<br /><br /> SERVER_DDL_TRIGGER|  
|is_caller_dependent|**bit**|Gibt an, dass die Auflösung der Entität, auf die verwiesen wird, zur Laufzeit erfolgt, weil sie vom Schema des Aufrufers abhängt.<br /><br /> 1 = Die verweisende Entität kann zwar auf die Entität verweisen, doch die Auflösung der ID der Entität, auf die verwiesen wird, hängt vom Aufrufer ab und kann nicht bestimmt werden. Dies gilt nur für nicht schemagebundene Verweise auf eine gespeicherte Prozedur, eine erweiterte gespeicherte Prozedur oder eine benutzerdefinierte Funktion, die in einer EXECUTE-Anweisung aufgerufen wird.<br /><br /> 0 = Die Entität, auf die verwiesen wird, ist kein aufruferabhängiges Element.|  
  
## <a name="exceptions"></a>Ausnahmen  
 Gibt unter den folgenden Bedingungen ein leeres Resultset zurück:  
  
-   Ein Systemobjekt wird angegeben.  
  
-   Die angegebene Entität ist in der Datenbank nicht vorhanden.  
  
-   Die angegebene Entität verweist auf keine Entitäten.  
  
-   Ein ungültiger Parameter wird übergeben.  
  
 Gibt einen Fehler zurück, wenn die angegebene Entität, auf die verwiesen wird, eine nummerierte gespeicherte Prozedur ist.  
  
## <a name="remarks"></a>Remarks  
 In der folgenden Tabelle werden die Typen von Entitäten aufgelistet, für die Abhängigkeitsinformationen erstellt und verwaltet werden. Für Regeln, Standardwerte, temporäre Tabellen, temporär gespeicherte Prozeduren oder Systemobjekte werden keine Abhängigkeitsinformationen erstellt oder verwaltet.  
  
|Entitätstyp|Verweisende Entität|Entität, auf die verwiesen wird|  
|-----------------|------------------------|-----------------------|  
|Tabelle|Ja*|ja|  
|Ansicht|ja|ja|  
|In [!INCLUDE[tsql](../../includes/tsql-md.md)] gespeicherte Prozedur**|ja|ja|  
|Gespeicherte CLR-Prozedur|Nein|ja|  
|Benutzerdefinierte Funktion in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|ja|  
|CLR-benutzerdefinierte Funktion|Nein|ja|  
|CLR-Trigger (DML und DDL)|Nein|Nein|  
|DML-Trigger in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|Nein|  
|DDL-Trigger auf Datenbankebene in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|Nein|  
|DDL-Trigger auf Serverebene in [!INCLUDE[tsql](../../includes/tsql-md.md)]|ja|Nein|  
|Erweiterte gespeicherte Prozeduren|Nein|ja|  
|Warteschlange|Nein|ja|  
|Synonym|Nein|ja|  
|Typ (Alias und CLR-benutzerdefinierter Typ)|Nein|ja|  
|XML-Schemaauflistung|Nein|ja|  
|Partitionsfunktion|Nein|ja|  
  
 \* eine Tabelle in der Definition einer berechneten Spalte, einer Check-Einschränkung oder einer DEFAULT-Einschränkung nur als verweisende Entität nachverfolgt wird, wenn Sie auf ein [!INCLUDE[tsql](../../includes/tsql-md.md)] Modul, einen benutzerdefinierten Typ oder eine XML-Schema Auflistung verweist.  
  
 ** Nummerierte gespeicherte Prozeduren mit einem ganzzahligen Wert größer als 1 werden weder als verweisende Entität noch als Entität, auf die verwiesen wird, aufgezeichnet.  
  
## <a name="permissions"></a>Berechtigungen  
  
### <a name="includesskatmaiincludessskatmai-mdmd---includesssql11includessssql11-mdmd"></a>[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] - [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   Erfordert die CONTROL-Berechtigung für das Objekt, auf das verwiesen wird. Wenn es sich bei der Entität, auf die verwiesen wird, um eine Partitionsfunktion handelt, ist die CONTROL-Berechtigung für die Datenbank erforderlich.  
  
-   Erfordert die SELECT-Berechtigung für sys. dm_sql_referencing_entities. Standardmäßig wird die SELECT-Berechtigung der public-Rolle erteilt.  
  
### <a name="includesssql14includessssql14-mdmd---includesscurrentincludessscurrent-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] - [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
-   Erfordert keine Berechtigungen für das Objekt, auf das verwiesen wird. Teilergebnisse können zurückgegeben werden, wenn der Benutzer über die VIEW DEFINITION-Berechtigung auf nur einigen der verweisenden Entitäten verfügt.  
  
-   Erfordert die VIEW DEFINITION-Berechtigung für das Objekt, wenn es sich bei der verweisenden Entität um ein Objekt handelt.  
  
-   Erfordert die VIEW DEFINITION-Berechtigung für die Datenbank, wenn es sich bei der verweisenden Entität um einen DDL-Trigger auf Datenbankebene handelt.  
  
-   Erfordert die VIEW ANY DEFINITION-Berechtigung für den Server, wenn es sich bei der verweisenden Entität um einen DDL-Trigger auf Serverebene handelt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-the-entities-that-refer-to-a-given-entity"></a>A. Zurückgeben der Entitäten, die auf eine bestimmte Entität verweisen  
 Im folgenden Beispiel werden die Entitäten in der aktuellen Datenbank zurückgegeben, die auf die angegebene Tabelle verweisen.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('Production.Product', 'OBJECT');  
GO  
```  
  
### <a name="b-returning-the-entities-that-refer-to-a-given-type"></a>B. Zurückgeben der Entitäten, die auf einen bestimmten Typ verweisen  
 Im folgenden Beispiel werden die Entitäten zurückgegeben, die auf den Aliastyp `dbo.Flag` verweisen. Das Resultset zeigt an, dass zwei gespeicherte Prozeduren diesen Typ verwenden. Der `dbo.Flag`-Typ wird auch in der Definition mehrerer Spalten in der `HumanResources.Employee` Tabelle verwendet. Da sich der Typ jedoch nicht in der Definition einer berechneten Spalte, einer Check-Einschränkung oder einer DEFAULT-Einschränkung in der Tabelle befindet, werden für die `HumanResources.Employee` Tabelle keine Zeilen zurückgegeben.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
FROM sys.dm_sql_referencing_entities ('dbo.Flag', 'TYPE');  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 referencing_schema_name referencing_entity_name   referencing_id referencing_class_desc is_caller_dependent  
 ----------------------- -------------------------  ------------- ---------------------- -------------------  
 HumanResources          uspUpdateEmployeeHireInfo  1803153469    OBJECT_OR_COLUMN       0  
 HumanResources          uspUpdateEmployeeLogin     1819153526    OBJECT_OR_COLUMN       0  
 (2 row(s) affected)`  
 ``` 
 
## <a name="see-also"></a>Siehe auch  
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  
