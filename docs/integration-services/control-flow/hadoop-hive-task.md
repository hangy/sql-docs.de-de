---
title: Hadoop Hive-Task | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoophivetask.f1
ms.assetid: 10ff37c0-9f3f-442a-889b-c351afbdc74c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f157b2b802142f6f00b7a3e9ffb2596ef80f1773
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298259"
---
# <a name="hadoop-hive-task"></a>Hadoop Hive-Task

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Mithilfe eines Hadoop Hive-Tasks können Sie ein Hive-Skript in einem Hadoop-Cluster ausführen.  
  
 Zum Hinzufügen eines Hadoop Hive-Tasks ziehen Sie diesen auf den Designer. Doppelklicken Sie anschließend auf den Task, oder klicken Sie mit der rechten Maustaste darauf, und klicken Sie auf **Bearbeiten**, um das Dialogfeld **Editor für Hadoop-Hive-Aufgaben** zu öffnen.  
  
 ![Editor für Hadoop-Hive-Aufgaben](../../integration-services/control-flow/media/hadoop-hive-task.png "Editor für Hadoop-Hive-Aufgaben")  
  
## <a name="options"></a>enthalten  
 Konfigurieren Sie die folgenden Optionen im Dialogfeld **Editor für Hadoop-Hive-Aufgaben** .  
  
|Feld|und Beschreibung|  
|-----------|-----------------|  
|**Hadoop-Verbindung**|Geben Sie einen vorhandenen Hadoop-Verbindungs-Manager an, oder erstellen Sie einen neuen. Dieser Verbindungs-Manager gibt an, wo der Dienst WebHCat gehostet wird.|  
|**SourceType**|Geben Sie den Quelltyp der Abfrage an. Mögliche Werte sind **ScriptFile** und **DirectInput**.|  
|**InlineScript**|Wenn der Wert von **SourceType** **DirectInput**ist, geben Sie das Hive-Skript an.|  
|**HadoopScriptFilePath**|Wenn der Wert von **SourceType** **ScriptFile**ist, geben Sie den Pfad der Skriptdatei auf Hadoop an.|  
|**TimeoutInMinutes**|Geben Sie einen Timeoutwert in Minuten an. Wenn der Hadoop-Job vor Ablauf des Timeouts nicht abgeschlossen wurde, wird er abgebrochen. Geben Sie 0 ein, wenn der Hadoop-Job asynchron ausgeführt werden soll.|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Hadoop-Verbindungs-Manager](../../integration-services/connection-manager/hadoop-connection-manager.md)  
  
  
