---
title: InfoMessage-Ereignis (ADO) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::InfoMessage
- InfoMessage
helpviewer_keywords:
- InfoMessage event [ADO]
ms.assetid: 468c87dd-e3bc-4084-9941-94d10743d4e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 25eef06b7e25538cb874d99af98aee95495b95ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932334"
---
# <a name="infomessage-event-ado"></a>InfoMessage-Ereignis (ADO)
Die **InfoMessage** Ereignis wird immer dann aufgerufen, wenn eine Warnung ausgegeben, während wird eine **ConnectionEvent** Vorgang.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
InfoMessage pError, adStatus, pConnection  
```  
  
#### <a name="parameters"></a>Parameter  
 *pError*  
 Ein [Fehler](../../../ado/reference/ado-api/error-object.md) Objekt. Dieser Parameter enthält alle Fehler, die zurückgegeben werden. Wenn mehrere Fehler zurückgegeben werden, Auflisten der **Fehler** Auflistung, um Sie zu finden.  
  
 *adStatus*  
 Ein [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md) Statuswert. Wenn eine Warnung auftritt, *AdStatus* nastaven NA hodnotu **AdStatusOK** und *pError* enthält die Warnung.  
  
 Bevor Sie dieses Ereignis zurückgegeben wird, legen Sie diesen Parameter auf **AdStatusUnwantedEvent** , nachfolgende Benachrichtigungen zu verhindern.  
  
 *pConnection*  
 Ein [Verbindung](../../../ado/reference/ado-api/connection-object-ado.md) Objekt. Die Verbindung für die die Warnung aufgetreten ist. Warnungen können beispielsweise auftreten, wenn Sie öffnen ein **Verbindung** Objekt oder die Ausführung einer [Befehl](../../../ado/reference/ado-api/command-object-ado.md) auf eine **Verbindung**.  
  
## <a name="see-also"></a>Siehe auch  
 [ADO-Ereignismodell – Beispiel (VC++)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO-Ereignishandler – Zusammenfassung](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Connection-Objekt (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
