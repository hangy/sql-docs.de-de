---
title: sp_replmonitorchangepublicationthreshold (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replmonitorchangepublicationthreshold_TSQL
- sp_replmonitorchangepublicationthreshold
helpviewer_keywords:
- sp_replmonitorchangepublicationthreshold
ms.assetid: 2c3615d8-4a1a-4162-b096-97aefe6ddc16
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7fd8dd31b1468cb718af286f6c00e26cfa2e1ba0
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2019
ms.locfileid: "68771216"
---
# <a name="sp_replmonitorchangepublicationthreshold-transact-sql"></a>sp_replmonitorchangepublicationthreshold (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Ändert die Schwellenwertmetrik für die Überwachung einer Veröffentlichung. Diese gespeicherte Prozedur, die zur Überwachung der Replikation verwendet wird, wird auf dem Verteiler für die Verteilungsdatenbank ausgeführt.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_replmonitorchangepublicationthreshold [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
    [ , [ @publication_type = ] publication_type ]   
    [ , [ @metric_id = ] metric_id ]   
    [ , [ @thresholdmetricname = ] 'thresholdmetricname'   
    [ , [ @value = ] value ]   
    [ , [ @shouldalert = ] shouldalert ]   
    [ , [ @mode = ] mode ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @publisher = ] 'publisher'`Der Name des Verlegers. *Publisher* ist vom **Datentyp vom Datentyp sysname**und hat keinen Standardwert.  
  
`[ @publisher_db = ] 'publisher_db'`Der Name der veröffentlichten Datenbank. *publisher_db* ist vom **Datentyp vom Datentyp sysname**und hat keinen Standardwert.  
  
`[ @publication = ] 'publication'`Der Name der Veröffentlichung, für die die Überwachungs Schwellenwert Attribute geändert werden. *Publication* ist vom **Datentyp vom Datentyp sysname**und hat keinen Standardwert.  
  
`[ @publication_type = ] publication_type`Gibt an, ob der Typ der Veröffentlichung ist. *publication_type* ist vom Datentyp **int**und kann einen der folgenden Werte aufweisen.  
  
|Wert|Description|  
|-----------|-----------------|  
|**0**|Transaktionsveröffentlichung.|  
|**1**|Momentaufnahmeveröffentlichung.|  
|**2**|Mergeveröffentlichung.|  
|NULL (Standard)|Replikationsversuche zum Bestimmen des Veröffentlichungstyps.|  
  
`[ @metric_id = ] metric_id`Die ID der Schwellenwert Metrik für die Veröffentlichung, die geändert wird. *metric_id* ist vom Datentyp **int**und hat den Standardwert NULL. die folgenden Werte sind möglich:  
  
|Wert|Metrikname|  
|-----------|-----------------|  
|**1**|**expiration** - überwacht den bevorstehenden Ablauf von Abonnements für Transaktionsveröffentlichungen.|  
|**2**|**latency** - überwacht die Leistung von Abonnements für Transaktionsveröffentlichungen.|  
|**4**|**mergeexpiration** - überwacht den bevorstehenden Ablauf von Abonnements für Mergeveröffentlichungen.|  
|**5**|**mergeslowrunduration** : überwacht die Dauer von Mergesynchronisierungen über Verbindungen mit niedriger Bandbreite (DFÜ-Verbindungen).|  
|**6**|**mergefastrauunduration** : überwacht die Dauer von Mergesynchronisierungen über LAN-Verbindungen (Local Area Network) mit hoher Bandbreite.|  
|**7**|**mergefastrunspeed** - Überwachung der Synchronisierungsgeschwindigkeit von Mergesynchronisierungen über Verbindungen mit hoher Bandbreite (LAN-Verbindungen).|  
|**8**|**mergeslowrunspeed** : überwacht die Synchronisierungs Geschwindigkeit von Mergesynchronisierungen über Verbindungen mit niedriger Bandbreite (DFÜ-Verbindungen).|  
  
 Sie müssen entweder *metric_id* oder. Wenn " *stammoldmetricname* " angegeben ist, sollte " *metric_id* " NULL sein.  
  
`[ @thresholdmetricname = ] 'thresholdmetricname'`Der Name der Schwellenwert Metrik für die Veröffentlichung, die geändert wird. " *stammoldmetricname* " ist vom **Datentyp vom Datentyp sysname**und hat den Standardwert NULL. Sie müssen entweder den *Namen* "" für "" und " *metric_id*" angeben. Wenn *metric_id* angegeben wird, muss der Wert von "" für "".  
  
`[ @value = ] value`Der neue Wert der Schwellenwert Metrik für die Veröffentlichung. der *Wert* ist vom Datentyp **int**und hat den Standardwert NULL. Wenn der Wert **null**ist, wird der Metrikwert nicht aktualisiert.  
  
`[ @shouldalert = ] shouldalert`Gibt an, ob eine Warnung generiert wird, wenn eine Schwellenwert Metrik für die Veröffentlichung erreicht wird der Wert ist " **Bit**", der Standardwert ist NULL. Der Wert **1** bedeutet, dass eine Warnung generiert wird, und der Wert **0** bedeutet, dass keine Warnung generiert wird.  
  
`[ @mode = ] mode`Ist, wenn die Schwellenwert Metrik für die Veröffentlichung aktiviert ist. der *Modus* ist vom Datentyp **tinyint**. der Standardwert ist **1**. Der Wert **1** bedeutet, dass die Überwachung dieser Metrik aktiviert ist und der Wert **2** bedeutet, dass die Überwachung dieser Metrik deaktiviert ist.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 **0** (Erfolg) oder **1** (Fehler)  
  
## <a name="remarks"></a>Hinweise  
 **sp_replmonitorchangepublicationthreshold** wird für alle Replikations Typen verwendet.  
  
## <a name="permissions"></a>Berechtigungen  
 Nur Mitglieder der festen Daten Bank Rolle **db_owner** oder **replmonitor** in der Verteilungs Datenbank können **sp_replmonitorchangepublicationthreshold**ausführen.  
  
## <a name="see-also"></a>Siehe auch  
 [Programmgesteuertes Überwachen der Replikation](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)  
  
  
