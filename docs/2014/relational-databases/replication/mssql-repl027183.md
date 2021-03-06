---
title: MSSQL_REPL027183 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027183 error
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87adf79d9420f70e132fd9a6c41a9ddacf298fa7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022711"
---
# <a name="mssqlrepl027183"></a>MSSQL_REPL027183
    
## <a name="message-details"></a>Meldungsdetails  
  
|||  
|-|-|  
|Produktname|SQL Server|  
|Ereignis-ID|27183|  
|Ereignisquelle|MSSQLSERVER|  
|Komponente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Symbolischer Name||  
|Meldungstext|Vom Mergeprozess konnten Änderungen in Artikeln mit parametrisierten Zeilenfiltern nicht aufgezählt werden. Falls dieser Fehler weiterhin auftritt, erhöhen Sie das Abfragetimeout für diesen Prozess, reduzieren Sie die Beibehaltungsdauer für die Veröffentlichung, und verbessern Sie die Indizes für veröffentlichte Tabellen.|  
  
## <a name="explanation"></a>Erklärung  
 Dieser Fehler wird ausgelöst, wenn bei der Verarbeitung von Änderungen in einer gefilterten Veröffentlichung ein Merge-Agent-Timeout auftritt. Das Timeout kann durch eines der folgenden Probleme verursacht werden:  
  
-   Die Optimierung für vorausberechnete Partitionen wird nicht verwendet.  
  
-   In den beim Filtern verwendeten Spalten liegt eine Indexfragmentierung vor.  
  
-   Es sind umfangreiche Tabellen mit Mergemetadaten vorhanden, beispielsweise **MSmerge_tombstone**, **MSmerge_contents**und **MSmerge_genhistory**.  
  
-   Es sind gefilterte Tabellen, die nicht über einen eindeutigen Schlüssel verknüpft sind, und Joinsfilter mit einer großen Anzahl an Tabellen vorhanden.  
  
## <a name="user-action"></a>Benutzeraktion  
 So lösen Sie das Problem:  
  
-   Setzen Sie den Wert des **-QueryTimeOut** -Parameters für den Merge-Agent herauf, damit die Verarbeitung fortgesetzt werden kann und Sie sich der eigentlichen Ursache des Fehlers widmen können. Agentparameter können in den Agentprofilen und in der Befehlszeile angegeben werden. Weitere Informationen finden Sie in den folgenden Themen:  
  
    -   [Arbeiten mit Replikations-Agent-Profilen](agents/replication-agent-profiles.md)  
  
    -   [Anzeigen und Ändern von Befehlszeilenparametern des Replikations-Agents &#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Ausführbare Konzepte für die Programmierung von Replikations-Agents](concepts/replication-agent-executables-concepts.md)  
  
-   Verwenden Sie, sofern möglich, die Optimierung für vorausberechnete Partitionen. Diese Optimierung wird standardmäßig verwendet, wenn mehrere Veröffentlichungsanforderungen erfüllt sind. Weitere Informationen zu diesen Anforderungen finden Sie unter [Optimieren der Leistung parametrisierter Filter mithilfe vorausberechneter Partitionen](merge/parameterized-filters-optimize-for-precomputed-partitions.md). Wenn die Veröffentlichung diese Anforderungen nicht erfüllt, sollten Sie einen erneuten Entwurf der Veröffentlichung in Betracht ziehen.  
  
-   Geben Sie die kürzestmögliche Einstellung für die Beibehaltungsdauer der Veröffentlichung an, da die Replikation keinen Cleanup der Metadaten in den Veröffentlichungs- und den Abonnementdatenbanken ausführen kann, bevor die Beibehaltungsdauer erreicht wurde. Weitere Informationen finden Sie unter [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
-   Als Teil der Wartung für die Mergereplikation überprüfen Sie gelegentlich die Vergrößerung der Systemtabellen, die mit der Mergereplikation verbunden sind: **MSmerge_contents**, **MSmerge_genhistory**, and **MSmerge_tombstone**, **MSmerge_current_partition_mappings** und **MSmerge_past_partition_mappings**. Führen Sie eine regelmäßige Neuindizierung dieser Tabellen durch. Weitere Informationen finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../indexes/indexes.md).  
  
-   Stellen Sie sicher, dass die zum Filtern verwendeten Spalten richtig indiziert sind, und erstellen Sie die entsprechenden Indizes gegebenenfalls erneut. Weitere Informationen finden Sie unter [Neuorganisieren und Neuerstellen von Indizes](../indexes/indexes.md).  
  
-   Legen Sie für Joinsfilter, die auf eindeutigen Spalten basieren, die **join_unique_key** -Eigenschaft fest. Weitere Informationen finden Sie unter [Join Filters](merge/join-filters.md).  
  
-   Begrenzen Sie die Anzahl der Tabellen in der Joinsfilterhierarchie. Wenn Sie Joinsfilter für fünf oder mehr Tabellen erstellen, sollten Sie andere Lösungen in Betracht ziehen: Kleinere Tabellen, Tabellen, die nicht geändert werden, oder Tabellen, bei denen es sich primär um Nachschlagetabellen handelt, sollten in diesem Fall nicht gefiltert werden. Verwenden Sie Joinsfilter nur zwischen Tabellen, für die eine Partitionierung auf Abonnements erfolgen muss.  
  
-   Nehmen Sie zwischen Synchronisierungen weniger Änderungen an gefilterten Tabellen vor, oder führen Sie den Merge-Agent häufiger aus. Weitere Informationen zum Angeben von Synchronisierungszeitplänen finden Sie unter [Specify Synchronization Schedules](specify-synchronization-schedules.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Ereignisreferenz &#40;Replikation&#41;](errors-and-events-reference-replication.md)  
  
  
