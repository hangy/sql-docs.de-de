---
title: SQLInstallTranslator-Zuordnung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6433df796c88abd7873915266d1a2ca4041a5c62
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125727"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator-Zuordnung
Wenn eine ODBC *2.x* Anwendungsaufrufe **SQLInstallTranslator** über einen ODBC *3.x* Treiber, der Treiber-Manager ordnet den Aufruf von  **SQLInstallTranslatorEx**. Eine Anwendung sollte nicht aufrufen **SQLInstallTranslator** in die ODBC *3.x* Treiber-Manager mit der *LpszInfFile* -Argument auf einen anderen Wert als NULL festgelegt. Die ODBC. INF-Datei, die in ODBC verwendet *2.x* wird nicht mehr unterstützt, in ODBC *3.x*, dies gilt auch für die Abwärtskompatibilität.
