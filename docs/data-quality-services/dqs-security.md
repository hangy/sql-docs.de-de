---
title: DQS-Sicherheit | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 921927f5-1b1e-452a-a79e-c691829fd826
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c732645c526b2179265a6669055d005e944ee114
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992101"
---
# <a name="dqs-security"></a>DQS-Sicherheit

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Die [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS)-Sicherheitsinfrastruktur basiert auf der SQL Server-Sicherheitsinfrastruktur. Ein Datenbankadministrator gewährt einem Benutzer einen Satz von Berechtigungen, indem er dem Benutzer eine DQS-Rolle zuordnet. Auf diese Weise wird bestimmt, auf welche DQS-Ressourcen der Benutzer Zugriff hat und welche funktionalen Aktivitäten der Benutzer ausführen kann.  
  
## <a name="dqs-roles"></a>DQS-Rollen  
 Es gibt vier Rollen für DQS. Eine davon ist der Datenbankadministrator (DBA), der hauptsächlich für Produktinstallation, Datenbankwartung und Benutzerverwaltung zuständig ist. Diese Rolle verwendet meist eher SQL Server Management Studio als die [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] - Anwendung. Die Serverrolle ist „sysadmin“.  
  
 Die anderen Rollen sind „Information Workers“ und „Data Stewards“, die das Produkt direkt durch in der Anwendung [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] verwenden. Zu diesen Rollen gehören:  
  
-   Der **DQS-Administrator** (dqs_administrator-Rolle) kann im Rahmen des Produkts alle Vorgänge ausführen. Der Administrator kann ein Projekt bearbeiten und ausführen, eine Wissensdatenbank erstellen und bearbeiten, eine Aktivität beenden, einen Prozess innerhalb einer Aktivität stoppen und die Konfiguration sowie die Reference Data Services-Einstellungen ändern. Der DQS-Administrator kann jedoch nicht den Server installieren oder neue Benutzer hinzufügen. Dies ist Aufgabe des Datenbankadministrators.  
  
-   Der **DQS KB-Editor** (Rolle „dqs_kb_editor“) kann alle DQS-Aktivitäten mit Ausnahme von Verwaltungsaufgaben ausführen. Der KB-Editor kann ein Projekt bearbeiten und ausführen sowie eine Wissensdatenbank erstellen und bearbeiten. Er kann die Aktivitätsüberwachungsdaten anzeigen, die Aktivität jedoch weder abschließen noch stoppen oder Verwaltungsaufgaben ausführen.  
  
-   Der **DQS KB-Operator** (Rolle „dqs_kb_operator“) kann ein Projekt bearbeiten und ausführen. Er kann keinerlei Wissensverwaltung ausführen und keine Wissensdatenbank erstellen oder ändern. Er kann die Aktivitätsüberwachungsdaten anzeigen, die Aktivität jedoch nicht abschließen bzw. keine Verwaltungsaufgaben ausführen.  
  
## <a name="user-management"></a>Benutzerverwaltung  
 Der Datenbankadministrator (DBA) erstellt DQS-Benutzer und ordnet sie DQS-Rollen in SQL Server Management Studio zu. Der DBA verwaltet ihre Berechtigungen, indem er der DQS_MAIN-Datenbank SQL-Anmeldenamen als Benutzer hinzufügt und jeden Benutzer mit einer der DQS-Rollen verknüpft. Jeder Rolle werden Berechtigungen für einen Satz von gespeicherten Prozeduren in der DQS_MAIN-Datenbank gewährt. Die drei DQS-Rollen sind für die Datenbanken DQS_PROJECTS und DQS_STAGING_DATA nicht verfügbar.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Taskbeschreibung|Thema|  
|----------------------|-----------|  
|Beschreibt, wie Sie mit SQL Server Management Studio einen Benutzer erstellen und diesem DQS-Rollen gewähren.|[Verwalten von DQS-Benutzern in SSMS](https://msdn.microsoft.com/library/955af01d-00da-4c51-9311-f3848749df54)|  
  
  
