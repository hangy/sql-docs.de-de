---
title: Ungültige Zeichen und Escaperegeln | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, invalid characters
- FOR XML clause, escape rules
ms.assetid: f2e9b997-f400-4963-b225-59d46c6b93e8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aafacefa7a5bab5f8bc828f48384a79e17a13b11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241199"
---
# <a name="invalid-characters-and-escape-rules"></a>Ungültige Zeichen und Escaperegeln
  In diesem Thema wird beschrieben, wie ungültige XML-Zeichen von der FOR XML-Klausel behandelt werden, und die Escaperegeln für Zeichen aufgelistet, die in XML-Namen ungültig sind.  
  
## <a name="for-xml-and-invalid-characters"></a>FOR XML und ungültige Zeichen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ändert ungültige XML-Zeichen in Entitäten, wenn sie innerhalb von FOR XML-Abfragen zurückgegeben werden, die nicht die TYPE-Direktive verwenden.  
  
 Zwar lösen XML 1.0-konforme Parser Analysefehler unabhängig davon aus, ob diese Zeichen in Entitäten geändert wurden, die Entitätsform ist jedoch kompatibler mit XML 1.1. Die Entitätsform ist außerdem möglicherweise kompatibler mit zukünftigen Versionen des XML-Standards. Darüber hinaus vereinfacht sie das Debuggen, weil das Codeelement des ungültigen Zeichens sichtbar wird.  
  
 Für Benutzer von XML-Tools ist keine Problemumgehung erforderlich, weil der XML-Parser unter allen Umständen an dem Punkt fehlschlägt, an dem das ungültige Zeichen im Datenstrom auftritt. Wenn Sie Nicht-XML-Tools verwenden, kann diese Änderung das Aktualisieren der Programmierlogik erforderlich machen, damit diese nach diesen Zeichen als in Entitäten geänderte Werte sucht.  
  
 Die folgenden Leerzeichen werden in FOR XML-Abfragen auf andere Weise in Entitäten geändert, damit sie bei Roundtrips beibehalten werden:  
  
-   In Elementinhalten und -attributen: **hex(0D)** (Wagenrücklauf)  
  
-   In Attributinhalten: **hex(09)** (Tabulator), **hex(0A)** (Zeilenvorschub)  
  
 Diese Zeichen werden in der Ausgabe beibehalten und nicht von Parsern normalisiert.  
  
## <a name="escape-rules"></a>Escaperegeln  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Namen, die Zeichen enthalten, die in XML-Namen ungültig sind (wie etwa Leerzeichen), werden so in XML-Namen übersetzt, dass die ungültigen Zeichen in geschützte numerische Entitätscodierung übersetzt werden.  
  
 Nur zwei nicht alphabetische Zeichen können in einem XML-Namen auftreten: der Doppelpunkt (:) und der Unterstrich (_). Da der Doppelpunkt bereits für Namespaces vorbehalten ist, wurde der Unterstrich als Escapezeichen gewählt. Die folgenden Escaperegeln werden für die Codierung verwendet:  
  
-   Alle UCS-2-Zeichen, die keine gültigen Zeichen für XML-Namen gemäß der XML 1.0-Spezifikation sind, werden in _xHHHH\_umgewandelt. HHHH steht für den vierstelligen hexadezimalen UCS-2-Code für das Zeichen in einer nach Signifikanz geordneten Bitfolge. So wird z.B. der Tabellenname **Order Details** als Order_x0020_Details codiert.  
  
-   Zeichen außerhalb des UCS-2-Bereichs (die UCS-4-Erweiterungen des Bereichs U+00010000 bis U+0010FFFF) werden als _xHHHHHHHH\_codiert. Dabei steht HHHHHHHH für die achtstellige hexadezimale UCS-4-Codierung des Zeichens, wenn der Abwärtskompatibilitätsmodus von SQL Server 2000 verwendet wird. Anderenfalls werden die Zeichen als _xHHHHHH\_codiert, um dem ISO-Standard zu entsprechen.  
  
-   Der Unterstrich muss nur mit Escapezeichen versehen werden, wenn darauf das Zeichen x folgt. Der Tabellenname **Order_Details** wird z.B. nicht codiert.  
  
-   Der Doppelpunkt in Bezeichnern wird nicht in eine Escapezeichenfolge umgewandelt. Als Ergebnis können Element- und Attributnamen für Namespaces von der FOR XML-Abfrage generiert werden. So generiert z. B. die folgende Abfrage ein Namespaceattribut mit einem Doppelpunkt im Namen:  
  
    ```  
    SELECT 'namespace-urn' as 'xmlns:namespace',   
     1 as 'namespace:a'   
    FOR XML RAW  
    ```  
  
     Die Abfrage liefert folgendes Ergebnis:  
  
    ```  
    <row xmlns:namespace="namespace-urn" namespace:a="1"/>  
    ```  
  
     Beachten Sie, dass WITH XMLNAMESPACES das empfohlene Verfahren zum Hinzufügen von XML-Namespaces ist.  
  
## <a name="see-also"></a>Siehe auch  
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
