---
title: Mehrsprachige und globale bereit Stellungen
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c3d485f8-867c-4aa2-a90d-f38fda192534
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 79a18eca1f222a4b128847a9367c46cfbe4cf891
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728109"
---
# <a name="multi-lingual-and-global-deployments-master-data-services"></a>Mehrsprachige und globale Bereitstellungen (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] unterstützt die Bereitstellung von Komponenten und Tools in allen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]unterstützten Sprachen. Weitere Informationen finden Sie unter [Local Language Versions in SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
## <a name="how-languages-are-used"></a>Vorgehensweise bei der Verwendung von Sprachen  
 In der folgenden Tabelle wird die Sprachunterstützung für die Komponenten und Tools von [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] beschrieben.  
  
|Komponente oder Tool|Beschreibung|  
|-----------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Setup|Wählen Sie das englische Setupprogramm aus, wenn die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung in anderen Sprachen als der Setupsprache verfügbar sein und unterstützt werden soll. Weitere Informationen finden Sie in der Beschreibung zu [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] unten.|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]|Die Setupsprache bestimmt die Sprache von [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] . Wenn Sie Deutsch als Setupsprache auswählen, ist [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] auf dem betreffenden Computer z. B. in Deutsch verfügbar.|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Wenn Sie das Setup auf Englisch ausführen, wird die [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] -Webanwendung in allen Anwendungssprachen bereitgestellt und unterstützt. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] kann in jeder dieser Anwendungssprachen angezeigt werden und akzeptiert gebietsschemaspezifische Eingaben auf Grundlage der Spracheinstellungen des Clientwebbrowsers. Wenn die Spracheinstellungen für eine nicht unterstützte Anwendungssprache konfiguriert werden, verwendet [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] standardmäßig Englisch.<br /><br /> Wenn Sie das Setup in einer anderen Sprache als Englisch ausführen, sind Ressourcen für alle anderen Anwendungssprachen enthalten. Bei diesem Szenario kann [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] von den Clients jedoch nicht in einer anderen Sprache als der ausgewählten Setupsprache verwendet werden. Wenn Sie versuchen, in einer anderen Sprache als der Setupsprache auf [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] zuzugreifen, könnten Probleme bei der Anzeige und Eingabe von Daten in die Anwendung auftreten.|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Datenbank|Die Informationen in der [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] -Datenbank sind nicht spezifisch für ein bestimmtes Gebietsschema. Dadurch kann [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] selbst bestimmen, wie Informationen, z. B. Datumsangaben und Zahlen, in dem durch die Spracheinstellungen im Clientwebbrowser festgelegten Format angezeigt werden.|  
  
## <a name="see-also"></a>Siehe auch  
 [Installieren von Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
