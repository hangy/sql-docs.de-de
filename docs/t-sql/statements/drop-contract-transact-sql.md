---
title: DROP CONTRACT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_CONTRACT_TSQL
- DROP CONTRACT
dev_langs:
- TSQL
helpviewer_keywords:
- dropping contracts
- removing contracts
- deleting contracts
- contracts [Service Broker], dropping
- DROP CONTRACT statement
ms.assetid: fdd0f81e-3c22-4cdf-9416-b4977a6ac3b6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 479d00aec0cbd4c9cd81359a0a1f633e80bce521
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898266"
---
# <a name="drop-contract-transact-sql"></a>DROP CONTRACT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Löscht einen vorhandenen Vertrag aus einer Datenbank.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlinksymbol") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
DROP CONTRACT contract_name   
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *contract_name*  
 Der Name des zu löschenden Vertrags. Server-, Datenbank- und Schemaname können nicht angegeben werden.  
  
## <a name="remarks"></a>Bemerkungen  
 Sie können einen Vertrag nicht löschen, wenn Dienste oder Konversationsprioritäten auf ihn verweisen.  
  
 Wenn Sie einen Vertrag löschen, beendet [!INCLUDE[ssSB](../../includes/sssb-md.md)] alle vorhandenen Konversationen, die den Vertrag verwenden, mit einem Fehler.  
  
## <a name="permissions"></a>Berechtigungen  
 Standardmäßig verfügen der Besitzer des Vertrags, Mitglieder der festen Datenbankrollen db_ddladmin und db_owner sowie Mitglieder der festen Serverrolle sysadmin über die Berechtigung zum Löschen eines Vertrags.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel wird der Vertrag `//Adventure-Works.com/Expenses/ExpenseSubmission` aus der Datenbank entfernt.  
  
```  
DROP CONTRACT   
    [//Adventure-Works.com/Expenses/ExpenseSubmission] ;  
```  
  
## <a name="see-also"></a>Weitere Informationen  
 [ALTER BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-broker-priority-transact-sql.md)   
 [ALTER SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-service-transact-sql.md)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](../../t-sql/statements/create-contract-transact-sql.md)   
 [DROP BROKER PRIORITY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-broker-priority-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
