---
title: FirstChild (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c1bd2f37304131b881d49aaa874eaed13530fc0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032071"
---
# <a name="firstchild-mdx"></a>FirstChild (MDX)


  Gibt das erste untergeordnete Element eines angegebenen Elements zurück.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Member_Expression.FirstChild   
```  
  
## <a name="arguments"></a>Argumente  
 *Member_Expression*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
### <a name="example"></a>Beispiel  
 Die folgende Abfrage gibt das erste untergeordnete Element von Fiscal Year 2003 in der Fiscal-Hierarchie zurück, d. h. das erste Semester von Fiscal Year 2003.  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)   
 [MDX-Funktionsreferenz &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
