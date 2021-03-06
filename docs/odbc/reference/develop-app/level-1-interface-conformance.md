---
title: Schnittstellenübereinstimmung der Ebene 1 | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05cf381ccbb8c0747db88259acfb4ba218d3e0ae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135013"
---
# <a name="level-1-interface-conformance"></a>Schnittstellenübereinstimmung auf Ebene 1
Der Konformitätsgrad des Ebene-1-Schnittstelle enthält die Core-Standards auf Funktionen der Benutzeroberfläche sowie auf zusätzliche Funktionen, z. B. Transaktionen, die in der Regel in einer OLTP-relationale DBMS verfügbar sind. Ein Level 1-Schnittstelle-konformen Treiber kann die Anwendung, zusätzlich zu den Features in der Core-Schnittstelle-Konformitätsgrad Folgendes:  
  
|||  
|-|-|  
|101|Geben Sie das Schema der Datenbank, Tabellen und Sichten (mithilfe von zweiteiligen Namen). (Weitere Informationen finden Sie unter den dreiteiligen Benennung 201 im feature [Ebene-2-Schnittstellenübereinstimmung](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|Rufen Sie "true" asynchrone Ausführung der ODBC-Funktionen, in dem entsprechende ODBC-Funktionen für alle synchron oder alle asynchron auf eine bestimmte Verbindung sind.|  
|103|Verwenden Sie scrollfähige Cursor, und dadurch Zugriff auf ein Resultset in Methoden als Vorwärtscursor, durch den Aufruf **SQLFetchScroll** mit der *FetchOrientation* Argument als SQL_FETCH_NEXT. (Die SQL_FETCH_BOOKMARK *FetchOrientation* ist im Feature 204 [Ebene-2-Schnittstellenübereinstimmung](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|Abrufen von Primärschlüsseln von Tabellen, durch den Aufruf **SQLPrimaryKeys**.|  
|105|Verwenden von gespeicherten Prozeduren, durch die ODBC-Escapesequenz für Prozeduraufrufen und Abfragen von Wörterbuch mit den Daten in Bezug auf die gespeicherten Prozeduren, durch den Aufruf **SQLProcedureColumns** und **SQLProcedures**. (Der Prozess, mit dem Verfahren erstellt werden, und in der Datenquelle gespeichert, ist außerhalb des Bereichs dieses Dokuments.)|  
|106|Verbinden mit einer Datenquelle, indem Sie interaktiv Durchsuchen von den verfügbaren Servern, durch den Aufruf **SQLBrowseConnect**.|  
|107|Verwenden von ODBC-Funktionen anstelle von SQL-Anweisungen zum Ausführen bestimmter Datenbankvorgänge: **SQLSetPos** mit SQL_POSITION und SQL_REFRESH.|  
|108|Zugriff auf den Inhalt der Generierung von Batches und gespeicherte Prozeduren, durch den Aufruf mehrerer Resultsets **SQLMoreResults**.|  
|109|Trennen von Transaktionen über mehrere ODBC-Funktionen mit "true" Unteilbarkeit und die Option zum Angeben der SQL_ROLLBACK in hinweg **SQLEndTran**.|
