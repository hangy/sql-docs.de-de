---
title: Verwenden von Variablen und Parametern (MDX) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- parameters [MDX]
- queries [MDX], variables
- queries [MDX], parameters
- variables [MDX]
ms.assetid: a4754d16-d9c4-49f6-9be0-392180b912e4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eeb258266c489056994d8f78f80a6856602a174a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66073709"
---
# <a name="using-variables-and-parameters-mdx"></a>Verwenden von Variablen und Parametern (MDX)
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]können Sie eine MDX-Anweisung (Multidimensional Expressions) parametrisieren. Eine parametrisierte Anweisung ermöglicht Ihnen das Erstellen von allgemeinen Anweisungen, die während der Laufzeit angepasst werden können.  
  
 Beim Erstellen einer parametrisierten Anweisung kennzeichnen Sie den Parameternamen, indem Sie dem Namen das @-Zeichen voranstellen. Z. B. @Year wäre ein gültiger Parametername  
  
 MDX unterstützt Parameter nur für Literal- oder skalare Werte. Zum Erstellen eines Parameters, der auf ein Element, eine Menge oder ein Tupel verweist, müssen Sie eine Funktion verwenden (z. B. [StrToMember](/sql/mdx/strtomember-mdx) oder [StrToSet](/sql/mdx/strtoset-mdx)).  
  
 In der folgenden XML for Analysis (XMLA) beispielsweise die @CountryName Parameter enthält das Land, für welche Kunden Daten abgerufen werden:  
  
```  
<Envelope xmlns="http://schemas.xmlsoap.org/soap/envelope/">  
  <Body>  
    <Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <Command>  
        <Statement>  
select [Measures].members on 0,   
       Filter(Customer.[Customer Geography].Country.members,   
              Customer.[Customer Geography].CurrentMember.Name =  
              @CountryName) on 1  
from [Adventure Works]  
</Statement>  
      </Command>  
      <Properties />  
      <Parameters>  
        <Parameter>  
          <Name>CountryName</Name>  
          <Value>'United Kingdom'</Value>  
        </Parameter>  
      </Parameters>  
    </Execute>  
  </Body>  
</Envelope>  
```  
  
 Wenn Sie diese Funktionalität mit OLE DB verwenden möchten, verwenden Sie die `ICommandWithParameters`-Schnittstelle. Wenn Sie diese Funktionalität mit ADOMD.Net verwenden möchten, verwenden Sie die **AdomdCommand.Parameters** -Auflistung.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu MDX-Skripts &#40;Analysis Services&#41;](mdx-scripting-fundamentals-analysis-services.md)  
  
  
