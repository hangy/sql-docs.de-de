---
title: Für Konvertierungsprogrammspezifikationen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec94f3e02b720617e8f7369b12a916c2bbbe7b16
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093801"
---
# <a name="translator-specification-subkeys"></a>Unterschlüssel für Konvertierungsprogrammspezifikationen
Jede Konvertierer, die in der ODBC-Konvertierungsprogramme-Unterschlüssel aufgeführt verfügt über einen Unterschlüssel selbst. Dieser Unterschlüssel hat den gleichen Namen wie der entsprechende Wert unter dem Unterschlüssel für ODBC-Konvertierungsprogramme. Die Werte unter diesem Unterschlüssel auflisten, die vollständigen Pfade der Konvertierer, Translator-Setup-DLLs und die Verwendungsanzahl der. Die Formate der-Werte sind wie in der folgenden Tabelle gezeigt.  
  
|Name|Datentyp|Daten|  
|----------|---------------|----------|  
|Translator|REG_SZ|*translator-DLL-path*|  
|Setup|REG_SZ|*setup-DLL-path*|  
|UsageCount|REG_DWORD|*count*|  
  
 Informationen über die Verwendungszähler, finden Sie unter [zählen der Verwendung](../../../odbc/reference/install/usage-counting.md) weiter oben in diesem Abschnitt.  
  
 Anwendungen sollten nicht die Verwendungsanzahl der festlegen. ODBC wird dieser Zähler zu verwalten.  
  
 Nehmen wir beispielsweise an den Microsoft Translator verwenden Code Seite verfügt über einen Konvertierungs-DLL, die mit dem Namen Mscpxl32.dll, die die Translator-Setup-Funktionen in der gleichen DLL sind und dass der Konvertierer drei Mal installiert wurde. Die Werte unter dem Unterschlüssel Microsoft Code Seite Translator könnte folgendermaßen aussehen:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
