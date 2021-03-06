---
title: Auslösen und Definieren von Ereignissen in einer Datenflusskomponente | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], events
- events [Integration Services], custom
- custom events [Integration Services]
- custom data flow components [Integration Services], events
- events [Integration Services], raising
- predefined events [Integration Services]
ms.assetid: 1d8c5358-9384-47a8-b7cb-7b0650384119
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f3d0feff8d95a8fb0d1e7b6279e36567e06c7f81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896312"
---
# <a name="raising-and-defining-events-in-a-data-flow-component"></a>Auslösen und Definieren von Ereignissen in einer Datenflusskomponente
  Komponentenentwickler können eine Teilmenge der Ereignisse, die in der <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents>-Schnittstelle definiert sind, auslösen, indem sie die in der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>-Eigenschaft verfügbaren Methoden aufrufen. Außerdem können Sie benutzerdefinierte Ereignisse mit der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A>-Auflistung definieren und sie während der Ausführung mit der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>-Methode auslösen. In diesem Abschnitt wird beschrieben, wie Sie ein Ereignis erstellen und auslösen können und es werden Richtlinien bereitgestellt, wann Ereignisse zur Entwurfszeit ausgelöst werden sollen.  
  
## <a name="raising-events"></a>Auslösen von Ereignissen  
 Komponenten lösen Ereignisse mit den **Fire\<X>** -Methoden der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>-Schnittstelle aus. Sie können während des Entwurfs und der Ausführung von Komponenten Ereignisse auslösen. In der Regel werden während der Überprüfung beim Entwurf der Komponenten die <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A>- und <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A>-Methoden aufgerufen. Diese Ereignisse zeigen Meldungen im Bereich **Fehlerliste** von [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] an und stellen für die Benutzer der Komponente Feedback bereit, wenn eine Komponente nicht richtig konfiguriert ist.  
  
 Komponenten können auch zu einem beliebigen Zeitpunkt während der Ausführung Ereignisse auslösen. Ereignisse ermöglichen es Komponentenentwicklern, während der Ausführung einer Komponente Feedback für deren Benutzer bereitzustellen. Bei Aufruf der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A>-Methode während der Ausführung ist ein Versagen des Pakets wahrscheinlich.  
  
## <a name="defining-and-raising-custom-events"></a>Definieren und Auslösen von benutzerdefinierten Ereignissen  
  
### <a name="defining-a-custom-event"></a>Definieren eines benutzerdefinierten Ereignisses  
 Benutzerdefinierte Ereignisse werden erstellt, indem die <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A>-Methode der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A>-Auflistung aufgerufen wird. Diese Auflistung wird durch den Datenflusstask festgelegt und dem Komponentenentwickler über die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>-Basisklasse als Eigenschaft bereitgestellt. Diese Klasse enthält durch den Datenflusstask definierte sowie durch die Komponente während der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A>-Methode definierte benutzerdefinierte Ereignisse.  
  
 Die benutzerdefinierten Ereignisse einer Komponente werden nicht permanent im Paket-XML beibehalten. Daher wird sowohl während der Entwicklung als auch während der Ausführung die <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A>-Methode aufgerufen, um der Komponente die Definition der von ihr ausgelösten Ereignisse zu ermöglichen.  
  
 Der *allowEventHandlers*-Parameter der <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A>-Methode gibt an, ob die Komponente die Erstellung von <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>-Objekten für das Ereignis zulässt. Beachten Sie, dass <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> synchron sind. Daher setzt die Komponente die Ausführung erst dann fort, wenn ein an das benutzerdefinierte Ereignis angefügter <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> die Ausführung abgeschlossen hat. Wenn die *AllowEventHandlers* Parameter `true`, jeden Parameter des Ereignisses automatisch eine zur Verfügung gestellt wird <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> -Objekten über Variablen, die erstellt und automatisch ausgefüllt, durch die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] Common Language Runtime.  
  
### <a name="raising-a-custom-event"></a>Auslösen eines benutzerdefinierten Ereignisses  
 Komponenten lösen benutzerdefinierter Ereignisse durch Aufrufen der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>-Methode aus, und stellen den Namen, den Text und die Parameter des Ereignisses bereit. Wenn die *AllowEventHandlers* Parameter `true`, <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> , die erstellt werden, für das benutzerdefinierte Ereignis werden ausgeführt, indem die [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Runtime-Engine.  
  
### <a name="custom-event-sample"></a>Beispiel für ein benutzerdefiniertes Ereignis  
 Im folgenden Codebeispiel wird eine Komponente gezeigt, die während der <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A>-Methode ein benutzerdefiniertes Ereignis definiert und dann durch Aufrufen der <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>-Methode das Ereignis zur Laufzeit auslöst.  
  
```csharp  
public override void RegisterEvents()  
{  
    string [] parameterNames = new string[2]{"RowCount", "StartTime"};  
    ushort [] parameterTypes = new ushort[2]{ DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)};  
    string [] parameterDescriptions = new string[2]{"The number of rows to sort.", "The start time of the Sort operation."};  
    EventInfos.Add("StartingSort","Fires when the component begins sorting the rows.",false,ref parameterNames, ref parameterTypes, ref parameterDescriptions);  
}  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
    while (buffer.NextRow())  
    {  
       // Process buffer rows.  
    }  
  
    IDTSEventInfo100 eventInfo = EventInfos["StartingSort"];  
    object []arguments = new object[2]{buffer.RowCount, DateTime.Now };  
    ComponentMetaData.FireCustomEvent("StartingSort", "Beginning sort operation.", ref arguments, ComponentMetaData.Name, ref FireSortEventAgain);  
}  
```  
  
```vb  
Public  Overrides Sub RegisterEvents()   
  Dim parameterNames As String() = New String(2) {"RowCount", "StartTime"}   
  Dim parameterTypes As System.UInt16() = New System.UInt16(2) {DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)}   
  Dim parameterDescriptions As String() = New String(2) {"The number of rows to sort.", "The start time of the Sort operation."}   
  EventInfos.Add("StartingSort", "Fires when the component begins sorting the rows.", False, parameterNames, parameterTypes, parameterDescriptions)   
End Sub   
  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
  While buffer.NextRow   
  End While   
  Dim eventInfo As IDTSEventInfo100 = EventInfos("StartingSort")   
  Dim arguments As Object() = New Object(2) {buffer.RowCount, DateTime.Now}   
  ComponentMetaData.FireCustomEvent("StartingSort", _  
    "Beginning sort operation.", arguments, _  
    ComponentMetaData.Name, FireSortEventAgain)   
End Sub  
```  
  
![Integration Services (kleines Symbol)](../../media/dts-16.gif "Integration Services (kleines Symbol)")**bleiben oben, um das Datum mit Integration Services**<br /> Die neuesten Downloads, Artikel, Beispiele und Videos von Microsoft sowie ausgewählte Lösungen aus der Community finden Sie auf MSDN auf der [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] -Seite:<br /><br /> [Besuchen Sie die Integration Services-Seite auf MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Abonnieren Sie die auf der Seite verfügbaren RSS-Feeds, um automatische Benachrichtigungen zu diesen Updates zu erhalten.  
  
## <a name="see-also"></a>Siehe auch  
 [Integration Services-Ereignishandler &#40;SSIS&#41;](../../integration-services-ssis-event-handlers.md)   
 [Hinzufügen eines Ereignishandlers zu einem Paket](../../add-an-event-handler-to-a-package.md)  
  
  
