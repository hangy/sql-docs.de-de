---
title: IsSibling (MDX) | Microsoft-Dokumentation
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 15c80cec67b0a40c8ac4c436a45a4551132858f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105350"
---
# <a name="issibling-mdx"></a>IsSibling (MDX)


  Gibt zurück, ob ein angegebenes Element ein gleichgeordnetes Element eines anderen angegebenen Elements ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
IsSibling(Member_Expression1, Member_Expression2)   
```  
  
## <a name="arguments"></a>Argumente  
 *Element_Ausdruck1*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
 *Element_Ausdruck2*  
 Ein gültiger MDX-Ausdruck (Multidimensional Expressions), der ein Element zurückgibt.  
  
## <a name="remarks"></a>Hinweise  
 Die **IsSibling** -Funktion zurückgegeben **"true"** , wenn die erste angegebene Element ein gleichgeordnetes Element eines zweiten angegebenen Elements. Die Funktion hingegen gibt **"false"** .  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird TRUE zurückgegeben, wenn das aktuelle Element auf der Fiscal-Hierarchie der Date-Dimension ein gleichgeordnetes Element aus dem Juli 2002 ist:  
  
 `WITH MEMBER MEASURES.ISSIBLINGDEMO AS`  
  
 `IsSibling([Date].[Fiscal].CURRENTMEMBER, [Date].[Fiscal].[Month].&[2002]&[7])`  
  
 `SELECT {MEASURES.ISSIBLINGDEMO} ON 0,`  
  
 `[Date].[Fiscal].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Siehe auch  
 [MDX-Funktionsreferenz &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
