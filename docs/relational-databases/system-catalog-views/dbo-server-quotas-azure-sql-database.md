---
title: dbo. server_quotas (Azure SQL-Datenbank) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/02/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dbo.server_quotas
- dbo.server_quotas_TSQL
- server_quotas
- server_quotas_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- server_quotas
ms.assetid: 34423903-1aaa-4a55-88a6-8228315d84e7
author: stevestein
ms.author: sstein
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 90df7425c7265db141d393b774728a8fe2662061
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68033038"
---
# <a name="dboserverquotas-azure-sql-database"></a>dbo.server_quotas (Azure SQL-Datenbank)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

    
> **WICHTIG!** Dies gilt für  **[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]V11 nur!**  
>   
>  Diese Funktion befindet sich in einem Vorschauzustand. Erstellen Sie keine Abhängigkeit von der spezifischen Implementierung dieser Funktion, da die Funktion in zukünftigen Versionen ggf. geändert oder entfernt werden kann.  
  
 Gibt die auf dem Server verfügbaren Datenbank-Kontingenttypen zurück.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|quota_name|**nvarchar**|Der Kontingenttyp für den Server. Der **Premium_database** -Typ entspricht Datenbanken mit einer Ressourcenreservierung.|  
|quota_value|**int**|Die Anzahl der im Server zulässigen Kontingenttypen.|  
  
## <a name="permissions"></a>Berechtigungen  
 Alle Benutzerrollen, die berechtigt sind, eine Verbindung mit der virtuellen **master** -Datenbank herzustellen, haben Zugriff auf diese Sicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Premium-Datenbanken](https://go.microsoft.com/fwlink/?LinkID=311927)  
  
  
