---
title: Behandlung großer Objekte (LOB)-Parametern in der CLR | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 09797eac229a4b3b92f94a60b6e1c06c9ec12f08
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62919502"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Behandlung von LOB-Parametern (Large Object) in der CLR-Routine
  Verwenden Sie `SqlBytes` und `SqlChars`, um binäre LOB-Parameter (`varbinary(max)`) bzw. LOB-Zeichenparameter (`nvarchar(max)`) zu übergeben. Mithilfe dieser Parameter können die LOB-Werte von der Datenbank an die CLR-Routine (Common Language Runtime) in einem Strom übergeben werden, sodass nicht der gesamte Wert in einen verwalteten Bereich kopiert werden muss. `SqlBinary` und `SqlString` dürden nur für kleine Binär- und Zeichenfolgenwerte verwendet werden.  
  
## <a name="see-also"></a>Siehe auch  
 [SQL Server-Datentypen in .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
