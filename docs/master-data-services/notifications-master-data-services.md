---
title: Benachrichtigungen
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- notifications [Master Data Services]
- notifications [Master Data Services], about notifications
- e-mail [Master Data Services]
- e-mail [Master Data Services], about e-mail notifications
ms.assetid: d7ad32d5-9fe5-48fd-8c61-0b00c0aff082
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ec76228a4f8307813a2bb098b648133e065c5cd5
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727955"
---
# <a name="notifications-master-data-services"></a>Benachrichtigungen (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] kann konfiguriert werden, um eine E-Mail-Benachrichtigung zu senden, wenn die Überprüfung der Geschäftsregel fehlschlägt oder sich der Status einer Modellversion oder eines Changesets ändert.  
  
## <a name="how-notifications-are-sent"></a>Senden von Benachrichtigungen  
 Benachrichtigungen werden in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]konfiguriert. Die Benachrichtigungsfunktion sendet auf der Instanz von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] that hosts the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database. Weitere Informationen zu Datenbank-E-Mails finden Sie unter [Konfigurationsobjekte für Datenbank-E-Mail](../relational-databases/database-mail/database-mail-configuration-objects.md) in der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -Onlinedokumentation.  
  
## <a name="when-notifications-are-sent"></a>Zeitpunkt des Sendens von Benachrichtigungen  
 Nachdem Benachrichtigungen konfiguriert wurden, können automatisierte E-Mail-Benachrichtigungen in den folgenden Instanzen gesendet werden.  
  
|Instanz|Beschreibung|  
|--------------|-----------------|  
|Daten haben die Geschäftsregelüberprüfung nicht bestanden.|Es müssen separate Geschäftsregeln konfiguriert werden, um E-Mails zu senden, wenn ein Attributwert die Geschäftsregelüberprüfung nicht besteht. Die Benachrichtigung enthält die folgenden Informationen.<br /><br /> Modell<br /><br /> Version<br /><br /> Entität<br /><br /> Elementcode<br /><br /> Fehlgeschlagene Geschäftsregel<br /><br /> Link zum Element, für das der Attributwert die Geschäftsregelüberprüfung nicht bestanden hat<br /><br /> Zeitpunkt der Benachrichtigungsausgabe<br /><br /> Weitere Informationen finden Sie unter [Konfigurieren von Geschäftsregeln für das Senden von Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md).|  
|Der Status einer Modellversion ändert sich.|Jedes Mal, wenn sich der Status einer Modellversion ändert, erhalten Modelladministratoren automatisch eine Benachrichtigung. Die Benachrichtigung enthält die folgenden Informationen.<br /><br /> Modell<br /><br /> Version<br /><br /> Vorheriger und neuer Status der Version<br /><br /> Zeitpunkt der Benachrichtigungsausgabe<br /><br /> Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).|  
|Changesetstatus ändert sich|Bei jeder Änderung eines Changesetstatus für eine Entität, die genehmigt werden muss, erhalten Entitätsadministratoren und/oder Changesetbesitzer automatisch eine Benachrichtigung. Die Benachrichtigung enthält die folgenden Informationen.<br /><br /> Modell<br /><br /> Version<br /><br /> Changesetname<br /><br /> Vorheriger Status<br /><br /> Neuer Status<br /><br /> einen Link für das Anwenden des Changesets, um die ausstehenden Änderungen anzuzeigen und zu ändern<br /><br /> Weitere Informationen finden Sie unter [Changesets &#40;Master Data Services&#41;](../master-data-services/changesets-master-data-services.md).|  
  
## <a name="system-settings"></a>Systemeinstellungen  
 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] verfügt über Einstellungen, die sich auf Benachrichtigungen auswirken. Sie können diese Einstellungen in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] oder direkt in der Tabelle Systemeinstellungen der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] -Datenbank anpassen. Weitere Informationen finden Sie unter [Systemeinstellungen &#40;Master Data Services&#41;](../master-data-services/system-settings-master-data-services.md).  
  
## <a name="related-tasks"></a>Verwandte Aufgaben  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Konfigurieren Sie [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , um E-Mail-Benachrichtigungen zu senden.|[Konfigurieren von E-Mail-Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/configure-email-notifications-master-data-services.md)|  
|Konfigurieren Sie [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], um Benachrichtigungen zu senden, wenn sich Attributwerte ändern.|[Konfigurieren von Geschäftsregeln für das Senden von Benachrichtigungen &#40;Master Data Services&#41;](../master-data-services/configure-business-rules-to-send-notifications-master-data-services.md)|  
  
## <a name="related-content"></a>Verwandte Inhalte  
  
-   [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
-   [Versionen &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
-   [Problembehandlung für E-Mail-Benachrichtigungen (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-email-notifications-master-data-services.aspx)  
  
  
