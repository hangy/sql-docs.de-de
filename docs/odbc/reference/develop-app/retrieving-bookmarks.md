---
title: Abrufen von Lesezeichen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020575"
---
# <a name="retrieving-bookmarks"></a>Abrufen von Textmarken
Wenn die Anwendung zu Lesezeichen verwenden, muss er das SQL_ATTR_USE_BOOKMARKS-Anweisungsattribut auf SQL_UB_VARIABLE vor dem Vorbereiten oder Ausführen der Anweisung festgelegt. Dies ist erforderlich, da beim Erstellen und Verwalten von Lesezeichen können teuer sein, damit Lesezeichen aktiviert werden soll, nur, wenn eine Anwendung gut machen kann, dass diese verwenden.  
  
 Lesezeichen werden als 0-Spalte des Resultsets zurückgegeben. Es gibt drei Möglichkeiten, die eine Anwendung abgerufen werden kann:  
  
-   Binden Sie die Spalte 0 des Resultsets. **SQLFetch** oder **SQLFetchScroll** Lesezeichen gibt, für jede Zeile im Rowset zusammen mit den Daten für andere Spalten gebunden.  
  
-   Rufen Sie **SQLSetPos** auf eine Zeile im Rowset zu positionieren, und rufen Sie anschließend **SQLGetData** für die Spalte 0. Wenn ein Treiber Lesezeichen unterstützt, müssen sie immer die Möglichkeit zum Aufrufen unterstützen **SQLGetData** für die Spalte 0 ist, auch wenn dies nicht zulässt, dass Anwendungen Aufrufen **SQLGetData** für andere Spalten, bevor Sie den letzten Grenzwert die Spalte.  
  
-   Rufen Sie **SQLBulkOperations** mit der *Vorgang* -Argument auf SQL_ADD und Spalte 0 gebunden. Der Cursor die Zeile eingefügt, und gibt das Lesezeichen für die Zeile im gebundenen Puffer zurück.
