---
title: Sp_helplanguage (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d46e178fc1872a84bb573f16629803c59f2fb6c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68122512"
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Gibt Informationen zu einer bestimmten alternativen Sprache oder zu allen Sprachen in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @language = ] 'language'` Ist der Name der alternativen Sprache, für die Anzeige von Informationen. *language* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *Sprache* wird angegeben, werden Informationen zu der angegebenen Sprache zurückgegeben. Wenn Language nicht angegeben ist, Informationen zu allen Sprachen in der **sys.syslanguages** -kompatibilitätssicht zurückgegeben.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|Sprachen-ID|  
|**dateformat**|**NCHAR(3)**|Datumsformat.|  
|**DATEFIRST**|**tinyint**|Erster Tag der Woche: 1 für Montag, 2 für Dienstag usw., bis 7 für Sonntag.|  
|**upgrade**|**int**|Version des letzten Upgrades von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] für diese Sprache.|  
|**name**|**sysname**|Name der Sprache.|  
|**alias**|**sysname**|Alternativer Name der Sprache|  
|**Monate**|**nvarchar(372)**|Monatsnamen|  
|**shortmonths**|**nvarchar(132)**|Kurznamen für die Monate|  
|**Tage**|**nvarchar(217)**|Tagesnamen|  
|**lcid**|**int**|Windows-Gebietsschema-ID für die Sprache.|  
|**msglangid**|**smallint**|ID der Meldungsgruppe von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-information-about-a-single-language"></a>A. Zurückgeben von Informationen zu einer einzelnen Sprache  
 Das folgende Beispiel zeigt Informationen zur alternativen Sprache `French` an.  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. Zurückgeben von Informationen zu allen Sprachen  
 Das folgende Beispiel zeigt Informationen zu allen installierten alternativen Sprachen an.  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank-Engine gespeicherten Prozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
