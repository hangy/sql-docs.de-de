---
title: Editor für den Analysis Services Verarbeitungs Task (Seite Analysis Services) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.asprocessingtask.as.f1
helpviewer_keywords:
- Analysis Services Processing Task Editor
ms.assetid: 5612be78-57cf-4e4e-92cf-6bfa9f971040
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 59220dd32388eed75ed725e7a8b5956394ae575d
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68890371"
---
# <a name="analysis-services-processing-task-editor-analysis-services-page"></a>Editor für den Analysis Services-Verarbeitungstask (Seite Analysis Services)
  Auf der Seite **Analysis Services** des Dialogfelds **Editor für den Analysis Services-Verarbeitungstask** können Sie den Analysis Services-Verbindungs-Manager angeben, die zu verarbeitenden Analyseobjekte auswählen und die Verarbeitungs- und Fehlerbehandlungsoptionen festlegen.  
  
 Beim Verarbeiten von tabellarischen Modellen müssen Sie Folgendes berücksichtigen:  
  
1.  Sie können keine Auswirkungsanalyse auf tabellarische Modelle ausführen.  
  
2.  Einige Verarbeitungsoptionen für den tabellarischen Modus werden nicht verfügbar gemacht, z. B. "Defragmentierung verarbeiten" und "Neuberechnung verarbeiten". Sie können diese Funktionen mithilfe des Execute DDL-Tasks ausführen.  
  
3.  Einige bereitgestellte Verarbeitungsoptionen, beispielsweise Verarbeitungsindizes, eignen sich nicht für tabellarische Modelle und sollten daher nicht verwendet werden.  
  
4.  Batcheinstellungen werden für tabellarische Modelle ignoriert.  
  
 Informationen, um sich mit diesem Thema vertraut zu machen, finden Sie unter [Analysis Services Processing Task](control-flow/analysis-services-processing-task.md).  
  
## <a name="options"></a>Optionen  
 **Analysis Services-Verbindungs-Manager**  
 Wählen Sie einen vorhandenen Analysis Services-Verbindungs-Manager aus der Liste aus, oder klicken Sie auf **Neu** , um einen neuen Verbindungs-Manager zu erstellen.  
  
 **Neu**  
 Erstellen Sie einen neuen Analysis Services-Verbindungs-Manager.  
  
 **Verwandte Themen:** [Analysis Services-Verbindungs-Manager](connection-manager/analysis-services-connection-manager.md), [Referenz zur Benutzeroberfläche des Dialogfelds Analysis Services-Verbindungs-Manager hinzufügen](connection-manager/add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 **Objektliste**  
 |Eigenschaft|Beschreibung|  
|--------------|-----------------|  
|**Objektname**|Listet die angegebenen Objektnamen auf.|  
|**Typ**|Listet die Typen der angegebenen Objekte auf.|  
|**Verarbeitungsoptionen**|Wählen Sie eine Verarbeitungsoption in der Liste aus.<br /><br /> **Verwandte Themen:** [Objekt Verarbeitung für mehrdimensionale Modelle](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services)|  
|**Einstellungen**|Listet die Verarbeitungseinstellungen für die angegebenen Objekte auf.|  
  
 **Hinzufügen**  
 Fügen Sie der Liste ein [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] -Objekt hinzu.  
  
 **Entfernen**  
 Wählen Sie ein Objekt aus, und klicken Sie auf **Löschen**.  
  
 **Auswirkungsanalyse**  
 Führen Sie für das ausgewählte Objekt eine Auswirkungsanalyse aus.  
  
 **Verwandte Themen:** [Dialogfeld „Auswirkungsanalyse“ &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../2014/analysis-services/impact-analysis-dialog-box-analysis-services-multidimensional-data.md)  
  
 **Zusammenfassung der Batcheinstellungen**  
 |Eigenschaft|Beschreibung|  
|--------------|-----------------|  
|**Verarbeitungsreihenfolge**|Gibt an, ob die Objekte nacheinander oder als Batch verarbeitet werden; bei Verwendung der parallelen Verarbeitung wird die Anzahl der gleichzeitig verarbeiteten Objekte angegeben.|  
|**Transaktionsmodus**|Gibt den Transaktionsmodus für die sequenzielle Verarbeitung an.|  
|**Dimensionsfehler**|Gibt das Verhalten des Tasks bei Auftreten eines Fehlers an.|  
|**Fehlerprotokollpfad für Dimensionsschlüssel**|Gibt den Pfad der Datei an, in der Fehler protokolliert werden.|  
|**Betroffene Objekte verarbeiten**|Kennzeichnet, ob abhängige oder betroffene Objekte auch verarbeitet werden.|  
  
 **Einstellungen ändern**  
 Ändern Sie die Verarbeitungsoptionen und die Fehlerbehandlung bei Dimensionsschlüsseln.  
  
 **Verwandte Themen:** [Dialogfeld „Einstellungen ändern“ &#40;Analysis Services – Mehrdimensionale Daten&#41;](../../2014/analysis-services/change-settings-dialog-box-analysis-services-multidimensional-data.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Fehler- und Meldungsreferenz von Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor für den Analysis Services-Verarbeitungstask &#40;Seite „Allgemein“&#41;](general-page-of-integration-services-designers-options.md)   
 [DDL ausführen (Analysis Services-Task)](control-flow/analysis-services-execute-ddl-task.md)  
  
  
