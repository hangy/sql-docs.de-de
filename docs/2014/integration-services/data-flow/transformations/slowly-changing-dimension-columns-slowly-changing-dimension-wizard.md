---
title: Spalten von langsam veränderlichen Dimensionen (Assistent für langsam veränderliche Dimensionen) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c49f0ce7498215d5758557fba4c67740dca1239e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770664"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>Spalten von langsam veränderlichen Dimensionen (Assistent für langsam veränderliche Dimensionen)
  Im Dialogfeld **Spalten von langsam veränderlichen Dimensionen** können Sie für jede Spalte einer langsam veränderlichen Dimension einen Änderungstyp auswählen.  
  
 Weitere Informationen zu diesem Assistenten finden Sie unter [Slowly Changing Dimension Transformation](slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Optionen  
 **Dimensionsspalten**  
 Wählen Sie eine Dimensionsspalte aus der Liste aus.  
  
 **Änderungstyp**  
 Wählen Sie ein **Festes Attribut**oder einen der beiden Typen von veränderlichen Attributen aus. Verwenden Sie **Festes Attribut** , wenn sich der Wert in einer Spalte nicht ändern soll; [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] behandelt Änderungen dann als Fehler. Verwenden Sie **Veränderliches Attribut** , wenn vorhandene Werte von geänderten Werten überschrieben werden sollen. Verwenden Sie **Verlaufsattribut** , wenn geänderte Werte in neuen Datensätzen gespeichert werden sollen, während die vorigen Datensätze gleichzeitig als veraltet gekennzeichnet werden.  
  
 **Entfernen**  
 Wählen Sie eine Dimensionsspalte aus, und entfernen Sie sie aus der Liste der zugeordneten Spalten, indem Sie auf **Entfernen**klicken.  
  
## <a name="see-also"></a>Siehe auch  
 [Konfiguration von Ausgaben mithilfe des Assistenten für langsam veränderliche Dimensionen](configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
