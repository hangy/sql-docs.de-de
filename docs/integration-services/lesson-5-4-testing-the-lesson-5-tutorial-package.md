---
title: 'Schritt 4: Testen des Pakets aus Lektion 5 | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 342845789df01a7803196076ea20c03a80dac9f9
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2019
ms.locfileid: "71283080"
---
# <a name="lesson-5-4-test-the-lesson-5-package"></a>Lektion 5.4: Testen des Pakets aus Lektion 5

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Das Paket erhält den Wert für die **Directory**-Eigenschaft zur Laufzeit aus einer Variablen statt aus dem Verzeichnisnamen, den Sie beim Erstellen des Pakets angegeben haben. Der Wert der Variablen stammt aus der XML-Datei **SSISTutorial.dtsConfig**.  
  
Führen Sie das Paket aus, um zu überprüfen, ob die **Directory**-Eigenschaft vom Paket während der Laufzeit auf den neuen Wert aktualisiert wird. Da sich im neuen Verzeichnis nur drei Beispieldatendateien befinden, wird der Datenfluss nur dreimal ausgeführt.  
  
## <a name="checking-the-package-layout"></a>Überprüfen des Paketlayouts  
Bevor Sie das Paket testen, überprüfen Sie, ob Ablaufsteuerung und Datenfluss im Paket aus Lektion 5 die in den folgenden Diagrammen gezeigten Objekte enthalten.  
  
**Ablaufsteuerung**  
  
![Ablaufsteuerung im Paket](../integration-services/media/task4lesson2control.gif "Ablaufsteuerung im Paket")  
  
**Datenfluss**  
  
![Datenfluss im Paket](../integration-services/media/task9lesson1data.gif "Datenfluss im Paket")  
  
## <a name="test-the-lesson-5-package"></a>Testen des Pakets aus Lektion 5  
  
1.  Klicken Sie im Menü **Debuggen** auf **Start Debugging** (Debuggen starten).  
  
2.  Klicken Sie nach dem Ausführen des Pakets im Menü **Debuggen** auf **Stop Debugging** (Debuggen beenden).  
  
## <a name="next-lesson"></a>Nächste Lektion  
[Lektion 6: Verwenden von Parametern mit dem Projektbereitstellungsmodell in SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
