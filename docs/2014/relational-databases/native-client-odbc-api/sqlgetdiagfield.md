---
title: SQLGetDiagField | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLGetDiagField function
ms.assetid: 395245ba-0372-43ec-b9a4-a29410d85a6d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8fb158b2c11f48733c5eacb3827a43a3303c4a51
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62657703"
---
# <a name="sqlgetdiagfield"></a>SQLGetDiagField
  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber gibt an, die folgenden zusätzlichen Diagnosefelder für `SQLGetDiagField`. Diese Felder unterstützen eine umfangreiche Fehlerberichterstellung für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anwendungen und sind in allen Diagnosedatensätzen verfügbar, die für verbundene ODBC-Verbindungshandles und ODBC-Anweisungshandles generiert werden. Die Felder werden in sqlncli.h definiert.  
  
|Diagnosedatensatzfeld|Description|  
|------------------------------|-----------------|  
|SQL_DIAG_SS_LINE|Meldet die Zeilennummer einer gespeicherten Prozedur, die einen Fehler verursacht. Der Wert von SQL_DIAG_SS_LINE ist nur aussagekräftig, wenn SQL_DIAG_SS_PROCNAME einen Wert zurückgibt. Der Wert wird als 16-Bit-Ganzzahl ohne Vorzeichen zurückgegeben.|  
|SQL_DIAG_SS_MSGSTATE|Der Status einer Fehlermeldung. Informationen über den Status der Fehlermeldung finden Sie unter [RAISERROR](/sql/t-sql/language-elements/raiserror-transact-sql). Der Wert wird als 32-Bit-Ganzzahl mit Vorzeichen zurückgegeben.|  
|SQL_DIAG_SS_PROCNAME|Der Name der gespeicherten Prozedur, die einen Fehler generiert, falls zutreffend. Der Wert wird als Zeichenfolge zurückgegeben. Die Länge der Zeichenfolge (in Zeichen) hängt von der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Version ab. Sie kann bestimmt werden, indem die [SQLGetInfo](sqlgetinfo.md) -Funktion, die den Wert für SQL_MAX_PROCEDURE_NAME_LEN anfordert, aufgerufen wird.|  
|SQL_DIAG_SS_SEVERITY|Der Schweregrad der zugehörigen Fehlermeldung. Der Wert wird als 32-Bit-Ganzzahl mit Vorzeichen zurückgegeben.|  
|SQL_DIAG_SS_SRVNAME|Der Name des Servers, auf dem der Fehler aufgetreten ist. Der Wert wird als Zeichenfolge zurückgegeben. Die Länge der Zeichenfolge (in Zeichen) wird in sqlncli.h durch das SQL_MAX_SQLSERVERNAME-Makro definiert.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-spezifische Diagnosefelder, die Zeichendaten, SQL_DIAG_SS_PROCNAME und SQL_DIAG_SS_SRVNAME enthalten, geben diese Daten an den Client mit NULL-Terminierung oder als ANSI- bzw. Unicode-Zeichenfolgen zurück. Falls notwendig sollte die Anzahl von Zeichen der Zeichenbreite entsprechend angepasst werden. Alternativ kann die korrekte Länge der Programmvariablen mit einem übertragbaren C-Datentyp wie TCHAR oder SQLTCHAR sichergestellt werden.  
  
 Der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC-Treiber meldet die folgenden zusätzlichen dynamischen Funktionscodes, die die zuletzt versuchte [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Anweisung identifizieren. Der dynamische Funktionscode wird im Header (Datensatz 0) des Diagnosedatensatzes zurückgegeben und ist daher bei jeder Ausführung verfügbar (unabhängig davon, ob diese erfolgreich ist oder nicht).  
  
|Dynamischer Funktionscode|Source|  
|---------------------------|------------|  
|SQL_DIAG_DFC_SS_ALTER_DATABASE|ALTER DATABASE-Anweisung|  
|SQL_DIAG_DFC_SS_CHECKPOINT|CHECKPOINT-Anweisung|  
|SQL_DIAG_DFC_SS_CONDITION|Ein Fehler ist in der WHERE-Klausel oder der HAVING-Klausel einer Anweisung aufgetreten.|  
|SQL_DIAG_DFC_SS_CREATE_DATABASE|CREATE DATABASE-Anweisung|  
|SQL_DIAG_DFC_SS_CREATE_DEFAULT|CREATE DEFAULT-Anweisung|  
|SQL_DIAG_DFC_SS_CREATE_PROCEDURE|CREATE PROCEDURE-Anweisung|  
|SQL_DIAG_DFC_SS_CREATE_RULE|CREATE RULE-Anweisung|  
|SQL_DIAG_DFC_SS_CREATE_TRIGGER|CREATE TRIGGER-Anweisung|  
|SQL_DIAG_DFC_SS_CURSOR_DECLARE|DECLARE CURSOR-Anweisung|  
|SQL_DIAG_DFC_SS_CURSOR_OPEN|OPEN-Anweisung|  
|SQL_DIAG_DFC_SS_CURSOR_FETCH|FETCH-Anweisung|  
|SQL_DIAG_DFC_SS_CURSOR_CLOSE|CLOSE-Anweisung|  
|SQL_DIAG_DFC_SS_DEALLOCATE_CURSOR|DEALLOCATE-Anweisung|  
|SQL_DIAG_DFC_SS_DBCC|DBCC-Anweisung|  
|SQL_DIAG_DFC_SS_DENY|DENY-Anweisung|  
|SQL_DIAG_DFC_SS_DROP_DATABASE|DROP DATABASE-Anweisung|  
|SQL_DIAG_DFC_SS_DROP_DEFAULT|DROP DEFAULT-Anweisung|  
|SQL_DIAG_DFC_SS_DROP_PROCEDURE|DROP PROCEDURE-Anweisung|  
|SQL_DIAG_DFC_SS_DROP_RULE|DROP RULE-Anweisung|  
|SQL_DIAG_DFC_SS_DROP_TRIGGER|DROP TRIGGER-Anweisung|  
|SQL_DIAG_DFC_SS_DUMP_DATABASE|BACKUP oder DUMP DATABASE-Anweisung|  
|SQL_DIAG_DFC_SS_DUMP_TABLE|DUMP TABLE-Anweisung|  
|SQL_DIAG_DFC_SS_DUMP_TRANSACTION|BACKUP oder DUMP TRANSACTION-Anweisung Auch für eine CHECKPOINT-Anweisung zurückgegeben, wenn die **Trunc. Log auf Chkpt.** aktiviert ist.|  
|SQL_DIAG_DFC_SS_GOTO|GOTO-Anweisung zur Ablaufsteuerung|  
|SQL_DIAG_DFC_SS_INSERT_BULK|INSERT BULK-Anweisung|  
|SQL_DIAG_DFC_SS_KILL|KILL-Anweisung|  
|SQL_DIAG_DFC_SS_LOAD_DATABASE|LOAD oder RESTORE DATABASE-Anweisung|  
|SQL_DIAG_DFC_SS_LOAD_HEADERONLY|LOAD oder RESTORE HEADERONLY-Anweisung|  
|SQL_DIAG_DFC_SS_LOAD_TABLE|LOAD TABLE-Anweisung|  
|SQL_DIAG_DFC_SS_LOAD_TRANSACTION|LOAD oder RESTORE TRANSACTION-Anweisung|  
|SQL_DIAG_DFC_SS_PRINT|PRINT-Anweisung|  
|SQL_DIAG_DFC_SS_RAISERROR|RAISERROR-Anweisung|  
|SQL_DIAG_DFC_SS_READTEXT|READTEXT-Anweisung|  
|SQL_DIAG_DFC_SS_RECONFIGURE|RECONFIGURE-Anweisung|  
|SQL_DIAG_DFC_SS_RETURN|RETURN-Anweisung zur Ablaufsteuerung|  
|SQL_DIAG_DFC_SS_SELECT_INTO|SELECT INTO-Anweisung|  
|SQL_DIAG_DFC_SS_SET|SET-Anweisung (generisch, alle Optionen)|  
|SQL_DIAG_DFC_SS_SET_IDENTITY_INSERT|SET IDENTITY_INSERT-Anweisung|  
|SQL_DIAG_DFC_SS_SET_ROW_COUNT|SET ROWCOUNT-Anweisung|  
|SQL_DIAG_DFC_SS_SET_STATISTICS|SET STATISTICS IO- oder SET STATISTICS TIME-Anweisung|  
|SQL_DIAG_DFC_SS_SET_TEXTSIZE|SET TEXTSIZE-Anweisung|  
|SQL_DIAG_DFC_SS_SETUSER|SETUSER-Anweisung|  
|SQL_DIAG_DFC_SS_SET_XCTLVL|SET TRANSACTION ISOLATION LEVEL-Anweisung|  
|SQL_DIAG_DFC_SS_SHUTDOWN|SHUTDOWN-Anweisung|  
|SQL_DIAG_DFC_SS_TRANS_BEGIN|BEGIN TRAN-Anweisung|  
|SQL_DIAG_DFC_SS_TRANS_COMMIT|COMMIT TRAN-Anweisung|  
|SQL_DIAG_DFC_SS_TRANS_PREPARE|Vorbereiten, um einen Commit für eine verteilte Transaktion auszuführen|  
|SQL_DIAG_DFC_SS_TRANS_ROLLBACK|ROLLBACK TRAN-Anweisung|  
|SQL_DIAG_DFC_SS_TRANS_SAVE|SAVE TRAN-Anweisung|  
|SQL_DIAG_DFC_SS_TRUNCATE_TABLE|TRUNCATE TABLE-Anweisung|  
|SQL_DIAG_DFC_SS_UPDATE_STATISTICS|UPDATE STATISTICS-Anweisung|  
|SQL_DIAG_DFC_SS_UPDATETEXT|UPDATETEXT-Anweisung|  
|SQL_DIAG_DFC_SS_USE|USE-Anweisung|  
|SQL_DIAG_DFC_SS_WAITFOR|WAITFOR-Anweisung zur Ablaufsteuerung|  
|SQL_DIAG_DFC_SS_WRITETEXT|WRITETEXT-Anweisung|  
  
## <a name="sqlgetdiagfield-and-table-valued-parameters"></a>SQLGetDiagField und Tabellenwertparameter  
 SQLGetDiagField kann verwendet werden, um zwei Diagnosefelder abzurufen: SQL_DIAG_SS_TABLE_COLUMN_NUMBER und SQL_DIAG_SS_TABLE_ROW_NUMBER. Mithilfe dieser Felder können Sie bestimmen, welcher Wert den Fehler oder die Warnung im Zusammenhang mit dem Diagnosedatensatz verursacht hat.  
  
 Weitere Informationen zu Tabellenwertparametern finden Sie unter [Table-Valued Parameters &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Siehe auch  
 [SQLGetDiagField Function](https://go.microsoft.com/fwlink/?LinkId=59352)   
 [ODBC-API-Implementierungsdetails](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
