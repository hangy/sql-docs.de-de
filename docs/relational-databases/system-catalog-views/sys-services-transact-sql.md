---
title: Sys.Services (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.services
- services
- services_TSQL
- sys.services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.services catalog view
ms.assetid: 16d0b0c5-5cce-469b-aa3d-4b9248e0c085
author: stevestein
ms.author: sstein
ms.openlocfilehash: c19e65117a03de6b473eced3c7c1379943c851a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078661"
---
# <a name="sysservices-transact-sql"></a>sys.services (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Diese Katalogsicht enthält eine Zeile für jeden Dienst in der Datenbank.  
  
|Spaltenname|Datentyp|Beschreibung|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nach Groß-/Kleinschreibung unterschiedener Name des in der Datenbank eindeutigen Diensts. Lässt keine NULL-Werte zu.|  
|**service_id**|**int**|Bezeichner des Diensts. Lässt keine NULL-Werte zu.|  
|**principal_id**|**int**|Bezeichner des Datenbankprinzipals, der diesen Dienst besitzt. Lässt NULL-Werte zu.|  
|**service_queue_id**|**int**|Objekt-ID der Warteschlange, die dieser Dienst verwendet. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Weitere Informationen finden Sie unter [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
  
