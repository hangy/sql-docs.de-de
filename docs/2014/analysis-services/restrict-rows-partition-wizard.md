---
title: Einschränken der Zeilen (Partitions-Assistent) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.typefilterexpression.f1
ms.assetid: eec8da8f-eab4-4ac4-a81d-995c814f88ca
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 59bff3eac690b7352b75d02bd7b266dfa8f303f8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070213"
---
# <a name="restrict-rows-partition-wizard"></a>Zeilen einschränken (Partitions-Assistent)
  Mithilfe der Seite **Zeilen einschränken** können Sie die Zeilen einschränken, die aus der angegebenen Tabelle abgerufen, aggregiert und in die Partition eingeschlossen werden.  
  
> [!NOTE]  
>  Diese Seite wird nur angezeigt, wenn Sie auf der Seite **Quellinformationen angeben** eine einzelne Tabelle ausgewählt haben.  
  
> [!CAUTION]  
>  Wenn Sie auf der Seite **Quellinformationen angeben** unter **Verfügbare Tabellen** eine Tabelle angeben, die auch von einer anderen Partition verwendet wird, müssen Sie auf der Seite **Zeilen einschränken** eine Abfrage bereitstellen, da andernfalls die Gefahr besteht, dass die Daten im Cube dupliziert werden.  
  
## <a name="options"></a>Optionen  
 **Geben Sie eine Abfrage zum Einschränken der Zeilen**  
 Wählen Sie diese Option aus, um eine Abfrage in das Feld **Abfrage** einzugeben, die die Zeilen einschränkt.  
  
 Wenn beim Auswählen dieser Option das Feld **WHERE-Klausel hinzufügen** leer ist, wird dort eine SQL-Anweisung eingetragen, die alle Spalten und Zeilen aus der zuvor ausgewählten Tabelle abruft.  
  
 **Dataseteigenschaften**  
 Geben Sie die SQL-Anweisung ein, die während der Verarbeitung der Partition zum Abrufen von Zeilen aus der Tabelle verwendet wird, oder ändern Sie diese.  
  
> [!IMPORTANT]  
>  Wenn Sie eine WHERE-Klausel angeben, kann für diese Partition eine Teilmenge von Datensätzen verwendet werden. Dies ist von wesentlicher Bedeutung, um das Duplizieren von Daten zu verhindern, wenn mehrere Partitionen auf einer einzigen Faktentabelle basieren.  
  
 **Check**  
 Überprüft, ob es sich bei der Anweisung in **Abfrage** um eine gültige SQL-Anweisung handelt.  
  
## <a name="see-also"></a>Siehe auch  
 [Partitionen &#40;Analysis Services – Mehrdimensionale Daten&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
