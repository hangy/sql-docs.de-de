---
title: lower-case-Funktion (XQuery) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- lower-case Function (XQuery)
- lower-case
ms.assetid: 5222c4ff-890c-4d57-8506-c065a5ebfd3e
author: rothja
ms.author: jroth
ms.openlocfilehash: a80d869afe67317476a1d68c28afa5456a4a7366
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077659"
---
# <a name="functions-on-string-values---lower-case"></a>Funktionen für Zeichenfolgenwerte – lower-case
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Die lower-case-Funktion konvertiert jedes Zeichen in *$arg* auf entsprechende kleingeschriebene Variante. Die binäre Konvertierung der Groß-/Kleinschreibung für Unicode-Codepunkte von Microsoft Windows gibt an, wie Zeichen in Kleinbuchstaben konvertiert werden. Dieser Standard unterscheidet sich vom Unicode-Standard zum Zuordnen von Codepunkten.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
fn:lower-case($arg as xs:string?) as xs:string  
```  
  
## <a name="arguments"></a>Argumente  
  
|||  
|-|-|  
|Begriff|Definition|  
|*$arg*|Der Zeichenfolgenwert, der in Kleinbuchstaben konvertiert werden soll.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Wert des *$arg* ist leer, wird eine leere Zeichenfolge zurückgegeben.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-changing-a-string-to-upper-case"></a>A. Ändern einer Zeichenfolge in Großbuchstaben  
 Im folgenden Beispiel wird die Eingabezeichenfolge ' AbcDEF! @4"in Kleinbuchstaben.  
  
```  
DECLARE @x xml = N'abcDEF!@4';  
SELECT @x.value('fn:lower-case(/text()[1])', 'nvarchar(10)');  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `abcdef!@4`  
  
### <a name="b-search-for-a-specific-character-string"></a>B. Suchen Sie nach einer bestimmten Zeichenfolge  
 In diesem Beispiel wird gezeigt, wie die lower-case-Funktion in einer Suche verwendet werden kann, bei der nicht zwischen Groß- und Kleinschreibung unterschieden werden soll.  
  
```  
USE AdventureWorks  
GO  
--WITH XMLNAMESPACES clause specifies the namespace prefix  
--to use.   
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
--The XQuery contains() function is used to determine whether  
--any of the text nodes below the <Summary> element contain  
--the word 'frame'. The lower-case() function makes the   
--case insensitive.  
  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
/pd:ProductDescription/pd:Summary//text()[  
          contains(lower-case(.), "FRAME")]')  = 1  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `19     <Prod ProductModelID="19">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike.`  
  
 `Performance-enhancing options include the innovative HL Frame,`  
  
 `super-smooth front suspension, and traction for all terrain.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
 `25     <Prod ProductModelID="25">`  
  
 `<pd:Summary xmlns:pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">This bike is ridden by race winners. Developed with the`  
  
 `Adventure Works Cycles professional race team, it has a extremely light`  
  
 `heat-treated aluminum frame, and steering that allows precision control.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery Functions against the xml Data Type (XQuery-Funktionen für den xml-Datentyp)](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
