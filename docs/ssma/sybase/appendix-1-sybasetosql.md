---
title: Anhang – 1 (SybaseToSQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Appendix
ms.assetid: 6dcfd6d5-772c-4876-aa94-a7f43c4b9d59
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9d2d58b06c1a222a2ff6042bb5ca46338f752f7c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083538"
---
# <a name="appendix---1-sybasetosql"></a>Anhang 1 (SybaseToSQL)
Schnelle Übersicht über die Befehlszeilenoptionen von SSMA-Konsole:  
  
|Sl. Nein.|Schalter|Erforderlich?|Switch-Argument|Zulässige Werte|  
|-----------|----------|-------------|-------------------|--------------------|  
|1|-s/script|Ja|scriptfile|XML-Dateiname ist ungültig.<br /><br />Definition des Skriptdatei-Konsole.|  
|2|-V/variable|Nein|variablevaluefile|XML-Dateiname ist ungültig.<br /><br />Wenn die Variable im Skriptdatei verwendet werden, muss diese Datei angegeben werden.|  
|3|-c/serverconnection|Nein|serverconnectionfile|XML-Dateiname ist ungültig.<br /><br />Diese Datei enthält die Verbindungsinformationen.|  
|4|-x/xmloutput|Nein|xmloutputfile|Diese Option gibt die Ausgabe im XML-Format in der Konsole an. Wenn diese Option nicht angegeben ist, wird die standardmäßigen Ausgabe im Textformat.<br /><br />Wenn Xmloutputfile nicht angegeben ist, wird die XML-Ausgabe an "stdout" weitergeleitet.<br /><br />Xmloutputfile ist der Name der Datei in der die Ausgabe der Konsole in der XML-Format geschrieben wird.|  
|5|-l/log|Nein|logfile|Der Dateiname ist ungültig.|  
|6|-e/projectenvironment|Nein|projectenvironmentfolder|Gültigen Ordnernamen ein, die Dateien der SSMA-Projekt enthält.|  
|7|-p/securepassword|Nein|-a/hinzufügen {< Server_id > [,... n] &#124; alle} - C&#124;Serverconnection < Server-Verbindung-File > [-V&#124;Variable < Variable-Wert-File >] [-o/overwrite]<br /><br />oder<br /><br />-a/hinzufügen {< Server_id > [,... n] &#124; alle} -s&#124;Skript < Script-File > [-V&#124;Variable < Variable-Wert-File >] [-o/overwrite]<br /><br />-r/Remove {< Server_id > [,... n] &#124; alle}<br /><br />-l/Auflisten<br /><br />-e/Export {< Server-Id > [,... n] &#124; alle} < verschlüsselt – Kennwort - Datei ><br /><br />-i / import {< Server-Id > [,... n] &#124; alle} < verschlüsselt-Kennwort-File >|Wenn angegeben, muss diese Option nicht mit anderen Optionen kombiniert werden.<br /><br />Server-Id: Eine eindeutige ID für einen Server {String} bereitgestellt<br /><br />Server-Connection-Datei: Server-Definitionsdatei (Serverconnectionfile oder Scriptfile).<br /><br />Variable-Wert-Datei: Es ist eine Variablendefinition-Datei, und klicken Sie in Server-Connection-Datei verwendet.<br /><br />verschlüsselt das Kennwort-Datei: Es handelt sich um eine Server-Kennwörter-Datei mit einer benutzerdefinierten-Passphrase verschlüsselt.|  
|8|-?|Nein|Nicht zutreffend|Nicht zutreffend|  
  
## <a name="see-also"></a>Siehe auch  
[Executing the SSMA Console ausführen (Sybase)](https://msdn.microsoft.com/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
