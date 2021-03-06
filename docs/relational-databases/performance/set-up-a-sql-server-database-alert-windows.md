---
title: Einrichten einer SQL Server-Datenbankwarnung (Windows) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f76c6f4f4d65273c35dffb1cb17e664fceac0328
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113336"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>Einrichten einer SQL Server-Datenbankwarnung (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Sie können mithilfe des Systemmonitors eine Warnung erstellen, die ausgelöst wird, sobald ein Schwellenwert für einen Leistungsindikator des Systemmonitors erreicht wird. Als Reaktion auf die Warnung kann der Systemmonitor eine Anwendung starten, wie z. B. eine benutzerdefinierte Anwendung, die für das Verarbeiten der Warnung geschrieben wurde. Sie können beispielsweise eine Warnung erstellen, die ausgelöst wird, wenn die Anzahl der Deadlocks einen bestimmten Wert überschreitet. 
  
 Warnungen können auch mit Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] und dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent definiert werden. Weitere Informationen finden Sie unter [Warnungen](../../ssms/agent/alerts.md).  
  
## <a name="set-up-a-sql-server-database-alert"></a>Einrichten einer SQL Server-Datenbankwarnung  
  
1. Erweitern Sie in der Navigationsstruktur des Fensters **Leistung** die Option **Leistungsprotokolle und Warnungen**.  
  
2. Klicken Sie mit der rechten Maustaste auf **Warnungen**, und wählen Sie dann **Neue Warnungseinstellungen** aus.
  
3. Geben Sie im Dialogfeld **Neue Warnungseinstellungen** einen Namen für die neue Warnung ein, und wählen Sie dann **OK**.  
  
4. Fügen Sie im Dialogfeld für die neue Warnung auf der Registerkarte **Allgemein** einen **Kommentar**hinzu. Wählen Sie **Hinzufügen** aus, um der Warnung einen Leistungsindikator hinzuzufügen.  
  
     Jede Warnung muss mindestens einen Leistungsindikator aufweisen.  
  
5. Wählen Sie im Dialogfeld **Indikatoren hinzufügen** in der Liste **Leistungsobjekt** ein SQL Server-Objekt aus. Wählen Sie in **Indikatoren aus Liste auswählen** einen Indikator aus.  
  
6. Wählen Sie **Hinzufügen** aus, um der Warnung den Leistungsindikator hinzuzufügen. Sie können weitere Leistungsindikatoren hinzufügen, oder wählen Sie **Schließen** aus, um zum Dialogfeld für die neue Warnung zurückzukehren.  
  
7. Wählen Sie im Dialogfeld für die neue Warnung entweder **größer als** oder **kleiner als** in der Liste **Warnung bei folgendem Wert** aus. Geben Sie dann einen Schwellenwert in **Grenzwert** ein.  
  
     Die Warnung wird generiert, wenn der Wert für den Leistungsindikator größer oder kleiner als der Schwellwert ist (je nachdem, ob Sie **größer als** oder **kleiner als** gewählt haben).  
  
8. Legen Sie in den Feldern **Daten erfassen alle** die Stichprobenfrequenz fest.  
  
9. Legen Sie auf der Registerkarte **Aktion** die Aktionen fest, die jedes Mal ausgeführt werden, wenn die Warnung ausgelöst wird.  
  
10. Legen Sie auf der Registerkarte **Zeitplan** den Beginn und das Ende des Zeitplans für die Warnungssuche fest.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer SQL Server-Datenbankwarnung](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
