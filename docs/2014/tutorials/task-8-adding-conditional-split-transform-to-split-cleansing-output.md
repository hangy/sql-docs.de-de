---
title: 'Aufgabe 8: Hinzufügen von bedingter Split Transformation zum Aufteilen der Bereinigung der Ausgabe | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d4ebe420-a4a9-4076-89d3-41abe726fc5c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d5a55f0694094e6fe88a42946bcff34f420210f4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "65489669"
---
# <a name="task-8-adding-conditional-split-transform-to-split-cleansing-output"></a>Aufgabe 8: Hinzufügen der Transformation „Bedingtes Teilen“ zur Teilung der Bereinigungsausgabe
  In dieser Aufgabe fügen Sie eine Transformation "Bedingtes Teilen" zum Datenfluss hinzu. Die Transformation "Bedingtes Teilen" kann Zeilen je nach Dateninhalt an andere Ausgaben routen. In diesem Tutorial verwenden Sie die **Datensatzstatus** Ausgabespalte von der DQS-bereinigungstransformation. Sie laden in diesem Lernprogramm nur richtige oder korrigierte Datensätze zu MDS-Server hoch. Aus diesem Grund Sie überprüfen, ob die **Datensatzstatus** ist **richtig** oder **korrigiert**, und kombinieren die Datensätze vor dem die Datensätze in MDS hochladen.  
  
1.  Drag & Drop **Transformation für bedingtes Teilen** aus **allgemeine** im Abschnitt der **SSIS-Toolbox** auf die **Datenfluss** Registerkarte unter **Lieferantendaten Bereinigen**.  
  
2.  Mit der rechten Maustaste **für bedingtes Teilen**, und klicken Sie auf **umbenennen**. Typ **Pick Correct and Corrected Records** , und drücken Sie **EINGABETASTE**.  
  
3.  Herstellen einer mit **Cleanse Supplier Data** und **Pick Correct and Corrected Records** mithilfe des blauen Konnektors.  
  
     ![Cleanse Supplier Data -> richtige auswählen & korrigiert](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-01.jpg "Cleanse Supplier Data -> richtige auswählen & korrigiert")  
  
4.  Doppelklicken Sie auf **Pick Correct and Corrected Records** in die **Datenfluss** Registerkarte.  
  
5.  Ändern der **Standardausgabename** am unteren Rand des Bildschirms **richtig**.  
  
6.  Erweitern Sie **Spalten** in die **linken oberen Bereich**.  
  
     ![Conditional Split Transformation Editor](../../2014/tutorials/media/et-addingcsttosplitcleansingoutput-02.jpg "Conditional Split Transformation Editor")  
  
7.  Drag & Drop **Datensatzstatus** auf die **Bedingung** Spalte.  
  
8.  Typ **== "Corrected"** neben **[Datensatzstatus]** für die **Bedingung** Spalte.  
  
9. Klicken Sie auf **Fall 1** in die **Name der Ausgabespalte**, und ändern Sie den Namen in **korrigiert**.  
  
10. Klicken Sie auf **OK** schließen die **Conditional Split Transformation Editor** Dialogfeld.  
  
## <a name="next-step"></a>Nächster Schritt  
 [Aufgabe 9: Hinzufügen der Union aller Transformation um richtige und korrigierte Datensätze zu kombinieren.](../../2014/tutorials/task-9-adding-union-all-transform-to-combine-correct-and-corrected-records.md)  
  
  
