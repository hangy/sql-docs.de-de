---
title: sp_validate_replica_hosts_as_publishers (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_replica_hosts_as_publishers_TSQL
- sp_validate_replica_hosts_as_publishers
helpviewer_keywords:
- sp_validate_replica_hosts_as_publishers
ms.assetid: 45001fc9-2dbd-463c-af1d-aa8982d8c813
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8df9c4fcc88f568c920f0a5959338f195d79d925
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252111"
---
# <a name="sp_validate_replica_hosts_as_publishers-transact-sql"></a>sp_validate_replica_hosts_as_publishers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  **sp_validate_replica_hosts_as_publishers** ist eine Erweiterung von **sp_validate_redirected_publisher** , mit der alle sekundären Replikate überprüft werden können, und nicht nur das aktuelle primäre Replikat. **sp_validate_replicat_hosts_as_publisher** überprüft eine gesamte Always on Replikations Topologie. **sp_validate_replica_hosts_as_publishers** muss direkt auf dem Verteiler ausgeführt werden, indem eine Remote Desktop Sitzung verwendet wird, um einen Double-Hop-Sicherheitsfehler (21892) zu vermeiden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_validate_replica_hosts_as_publishers   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>Argumente  
`[ @original_publisher = ] 'original_publisher'` der Name der Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], von dem die Datenbank ursprünglich veröffentlicht wurde. *original_publisher* ist vom **Datentyp vom Datentyp sysname**und hat keinen Standardwert.  
  
`[ @publisher_db = ] 'publisher_db'` den Namen der Datenbank, die veröffentlicht wird. *publisher_db* ist vom **Datentyp vom Datentyp sysname**und hat keinen Standardwert.  
  
`[ @redirected_publisher = ] 'redirected_publisher'` das Ziel der Umleitung, wenn **sp_redirect_publisher** für das ursprüngliche Verleger-/Veröffentlichungs-Datenbankpaar aufgerufen wurde. *redirected_publisher* ist vom **Datentyp vom Datentyp sysname**und hat keinen Standardwert.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
 Keine.  
  
## <a name="remarks"></a>Hinweise  
 Wenn kein Eintrag für den Verleger und die Veröffentlichungs Datenbank vorhanden ist, gibt **sp_validate_redirected_publisher** für den Output *-Parameter \@redirected_publisher*den Wert NULL zurück. Andernfalls wird der zugeordnete umgeleitete Verleger zurückgegeben, sowohl bei Erfolg und als auch bei Fehler.  
  
 Wenn die Überprüfung erfolgreich ist, gibt **sp_validate_redirected_publisher** einen Erfolgsindikator zurück.  
  
 Wenn die Überprüfung fehlschlägt, werden entsprechende Fehler ausgelöst.  **sp_validate_redirected_publisher** hat den besten Aufwand, alle Probleme und nicht nur den ersten gefundenen zu beheben.  
  
> [!NOTE]  
>  **sp_validate_replica_hosts_as_publishers** schlägt bei der Überprüfung sekundärer Replikathosts, die keinen Lesezugriff zulassen oder die Angabe der Leseabsicht erfordern, mit dem folgenden Fehler fehl.  
>   
>  Meldung 21899, Ebene 11, Status 1, Prozedur **sp_hadr_verify_subscribers_at_publisher**, Zeile 109  
>   
>  Die Abfrage beim umgeleiteten Verleger „MyReplicaHostName“ zur Bestimmung, ob sysserver-Einträge für die Abonnenten des ursprünglichen Verlegers „MyOriginalPublisher“ vorliegen, ist mit Fehler 976 und folgender Meldung fehlgeschlagen: „Fehler 976, Stufe 14, Status 1, Meldung: The target database, 'MyPublishedDB', is participating in an availability group and is currently not accessible for queries. (Die Zieldatenbank „MyPublishedDB“ ist an einer Verfügbarkeitsgruppe beteiligt, und Abfragen können derzeit nicht darauf zugreifen.) Entweder die Datenverschiebung wurde angehalten, oder für das Verfügbarkeitsreplikat wurde kein Schreibzugriff aktiviert. Um schreibgeschützten Zugriff auf diese und andere Datenbanken in der Verfügbarkeitsgruppe zuzulassen, aktivieren Sie den Lesezugriff auf mindestens ein sekundäres Verfügbarkeitsreplikat in der Gruppe.  Weitere Informationen finden Sie in der **ALTER AVAILABILITY GROUP** -Anweisung in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Onlinedokumentation.  
>   
>  Es sind ein oder mehrere Verlegerüberprüfungsfehler für Replikathost 'MyReplicaHostName' aufgetreten.  
  
## <a name="permissions"></a>Berechtigungen  
 Der Aufrufer muss entweder ein Mitglied der festen Server Rolle **sysadmin** , der festen Daten Bank Rolle **db_owner** für die Verteilungs Datenbank oder ein Mitglied einer Veröffentlichungs Zugriffsliste für eine der Verleger Datenbank zugeordnete definierte Veröffentlichung sein.  
  
## <a name="see-also"></a>Siehe auch  
 [Gespeicherte Replikationsprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)  
  
  
