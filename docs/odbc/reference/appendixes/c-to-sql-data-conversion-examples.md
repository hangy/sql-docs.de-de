---
title: C, um Beispiele für die Konvertierung von SQL-Daten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e475abb699c7fa7240ca6eb39b1b32f1730d33c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125738"
---
# <a name="c-to-sql-data-conversion-examples"></a>Beispiele für die Datenkonvertierung von C zu SQL
Die folgenden Beispiele veranschaulichen, wie der Treiber C-Daten in SQL-Daten konvertiert:  
  
|C-Typ-ID|Wert der C-Daten|SQL-Typ<br /><br /> Bezeichner (identifier)|Spalte<br /><br /> Länge|SQL data<br /><br /> Wert|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|6|abcdef|n/v|  
|SQL_C_CHAR|abcdef\0 [a]|SQL_CHAR|5|abcde|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|8 [b]|1234.56|n/v|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|7 [b]|1234.5|22001|  
|SQL_C_CHAR|1234.56\0 [a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|n/v|1234.56|n/v|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|n/v|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|n/v|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|10|1992-12-31|n/v|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31 [c]|SQL_TIMESTAMP|n/v|1992-12-31 00:00:00.0|n/v|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|22|1992-12-31 23:45:55.12|n/v|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000 [d]|SQL_CHAR|18|----|22003|  
  
 [a] "\0" stellt einen Null-Terminierung Byte dar. Das Null-Terminierung Byte ist erforderlich, nur, wenn die Länge der Daten SQL_NTS ist.  
  
 [b] zusätzlich zu der Bytes für Zahlen ein Byte für eine Anmeldung erforderlich ist, und eine andere Byte ist erforderlich, damit dem Dezimaltrennzeichen an.  
  
 [c] die Zahlen in dieser Liste sind die Zahlen in den Feldern der SQL_DATE_STRUCT-Struktur gespeichert.  
  
 [d] die Zahlen in dieser Liste sind die Zahlen in den Feldern der SQL_TIMESTAMP_STRUCT Struktur gespeichert.
