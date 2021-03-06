---
title: Erstellen einer Warnung mithilfe von Schweregraden | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 696527b77cba555ad5c70a8ee65c8409295d18e4
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70846799"
---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In einer [verwalteten Azure SQL-Datenbank-Instanz](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) werden die meisten, aber nicht alle, SQL Server-Agent-Features unterstützt. Weitere Informationen finden Sie unter [T-SQL-Unterschiede zwischen einer verwalteten Azure SQL-Datenbank-Instanz und SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In diesem Thema wird beschrieben, wie eine Warnung des [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] oder [!INCLUDE[tsql](../../includes/tsql-md.md)]erstellt wird, die beim Auftreten eines Ereignisses mit einem bestimmten Schweregrad ausgelöst wird.  
  
## <a name="BeforeYouBegin"></a>Vorbereitungen  
  
### <a name="Restrictions"></a>Einschränkungen  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] lässt sich das gesamte Warnungssystem auf einfache Weise mit einer grafischen Oberfläche verwalten. Dies ist die empfohlene Vorgehensweise, um eine Warnungsinfrastruktur zu konfigurieren.  
  
-   Ereignisse, die mit **xp_logevent** generiert werden, treten in der master-Datenbank auf. Daher wird von **xp_logevent** erst dann eine Warnung ausgelöst, wenn der **\@database_name**-Wert für die Warnung den Wert **'master'** oder NULL aufweist.  
  
-   Bei den Schweregraden 19 bis 25 wird eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Meldung an das Anwendungsprotokoll von [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows gesendet und eine Warnung ausgelöst. Ereignisse mit einem Schweregrad unter 19 lösen nur dann Warnungen aus, wenn Sie **sp_altermessage**, RAISERROR WITH LOG oder **xp_logevent** verwendet haben, um zu erzwingen, dass die Warnungen in das Windows-Anwendungsprotokoll geschrieben werden.  
  
### <a name="Security"></a>Sicherheit  
  
#### <a name="Permissions"></a>Berechtigungen  
Standardmäßig können nur Mitglieder der festen Serverrolle **sysadmin** die Prozedur **sp_add_alert**ausführen.  
  
## <a name="SSMSProcedure"></a>Verwenden von SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-severity-level"></a>So erstellen Sie eine Warnung mithilfe von Schweregraden  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, auf dem Sie eine Warnung mithilfe des Schweregrads erstellen möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Warnungen** , und wählen Sie **Neue Warnung**aus.  
  
4.  Geben Sie im Dialogfeld **Neue Warnung** einen **Namen** für diese Warnung ein.  
  
5.  Klicken Sie in der Liste **Typ** auf **SQL Server-Ereigniswarnung**.  
  
6.  Klicken Sie in der Liste **Datenbankname**auf den **Datenbanknamen**, um die Warnung auf eine bestimmte Datenbank zu beschränken.  
  
7.  Klicken Sie unter **Warnungen werden ausgelöst basierend auf**auf **Schweregrad** , und wählen Sie dann den bestimmten Schweregrad aus, womit die Warnung ausgelöst wird.  
  
8.  Aktivieren Sie das Kontrollkästchen neben **Warnung auslösen, wenn eine Meldung Folgendes enthält** , um die Warnung auf eine bestimmte Zeichenfolge zu beschränken, und geben Sie dann ein Schlüsselwort oder Zeichenfolge für den **Meldungstext**ein. Es können maximal 100 Zeichen eingegeben werden.  
  
9. Klicken Sie auf **OK**.  
  
## <a name="TsqlProcedure"></a>Verwenden von Transact-SQL  
  
#### <a name="to-create-an-alert-using-severity-level"></a>So erstellen Sie eine Warnung mithilfe von Schweregraden  
  
1.  Stellen Sie im **Objekt-Explorer** eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde_md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Adds an alert (Test Alert) that notifies the
    -- Alert Operator via email when an error with a 
    -- severity of 23 is detected.
    
    -- Assumes that the Alert Operator already exists 
    -- and that database mail is configured.
    
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert @name=N'Test Alert', 
      @message_id = 0, 
      @severity = 23, 
      @enabled = 1, 
      @include_event_description_in = 1
    ;
    GO
    
    EXEC dbo.sp_add_notification @alert_name=N'Test Alert',
      @operator_name=N'Alert Operator',
      @notification_method=1
    ;
    GO

    ```  
  
Weitere Informationen finden Sie unter [sp_add_alert (Transact-SQL)](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09).  
  
