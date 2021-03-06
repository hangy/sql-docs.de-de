---
title: SET NOCOUNT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- NOCOUNT
- SET_NOCOUNT_TSQL
- NOCOUNT_TSQL
- SET NOCOUNT
dev_langs:
- TSQL
helpviewer_keywords:
- NOCOUNT option
- number of rows affected by statement
- row affected by statements [SQL Server]
- counting rows
- SET NOCOUNT statement
ms.assetid: eb3e6727-cb26-4bc2-84c7-171cbac02029
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f3593709dfbae0406e9952392ef82e184f205208
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68034953"
---
# <a name="set-nocount-transact-sql"></a>SET NOCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-xxx-md.md)]

  Bewirkt, dass die Meldung bezüglich der Anzahl der von einer [!INCLUDE[tsql](../../includes/tsql-md.md)]-Anweisung oder gespeicherten Prozedur betroffenen Zeilen nicht mehr als Teil des Resultsets zurückgegeben wird.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
SET NOCOUNT { ON | OFF }   
```  
  
## <a name="remarks"></a>Bemerkungen  
 Wenn SET NOCOUNT auf ON festgelegt ist, wird die Anzahl nicht zurückgegeben. Wenn SET NOCOUNT auf OFF festgelegt ist, wird die Anzahl zurückgegeben.  
  
 Die @@ROWCOUNT-Funktion wird aktualisiert, auch wenn SET NOCOUNT auf ON festgelegt ist.  
  
 SET NOCOUNT ON verhindert das Senden der DONE_IN_PROC-Meldungen an den Client, die sonst für jede Anweisung in einer gespeicherten Prozedur gesendet werden. Bei gespeicherten Prozeduren mit mehreren Anweisungen, die wenige tatsächliche Daten zurückgeben, oder für Prozeduren, die [!INCLUDE[tsql](../../includes/tsql-md.md)]-Schleifen enthalten, kann das Festlegen von SET NOCOUNT auf ON eine erhebliche Leistungssteigerung bewirken, da der Netzwerkverkehr stark reduziert wird.  
  
 Die mit SET NOCOUNT angegebene Einstellung ist zur Ausführungszeit und nicht zur Analysezeit wirksam.  
  
 Um die aktuelle Einstellung anzuzeigen, führen Sie die folgende Abfrage aus.  
  
```  
DECLARE @NOCOUNT VARCHAR(3) = 'OFF';  
IF ( (512 & @@OPTIONS) = 512 ) SET @NOCOUNT = 'ON';  
SELECT @NOCOUNT AS NOCOUNT;  
  
```  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die Mitgliedschaft in der **public** -Rolle.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird verhindert, dass die Meldung zur Anzahl der betroffenen Zeilen angezeigt wird.  
  
```  
USE AdventureWorks2012;  
GO  
SET NOCOUNT OFF;  
GO  
-- Display the count message.  
SELECT TOP(5)LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- SET NOCOUNT to ON to no longer display the count message.  
SET NOCOUNT ON;  
GO  
SELECT TOP(5) LastName  
FROM Person.Person  
WHERE LastName LIKE 'A%';  
GO  
-- Reset SET NOCOUNT to OFF  
SET NOCOUNT OFF;  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [@@ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/rowcount-transact-sql.md)   
 [SET-Anweisungen &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
