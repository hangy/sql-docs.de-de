---
title: Länge der Spaltendaten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8d2998eace4772624a1e6590ab2541577147f5c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041610"
---
# <a name="length-of-column-data"></a>Länge von Spaltendaten
> [!IMPORTANT]  
>  Dieses Feature wird in einer zukünftigen Version von Windows entfernt werden. Zu vermeiden Sie, verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen und Änderung von Anwendungen, die derzeit auf dieses Feature verwenden möchten. Microsoft empfiehlt die Verwendung von Cursor-Funktionalität des Treibers.  
  
 Die Cursorbibliothek erstellt einen Puffer in den Cache für jede an das Resultset mit gebundenen Längen-/Indikatorpuffer **SQLBindCol**. Er verwendet die Werte in diesen Puffern zum Erstellen einer **, in denen** -Klausel, wenn es emuliert positioniertes Update oder delete-Anweisungen. Diese Puffer von den Puffern Rowset aktualisiert, wenn er ruft Daten aus der Datenquelle und die Ausführung der positionierte Update-Anweisungen ab.  
  
 Wenn der C-Typ, der einen Datenpuffer SQL_C_CHAR oder sql_c_binary angegeben ist und der Längenindikator /-Wert SQL_NTS ist, wird die Länge der Zeichenfolge der Daten in den Längen-/Indikatorpuffer versetzt.  
  
> [!NOTE]  
>  Die Cursorbibliothek nicht seinem Cache nach einer Spalte aktualisiert, wenn **StrLen_or_IndPtr* in das entsprechende Rowset Puffer SQL_DATA_AT_EXEC oder das Ergebnis des Makros SQL_LEN_DATA_AT_EXEC ist.
