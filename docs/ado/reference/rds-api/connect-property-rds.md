---
title: Connect-Eigenschaft (RDS) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Connect property [ADO]
ms.assetid: dbad5e77-b213-4eb8-aecf-d60f203fdb59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba8b5aa1f59fbb161da878f5930f83d2f6ff0bdd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964563"
---
# <a name="connect-property-rds"></a>Connect-Eigenschaft (RDS)
Gibt den Namen der Datenbank, von dem die Abfrage und Update-Vorgänge ausgeführt werden.  
  
 Sie können festlegen, die **Connect** Eigenschaft zur Entwurfszeit in den [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) Objekttags des Objekts, oder zur Laufzeit im Skriptcode (z. B. VBScript).  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in das Windows-Betriebssystem enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) Einzelheiten). RDS-Client-Komponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS zu migrieren sollten [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Design time: <PARAM NAME="Connect" VALUE="ConnectionString">  
Run time: DataControl.Connect = "ConnectionString"  
```  
  
#### <a name="parameters"></a>Parameter  
 *ConnectionString*  
 Eine gültige Verbindungszeichenfolge. Weitere allgemeine Informationen zu Verbindungszeichenfolgen finden Sie unter den ["ConnectionString"](../../../ado/reference/ado-api/connectionstring-property-ado.md) Eigenschaft oder der Dokumentation Ihres Anbieters.  
  
> [!NOTE]
>  Angeben von MS Remote als Anbieter für die **RDS. DataControl** würde ein Szenario mit vier Ebenen erstellen. Szenarien, die mehr als drei Ebenen wurden nicht getestet und sollte nicht erforderlich.  
  
 *DataControl*  
 Eine Objektvariable, steht ein **RDS. DataControl** Objekt.  
  
## <a name="applies-to"></a>Gilt für  
 [DataControl-Objekt (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Connect-Eigenschaft – Beispiel (VBScript)](../../../ado/reference/rds-api/connect-property-example-vbscript.md)   
 [Abfragemethode (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh-Methode (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges-Methode (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


