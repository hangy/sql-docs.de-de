---
title: Erstellen und bewerten eines Vorhersagemodells in R
titleSuffix: SQL Server Machine Learning Services
description: Erstellen Sie ein einfaches Vorhersagemodell in R mithilfe SQL Server Machine Learning Services, und prognostizieren Sie dann mithilfe neuer Daten ein Ergebnis.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9acfe1e546c332801e9a5c1a7d97758053d9a0f4
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542123"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>Schnellstart: Erstellen und bewerten eines Vorhersagemodells in R mit SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

In dieser Schnellstartanleitung erstellen und trainieren Sie ein Vorhersagemodell mithilfe von R. speichern Sie das Modell in einer Tabelle in Ihrer SQL Server Instanz, und verwenden Sie dann das Modell, um Werte aus neuen Daten mithilfe [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md)vorherzusagen.

Sie erstellen und führen zwei gespeicherte Prozeduren aus, die in SQL ausgeführt werden. Der erste verwendet das **mtcars** -DataSet, das in R enthalten ist, und generiert ein einfaches generelles lineares Modell (GLM), das die Wahrscheinlichkeit vorhersagt, dass ein Fahrzeug mit einer manuellen Übertragung ausgestattet wurde. Das zweite Verfahren dient der Bewertung: Es wird das im ersten Verfahren generierte Modell aufgerufen, um einen Satz von Vorhersagen basierend auf neuen Daten auszugeben. Wenn Sie R-Code in einer gespeicherten SQL-Prozedur platzieren, sind Vorgänge in SQL enthalten, sind wiederverwendbar und können von anderen gespeicherten Prozeduren und Client Anwendungen aufgerufen werden.

> [!TIP]
> Wenn Sie ein Aktualisierungs Programm für lineare Modelle benötigen, testen Sie dieses Tutorial, das den Prozess der Anpassung eines Modells mithilfe von rxlinmod: [Anpassen linearer Modelle](/machine-learning-server/r/how-to-revoscaler-linear-model) beschreibt.

Durch die Durchführung dieses Schnellstarts lernen Sie Folgendes:

> [!div class="checklist"]
> - Einbetten von R-Code in eine gespeicherte Prozedur
> - Übergeben von Eingaben an Ihren Code mithilfe von Eingaben für die gespeicherte Prozedur
> - Verwenden gespeicherter Prozeduren zum operationalisieren von Modellen

## <a name="prerequisites"></a>Prerequisites

- Diese Schnellstartanleitung erfordert Zugriff auf eine Instanz von SQL Server mit [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) , auf der die R-Sprache installiert ist.

  Ihre SQL Server Instanz kann sich auf einem virtuellen Azure-Computer oder lokal befinden. Beachten Sie, dass das Feature für die externe Skripterstellung standardmäßig deaktiviert ist. Daher müssen Sie möglicherweise [externe Skripterstellung aktivieren](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) und überprüfen, ob **SQL Server-Launchpad-Dienst** ausgeführt wird, bevor Sie beginnen.

- Außerdem benötigen Sie ein Tool zum Ausführen von SQL-Abfragen, die R-Skripts enthalten. Sie können diese Skripts mit einem beliebigen Daten Bank Verwaltungs-oder Abfrage Tool ausführen, solange eine Verbindung mit einer SQL Server Instanz hergestellt und eine T-SQL-Abfrage oder eine gespeicherte Prozedur ausgeführt werden kann. In diesem Schnellstart wird [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)verwendet.

## <a name="create-the-model"></a>Erstellen des Modells

Um das Modell zu erstellen, erstellen Sie Quelldaten für das Training, erstellen das Modell und trainieren es mithilfe der Daten. speichern Sie das Modell dann in einer SQL-Datenbank, in der es zum Generieren von Vorhersagen mit neuen Daten verwendet werden kann.

### <a name="create-the-source-data"></a>Erstellen der Quelldaten

1. Öffnen Sie SSMS, stellen Sie eine Verbindung mit Ihrer SQL Server Instanz her, und öffnen Sie ein neues Abfragefenster.

1. Erstellen Sie eine Tabelle zum Speichern der Trainingsdaten.

   ```sql
   CREATE TABLE dbo.MTCars(
       mpg decimal(10, 1) NOT NULL,
       cyl int NOT NULL,
       disp decimal(10, 1) NOT NULL,
       hp int NOT NULL,
       drat decimal(10, 2) NOT NULL,
       wt decimal(10, 3) NOT NULL,
       qsec decimal(10, 2) NOT NULL,
       vs int NOT NULL,
       am int NOT NULL,
       gear int NOT NULL,
       carb int NOT NULL
   );
   ```

1. Fügen Sie die Daten aus dem integrierten DataSet `mtcars` ein.

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > Viele kleine und große Datasets sind in der R-Laufzeit enthalten. Geben Sie `library(help="datasets")` von einer R-Eingabeaufforderung ein, um eine Liste der mit R installierten Datasets zu erhalten.

### <a name="create-and-train-the-model"></a>Erstellen und trainieren des Modells

Die Auto Geschwindigkeitsdaten enthalten zwei Spalten: "numeric" (`hp`) und "Weight" (`wt`). Aus diesen Daten erstellen Sie ein generalisiertes lineares Modell (GLM), das die Wahrscheinlichkeit schätzt, dass ein Fahrzeug mit einer manuellen Übertragung ausgestattet wurde.

Um das Modell zu erstellen, definieren Sie die Formel in Ihrem R-Code und übergeben die Daten als Eingabeparameter.

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

- Das erste Argument für `glm` ist der *Formel* Parameter, der `am` als abhängig von `hp + wt` definiert.
- Die Eingabedaten werden in der Variable `MTCarsData` gespeichert, die durch die SQL-Abfrage aufgefüllt wird. Wenn Sie Ihren Eingabedaten keinen spezifischen Namen zuweisen, ist der Standardvariablenname _InputDataSet_.

### <a name="store-the-model-in-the-sql-database"></a>Speichern des Modells in der SQL-Datenbank

Als nächstes speichern Sie das Modell in einer SQL-Datenbank, sodass Sie es für Vorhersagen verwenden und es erneut trainieren können. 

1. Erstellen Sie eine Tabelle, in der das Modell gespeichert wird.

   Die Ausgabe eines R-Pakets, das ein Modell erstellt, ist in der Regel ein binäres Objekt. Daher muss in der Tabelle, in der das Modell gespeichert wird, eine Spalte vom Typ **varbinary (max)** bereitgestellt werden.

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. Führen Sie die folgende Transact-SQL-Anweisung aus, um die gespeicherte Prozedur aufzurufen, das Modell zu generieren und in der Tabelle zu speichern, die Sie erstellt haben.

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > Wenn Sie diesen Code ein zweites Mal ausführen, erhalten Sie den folgenden Fehler: "Verletzung der PRIMARY KEY-Einschränkung... Ein doppelter Schlüssel kann in das Objekt dbo. stopping_distance_models "nicht eingefügt werden. Eine Möglichkeit zur Vermeidung dieses Fehlers besteht darin, den Namen für jedes neue Modell zu aktualisieren. Sie können den Namen z.B. in einen aussagekräftigeren Namen ändern und den Modelltyp, den Erstellungstag usw. mit aufnehmen.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>Bewerten neuer Daten mit dem trainierten Modell

Die *Bewertung* ist ein Begriff, der in Data Science verwendet wird, um Vorhersagen, Wahrscheinlichkeiten oder andere Werte basierend auf neuen Daten zu generieren, die in ein trainiertes Modell eingespeist werden. Sie verwenden das Modell, das Sie im vorherigen Abschnitt erstellt haben, um Vorhersagen für neue Daten zu bewerten.

### <a name="create-a-table-of-new-data"></a>Erstellen einer Tabelle mit neuen Daten

Erstellen Sie zunächst eine Tabelle mit neuen Daten.

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

### <a name="predict-manual-transmission"></a>Prognose der manuellen Übertragung

Um Vorhersagen basierend auf Ihrem Modell zu erhalten, schreiben Sie ein SQL-Skript, das Folgendes bewirkt:

1. Ruft das gewünschte Modell ab
1. Ruft die neuen Eingabedaten ab
1. Ruft eine R-Vorhersagefunktion auf, die mit dem Modell kompatibel ist

Im Laufe der Zeit kann die Tabelle mehrere R-Modelle enthalten, die alle mit unterschiedlichen Parametern oder Algorithmen erstellt wurden oder auf unterschiedlichen Teilmengen von Daten trainiert wurden. In diesem Beispiel verwenden wir das Modell mit dem Namen `default model`.

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

Das obige Skript führt die folgenden Schritte aus:

- Verwenden Sie eine SELECT-Anweisung, um ein einzelnes Modell aus der Tabelle abzurufen, und übergeben Sie es als Eingabeparameter.

- Rufen Sie nach dem Abruf des Modells aus der Tabelle die `unserialize`-Funktion auf dem Modell auf.

- Wenden Sie die `predict`-Funktion mit geeigneten Argumenten auf das Modell an, und stellen Sie die neuen Eingabedaten bereit.

> [!NOTE]
> Im Beispiel wird die `str`-Funktion während der Testphase hinzugefügt, um das Schema der von R zurückgegebenen Daten zu überprüfen. Sie können die Anweisung später entfernen.
>
> Die Spaltennamen, die im R-Skript verwendet werden, werden nicht notwendigerweise an die Ausgabe der gespeicherten Prozedur übermittelt. Hier wird die with results-Klausel verwendet, um einige neue Spaltennamen zu definieren.

**Ergebnisse**

![Resultset für die Vorhersage der Zulässigkeit der manuellen Übertragung](./media/r-predict-am-resultset.png)

Es ist auch möglich, die [Vorhersage (Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) -Anweisung zu verwenden, um einen vorhergesagten Wert oder eine Bewertung auf der Grundlage eines gespeicherten Modells zu generieren.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum SQL Server Machine Learning Services finden Sie unter:

- [Was ist SQL Server Machine Learning Services (python und R)?](../what-is-sql-server-machine-learning.md)
