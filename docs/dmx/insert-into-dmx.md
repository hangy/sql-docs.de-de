---
title: INSERT INTO (DMX) | Microsoft-Dokumentation
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 210ab8c5750fdcb38bcbca324d77eecd926042d1
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892724"
---
# <a name="insert-into-dmx"></a>INSERT INTO (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Verarbeitet das angegebene Data Mining-Objekt. Weitere Informationen zum Verarbeiten von Mining Modellen und Mining Strukturen finden Sie unter [Verarbeiten von Anforderungen &#40;und über&#41;Legungen zum Data Mining](https://docs.microsoft.com/analysis-services/data-mining/processing-requirements-and-considerations-data-mining).  
  
 Wenn eine Miningstruktur angegeben ist, verarbeitet die Anweisung die Miningstruktur sowie alle Miningmodelle, die der Struktur zugeordnet sind. Ist ein Miningmodell angegeben, verarbeitet die Anweisung nur das Miningmodell.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure> (<mapped model columns>) <source data query>  
INSERT INTO [MINING MODEL]|[MINING STRUCTURE] <model>|<structure>.COLUMN_VALUES (<mapped model columns>) <source data query>  
```  
  
## <a name="arguments"></a>Argumente  
 *model*  
 Ein Modellbezeichner.  
  
 *Werks*  
 Ein Strukturbezeichner.  
  
 *zugeordnete Modell Spalten*  
 Eine durch Trennzeichen getrennte Liste mit Spaltenbezeichnern und geschachtelten Bezeichnern.  
  
 *Quelldaten Abfrage*  
 Die Quellabfrage im anbieterdefinierten Format.  
  
## <a name="remarks"></a>Hinweise  
 Wenn Sie kein **Mining Modell** oder keine **Mining Struktur**angeben, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sucht nach dem Objekttyp, der auf dem Namen basiert, und verarbeitet das richtige Objekt. Wenn der Server eine Miningstruktur und ein Miningmodell enthält, die denselben Namen haben, wird ein Fehler zurückgegeben.  
  
 Wenn Sie das zweite Syntax Formular verwenden, fügen Sie in *\<Objekt >* ein. COLUMN_VALUES, Sie können Daten direkt in die Modell Spalten einfügen, ohne das Modell zu trainieren. Bei dieser Methode werden dem Modell Spaltendaten in einer übersichtlichen, geordneten Weise bereitgestellt, die sich anbietet, wenn Sie mit Datasets arbeiten, die Hierarchien oder geordnete Spalten enthalten.  
  
 Wenn Sie **INSERT INTO** mit einem Mining Modell oder einer Mining Struktur verwenden und die \<zugeordneten Modell Spalten > und \<> Argumente der Quelldaten Abfrage weglassen, verhält sich die Anweisung wie **ProcessDefault**, wobei Bindungen verwendet werden, die ist bereits vorhanden. Wenn keine Bindungen vorhanden sind, gibt die Anweisung einen Fehler zurück. Weitere Informationen zu **ProcessDefault**finden Sie unter [Verarbeitungsoptionen und- &#40;Einstellungen&#41;Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/processing-options-and-settings-analysis-services). Das folgende Beispiel zeigt die Syntax:  
  
```  
INSERT INTO [MINING MODEL] <model>  
```  
  
 Wenn Sie ein **Mining Modell** angeben und zugeordnete Spalten und eine Quelldaten Abfrage bereitstellen, werden das Modell und die zugehörige Struktur verarbeitet.  
  
 In der folgenden Tabelle sind die vom Status der Objekte abhängigen Ergebnisse der unterschiedlichen Formen der Anweisung beschrieben.  
  
|-Anweisung.|Status der Objekte|Ergebnis|  
|---------------|----------------------|------------|  
|> In Mining Modell *\<Modell einfügen*|Miningstruktur wird verarbeitet.|Miningmodell wird verarbeitet.|  
||Miningstruktur wird nicht verarbeitet.|Miningmodell und Miningstruktur werden verarbeitet.|  
||Miningstruktur enthält weitere Miningmodelle.|Fehler bei der Verarbeitung. Sie müssen die Struktur und die zugeordneten Miningmodelle erneut verarbeiten.|  
|In Mining Struktur *\<Struktur einfügen >*|Miningstruktur wird verarbeitet oder nicht verarbeitet.|Miningstruktur und zugeordnete Miningmodelle werden verarbeitet.|  
|Einfügen in Mining Modell *\<Modell->* , das eine Quell Abfrage enthält<br /><br /> oder<br /><br /> > In Mining Struktur *\<Struktur* einfügen, die eine Quell Abfrage enthält|Entweder die Struktur oder das Modell enthält bereits Inhalt.|Fehler bei der Verarbeitung. Sie müssen die Objekte löschen, bevor Sie diesen Vorgang ausführen, indem [Sie &#40;DMX&#41;löschen](../dmx/delete-dmx.md)verwenden.|  
  
## <a name="mapped-model-columns"></a>Zugeordnete Modellspalten (Mapped Model Columns)  
 Mithilfe der \<> Elemente zugeordneten Modell Spalten können Sie die Spalten aus der Datenquelle den Spalten im Mining Modell zuordnen. Die \<zugeordneten Modell Spalten > Elements hat folgendes Format:  
  
```  
<column identifier> | SKIP | <table identifier> (<column identifier> | SKIP), ...  
```  
  
 Mithilfe von **Skip**können Sie bestimmte Spalten ausschließen, die in der Quell Abfrage vorhanden sein müssen, die jedoch im Mining Modell nicht vorhanden sind. SKIP ist hilfreich, wenn Sie keine Kontrolle über die Spalten haben, die in einem Eingaberowset enthalten sind. Wenn Sie Ihre eigene OPENQUERY schreiben, wird anstelle der Verwendung von SKIP empfohlen, die Spalte in der SELECT-Spaltenliste auszulassen.  
  
 SKIP ist auch nützlich, wenn eine Spalte aus dem Eingaberowset benötigt wird, um einen Join durchzuführen, die Spalte jedoch nicht von der Miningstruktur verwendet wird. Ein typisches Beispiel dafür sind eine Miningstruktur und ein Miningmodell, die eine geschachtelte Tabelle enthalten. Das Eingaberowset für diese Struktur umfasst eine Fremdschlüsselspalte, mit der ein hierarchisches Rowset mithilfe der SHAPE-Klausel erstellt wird. Die Fremdschlüsselspalte wird jedoch kaum im Modell verwendet.  
  
 Die Syntax für SKIP erfordert, dass Sie SKIP an der Position der einzelnen Spalte im Eingaberowset einfügen, das über keine entsprechende Miningstrukturspalte verfügt. Beispielsweise muss in der Beispiel Tabelle der Tabelle "Tabelle" in der APPEND-Klausel "OrderNumber" ausgewählt werden, damit Sie in der Beziehung-Klausel zum Angeben des Joins verwendet werden kann. Sie möchten jedoch nicht die OrderNumber-Daten in die-Tabelle in der Mining Struktur einfügen. Daher wird im Beispiel im INSERT INTO-Argument das Skip-Schlüsselwort anstelle von OrderNumber verwendet.  
  
## <a name="source-data-query"></a>Quelldatenabfrage (Source Data Query)  
 Die \<Quelldaten Abfrage >-Element kann die folgenden Datenquellen Typen enthalten:  
  
-   **OPENQUERY**  
  
-   **OPENROWSET**  
  
-   **GEBILDET**  
  
-   Jede [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]-Abfrage, die ein Rowset zurückgibt  
  
 Weitere Informationen zu Datenquellen Typen finden [ &#60;Sie unter Quelldaten Abfragen&#62;](../dmx/source-data-query.md).  
  
## <a name="basic-example"></a>Elementares Beispiel  
 Im folgenden Beispiel wird **OPENQUERY** verwendet, um ein Naive Bayes-Modell basierend auf den Ziel-Mailing [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] Daten in der-Datenbank zu trainieren.  
  
```  
INSERT INTO NBSample (CustomerKey, Gender, [Number Cars Owned],  
    [Bike Buyer])  
OPENQUERY([AdventureWorksDW2012],'Select CustomerKey, Gender, [NumberCarsOwned], [BikeBuyer]   
FROM [vTargetMail]')  
```  
  
## <a name="nested-table-example"></a>Beispiel für eine geschachtelte Tabelle  
 Im folgenden Beispiel wird die **Form** zum Trainieren eines Association-Mining Modells verwendet, das eine in einer Tabelle enthaltene Tabelle enthält. Beachten Sie, dass die Faust Zeile **Skip** anstelle von OrderNumber enthält, was in der **SHAPE_APPEND** -Anweisung erforderlich ist, aber nicht im Mining Modell verwendet wird.  
  
```  
INSERT INTO MyAssociationModel  
    ([OrderNumber],[Models] (SKIP, [Model])  
    )  
SHAPE {  
    OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([AdventureWorksDW2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
AS [Models]  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Data Mining- &#40;Erweiterungen DMX&#41; -Daten Definitions Anweisungen](../dmx/dmx-statements-data-definition.md)   
 [Data Mining- &#40;Erweiterungen DMX&#41; -Daten Bearbeitungsanweisungen](../dmx/dmx-statements-data-manipulation.md)   
 [Data Mining-Erweiterungen &#40;DMX&#41; – Anweisungsreferenz](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
