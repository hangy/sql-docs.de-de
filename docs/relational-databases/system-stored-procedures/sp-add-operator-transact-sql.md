---
title: sp_add_operator (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: f410024e1458d20e436df72cc2978ce41b5d60df
ms.sourcegitcommit: 15fe0bbba963d011472cfbbc06d954d9dbf2d655
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2019
ms.locfileid: "74095504"
---
# <a name="sp_add_operator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Erstellt einen Operator (Benachrichtigungsempfänger) für Warnungen und Aufträge.  
  
 
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Themenlink (Symbol)") [Transact-SQL-Syntaxkonventionen](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]   
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]   
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]   
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]   
```  
  
## <a name="arguments"></a>Argumente  
`[ @name = ] 'name'` den Namen eines Operators (Benachrichtigungs Empfänger). Dieser Name muss eindeutig sein und darf kein Prozentzeichen ( **%** ) enthalten. *Name ist vom Datentyp* **vom Datentyp sysname**und hat keinen Standardwert.  
  
`[ @enabled = ] enabled` gibt den aktuellen Status des Operators an. *aktiviert* ist vom Datentyp **tinyint**. der Standardwert ist **1** (aktiviert). Wenn der Wert **0**ist, ist der Operator nicht aktiviert, und es werden keine Benachrichtigungen empfangen.  
  
`[ @email_address = ] 'email_address'` die e-Mail-Adresse des Operators. Diese Zeichenfolge wird direkt an das E-Mail-System übergeben. *email_address* ist vom Datentyp **nvarchar (100)** und hat den Standardwert NULL.  
  
 Sie können entweder eine physische e-Mail-Adresse oder einen Alias für *email_address*angeben. Zum Beispiel:  
  
 '**jdoe**' oder '**jdoe\@XYZ.com**'  
  
> [!NOTE]  
>  Für Datenbank-E-Mail muss die E-Mail-Adresse verwendet werden.  
  
`[ @pager_address = ] 'pager_address'` die Pager-Adresse des Operators. Diese Zeichenfolge wird direkt an das E-Mail-System übergeben. *pager_address* ist vom Datentyp **nvarchar (100)** und hat den Standardwert NULL.  
  
`[ @weekday_pager_start_time = ] weekday_pager_start_time` die Zeit ab, nach der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent Pager-Benachrichtigungen an den angegebenen Operator an den Wochentagen sendet, von Montag bis Freitag. *weekday_pager_start_time*ist vom Datentyp **int**. der Standardwert ist **090000**. der Wert ist 9:00 Uhr. im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
`[ @weekday_pager_end_time = ] weekday_pager_end_time` die Zeit, nach der der **SQLServerAgent** -Dienst von Montag bis Freitag keine Pager-Benachrichtigung mehr an den angegebenen Operator an den Wochentagen sendet. *weekday_pager_end_time*ist vom Datentyp **int**und hat den Standardwert 180000, der 6:00 Uhr angibt. im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
`[ @saturday_pager_start_time = ] saturday_pager_start_time` den Zeitraum ab, nach dem der **SQLServerAgent** -Dienst Pager-Benachrichtigungen an den angegebenen Operator an einem Samstag sendet. *saturday_pager_start_time* ist vom Datentyp **int**. der Standardwert ist 090000. der Wert ist 9:00 Uhr. im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
`[ @saturday_pager_end_time = ] saturday_pager_end_time` die Zeit, nach der der **SQLServerAgent** -Dienst die Pager-Benachrichtigung nicht mehr an den angegebenen Operator an einem Samstag sendet. *saturday_pager_end_time*ist vom Datentyp **int**und hat den Standardwert **180000**, der 6:00 Uhr angibt. im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
`[ @sunday_pager_start_time = ] sunday_pager_start_time` den Zeitraum ab, nach dem der **SQLServerAgent** -Dienst eine Pager-Benachrichtigung an den angegebenen Operator an Sonntags sendet. *sunday_pager_start_time*ist vom Datentyp **int**. der Standardwert ist **090000**. der Wert ist 9:00 Uhr. im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
`[ @sunday_pager_end_time = ] sunday_pager_end_time` die Zeit, nach der der **SQLServerAgent** -Dienst keine Pager-Benachrichtigung mehr an den angegebenen Operator an Sonntags sendet. *sunday_pager_end_time*ist vom Datentyp **int**und hat den Standardwert **180000**, der 6:00 Uhr angibt. im 24-Stunden-Format an und muss im Format HHMMSS eingegeben werden.  
  
`[ @pager_days = ] pager_days` ist eine Zahl, die die Tage angibt, an denen der Operator für Seiten verfügbar ist (abhängig von den angegebenen Start-und Endzeiten). *pager_days*ist vom Datentyp **tinyint**. der Standardwert ist **0** , was bedeutet, dass der Operator nie zum Empfangen einer Seite verfügbar ist. Gültige Werte sind **0** bis **127**. *pager_days*wird berechnet, indem die einzelnen Werte für die erforderlichen Tage addiert werden. Beispielsweise ist von Montag bis Freitag **2**+**4**+**8**+**16**+**32** = **62**. In der folgenden Tabelle werden die Werte für die einzelnen Wochentage aufgelistet.  
  
|ReplTest1|und Beschreibung|  
|-----------|-----------------|  
|**1**|Sonntag|  
|**2**|Montag|  
|**4**|Dienstag|  
|**8**|Mittwoch|  
|**16**|Donnerstag|  
|**32**|Freitag|  
|**64**|Samstag|  
  
`[ @netsend_address = ] 'netsend_address'` die Netzwerkadresse des Operators, an den die Netzwerk Nachricht gesendet wird. *netsend_address*ist vom Datentyp **nvarchar (100)** und hat den Standardwert NULL.  
  
`[ @category_name = ] 'category'` den Namen der Kategorie für diesen Operator. *Category* ist vom **Datentyp vom Datentyp sysname**und hat den Standardwert NULL.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine  
  
## <a name="remarks"></a>Remarks  
 **sp_add_operator** müssen von der **msdb** -Datenbank aus ausgeführt werden.  
  
 Pagerbenachrichtigungen werden mithilfe des E-Mail-Systems durchgeführt. Daher muss das zugrunde liegende E-Mail-System in der Lage sein, Nachrichten an Pager zu senden.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] können Aufträge problemlos mithilfe einer grafischen Oberfläche verwaltet werden. Dies ist die empfohlene Vorgehensweise für die Erstellung und Verwaltung der Auftragsinfrastruktur.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Server Rolle **sysadmin** können **sp_add_operator**ausführen.  
  
## <a name="examples"></a>Beispiele  
 Im folgenden Beispiel werden die Operatorinformationen für `danwi` eingerichtet. Der Operator ist aktiviert. Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent sendet montags bis freitags von 8 bis 17 Uhr Benachrichtigungen per Pager.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>Siehe auch  
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
