---
title: Ändern des Verfügbarkeitsmodus eines Replikats innerhalb einer Verfügbarkeitsgruppe
description: In diesem Artikel finden Sie eine Anleitung dafür, wie Sie den Verfügbarkeitsmodus eines Verfügbarkeitsreplikats in einer Always On-Verfügbarkeitsgruppe mit Transact-SQL (T-SQL), PowerShell oder SQL Server Management Studio ändern.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], availability modes
ms.assetid: c4da8f25-fb1b-45a4-8bf2-195df6df634c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c17beebfd689e5e768450d92353b87f8fcfa1ae2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988589"
---
# <a name="change-the-availability-mode-of-a-replica-within-an-always-on-availability-group"></a>Ändern des Verfügbarkeitsmodus eines Replikats innerhalb einer Always On-Verfügbarkeitsgruppe
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In diesem Thema wird beschrieben, wie der Verfügbarkeitsmodus eines Verfügbarkeitsreplikats in einer Always On-Verfügbarkeitsgruppe in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]oder PowerShell geändert wird. Der Verfügbarkeitsmodus ist eine Replikateigenschaft, die steuert, ob das Replikat einen asynchronen oder synchronen Commit ausführt. Der*asynchrone Commitmodus* maximiert die Leistung auf Kosten der Hochverfügbarkeit und unterstützt nur erzwungene manuelle Failovervorgänge (mit möglichem Datenverlust), in der Regel *erzwungenes Failover*genannt. Der*synchrone Commitmodus* bevorzugt Hochverfügbarkeit gegenüber Leistung und unterstützt, sobald das sekundäre Replikat synchronisiert ist, manuelle Failovervorgänge und optional automatische Failovervorgänge.  
    
##  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
Sie müssen mit der Serverinstanz verbunden sein, die das primäre Replikat hostet.  
  

##  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER AVAILABILITY GROUP-Berechtigung für die Verfügbarkeitsgruppe, die CONTROL AVAILABILITY GROUP-Berechtigung, die ALTER ANY AVAILABILITY GROUP-Berechtigung oder die CONTROL SERVER-Berechtigung.  
  
##  <a name="SSMSProcedure"></a> Verwenden von SQL Server Management Studio  
 **So ändern Sie den Verfügbarkeitsmodus einer Verfügbarkeitsgruppe**  
  
1.  Stellen Sie im Objekt-Explorer eine Verbindung mit der Serverinstanz her, die das primäre Verfügbarkeitsreplikat hostet, und erweitern Sie die Serverstruktur.  
  
2.  Erweitern Sie den Knoten **Hohe Verfügbarkeit (immer aktiviert)** und den Knoten **Verfügbarkeitsgruppen** .  
  
3.  Klicken Sie auf die Verfügbarkeitsgruppe, deren Replikat geändert werden soll.  
  
4.  Klicken Sie mit der rechten Maustaste auf das Replikat, und klicken Sie auf **Eigenschaften**.  
  
5.  Verwenden Sie im Dialogfeld **Eigenschaften des Verfügbarkeitsreplikats** die Dropdownliste **Verfügbarkeitsmodus** , um den Verfügbarkeitsmodus für dieses Replikat zu ändern.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
 **So ändern Sie den Verfügbarkeitsmodus einer Verfügbarkeitsgruppe**  
  
1.  Stellen Sie eine Verbindung mit der Serverinstanz her, die das primäre Replikat hostet.  
  
2.  Verwenden Sie die [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md) -Anweisung wie folgt:  
  
     ALTER AVAILABILITY GROUP *Gruppenname* MODIFY REPLICA ON '*Servername*'  
  
     WITH ( {  
  
     AVAILABILITY_MODE = { SYNCHRONOUS_COMMIT | ASYNCHRONOUS_COMMIT }  
  
     | FAILOVER_MODE = { AUTOMATIC | MANUAL }  
  
     } )  
  
     Dabei ist *Gruppenname* der Name der Verfügbarkeitsgruppe und *Servername* der Name der Serverinstanz, die das Replikat hostet, das geändert werden soll.  
  
    > [!NOTE]  
    >  FAILOVER_MODE = AUTOMATIC wird nur unterstützt, wenn Sie auch AVAILABILITY_MODE = SYNCHRONOUS_COMMIT angeben.  
  
     Im folgenden, für das primäre Replikat der `AccountsAG` -Verfügbarkeitsgruppe eingegebenen Beispiel werden der Verfügbarkeitsmodus und der Failovermodus für das von der `INSTANCE09` -Serverinstanz gehostete Replikat in den Modus für synchrone Commits bzw. automatisches Failover geändert.  
  
    ```  
  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (AVAILABILITY_MODE = SYNCHRONOUS_COMMIT);  
    ALTER AVAILABILITY GROUP AccountsAG MODIFY REPLICA ON 'INSTANCE09'  
       WITH (FAILOVER_MODE = AUTOMATIC);  
    ```  
  
##  <a name="PowerShellProcedure"></a> PowerShell  
 **So ändern Sie den Verfügbarkeitsmodus einer Verfügbarkeitsgruppe**  
  
1.  Wechseln Sie mit**cd**in das Verzeichnis der Serverinstanz, die das primäre Replikat hostet.  
  
2.  Verwenden Sie das **Set-SqlAvailabilityReplica** -Cmdlet mit dem **AvailabilityMode** -Parameter und optional mit dem **FailoverMode** -Parameter.  
  
     Beispielsweise wird durch diesen Befehl das Replikat `MyReplica` in der Verfügbarkeitsgruppe `MyAg` so geändert, dass der Verfügbarkeitsmodus für synchrone Commits verwendet und automatische Failover unterstützt werden.  
  
    ```  
    Set-SqlAvailabilityReplica -AvailabilityMode "SynchronousCommit" -FailoverMode "Automatic" `   
    -Path SQLSERVER:\Sql\PrimaryServer\InstanceName\AvailabilityGroups\MyAg\AvailabilityReplicas\MyReplica  
    ```  
  
    > [!NOTE]  
    >  Um die Syntax eines Cmdlets anzuzeigen, verwenden Sie das **Get-Help** -Cmdlet in der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell-Umgebung. Weitere Informationen finden Sie unter [Get Help SQL Server PowerShell](../../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
 **Einrichten und Verwenden des SQL Server PowerShell-Anbieters**  
  
-   [SQL Server PowerShell-Anbieter](../../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
## <a name="see-also"></a>Weitere Informationen  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verfügbarkeitsmodi &#40;Always On-Verfügbarkeitsgruppen&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [Failover und Failovermodi (Always On-Verfügbarkeitsgruppen)](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)  
  
  
