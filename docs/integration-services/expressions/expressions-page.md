---
title: Seite Ausdrücke | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.expressionspage.f1
helpviewer_keywords:
- Expressions Page dialog box
ms.assetid: c9016ec6-11c1-4ebd-b2a7-0fa6631fd9e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9e3bbe6e788512144211ed35d1cfa8326d8f3ef7
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2019
ms.locfileid: "71290017"
---
# <a name="expressions-page"></a>Seite Ausdrücke

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Mithilfe der Seite **Ausdrücke** können Sie Eigenschaftsausdrücke bearbeiten und auf die Dialogfelder **Eigenschaftsausdrucks-Editor** und **Eigenschaftsausdrucks-Generator** zugreifen.  
  
 Eigenschaftsausdrücke aktualisieren die Werte von Eigenschaften, wenn das Paket ausgeführt wird. Eigenschaftsausdrücke können mit den Eigenschaften von Paketen, Tasks, Containern, Verbindungs-Managern sowie einigen Datenflusskomponenten verwendet werden. Die Ausdrücke werden ausgewertet und ihre Ergebnisse werden anstelle der Werte verwendet, auf die Sie die Eigenschaften festgelegt haben, als Sie das Paket und die Paketobjekte konfiguriert haben. Die Ausdrücke können Variablen und die Funktionen und Operatoren enthalten, die die Ausdruckssprache bereitstellt. Beispielsweise können Sie die Betreffzeile für den Task Mail senden generieren, indem Sie den Wert einer Variablen, die die Zeichenfolge "Weather forecast for " enthält, und die zurückgegebenen Ergebnisse der GETDATE()-Funktion zu der Zeichenfolge "Weather forecast for 4/5/2006" verketten.  
  
 Weitere Informationen zum Schreiben von Ausdrücken und zum Verwenden von Eigenschaftsausdrücken finden Sie unter [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md) und [Verwenden von Eigenschaftsausdrücken in Paketen](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## <a name="options"></a>enthalten  
 **Ausdrücke (...)**  
 Klicken Sie auf die Auslassungspunkte (...), um das Dialogfeld **Eigenschaftsausdrucks-Editor** zu öffnen. Weitere Informationen finden Sie unter [Property Expressions Editor](../../integration-services/expressions/property-expressions-editor.md).  
  
 **\<Eigenschaftsname>**  
 Klicken Sie auf die Schaltfläche mit den drei Punkten, um das Dialogfeld **Ausdrucks-Generator** zu öffnen. Weitere Informationen finden Sie unter [Expression Builder](../../integration-services/expressions/expression-builder.md).  
  
## <a name="see-also"></a>Weitere Informationen  
 [Integration Services-Variablen &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Systemvariablen](../../integration-services/system-variables.md)   
 [Integration Services-Ausdrücke &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md)  
  
  
