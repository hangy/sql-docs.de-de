---
title: Verwenden von grundlegenden Datentypen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d7044936-5b8c-4def-858c-28a11ef70a97
author: MightyPen
ms.author: genemi
ms.openlocfilehash: abbd2aa3c277ad36f419de849b02433f17d27403
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026514"
---
# <a name="using-basic-data-types"></a>Verwenden von Standarddatentypen

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Der [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] verwendet die JDBC-Standarddatentypen für die Konvertierung der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Datentypen in ein Format, das von der Programmiersprache Java verarbeitet werden kann, und umgekehrt. Der JDBC-Treiber bietet Unterstützung für die JDBC 4,0-API, die den **SQLXML** -Datentyp und nationale (Unicode-) Datentypen wie **NCHAR**, **nvarchar**, **LONGNVARCHAR**und **NCLOB**enthält.  
  
## <a name="data-type-mappings"></a>Datentypzuordnungen

Die folgende Tabelle enthält eine Liste der Standardzuordnungen zwischen den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Standarddatentypen, den JDBC-Datentypen und den von der Programmiersprache Java verwendeten Datentypen:  
  
| SQL Server-Typen   | JDBC-Typen (java.sql.Types)                        | Java-Typen          |
| ------------------ | -------------------------------------------------- | ---------------------------- |
| BIGINT             | bigint                                             | long                         |
| BINARY             | BINARY                                             | byte[]                       |
| bit                | BIT                                                | boolean                      |
| char               | CHAR                                               | Zeichenfolge                       |
| date               | DATE                                               | java.sql.Date                |
| DATETIME           | timestamp                                          | java.sql.Timestamp           |
| datetime2          | timestamp                                          | java.sql.Timestamp           |
| datetimeoffset (2) | microsoft.sql.Types.DATETIMEOFFSET                 | microsoft.sql.DateTimeOffset |
| Decimal            | DEZIMAL                                            | java.math.BigDecimal         |
| FLOAT              | DOUBLE                                             | double                       |
| image              | LONGVARBINARY                                      | byte[]                       |
| INT                | INTEGER                                            | INT                          |
| money              | DEZIMAL                                            | java.math.BigDecimal         |
| NCHAR              | CHAR<br /><br /> NCHAR (Java SE 6.0)               | Zeichenfolge                       |
| ntext              | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | Zeichenfolge                       |
| NUMERIC            | NUMERIC                                            | java.math.BigDecimal         |
| NVARCHAR           | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | Zeichenfolge                       |
| nvarchar(max)      | VARCHAR<br /><br /> NVARCHAR (Java SE 6.0)         | Zeichenfolge                       |
| REAL               | real                                               | FLOAT                        |
| smalldatetime      | timestamp                                          | java.sql.Timestamp           |
| SMALLINT           | SMALLINT                                           | short                        |
| SMALLMONEY         | DEZIMAL                                            | java.math.BigDecimal         |
| text               | LONGVARCHAR                                        | Zeichenfolge                       |
| time               | TIME (1)                                           | java.sql.Time (1)            |
| timestamp          | BINARY                                             | byte[]                       |
| TINYINT            | TINYINT                                            | short                        |
| udt                | VARBINARY                                          | byte[]                       |
| UNIQUEIDENTIFIER   | CHAR                                               | Zeichenfolge                       |
| varbinary          | VARBINARY                                          | byte[]                       |
| varbinary(max)     | VARBINARY                                          | byte[]                       |
| varchar            | VARCHAR                                            | Zeichenfolge                       |
| varchar(max)       | VARCHAR                                            | Zeichenfolge                       |
| xml                | LONGVARCHAR<br /><br /> LONGNVARCHAR (Java SE 6.0) | Zeichenfolge<br /><br /> SQLXML    |
| sqlvariant         | SQLVARIANT                                         | Objekt                       |
| Geometrie           | VARBINARY                                          | byte[]                       |
| geography          | VARBINARY                                          | byte[]                       |
  
(1) Zur Verwendung von java.sql.Time mit dem Zeittyp [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen Sie die Verbindungseigenschaft **sendTimeAsDatetime** auf „false“ festlegen.  
  
(2) Sie können Programm gesteuert auf die Werte von **DateTimeOffset** mit der [DateTimeOffset-Klasse](../../connect/jdbc/reference/datetimeoffset-class.md)zugreifen.  
  
Die folgenden Abschnitte enthalten Beispiele für die Verwendung des JDBC-Treibers und der Standarddatentypen. Ein ausführlicheres Beispiel für die Verwendung der Standarddatentypen in einer Java-Anwendung finden Sie unter [Standarddatentypen – Beispiel](../../connect/jdbc/basic-data-types-sample.md).  
  
## <a name="retrieving-data-as-a-string"></a>Abrufen von Daten als Zeichenfolge

Wenn Sie Daten aus einer Datenquelle abrufen müssen, die einem der JDBC-Standarddatentypen zugeordnet ist und als Zeichenfolge angezeigt werden soll, oder wenn stark typisierte Daten nicht erforderlich sind, können Sie die [getString](../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)-Methode der [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)-Klasse verwenden, wie in folgendem Beispiel gezeigt:  
  
[!code[JDBC#UsingBasicDataTypes1](../../connect/jdbc/codesnippet/Java/using-basic-data-types_1.java)]  
  
## <a name="retrieving-data-by-data-type"></a>Abrufen von Daten nach Datentyp

Wenn Sie Daten aus einer Datenquelle abrufen müssen und den Typ der abgerufenen Daten kennen, verwenden Sie eine der get\<Type>-Methoden der SQLServerResultSet-Klasse, die auch als *getter*-Methoden bezeichnet werden. Sie können bei den get\<Type>-Methoden einen Spaltennamen oder einen Spaltenindex verwenden, wie im Folgenden dargestellt:  
  
[!code[JDBC#UsingBasicDataTypes2](../../connect/jdbc/codesnippet/Java/using-basic-data-types_2.java)]  
  
> [!NOTE]  
> Die Methoden getUnicodeStream und getBigDecimal mit Skalierung sind veraltet und werden vom JDBC-Treiber nicht unterstützt.

## <a name="updating-data-by-data-type"></a>Aktualisieren von Daten nach Datentyp

Wenn Sie den Wert eines Felds in einer Datenquelle aktualisieren müssen, verwenden Sie einen der\<Updatetyp > Methoden der SQLServerResultSet-Klasse. Im folgenden Beispiel wird die [updateInt](../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)-Methode zusammen mit der [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)-Methode verwendet, um die Daten in der Datenquelle zu aktualisieren:  
  
[!code[JDBC#UsingBasicDataTypes3](../../connect/jdbc/codesnippet/Java/using-basic-data-types_3.java)]  
  
> [!NOTE]  
> Der JDBC-Treiber kann keine SQL Server-Spalte mit einem Spaltennamen aktualisieren, dessen Länge mehr als 127 Zeichen beträgt. Wenn ein Update einer Spalte, deren Name mehr als 127 Zeichen umfasst, ausgeführt werden soll, wird eine Ausnahme ausgegeben.  
  
## <a name="updating-data-by-parameterized-query"></a>Aktualisieren von Daten durch parametrisierte Abfragen

Wenn Sie Daten in einer Datenquelle durch eine parametrisierte Abfrage aktualisieren müssen, können Sie den Datentyp der Parameter mit einer der set\<Type>-Methoden der [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)-Klasse festlegen, die auch als *setter-Methoden* bezeichnet werden. Im folgenden Beispiel wird die parametrisierte Abfrage mit der [prepareStatement](../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)-Methode vorkompiliert, dann wird die [setString](../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)-Methode verwendet, um vor dem Aufrufen der [executeUpdate](../../connect/jdbc/reference/executeupdate-method.md)-Methode den string-Wert des Parameters festzulegen.  
  
[!code[JDBC#UsingBasicDataTypes4](../../connect/jdbc/codesnippet/Java/using-basic-data-types_4.java)]  
  
Weitere Informationen zu parametrisierten Abfragen finden Sie unter [Verwenden einer SQL-Anweisung mit Parametern](../../connect/jdbc/using-an-sql-statement-with-parameters.md).  

## <a name="passing-parameters-to-a-stored-procedure"></a>Übergeben von Parametern an gespeicherte Prozeduren

Wenn Sie typisierte Parameter an eine gespeicherte Prozedur übergeben müssen, können Sie die Parameter mit einer der set\<Type>-Methoden der [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)-Klasse nach Namen oder Index festlegen. Im folgenden Beispiel wird der Aufruf der gespeicherten Prozedur mit der [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)-Methode eingerichtet, dann wird die [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)-Methode verwendet, um vor dem Aufrufen der [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)-Methode den Parameter für den Aufruf festzulegen.  
  
[!code[JDBC#UsingBasicDataTypes5](../../connect/jdbc/codesnippet/Java/using-basic-data-types_5.java)]  
  
> [!NOTE]  
> In diesem Beispiel wird ein Resultset zurückgegeben, das die Ergebnisse der gespeicherten Prozedur enthält.

Weitere Informationen zum Verwenden des JDBC-Treibers mit gespeicherten Prozeduren und Eingabe Parametern finden Sie unter [Verwenden einer gespeicherten Prozedur mit Eingabe Parametern](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md).  

## <a name="retrieving-parameters-from-a-stored-procedure"></a>Abrufen von Parametern von gespeicherten Prozeduren

Wenn Sie Parameter wieder aus einer gespeicherten Prozedur abrufen müssen, müssen Sie zuerst mit der [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)-Methode der SQLServerCallableStatement-Klasse einen out-Parameter nach Name oder Index registrieren und dann nach Aufruf der gespeicherten Prozedur den zurückgegebenen out-Parameter einer geeigneten Variablen zuordnen. Im folgenden Beispiel wird der Aufruf der gespeicherten Prozedur mit der prepareCall-Methode eingerichtet, mit der registerOutParameter-Methode wird der out-Parameter eingerichtet, und dann wird die [setString](../../connect/jdbc/reference/setstring-method-sqlservercallablestatement.md)-Methode verwendet, um vor dem Aufruf der executeQuery-Methode den Parameter für den Aufruf festzulegen. Der vom out-Parameter der gespeicherten Prozedur zurückgegebene Wert wird mit der [getShort](../../connect/jdbc/reference/getshort-method-sqlservercallablestatement.md)-Methode abgerufen.  
  
[!code[JDBC#UsingBasicDataTypes6](../../connect/jdbc/codesnippet/Java/using-basic-data-types_6.java)]  
  
> [!NOTE]  
> Zusätzlich zum zurückgegebenen out-Parameter kann auch ein Resultset zurückgegeben werden, das die Ergebnisse der gespeicherten Prozedur enthält.  
  
Weitere Informationen zum Verwenden des JDBC-Treibers mit gespeicherten Prozeduren und Ausgabeparametern finden [Sie unter Verwenden einer gespeicherten Prozedur mit Ausgabeparametern](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md).  

## <a name="see-also"></a>Siehe auch

[Grundlegendes zu den Datentypen des JDBC-Treibers](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
