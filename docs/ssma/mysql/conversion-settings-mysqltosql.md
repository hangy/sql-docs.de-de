---
title: Konvertierungseinstellungen (MySQLToSQL)) | Microsoft-Dokumentation
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f551cf6e-1575-4206-9cca-975b5b43a6b8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: debdd549dc010f7be6b9d9b37a4caf649d4e106a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103121"
---
# <a name="conversion-settings-mysqltosql"></a>Konvertierungseinstellungen (MySqlToSql)
Die **"Einstellungen"** Registerkarte kann der Benutzer knoteneinstellungen festlegen. Die Registerkarte wird in der folgenden Metabase-Knoten verfügbar sein:  
  
-   Knoten "Datenbank"  
  
-   Kategorie "Funktionen"  
  
-   Funktionsknoten  
  
-   Tabellen-Kategorie  
  
-   Table-Knoten  
  
## <a name="specifications"></a>Spezifikationen:  
Die **Einstellungen** Registerkarte verfügt über zwei benutzereinstellungen viz.:  
  
1.  Funktion-Konvertierung  
  
2.  Tabellenkonvertierung  
  
Diese Einstellungen werden basierend auf den Typ des Metabase-Knotens. Beispielsweise ist-Funktion, Konvertierung im Zusammenhang festlegen auf den Tabellenknoten nicht verfügbar  
  
> [!NOTE]  
> -   Die vom Benutzer vorgenommenen Änderungen werden im Arbeitsbereich "Projekt" als einer separaten Einstellungsdatei gespeichert werden.  
> -   Die Erweiterung dieser Datei werden **Ccprefs**.  
  
1.  **Einstellung für die Konvertierung von Funktion:**  
  
    1.  Diese Registerkarte enthält **"Erzwingen der Konvertierung von Funktion"** Option. Die Option kann es sich um einen der folgenden vier Werten aufweisen:  
  
        -   Konvertieren Sie gemäß den projekteinstellungen [geerbt]  
  
        -   In einer Funktion immer konvertieren  
  
        -   Immer in einer Prozedur konvertieren  
  
        -   Konvertieren Sie gemäß den projekteinstellungen  
  
    2.  Basierend auf den Einstellungen, wird die Funktion an eine Funktion oder einer gespeicherten Prozedur konvertiert werden.  
  
    3.  Die vom Benutzer vorgenommenen Einstellungen werden gespeichert, in der Einstellungsdatei kaskadierenden durch Klicken auf **übernehmen** Schaltfläche.  
  
2.  **Einstellung bei der Konvertierung der Tabelle:**  
  
    1.  Diese Registerkarte enthält **"ROWID unterdrücken zusätzlichen Spalte Generation"** Option. Die Option kann es sich um einen der folgenden vier Werten aufweisen:  
  
        -   Konvertieren Sie gemäß den projekteinstellungen [geerbt]  
  
        -   Ja  
  
        -   Nein  
  
        -   Konvertieren Sie gemäß den projekteinstellungen  
  
    2.  Wenn **'Ja'** , diese Einstellung verhindert die Erstellung von ROWID zusätzlichen Spalte erstellen, auf die Zieltabellen.  
  
    3.  Die vom Benutzer vorgenommenen Einstellungen werden in kaskadierenden Einstellungsdatei durch Klicken auf gespeichert **übernehmen** Schaltfläche.  
  
## <a name="see-also"></a>Siehe auch  
[Project Settings (Conversion) (MySQL zu SQL)](https://msdn.microsoft.com/7ad5fe44-6445-4ba8-a457-5af792631f11)  
  
