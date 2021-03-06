---
title: MSSQL_ENG003724 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG003724 error
ms.assetid: 10cb119d-92df-4124-b85d-cd2f2666c99c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 774d53b8e11e7daefab7c51e0009739d646303ef
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2019
ms.locfileid: "68766675"
---
# <a name="mssqleng003724"></a>MSSQL_ENG003724
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|3724|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Das %1!s! von '%3!s!' (%2!s!) ist nicht möglich, da das Objekt für die Replikation verwendet wird.|  
  
## <a name="explanation"></a>Erklärung  
 Wenn Sie Objekte in einer Datenbank replizieren, werden diese Objekte in der **sysarticles** -Systemtabelle (bei Momentaufnahmen- und Transaktionsveröffentlichungen) bzw. **sysmergearticles** (bei Mergeveröffentlichungen) als repliziert gekennzeichnet. Dieser Fehler wird ausgelöst, wenn Sie versuchen, ein repliziertes Objekt zu löschen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Stellen Sie vor dem Löschen sicher, dass das Datenbankobjekt nicht repliziert ist. Beispiel:  
  
-   Tritt der Fehler in der Veröffentlichungsdatenbank auf, löschen Sie den Artikel aus der Veröffentlichung, bevor Sie das Objekt löschen. Weitere Informationen finden Sie unter [Hinzufügen und Löschen von Artikeln aus vorhandenen Veröffentlichungen](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
-   Tritt der Fehler in der Abonnementdatenbank auf, löschen Sie das Abonnement, bevor Sie das Objekt löschen. Weitere Informationen finden Sie unter [Veröffentlichungen abonnieren](../../relational-databases/replication/subscribe-to-publications.md). Bei Abonnements für Transaktionsreplikationen besteht die Möglichkeit, nicht gleich die gesamte Veröffentlichung zu löschen, sondern nur das Abonnement eines einzelnen Artikels zu löschen. Weitere Informationen finden Sie unter [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md).  
  
 Falls dieser Fehler in einer Datenbank auftritt, die nicht repliziert wird, führen Sie [sp_removedbreplication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) aus, um sicherzustellen, dass die Objekte in der Datenbank nicht als repliziert hervorgehoben sind.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
