---
title: Speichern von Ablaufverfolgungsergebnissen in einer Tabelle (SQL Server Profiler) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- saving traces
- traces [SQL Server], saving
ms.assetid: edbecf74-683b-4e43-a1ef-7a3d5f5e27f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8571f7273cc2667040ffffc8ffbfb0df4e2a6ef6
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792689"
---
# <a name="save-trace-results-to-a-table-sql-server-profiler"></a>Speichern von Ablaufverfolgungsergebnissen in einer Tabelle (SQL Server Profiler)
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
  
7.  In der **Ablaufverfolgungseigenschaften** wählen Sie im Dialogfeld die **maximale Zeilenzahl festlegen (in Schritten von Tausend)** Kontrollkästchen, um die maximale Anzahl zu speichernder Zeilen anzugeben.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
