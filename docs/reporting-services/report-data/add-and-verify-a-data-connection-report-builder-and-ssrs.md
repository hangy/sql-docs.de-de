---
title: Hinzufügen und Prüfen einer Datenverbindung (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 03/01/2017
ms.openlocfilehash: 9b8eca48287388eba7f8e1f13ba4c6e5692a278d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251063"
---
# <a name="add-and-verify-a-data-connection-report-builder-and-ssrs"></a>Hinzufügen und Prüfen einer Datenverbindung (Berichts-Generator und SSRS)

Im Berichts-Generator können Sie eine freigegebene Datenquelle des Berichtsservers hinzufügen oder eine eingebettete Datenquelle für Ihren Bericht erstellen. Im Berichts-Designer können Sie eine freigegebene Datenquelle oder eine eingebettete Datenquelle erstellen und sie auf einem Berichtsserver bereitstellen.

Navigieren Sie zu einem Berichtsserver, und wählen Sie eine freigegebene Datenquelle aus, um diese in den Bericht aufzunehmen. Die freigegebene Datenquelle im Bericht verweist auf die freigegebene Datenquellendefinition auf dem Berichtsserver.

Zum Erstellen einer eingebetteten Datenquelle benötigen Sie Informationen über die Verbindung mit der externen Datenquelle, und Sie müssen wissen, welche Berechtigungen für den Zugriff auf die Daten erforderlich sind. Diese Informationen erhalten Sie normalerweise vom Besitzer der Datenquelle. Sie können die Verbindung testen, um zu überprüfen, ob die angegebenen Anmeldeinformationen ausreichend sind.

Weitere Informationen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen im Berichts-Generator](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) und [Angeben von Anmeldeinformationen im Berichts-Generator](https://docs.microsoft.com/sql/reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources?view=sql-server-2017).

> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="to-create-a-connection-to-a-shared-data-source-in-report-builder"></a>So erstellen Sie eine Verbindung zu einer freigegebenen Datenquellen im Berichts-Generator

1. Klicken Sie im Berichtsdatenbereich auf der Symbolleiste auf **Neu** und anschließend auf **Datenquelle**. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.

2. Geben Sie in das Textfeld **Name** einen Namen für die Datenquelle ein.

    > [!NOTE]  
    >  Dieser Name wird in der lokalen Berichtsdefinition gespeichert. Der Name entspricht nicht dem Namen der freigegebenen Datenquelle auf dem Berichtsserver. 

3. Wählen Sie **Freigegebene Verbindung oder Berichtsmodell verwenden**aus. Die Liste der zuletzt verwendeten freigegebenen Datenquellen und Berichtsmodelle wird angezeigt. Klicken Sie zum Auswählen einer Datenquelle auf **Durchsuchen** , und suchen Sie den Ordner auf dem Berichtsserver mit den freigegebenen Datenquellen.

4. Wählen Sie die freigegebene Datenquelle aus, und klicken Sie dann auf **Öffnen**.

5. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

Die Datenquelle wird im Berichtsdatenbereich angezeigt.

### <a name="to-verify-a-data-connection"></a>So überprüfen Sie eine Datenverbindung  

1. Doppelklicken Sie auf der Symbolleiste im Berichtsdatenbereich auf die Datenquelle. Das Dialogfeld **Datenquelleneigenschaften** wird angezeigt.

2. Klicken Sie auf **Verbindung testen**.

3. Bei einer erfolgreichen Verbindung wird die folgende Meldung angezeigt: "Die Verbindung wurde erfolgreich erstellt". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

4. Wenn die Verbindung nicht erfolgreich hergestellt werden kann, wird die folgende Meldung angezeigt: "Es konnte keine Verbindung mit der Datenquelle hergestellt werden".  

5. Klicken Sie auf **Details**, und beheben Sie das Problem mithilfe der angezeigten Informationen.

    Weitere Informationen finden Sie unter [Angeben von Anmeldeinformationen im Berichts-Generator](https://docs.microsoft.com/sql/reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources?view=sql-server-2017).

6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>Siehe auch

- [Berichtsdatasets &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
- [Erstellen von Berichten zu eingebetteten und freigegebenen Datasets &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)
- [Suchen, Anzeigen und Verwalten von Berichten (Berichts-Generator und SSRS )](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
- [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)