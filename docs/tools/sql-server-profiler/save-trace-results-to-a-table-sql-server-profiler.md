---
title: Speichern von Ablaufverfolgungsergebnissen in einer Tabelle (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9191c2ab44f4152a54211a1a66a5d843c0d6c12c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67928756"
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>Speichern von Ablaufverfolgungsergebnissen in einer Tabelle (SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie Ablaufverfolgungsergebnisse mithilfe von [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]in einer Datenbanktabelle gespeichert werden.  
  
### <a name="to-save-trace-results-to-a-table"></a>So speichern Sie Ablaufverfolgungsergebnisse in einer Tabelle  
  
1.  Klicken Sie im Menü **Datei** auf **Neue Ablaufverfolgung**, und stellen Sie dann eine Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]her.  
  
     Das Dialogfeld **Ablaufverfolgungseigenschaften**wird angezeigt.  
  
    > [!NOTE]  
    >  Bei der Auswahl von **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten**wird das Dialogfeld **Ablaufverfolgungseigenschaften**nicht angezeigt. Stattdessen beginnt die Ablaufverfolgung. Um diese Einstellung zu deaktivieren, klicken Sie im Menü **Extras**auf **Optionen**, und deaktivieren Sie das Kontrollkästchen **Ablaufverfolgung sofort nach dem Herstellen der Verbindung starten** .  
  
2.  Geben Sie im Feld **Ablaufverfolgungsname** einen Namen für die Ablaufverfolgung ein, und klicken Sie dann auf **In Tabelle speichern**.  
  
3.  Stellen Sie im Dialogfeld **Verbindung mit Server herstellen** eine Verbindung mit der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbank her, die die Ablaufverfolgungstabelle enthalten wird.  
  
4.  Geben Sie im Feld **Zieltabelle** in der Liste **Datenbank**eine Datenbank aus.  
  
5.  Wählen Sie in der Liste **Besitzer** den Besitzer für die Ablaufverfolgung aus.  
  
6.  Geben Sie im Feld **Tabelle** den Tabellennamen für die Ablaufverfolgungsergebnisse ein, oder wählen Sie den Namen aus. Klicken Sie auf **OK.**  
  
7.  Aktivieren Sie im Dialogfeld **Ablaufverfolgungseigenschaften** das Kontrollkästchen **Maximale Zeilenzahl festlegen (in Tausend)** , um die maximale Anzahl zu speichernder Zeilen anzugeben.  
  
## <a name="see-also"></a>Weitere Informationen  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
