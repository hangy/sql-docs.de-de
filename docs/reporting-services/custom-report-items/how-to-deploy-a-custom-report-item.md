---
title: 'Vorgehensweise: Bereitstellen eines benutzerdefinierten Berichtselements | Microsoft-Dokumentation'
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, deploying
ms.assetid: 80e97b0d-e355-4240-aebd-08cbc84089ed
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b28d1b2f29dca3ab23ba658c8718173fe5d09779
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194140"
---
# <a name="how-to-deploy-a-custom-report-item"></a>Vorgehensweise: Bereitstellen eines benutzerdefinierten Berichtselements
  Zum Bereitstellen eines benutzerdefinierten Berichtselements in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] müssen Sie die Konfigurationsdateien des Berichtsservers ändern und die Entwurfszeit- und die Laufzeitkomponentenassemblys in die entsprechenden Anwendungsordner für den Berichts-Designer und den Berichtsserver kopieren.  
  
### <a name="to-deploy-a-custom-report-item"></a>So stellen Sie ein benutzerdefiniertes Berichtselement bereit  
  
1.  Bearbeiten Sie die Datei Rsreportdesigner.config, um die Laufzeit- und Entwurfszeitkomponenten für ein benutzerdefiniertes Berichtselement für die Verwendung im Designer zu konfigurieren. Beachten Sie, dass der **ReportItemName**-Eintrag mit dem **CustomReportItemAttribute**-Attribut, das in Ihrer **CustomReportItemDesigner**-Klasse verwendet wird, übereinstimmen muss. Beispiel:  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    <ReportItemDesigner>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsDesigner, PolygonsDesigner" />  
    </ReportItemDesigner>  
    <ReportItemConverter>  
       <Converter Source="Chart" Target="Polygons" Type="PolygonsCRI.PolygonsConverter, PolygonsDesigner" />  
    </ReportItemConverter>  
    ```  
  
2.  Bearbeiten Sie die Datei Rsreportserver.config, um die Laufzeitkomponente für ein benutzerdefiniertes Berichtselement zu registrieren. Beispiel:  
  
    ```  
    <ReportItems>  
       <ReportItem Name="Polygons" Type="PolygonsCRI.PolygonsCRI,PolygonsCRI"/>  
    </ReportItems>  
    ```  
  
3.  Bearbeiten Sie die Datei „Rsssrvpolicy.config“, um eine **CodeGroup** hinzuzufügen, die dem benutzerdefinierten Berichtselement die richtigen Berechtigungen gewährt. Beispiel:  
  
    ```  
    <CodeGroup   
       class="UnionCodeGroup"   
       version="1"   
       PermissionSetName="FullTrust"  
       Description="This code group grants MyCustomReportItem.dll FullTrust permission. ">  
       <IMembershipCondition   
          class="UrlMembershipCondition"  
          version="1"  
       Url="C:\Program Files\Microsoft SQL Server\ MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin\MyCustomReportItem.dll" />  
    </CodeGroup>  
    ```  
  
4.  Kopieren Sie die Laufzeitkomponenten-DLL für ein benutzerdefiniertes Berichtselement in die Verzeichnisse %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies und \Programme\Microsoft SQL Server\MSRS10_50.SQLSERVER\Reporting Services\ReportServer\bin.  
  
5.  Kopieren Sie die Entwurfszeitkomponenten-DLL für ein benutzerdefiniertes Berichtselement in das Verzeichnis %ProgramFiles%\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Reporting Services-Konfigurationsdateien](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Custom Report Item Class Libraries (Klassenbibliotheken für ein benutzerdefiniertes Berichtselement)](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
