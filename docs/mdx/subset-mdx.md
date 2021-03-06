---
title: Teilmenge (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: b1f9a79c0e0ba6d578b82d7b1d072f3543888a1c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036702"
---
# <a name="subset-mdx"></a>Subset (MDX)


  Gibt eine Teilmenge von Tupeln aus einer angegebenen Menge zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Subset(Set_Expression, Start [ ,Count ] )  
```  
  
## <a name="arguments"></a>Argumente  
 *Set_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der eine Menge zurückgibt.  
  
 *Start*  
 Ein gültiger numerischer Ausdruck, der die Position des ersten zurückzugebenden Tupels angibt.  
  
 *Count*  
 Ein gültiger numerischer Ausdruck, der die Anzahl der Tupel angibt, die zurückgegeben werden sollen.  
  
## <a name="remarks"></a>Hinweise  
 Aus der angegebenen Menge der **Teilmenge** Funktionsergebnis ist eine Teilmenge, die die angegebene Anzahl von Tupeln, beginnend mit der angegebenen Startposition enthält. Die Startposition basiert auf einem nullbasierten Index, d. h., null (0) entspricht dem ersten Tupel in der Menge, 1 entspricht dem zweiten Tupel usw.  
  
 Wenn *Anzahl* nicht angegeben ist, wird die Funktion gibt alle Tupel von *starten* bis zum Ende des Satzes.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird das Reseller Sales-Measure für die fünf bestverkauften Produktunterkategorien unabhängig von der Hierarchie basierend auf Reseller Gross Profit zurückgegeben. Die **Teilmenge** Funktion wird verwendet, um nur die ersten fünf Mengen aus dem Ergebnis zurückzugeben, nach dem Sortieren des Ergebnisses mithilfe der **Reihenfolge** Funktion.  
  
```  
SELECT Subset  
   (Order   
      ([Product].[Product Categories].[SubCategory].members  
         ,[Measures].[Reseller Gross Profit]  
         ,BDESC  
      )  
   ,0  
   ,5  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
