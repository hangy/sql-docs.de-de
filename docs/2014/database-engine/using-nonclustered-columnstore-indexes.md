---
title: Verwenden von nicht gruppierten columnstore-Indizes | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e97aed3a5a4f5b49e482479b58928d2092a314f9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773787"
---
# <a name="using-nonclustered-columnstore-indexes"></a>Verwenden nicht gruppierter Columnstore-Indizes
  Beschreibt wichtige Aufgaben für die Verwendung eines nicht gruppierten Columnstore-Indexes für eine [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Tabelle.  
  
 Eine Übersicht über Columnstore-Indizes finden Sie unter [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).  
  
 Informationen zum Verwenden von gruppierten Columnstore-Indizes finden Sie unter [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="contents"></a>Inhalt  
  
-   [Erstellen Sie einen nicht gruppierten columnstore-Index](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)  
  
-   [Ändern der Daten in einen nicht gruppierten columnstore-Index](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)  
  
##  <a name="load"></a> Erstellen Sie einen nicht gruppierten columnstore-Index  
 Um Daten in einen nicht gruppierten columnstore-Index zuladen, laden Sie zuerst Daten in eine herkömmliche Rowstore-Tabelle gespeichert, die als Heap oder gruppierten index und dann [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) zum Erstellen einer columnstore-Index.  
  
 ![Laden von Daten in einen columnstore-Index](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "Laden von Daten in einen columnstore-Index")  
  
##  <a name="change"></a> Ändern der Daten in einen nicht gruppierten columnstore-Index  
 Wenn Sie einen nicht gruppierten Columnstore-Index für eine Tabelle erstellen, können Sie die Daten in dieser Tabelle nicht mehr direkt ändern. Eine Abfrage mit INSERT, UPDATE, MERGE oder DELETE schlägt fehl und gibt eine Fehlermeldung zurück. Um Daten in der Tabelle hinzuzufügen oder zu ändern, können Sie eine der folgenden Aktionen ausführen:  
  
-   Deaktivieren Sie den columnstore-Index. Anschließend können Sie die Daten in der Tabelle aktualisieren. Wenn Sie den Columnstore-Index deaktivieren, können Sie den Columnstore-Index nach dem Aktualisieren der Daten neu erstellen. Zum Beispiel:  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   Löschen Sie den columnstore-Index, aktualisieren Sie die Tabelle, und klicken Sie dann erstellen Sie den columnstore-Index mit CREATE COLUMNSTORE INDEX neu. Zum Beispiel:  
  
    ```  
    DROP INDEX mycolumnstoreindex ON mytable  
    -- update mytable --  
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;  
  
    ```  
  
-   Laden Sie Daten in eine Stagingtabelle ohne Columnstore-Index. Erstellen Sie einen Columnstore-Index für die Stagingtabelle. Wechseln Sie für die Stagingtabelle in eine leere Partition der Haupttabelle.  
  
-   Wechseln Sie für eine Partition in der Tabelle mit dem Columnstore-Index in eine leere Stagingtabelle. Wenn die Stagingtabelle über einen Columnstore-Index verfügt, deaktivieren Sie den Columnstore-Index. Nehmen Sie die gewünschten Updates vor. Erstellen bzw. erstellen Sie den Columnstore-Index neu. Wechseln Sie für die Stagingtabelle zurück in die (nun leere) Partition der Haupttabelle.  
  

  
  
