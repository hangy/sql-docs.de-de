---
title: Vorschau | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 551494c4-9e27-4592-9200-c6bf19e80c9a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cddf7bd9714a42cefa55d9af1e9a5ce5a59aeac6
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292120"
---
# <a name="preview"></a>Vorschau 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Verwenden Sie das Dialogfeld **Vorschau** , um die von der SAP BW-Quelle extrahierten Daten in der Vorschau anzuzeigen.  
  
> [!IMPORTANT]  
>  Die Daten werden tatsächlich mithilfe der Option **Vorschau** extrahiert, die im **Quellen-Editor für SAP BW** auf der Seite **Verbindungs-Manager**verfügbar ist. Wenn Sie SAP NetWeaver BW so konfiguriert haben, dass nur Daten extrahiert werden, die sich seit der letzten Extrahierung geändert haben, schließen Sie die in der Vorschau angezeigten Daten durch Auswahl von **Vorschau** aus der nachfolgenden Extrahierung aus.  
  
 Weitere Informationen zur SAP BW-Quellkomponente von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW finden Sie unter [SAP BW-Quelle](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
> [!IMPORTANT]  
>  Das Extrahieren von Daten aus SAP NetWeaver BW erfordert zusätzliche SAP-Lizenzen. Stimmen Sie diese Anforderungen mit SAP ab.  
  
 **So öffnen Sie das Dialogfeld "Vorschau"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem die SAP BW-Quelle enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die SAP BW-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für SAP BW**auf **Verbindungs-Manager** , um die Seite **Verbindungs-Manager** des Editors zu öffnen.  
  
4.  Konfigurieren Sie die SAP BW-Quelle.  
  
5.  Nachdem Sie die SAP BW-Quelle konfiguriert haben, klicken Sie auf der Seite **Verbindungs-Manager** auf **Vorschau** , um die Daten im Dialogfeld **Vorschau** anzuzeigen.  
  
    > [!NOTE]  
    >  Durch Klicken auf die Schaltfläche **Vorschau** öffnen Sie auch das Dialogfeld **Anforderungsprotokoll** . Weitere Informationen zu diesem Dialogfeld finden Sie unter [Request Log](../../integration-services/data-flow/request-log.md).  
  
## <a name="options"></a>enthalten  
 Im Dialogfeld **Vorschau** werden die Zeilen angezeigt, die vom SAP NetWeaver BW-System angefordert werden. Die angezeigten Spalten entsprechen den in den Quelldaten definierten Spalten.  
  
 Das Dialogfeld verfügt über keinen weiteren Optionen.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Quellen-Editor für SAP BW &#40;Seite „Verbindungs-Manager“&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [F1-Hilfe zum Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
