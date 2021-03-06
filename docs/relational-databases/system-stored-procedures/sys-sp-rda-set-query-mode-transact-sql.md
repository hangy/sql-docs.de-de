---
title: sys. sp_rda_set_query_mode (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_set_query_mode
- sys.sp_rda_set_query_mode_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_set_query_mode stored procedure
ms.assetid: 65a0b390-cf87-4db7-972a-1fdf13456c88
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 98796b89486ce59b289c83a74e5c466a6522b557
ms.sourcegitcommit: 710d60e7974e2c4c52aebe36fceb6e2bbd52727c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/11/2019
ms.locfileid: "72278324"
---
# <a name="syssp_rda_set_query_mode-transact-sql"></a>sys. sp_rda_set_query_mode (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Gibt an, ob Abfragen für die aktuelle Stretch-aktivierte Datenbank und Ihre Tabellen sowohl lokale als auch Remote Daten (Standard) oder lokale Daten zurückgeben.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_rda_set_query_mode [ @mode = ] @mode   
    [ , [ @force = ]  @force ]  
```  
  
## <a name="arguments"></a>Argumente  
 [@mode =] *\@-Modus*  
 Ist einer der folgenden Werte.  
  
-   **Deaktiviert** Alle Abfragen für Stretch-aktivierte Tabellen können nicht ausgeführt werden.  
  
-   **LOCAL_ONLY** Abfragen für Stretch-aktivierte Tabellen geben nur lokale Daten zurück.  
  
-   **LOCAL_AND_REMOTE** Abfragen für Stretch-aktivierte Tabellen geben sowohl lokale Daten als auch Remote Daten zurück. Dies ist das Standardverhalten.  
  
 [@force =]  *\@force*  
 Ist ein optionaler Bitwert, der auf 1 festgelegt werden kann, wenn Sie den Abfrage Modus ohne Validierung ändern möchten.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder > 0 (Fehler)  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert db_owner-Berechtigungen.  
  
## <a name="remarks"></a>Hinweise  
 Die folgenden erweiterten gespeicherten Prozeduren legen auch den Abfrage Modus für eine Stretch-aktivierte Datenbank fest.  
  
-   **sp_rda_deauthorize_db**  
  
     Nach dem Ausführen von **sp_rda_deauthorize_db** treten bei allen Abfragen für Datenbanken und Tabellen mit aktivierter Stretch-Datenbank Fehler auf. Das heißt, der Abfrage Modus ist auf "deaktiviert" festgelegt. Führen Sie eine der folgenden Aktionen aus, um diesen Modus zu beenden.  
  
    -   Führen Sie [sys. &#40;sp_rda_reauthorize_db Transact-&#41; SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) aus, um erneut eine Verbindung mit der Azure-Remote Datenbank herzustellen. Durch diesen Vorgang wird der Abfrage Modus automatisch auf LOCAL_AND_REMOTE zurückgesetzt. Dies ist das Standardverhalten für Stretch Database. Das heißt, dass Abfragen Ergebnisse sowohl aus lokalen als auch aus Remote Daten zurückgeben.  
  
    -   Führen Sie [sys. sp_rda_set_query_mode](../../relational-databases/system-stored-procedures/sys-sp-rda-set-query-mode-transact-sql.md) mit dem LOCAL_ONLY-Argument aus, damit Abfragen weiterhin nur für lokale Daten ausgeführt werden.  
  
-   **sp_rda_reauthorize_db**  
  
     Wenn Sie [sys. sp_rda_reauthorize_db &#40;&#41; Transact-SQL](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) ausführen, um erneut eine Verbindung mit der Azure-Remote Datenbank herzustellen, setzt dieser Vorgang den Abfrage Modus automatisch auf LOCAL_AND_REMOTE zurück. Dies ist das Standardverhalten für Stretch Database. Das heißt, dass Abfragen Ergebnisse sowohl aus lokalen als auch aus Remote Daten zurückgeben.  
  
## <a name="see-also"></a>Siehe auch  
 [sys.sp_rda_deauthorize_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
