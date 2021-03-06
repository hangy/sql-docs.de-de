---
title: sql_variant Unterstützung für Datums-und Uhrzeit Typen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sql_variant data type
ms.assetid: 12ff1ea6-e2cc-40e6-910c-3126974a90b3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f795f1848f3e4c9fe1239df79677c35c38ba3b58
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783511"
---
# <a name="sql_variant-support-for-date-and-time-types"></a>sql_variant-Unterstützung für Datums- und Uhrzeittypen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In diesem Thema wird beschrieben, wie der **sql_variant** -Datentyp erweiterte Datums-und Uhrzeit Funktionen unterstützt.  
  
 Das Spaltenattribut SQL_CA_SS_VARIANT_TYPE wird zur Rückgabe des C-Typs einer Variant-Ergebnisspalte verwendet. [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] führt ein zusätzliches Attribut ein, SQL_CA_SS_VARIANT_SQL_TYPE, mit dem der SQL-Typ einer Variant-Ergebnisspalte im Implementierungs Zeilen Deskriptor (IRD) festgelegt wird. SQL_CA_SS_VARIANT_SQL_TYPE können auch im Implementierungs Parameter Deskriptor (IPD) verwendet werden, um den SQL-Typ eines SQL_SS_TIME2 oder SQL_SS_TIMESTAMPOFFSET Parameters anzugeben, der SQL_C_BINARY C-Typ mit dem Typ SQL_SS_VARIANT gebunden ist.  
  
 Die neuen Typen SQL_SS_TIME2 und SQL_SS_TIMESTAMPOFFSET können von SQLColAttribute festgelegt werden. SQL_CA_SS_VARIANT_SQL_TYPE können von SQLGetDescField zurückgegeben werden.  
  
 Für Ergebnisspalten konvertiert der Treiber Daten von Variant- zu Datum-/Uhrzeit-Typen. Weitere Informationen finden Sie unter [Konvertierungen von SQL in C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md). Beim Binden an SQL_C_BINARY muss die Pufferlänge groß genug sein, um die Struktur zu empfangen, die dem SQL-Typ entspricht.  
  
 Bei den Parametern SQL_SS_TIME2 und SQL_SS_TIMESTAMPOFFSET konvertiert der Treiber C-Werte in **sql_variant** Werte, wie in der folgenden Tabelle beschrieben. Wenn ein Parameter als SQL_C_BINARY gebunden ist und der Servertyp SQL_SS_VARIANT lautet, dann wird er als Binärwert behandelt, sofern die Anwendung SQL_CA_SS_VARIANT_SQL_TYPE nicht auf einen anderen SQL-Typ festgelegt hat. In diesem Fall hat QL_CA_SS_VARIANT_SQL_TYPE Vorrang; d. h. wenn SQL_CA_SS_VARIANT_SQL_TYPE festgelegt wurde, wird damit das Standardverhalten überschrieben, wonach der SQL-Varianttyp vom C-Typ abgeleitet wird.  
  
|C-Typ|Servertyp|Kommentare|  
|------------|-----------------|--------------|  
|SQL_C_CHAR|varchar|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_WCHAR|nvarcar|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_TINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_STINYINT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SSHORT|smallint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_USHORT|int|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_LONG|int|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SLONG|int|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_ULONG|bigint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SBIGINT|bigint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_FLOAT|real|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_DOUBLE|float|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_BIT|bit|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_UTINYINT|tinyint|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_BINARY|varbinary|SQL_CA_SS_VARIANT_SQL_TYPE wird nicht festgelegt.|  
|SQL_C_BINARY|Uhrzeit|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIME2<br /><br /> Die Skala ist auf SQL_DESC_PRECISION (der *DecimalDigits* -Parameter von **SQLBindParameter**) festgelegt.|  
|SQL_C_BINARY|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE = SQL_SS_TIMESTAMPOFFSET<br /><br /> Die Skala ist auf SQL_DESC_PRECISION (der *DecimalDigits* -Parameter von **SQLBindParameter**) festgelegt.|  
|SQL_C_TYPE_DATE|Datum|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_TYPE_TIME|time(0)|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_TYPE_TIMESTAMP|datetime2|Die Skala ist auf SQL_DESC_PRECISION (der *DecimalDigits* -Parameter von **SQLBindParameter**) festgelegt.|  
|SQL_C_NUMERIC|DECIMAL|Die Genauigkeit wird auf SQL_DESC_PRECISION (der *ColumnSize* -Parameter von **SQLBindParameter**) festgelegt.<br /><br /> Skalierungs Gruppe auf SQL_DESC_SCALE (der *DecimalDigits* -Parameter von SQLBindParameter).|  
|SQL_C_SS_TIME2|Uhrzeit|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
|SQL_C_SS_TIMESTAMPOFFSET|datetimeoffset|SQL_CA_SS_VARIANT_SQL_TYPE wird ignoriert.|  
  
## <a name="see-also"></a>Siehe auch  
 [Verbesserungen &#40;bei Datum und Uhrzeit in ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
