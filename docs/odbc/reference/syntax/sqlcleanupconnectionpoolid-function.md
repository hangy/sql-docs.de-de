---
title: SQLCleanupConnectionPoolID-Funktion | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCleanupConnectionPoolID function [ODBC]
ms.assetid: 1fc61908-e003-4587-b91a-32f40569fb99
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ee8f9b9879a3533e8196bbc89f8ae0b0a132293a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036090"
---
# <a name="sqlcleanupconnectionpoolid-function"></a>SQLCleanupConnectionPoolID-Funktion
**Übereinstimmung mit Standards**  
 Eingeführt in Version: ODBC-3,81 Standardkompatibilität: ODBC  
  
 **Zusammenfassung**  
 **SQLCleanupConnectionPoolID** informiert einen Treiber, der Pool-ID Zeitlimit überschritten wurde. Timeout bei ein Pool ID können Timeout auf, wenn alle Verbindungen in einem Pool, der dieser Anwendungspool-ID zugeordnet wurden. Finden Sie unter [Verbindungspooling in der Microsoft Data Access Components](https://msdn.microsoft.com/library/ms810829.aspx) für Weitere Informationen zum Verbindungstimeout.  
  
## <a name="syntax"></a>Syntax  
  
```cpp
  
SQLRETURN  SQLCleanupConnectionPoolID (  
                SQLHENV    EnvironmentHandle  
                SQLPOOLID  PoolID );  
```  
  
## <a name="arguments"></a>Argumente  
 *EnvironmentHandle*  
 [Eingabe] Das Umgebungshandle des Pools.  
  
 *PoolID*  
 [Eingabe] Der Pool, die die Pool-ID, bei denen Timeout wurde zugeordnet sind.  
  
## <a name="returns"></a>Rückgabewert  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR oder SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnose  
 Der Treiber-Manager verarbeitet keine Diagnoseinformationen Merry **SQLCleanupConnectionPoolID**.  
  
 Eine Anwendung kann nicht vom Treiber zurückgegebene Fehlermeldung empfangen.  
  
## <a name="remarks"></a>Hinweise  
 **SQLCleanupConnectionPoolID** kann jederzeit aufgerufen werden, aber der Treiber-Manager wird sichergestellt, dass kein anderer Thread gleichzeitig aufrufen ist **SQLGetPoolID** und kein anderer Thread gleichzeitig ruft  **SQLRateConnection** und **SQLPoolConnect** mit einem Verbindungs-Info-Token mit diesem Pool-ID zugewiesen Aus diesem Grund muss der Treiber stellen Sie sicher, dass diese Funktion threadsicher ist.  
  
 Ein Treiber kann die Pool-ID zugeordneten Ressourcen bereinigen.  
  
 Anwendungen sollten diese Funktion nicht direkt aufrufen. Ein ODBC-Treiber, der treiberfähiges Verbindungspooling unterstützt, muss diese Funktion implementieren.  
  
 Umfassen Sie sqlspi.h für die Entwicklung von ODBC-Treiber.  
  
## <a name="see-also"></a>Siehe auch  
 [Entwickeln einen ODBC-Treiber](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Treiberfähiges Verbindungspooling](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Developing Connection-Pool Awareness in an ODBC Driver (Entwickeln von Verbindungspool-Unterstützung in einem ODBC-Treiber)](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
