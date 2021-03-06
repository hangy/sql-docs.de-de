---
title: affinity64 I/O mask (Serverkonfigurationsoption) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- binding processors [SQL Server]
- affinity64 I/O mask option
ms.assetid: d304eae7-5116-40ee-a0fa-0a3c0bc20c01
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9a0f63af10e8baf21cf17d316f64e66d4e663852
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013182"
---
# <a name="affinity64-input-output-mask-server-configuration-option"></a>affinity64 I/O mask (Serverkonfigurationsoption)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Die Option **affinity64 I/O mask** bindet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenträger-E/A an eine bestimmte Teilmenge der CPUs. Diese Option verhält sich ähnlich wie die Option **affinity I/O mask** . Verwenden Sie **affinity I/O mask** , um die ersten 32 Prozessoren zu binden, und mit **affinity64 I/O mask** binden Sie die restlichen Prozessoren auf dem Computer. Wenn Sie **affinity64 I/O mask**neu konfigurieren, müssen Sie die Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]neu starten. Diese Option wird nur in der 64-Bit-Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]angezeigt.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Affinity I/O Mask (Serverkonfigurationsoption)](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)   
 [Überwachen der Ressourcenverwendung &#40;Systemmonitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Serverkonfigurationsoptionen &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
