---
title: Massenkopieränderungen für verbesserte Datums- und Uhrzeittypen (OLE DB und ODBC) | Microsoft-Dokumentation
description: Massenkopieränderungen für verbesserte Datums- und Uhrzeittypen (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, bulk copy operations
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 417bf44993ffc850da03d090e36c29cae472c104
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68015833"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db"></a>Massenkopieränderungen für verbesserte Datums- und Uhrzeittypen (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  In diesem Artikel werden die Datums-/Uhrzeitverbesserungen zur Unterstützung von Massen Kopierfunktionen in OLE DB Treiber für SQL Server beschrieben.  
  
## <a name="format-files"></a>Formatdateien  
 Beim interaktiven Erstellen von Formatdateien beschreibt die folgende Tabelle die Eingaben, die zum Angeben von Datum-/Uhrzeittypen verwendet werden, sowie die entsprechenden Datentypnamen der Hostdatei.  
  
|Dateispeichertyp|Datentyp in der Hostdatei|Antwort auf die Eingabeaufforderung: „Geben Sie den Dateispeichertyp des Felds <Feldname> ein [\<Standardwert>]:“|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|DATETIME|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|date|SQLDATE|de|  
|Uhrzeit|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 Das XML-Formatdatei-XSD hat die folgenden Hinzufügungen:  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>Zeichendatendateien  
 In Zeichen Datendateien werden Datums-und Uhrzeitwerte entsprechend der Beschreibung im Abschnitt "Datenformate: Zeichen folgen und Literale" der [Datentyp Unterstützung für OLE DB Datums-und Uhrzeit Verbesserungen](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md) für OLE DB dargestellt.  
  
 In nativen Datendateien werden Datums- und Uhrzeitwerte für die vier neuen Typen als TDS-Entsprechungen mit sieben Dezimalstellen dargestellt, da es sich dabei um das von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] unterstützte Maximum handelt und bcp-Datendateien die Dezimalstellen dieser Spalten nicht speichern. Es erfolgt keine Änderung an der Speicherung der vorhandenen **datetime**- und **smalldatetime**-Typen oder ihrer Tabular Data Stream-Entsprechungen (TDS).  
  
 Die Speichergrößen für die anderen Speichertypen sind für OLE DB wie folgt:  
  
|Dateispeichertyp|Speichergröße (in Byte)|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|date|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
 
  
## <a name="bcp-types-in-msoledbsqlh"></a>BCP-Typen in msoledbsql. h  
 Die folgenden Typen sind in msoledbsql. h definiert. Diese Typen werden mit dem *eUserDataType* -Parameter von IBCPSession:: bcpcolf MT in OLE DB übergeben.  
  
|Dateispeichertyp|Datentyp in der Hostdatei|Geben Sie msoledbsql. h für die Verwendung mit IBCPSession:: bcpcolbmt ein.|value|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DATETIME|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIM4|0x3a|  
|date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Uhrzeit|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP-Datentypkonvertierungen  
 Die folgenden Tabellen enthalten Konvertierungsinformationen.  
  
 **OLE DB-Hinweis** Die folgenden Konvertierungen werden von IBCPSession ausgeführt. IRowsetFastLoad verwendet OLE DB Konvertierungen gemäß der Definition in [Konvertierungen, die vom Client zum Server ausgeführt werden](../../oledb/ole-db-date-time/conversions-performed-from-client-to-server.md). Beachten Sie, dass datetime-Werte auf 1/300stel einer Sekunde gerundet werden und dass für smalldatetime-Werte die Sekunden vom Server auf null festgelegt werden, nachdem die unten beschriebenen Clientkonvertierungen durchgeführt wurden. Datetime-Rundung wird durch Stunden und Minuten, aber nicht durch das Datum weitergegeben.  
  
|Bis --><br /><br /> Von|date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|date|1|-|1, 6|1, 6|1, 6|1, 5, 6|1, 3|1, 3|  
|Uhrzeit|–|1, 10|1, 7, 10|1, 7, 10|1, 7, 10|1, 5, 7, 10|1, 3|1, 3|  
|Smalldatetime|1, 2|1, 4, 10|1|1|1, 10|1, 5, 10|1, 11|1, 11|  
|DATETIME|1, 2|1, 4, 10|1, 12|1|1, 10|1, 5, 10|1, 11|1, 11|  
|Datetime2|1, 2|1, 4, 10|1, 12|1, 10|1, 10|1, 5, 10|1, 3|1, 3|  
|Datetimeoffset|1, 2, 8|1, 4, 8, 10|1, 8, 10|1, 8, 10|1, 8, 10|1, 10|1, 3|1, 3|  
|Char/wchar (date)|9|-|9, 6, 12|9, 6, 12|9, 6|9, 5, 6|–|–|  
|Char/wchar (time)|-|9, 10|9, 7, 10, 12|9, 7, 10, 12|9, 7, 10|9, 5, 7, 10|–|–|  
|Char/wchar (datetime)|9, 2|9, 4, 10|9, 10, 12|9, 10, 12|9, 10|9, 5, 10|–|–|  
|Char/wchar (datetimeoffset)|9, 2, 8|9, 4, 8, 10|9, 8, 10, 12|9, 8, 10, 12|9, 8, 10|9, 10|–|–|  
  
#### <a name="key-to-symbols"></a>Aufschlüsselung der Symbole  
  
|Symbol|Bedeutung|  
|------------|-------------|  
|-|Es wird keine Konvertierung unterstützt.<br />|  
|1|Wenn die bereitgestellten Daten ungültig sind, wird ein Fehler ausgegeben. Für datetimeoffset-Werte muss der Uhrzeitteil nach der Konvertierung in das UTC-Format innerhalb des gültigen Bereichs liegen, und zwar selbst dann, wenn keine Konvertierung in UTC angefordert wird. Das liegt daran, dass TDS und der Server immer die Uhrzeit in datetimeoffset-Werten für UTC normalisieren. Darum muss der Client überprüfen, dass sich die Zeitkomponenten innerhalb des nach Konvertierung zu UTC unterstützten Bereichs befinden.|  
|2|Die Uhrzeitkomponente wird ignoriert.|  
|3|Wenn eine Kürzung mit Datenverlust auftritt, wird ein Fehler generiert. Für „datetime2“ wird die Anzahl der Dezimalstellen für Sekundenbruchteile anhand der Größe der Zielspalte gemäß der folgenden Tabelle bestimmt: Für Spaltengrößen, die den Bereich in der Tabelle übersteigen, werden 9 Dezimalstellen impliziert. Diese Konvertierung sollte bis zu neun Dezimalstellen für Sekundenbruchteile ermöglichen, das von OLE&nbsp;DB zugelassene Maximum.<br /><br /> **Typ:** DBTIME2<br /><br /> **Implizierte Dezimalstellen 0** 8<br /><br /> **Implizierte Dezimalstellen 1..9**1..9<br /><br /> <br /><br /> **Typ:** DBTIMESTAMP<br /><br /> **Implizierte Dezimalstellen 0:** 19<br /><br /> **Implizierte Dezimalstellen 1..9:** 21..29<br /><br /> <br /><br /> **Typ:** DBTIMESTAMPOFFSET<br /><br /> **Implizierte Dezimalstellen 0:** 26<br /><br /> **Implizierte Dezimalstellen 1..9:** 28..36|  
|4|Die Datumskomponente wird ignoriert.|  
|5|Die Zeitzone wird auf UTC festgelegt (zum Beispiel 00:00).|  
|6|Die Uhrzeit wird auf 0 (Null) festgelegt.|  
|7|Das Datum wird auf den 01.01.1900 festgelegt.|  
|8|Der Zeitzonenoffset wird ignoriert.|  
|9|Die Zeichenfolge wird analysiert und je nach dem ersten Satzzeichen und dem Vorhandensein weiterer Komponenten in einen date-, datetime-, datetimeoffset- oder time-Wert konvertiert. Die Zeichenfolge wird dann in den Zieltyp konvertiert. Dabei wird nach den Regeln am Ende dieses Artikels für den Quelltyp vorgegangen, der von diesem Prozess ermittelt wird. Wenn die bereitgestellten Daten nicht fehlerfrei analysiert werden können, oder wenn ein Teil der Komponente außerhalb des zulässigen Bereichs liegt, oder wenn keine Konvertierung vom Literaltyp in den Zieltyp erfolgt, wird ein Fehler ausgegeben. Bei den Parametern "DateTime" und "smalldatetime" wird ein Fehler ausgegeben, wenn das Jahr außerhalb des Bereichs liegt, den diese Typen unterstützen.<br /><br /> Der Wert für datetimeoffset muss nach der Konvertierung in das UTC-Format innerhalb des gültigen Bereichs liegen und zwar selbst dann, wenn keine Konvertierung in UTC angefordert wird. Der Grund dafür ist, dass der TDS und der Server das Datum stets in datetimeoffset-Werte für UTC normalisieren, weshalb der Client prüfen muss, ob die Zeitkomponenten innerhalb des nach Konvertierung in UTC unterstützten Bereichs liegen. Wenn der Wert nicht innerhalb des unterstützten UTC-Bereichs liegt, wird ein Fehler ausgegeben.|  
|10|Bei Client-zu-Server-Konvertierungen wird ein Fehler ausgegeben, wenn eine Kürzung mit Datenverlust auftritt. Dieser Fehler tritt auch dann auf, wenn der Wert außerhalb des Bereichs liegt, der vom UTC-Bereich, den der Server verwendet, dargestellt werden kann. Wenn während einer Konvertierung vom Server zum Client eine Kürzung der Sekunden oder Sekundenbruchteile auftritt, wird lediglich eine Warnung angezeigt.|  
|11|Bei Client-zu-Server-Konvertierungen wird ein Fehler ausgegeben, wenn eine Kürzung mit Datenverlust auftritt.|
|12|Die Sekunden werden auf null festgelegt, und die Sekundenbruchteile werden verworfen. Kein Kürzungsfehler ist möglich.|  
|–|Das Verhalten von [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] und früheren Versionen ist beibehalten worden.|  
  
## <a name="see-also"></a>Weitere Informationen     
 [Date and Time Improvements &#40;OLE DB&#41; (Verbesserungen bei Datum und Uhrzeit &#40;OLE DB&#41;)](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
