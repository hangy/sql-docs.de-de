---
title: Grundlegendes zur DMX-SELECT-Anweisung | Microsoft-Dokumentation
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8cc28e9394cabee4dd32e8e84ee02517de415a75
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893073"
---
# <a name="understanding-the-dmx-select-statement"></a>Grundlegendes zur SELECT-Anweisung (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Die [Select](../dmx/select-dmx.md) -Anweisung ist die Grundlage für die meisten Abfragen, die Sie mit Data Mining-Erweiterungen (DMX) in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]erstellen. Mit dieser Anweisung können Sie viele unterschiedliche Aufgaben ausführen, so z. B. Durchsuchen von Data Mining-Modellen und Erstellen von Vorhersagen für Data Mining-Modelle.  
  
 Die folgenden Aufgaben können Sie mit der **Select** -Anweisung ausführen:  
  
-   Durchsuchen eines Data Mining-Modells. Das Schemarowset definiert die Struktur eines Modells.  
  
-   Ermitteln der möglichen Werte einer Miningmodellspalte.  
  
-   Durchsuchen der Fälle, die Knoten in einem Miningmodell zugewiesen sind, oder Abrufen eines repräsentativen Falls.  
  
-   Erstellen von Vorhersagen auf der Basis verschiedener Eingaben.  
  
-   Kopieren von Miningmodellen.  
  
 Jede dieser Aufgaben verwendet einen anderen Satz von Daten, die wir als *Daten Domäne*bezeichnen. Sie definieren die Daten Domäne in der **from** -Klausel der-Anweisung.  
  
-   Sie möchten Objekte im Data Mining-Modell selbst suchen, z. B. die Regel, durch die ein Dataset definiert wird, oder eine Formel für Vorhersagen.  
  
     In diesem Fall müssen Sie die Metadaten untersuchen, die im Modell selbst gespeichert sind. Deshalb besteht die Datendomäne aus den Spalten, die durch das Data Mining-Schemarowset definiert sind.  
  
-   Sie möchten detaillierte Informationen zu den Fällen abrufen, auf deren Grundlage das Modell erstellt wird.  
  
     In diesem Fall müssen Sie einen Drillthrough zur Miningstruktur, d. h. Ihrer Datendomäne, durchführen und die einzelnen Zeilen in den Spalten (Gender, Bike Buyer usw.) untersuchen.  
  
 **WICHTIG:** Alles, was in der Ausdrucks Liste oder in der **Where** -Klausel enthalten ist, muss aus der Daten Domäne stammen, die durch die **from** -Klausel definiert wird. Datendomänen können nicht gemischt werden.  
  
##  <a name="Select_Types"></a>Typen auswählen  
 Die Syntax der **Select** -Anweisung unterstützt viele verschiedene Tasks. Diese Aufgaben führen Sie mithilfe der folgenden Muster aus:  
  
-   [Sagt](#Predicting)  
  
-   [Browser](#Browsing)  
  
-   [Vorgänge](#Copying)  
  
-   [Drillthrough](#Drillthrough)  
  
###  <a name="Predicting"></a>Sagt  
 Mit folgenden Abfragetypen können Sie Vorhersagen ausführen, die auf einem Miningmodell basieren.  
  
 Sie können eine der SELECT-Anweisungen für das durch suchen oder Vorhersagen in den **from** -und **Where** -Klauseln einer **Select** -Anweisung für einen Vorhersage Join einschließen.  
  
|Abfragetyp|Beschreibung|  
|----------------|-----------------|  
|SELECT FROM [NATURAL] VORHERSAGE JOIN|Gibt eine Vorhersage zurück, die erstellt wurde, indem die Spalten des Miningmodells mit den Spalten einer internen Datenquelle verknüpft wurden.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus den vorhersagbaren Spalten aus dem Modell und den Spalten aus der Eingabedatenquelle.<br /><br /> [Wählen Sie &#60;aus&#62; der Modell &#40;Vorhersage Join DMX aus.&#41;](../dmx/select-from-model-prediction-join-dmx.md)<br /><br /> [Vorhersageabfragen &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
|*Aus\<Modell auswählen >*|Gibt nur auf Basis des Miningmodells den wahrscheinlichsten Status der vorhersagbaren Spalte zurück. Dieser Abfragetyp ist eine Abkürzung für das Erstellen einer Vorhersage mit einem leeren PREDICTION JOIN.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus den vorhersagbaren Spalten aus dem Modell.<br /><br /> [Aus &#60;Modell&#62; &#40;-DMX auswählen&#41;](../dmx/select-from-model-dmx.md)<br /><br /> [Vorhersageabfragen &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/prediction-queries-data-mining)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
###  <a name="Browsing"></a>Browser  
 Mit folgenden Abfragetypen können Sie die Inhalte eines Miningmodells durchsuchen.  
  
|Abfragetyp|Beschreibung|  
|----------------|-----------------|  
|Wählen Sie unterschiedliche from  *\<Model->*|Gibt alle Statuswerte vom Miningmodell für die angegebene Spalte zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp entspricht dem Data Mining-Modell.<br /><br /> [Wählen Sie im &#60;DMX-Modell &#62; &#40;eindeutig aus.&#41;](../dmx/select-distinct-from-model-dmx.md)<br /><br /> [Inhaltsabfragen &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Wählen Sie aus  *\<Modell >* aus. Inhaltliche|Gibt Inhalte mit Beschreibungen zum Miningmodell zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp entspricht dem CONTENT-Schemarowset.<br /><br /> [Wählen Sie &#60;aus&#62;dem Modell aus. Inhalt &#40;DMX&#41;](../dmx/select-from-model-content-dmx.md)<br /><br /> [Inhaltsabfragen &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-queries-data-mining)|  
|Wählen Sie aus  *\<Modell >* aus. DIMENSION_CONTENT|Gibt Inhalte mit Beschreibungen zum Miningmodell zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp entspricht dem CONTENT-Schemarowset.<br /><br /> [SELECT FROM &#60;model&#62;.DIMENSION_CONTENT &#40;DMX&#41;](../dmx/select-from-model-dimension-content-dmx.md)|  
|Wählen Sie aus  *\<Modell >* aus. PMML|Gibt für Algorithmen, die diese Funktionalität unterstützen, die PMML-Darstellung (Predictive Model Markup Language) des Miningmodells zurück.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem PMML-Schemarowset.<br /><br /> [DMSCHEMA_MINING_MODEL_CONTENT_PMML-Rowset](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
###  <a name="Copying"></a>Vorgänge  
 Sie können ein Miningmodell sowie dessen zugeordnete Miningstruktur in ein neues Modell kopieren und das Modell anschließend innerhalb der Anweisung umbenennen.  
  
|Abfragetyp|Beschreibung|  
|----------------|-----------------|  
|In neues Modell auswählen  *\<>*|Erstellt eine Kopie des Miningmodells.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem Data Mining-Modell.<br /><br /> [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
###  <a name="Drillthrough"></a>Drillthrough  
 Mit folgenden Abfragetypen können Sie die Fälle oder eine Darstellung der Fälle durchsuchen, die dazu verwendet wurden, das Modell zu trainieren.  
  
|Abfragetyp|Beschreibung|  
|----------------|-----------------|  
|Wählen Sie aus  *\<Modell >* aus. Denen|Gibt die Fälle zurück, die zum Trainieren des Miningmodells verwendet werden.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem Data Mining-Modell.<br /><br /> [Wählen Sie &#60;aus&#62;dem Modell aus. Fälle &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md)<br /><br /> [Erstellen von Drillthroughabfragen mit der DMX](https://docs.microsoft.com/analysis-services/data-mining/create-drillthrough-queries-using-dmx)|  
|Wählen Sie aus  *\<Modell >* aus. SAMPLE_CASES|Gibt einen Beispielfall zurück, der repräsentativ für die Fälle ist, die zum Trainieren des Miningmodells verwendet werden.<br /><br /> Die Datendomäne für diesen Abfragetyp besteht aus dem Data Mining-Modell.<br /><br /> [SELECT FROM &#60;model&#62;.SAMPLE_CASES &#40;DMX&#41;](../dmx/select-from-model-sample-cases-dmx.md)|  
|Wählen Sie aus  *\<Struktur >* aus. DENEN|Gibt die detaillierten Datenzeilen aus der zugrunde liegenden Miningstruktur zurück, auch wenn einige Details nicht zum Trainieren des Miningmodells verwendet wurden.<br /><br /> [Wählen Sie &#60;eine&#62;Struktur aus. Denen](../dmx/select-from-structure-cases.md)<br /><br /> [Drillthroughabfragen &#40;Data Mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/drillthrough-queries-data-mining)|  
  
 [Zurück zu Select-Typen](#Select_Types)  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining-Erweiterungen &#40;DMX&#41; – Referenz](../dmx/data-mining-extensions-dmx-reference.md)   
 [DMX&#41; - &#40;Anweisungs Referenz für Data Mining-Erweiterungen](../dmx/data-mining-extensions-dmx-statements.md)   
 [DMX&#41; - &#40;Syntax Konventionen für Data Mining-Erweiterungen](../dmx/data-mining-extensions-dmx-syntax-conventions.md)  
  
  
