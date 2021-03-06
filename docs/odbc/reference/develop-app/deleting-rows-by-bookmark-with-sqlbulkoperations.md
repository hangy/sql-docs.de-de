---
title: Löschen von Zeilen durch Lesezeichen mit SQLBulkOperations | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], SQLBulkOperations
- SQLBulkOperations function [ODBC], deleting rows
- updating data [ODBC], SQLBulkOperations
ms.assetid: 46139ec9-7095-481a-bf45-20200a2fdc03
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a34f96dd7f5c2f0e2ac4bbb3feae06ea4856a248
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076814"
---
# <a name="deleting-rows-by-bookmark-with-sqlbulkoperations"></a>Löschen von Zeilen durch Textmarken mit SQLBulkOperations
Beim Löschen einer Zeile durch Lesezeichen, **SQLBulkOperations** macht die Datenquelle, die eine oder mehrere ausgewählte Zeilen der Tabelle zu löschen. Die Zeilen werden durch das Lesezeichen in einer Lesezeichenspalte gebundene identifiziert.  
  
 Zum Löschen von Zeilen durch Lesezeichen mit **SQLBulkOperations**, die Anwendung führt Folgendes:  
  
1.  Ruft ab, und speichert die Lesezeichen aller Zeilen gelöscht werden soll. Wenn mehrere Lesezeichen vorhanden ist, und spaltenbezogene Bindungen verwendet wird, werden die Lesezeichen in einem Array gespeichert. Wenn mehrere Lesezeichen vorhanden ist, und die zeilenweise Bindung wird verwendet, werden die Lesezeichen in ein Array von Zeilenstrukturen gespeichert.  
  
2.  Legt das SQL_ATTR_ROW_ARRAY_SIZE-Anweisungsattribut auf die Anzahl von Lesezeichen und bindet den Puffer mit der Lesezeichenwert, oder das Array von Lesezeichen, an die Spalte 0.  
  
3.  Aufrufe **SQLBulkOperations** mit *Vorgang* SQL_DELETE_BY_BOOKMARK festgelegt.
