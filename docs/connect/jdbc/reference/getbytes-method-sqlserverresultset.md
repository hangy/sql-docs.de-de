---
title: getBytes-Methode (SQLServerResultSet) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getBytes
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d16a0aea-6144-4fcb-bcbc-5d7daa36d327
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64eb652fe7e5aa7e4d034fd2fa837ff9cca38a9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67953355"
---
# <a name="getbytes-method-sqlserverresultset"></a>getBytes-Methode (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ruft den Wert der angegebenen Spalte in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)-Objekts als Array vom Typ **byte** in der Programmiersprache Java ab.  
  
## <a name="overload-list"></a>Überladungsliste  
  
|Name|und Beschreibung|  
|----------|-----------------|  
|[getBytes (int)](../../../connect/jdbc/reference/getbytes-method-int-sqlserverresultset.md)|Ruft den Wert des angegebenen Spaltenindexes in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)-Objekts als Array vom Typ **byte** in der Programmiersprache Java ab.|  
|[getBytes (java.lang.String)](../../../connect/jdbc/reference/getbytes-method-java-lang-string-sqlserverresultset.md)|Ruft den Wert des angegebenen Spaltennamens in der aktuellen Zeile dieses [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)-Objekts als Array vom Typ **byte** in der Programmiersprache Java ab.|  
  
## <a name="remarks"></a>Bemerkungen  
 In einer früheren Version von [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] konnten Sie mithilfe von „SQLServerResultSet.getBytes“ Werte zwischen Bytearrays und dem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datentyp **date**, **time**, **datetime2** oder **datetimeoffset** konvertieren. Nun wird durch Verwendung der Methode mit diesen Datentypen eine Ausnahme ausgelöst, die angibt, dass die Konvertierung nicht unterstützt wird.  
  
## <a name="see-also"></a>Weitere Informationen  
 [SQLServerResultSet-Elemente](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet-Klasse](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
