---
title: Sp_trace_create (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_create_TSQL
- sp_trace_create
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_create
ms.assetid: f3a43597-4c5a-4520-bcab-becdbbf81d2e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7d698932bb7ef7e0fd37a0ced8ab536eeb0d5d68
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096032"
---
# <a name="sptracecreate-transact-sql"></a>sp_trace_create (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt eine Ablaufverfolgungsdefinition. Die neue Ablaufverfolgung weist einen beendeten Status auf.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Verwenden Sie stattdessen erweiterte Ereignisse.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_trace_create [ @traceid = ] trace_id OUTPUT   
          , [ @options = ] option_value   
          , [ @tracefile = ] 'trace_file'   
     [ , [ @maxfilesize = ] max_file_size ]  
     [ , [ @stoptime = ] 'stop_time' ]  
     [ , [ @filecount = ] 'max_rollover_files' ]  
```  
  
## <a name="arguments"></a>Argumente  
`[ @traceid = ] trace_id` Die Anzahl von zugewiesene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in die neue Ablaufverfolgung. Benutzereingaben werden ignoriert. *Trace_id* ist **Int**, hat den Standardwert NULL. Der Benutzer verwendet die *Trace_id* zu identifizieren, ändern und Steuern der Ablaufverfolgung, die von dieser gespeicherten Prozedur definierten Wert.  
  
`[ @options = ] option_value` Gibt die für die Ablaufverfolgung festgelegten Optionen. *Option_value* ist **Int**, hat keinen Standardwert. Benutzer können eine Kombination dieser Optionen wählen, indem sie den Summenwert der gewünschten Optionen angeben. Um die Optionen TRACE_FILE_ROLLOVER und SHUTDOWN_ON_ERROR zu aktivieren, geben Sie z. B. **6** für *Option_value*.  
  
 In der folgenden Tabelle werden die Optionen, Beschreibungen und die zugehörigen Werte aufgeführt.  
  
|Optionsname|Optionswert|Beschreibung|  
|-----------------|------------------|-----------------|  
|TRACE_FILE_ROLLOVER|**2**|Gibt an, dass die *Max_file_size* erreicht ist, wird die aktuelle Ablaufverfolgungsdatei wird geschlossen, und eine neue Datei erstellt wird. Alle neuen Datensätze werden in die neue Datei geschrieben. Die neue Datei hat den gleichen Namen wie die vorige, aber eine ganze Zahl wird angefügt werden, um der Sequenz anzuzeigen. Ist z. B. der Name der ursprünglichen Ablaufverfolgungsdatei filename.trc, so wird die nächste Datei mit filename_1.trc benannt, dann folgt filename_2.trc usw.<br /><br /> Wenn weitere Ablaufverfolgungs-Rolloverdateien erstellt werden, erhöht sich der an die Dateinamen angefügte ganzzahlige Wert sequenziell.<br /><br /> SQL Server verwendet standardmäßig den Wert *Max_file_size* (5 MB), wenn diese Option angegeben wird, ohne Angabe eines Werts für *Max_file_size*.|  
|SHUTDOWN_ON_ERROR|**4**|Gibt an, dass SQL Server heruntergefahren wird, wenn die Ablaufverfolgung nicht in die Datei geschrieben werden kann, unabhängig vom Grund. Diese Option ist beim Ausführen von Ablaufverfolgungen zur Sicherheitsüberwachung hilfreich.|  
|TRACE_PRODUCE_BLACKBOX|**8**|Gibt an, dass eine Aufzeichnung der letzten 5 MB der Ablaufverfolgungsinformationen, die vom Server erzeugt wurden, von diesem Server gespeichert werden. TRACE_PRODUCE_BLACKBOX ist mit keiner der anderen Optionen kompatibel.|  
  
`[ @tracefile = ] 'trace_file'` Gibt den Speicherort und Dateinamen, der die Ablaufverfolgung geschrieben wird. *Trace_file* ist **nvarchar(245)** hat keinen Standardwert. *Trace_file* kann entweder ein lokales Verzeichnis (beispielsweise N 'C:\MSSQL\Trace\trace.trc') oder einen UNC-Pfad für eine Freigabe oder ein Pfad sein (N'\\\\*Servername*\\*Sharename* \\ *Directory*\trace.trc').  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Fügt eine **trc** Erweiterung für alle Namen von Ablaufverfolgungsdateien. Wenn die Option TRACE_FILE_ROLLOVER und ein *Max_file_size* angegeben sind, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eine neue Ablaufverfolgungsdatei erstellt, wenn die maximale Größe die ursprünglichen Ablaufverfolgungsdatei erreicht. Die neue Datei hat den gleichen Namen wie die ursprüngliche Datei, aber __*n* angefügt wird, um anzugeben, die Reihenfolge, beginnend mit **1**. Wenn die erste Datei heißt beispielsweise **filename.trc**, ist die zweite Datei mit dem Namen **filename_1.trc**.  
  
 Wenn Sie die Option TRACE_FILE_ROLLOVER verwenden, sollten im ursprünglichen Dateinamen keine Unterstriche enthalten sein. Bei Verwendung von Unterstrichen tritt Folgendes auf:  
  
-   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] erfasst nicht automatisch laden, oder Sie werden aufgefordert, die Rolloverdateien (sofern eines dieser dateirolloveroptionen konfiguriert sind).  
  
-   Die Fn_trace_gettable-Funktion lädt keine Rolloverdateien (Wenn Sie mithilfe des Parameters der *Number_files* Argument), in dem der ursprüngliche Dateiname endet mit einem Unterstrich und einem numerischen Wert. (Dies gilt nicht für den Unterstrich und die Zahl, die beim Rollover automatisch angehängt werden.)  
  
> [!NOTE]  
>  Um diese beiden Probleme zu umgehen, können Sie die Dateien umbenennen und die Unterstriche im ursprünglichen Dateinamen entfernen. Wenn die ursprüngliche Datei heißt beispielsweise **my_trace.trc**, und die Rolloverdatei heißt **my_trace_1.trc**, können Sie die Dateien umbenennen **mytrace.trc** und **mytrace_1.trc** vor dem Öffnen der Dateien im [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
 *Trace_file* kann nicht angegeben werden, wenn die Option TRACE_PRODUCE_BLACKBOX verwendet wird.  
  
`[ @maxfilesize = ] max_file_size` Gibt an, dass die maximale Größe in Megabyte (MB) eine Ablaufverfolgungsdatei vergrößert werden kann. *Max_file_size* ist **Bigint**, hat den Standardwert des **5**.  
  
 Wenn dieser Parameter ohne die Option TRACE_FILE_ROLLOVER angegeben wird, beendet die Ablaufverfolgung Aufzeichnung in der Datei an, wenn der verwendete Speicherplatz den Wert überschreitet *Max_file_size*.  
  
`[ @stoptime = ] 'stop_time'` Gibt an, das Datum und die Uhrzeit, die die Ablaufverfolgung beendet wird. *Stop_time* ist **"DateTime"** , hat den Standardwert NULL. Beim Wert NULL wird die Ablaufverfolgung so lange ausgeführt, bis sie manuell beendet oder der Server heruntergefahren wird.  
  
 Wenn beide *Stop_time* und *Max_file_size* angegeben sind, TRACE_FILE_ROLLOVER ist nicht angegeben, die Ablaufverfolgung beendet wird, wenn entweder die angegebene Beendigungszeit oder die maximale Dateigröße erreicht ist. Wenn *Stop_time*, *Max_file_size*, und TRACE_FILE_ROLLOVER angegeben sind, wird die Ablaufverfolgung beendet wird an die angegebene Beendigungszeit, sofern die Ablaufverfolgung gänzlich nicht auf dem Laufwerk.  
  
`[ @filecount = ] 'max_rollover_files'` Gibt die maximale Anzahl von Ablaufverfolgungsdateien an, die mit dem gleichen Basisdateinamen verwaltet werden. *MAX_ROLLOVER_FILES* ist **Int**, größer als 1. Dieser Parameter ist nur dann gültig, wenn die Option TRACE_FILE_ROLLOVER angegeben wird. Wenn *Max_rollover_files* angegeben wird, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versucht, die keine Verwaltung mehr als *Max_rollover_files* Ablaufverfolgungsdateien, indem die älteste Ablaufverfolgungsdatei gelöscht wird, bevor Sie eine neue Ablaufverfolgungsdatei öffnen. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] wird das Alter von Ablaufverfolgungsdateien durch das Anfügen einer Nummer an den Basisdateinamen nachverfolgt.  
  
 Z. B., wenn die *Trace_file* -Parameter angegeben wird als "c:\mytrace", eine Datei mit dem Namen "c:\mytrace_123.trc" älter als eine Datei mit dem Namen "c:\mytrace_124.trc". Wenn *Max_rollover_files* und SQL Server die Datei "c:\mytrace_123.trc" löscht dann vor dem Erstellen der Ablaufverfolgungsdatei "c:\mytrace_125.trc" ist auf 2 festgelegt.  
  
 Beachten Sie, dass in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jede Datei nur einmal zu löschen versucht wird und eine Datei nicht gelöscht werden kann, wenn diese von einem anderen Prozess verwendet wird. Wenn in einer anderen Anwendung Ablaufverfolgungsdateien verwendet werden, während die Ablaufverfolgung ausgeführt wird, werden diese Ablaufverfolgungsdateien daher möglicherweise von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] im Dateisystem belassen.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 In der folgenden Tabelle werden die Codewerte beschrieben, die die Benutzer nach Abschluss der gespeicherten Prozedur möglicherweise erhalten.  
  
|Rückgabecode|Beschreibung|  
|-----------------|-----------------|  
|0|Kein Fehler.|  
|1|Unbekannter Fehler.|  
|10|Ungültige Optionen. Wird zurückgegeben, wenn angegebene Optionen inkompatibel sind.|  
|12|Datei nicht erstellt.|  
|13|Nicht genügend Arbeitsspeicher. Wird zurückgegeben, wenn nicht genügend Arbeitsspeicher zum Ausführen der angegebenen Aktion verfügbar ist.|  
|14|Ungültige Beendigungszeit. Wird zurückgegeben, wenn die angegebene Beendigungszeit bereits verstrichen ist.|  
|15|Parameter sind ungültig. Wird zurückgegeben, wenn der Benutzer inkompatible Parameter angegeben hat.|  
  
## <a name="remarks"></a>Hinweise  
 **Sp_trace_create** ist eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gespeicherten Prozedur, die viele der zuvor von ausgeführten Aktionen ausführt, **Xp_trace_\***  erweiterte gespeicherte Prozeduren, die in früheren Versionen von SQL Server verfügbar. Verwendung **Sp_trace_create** anstelle von:  
  
-   **xp_trace_addnewqueue**  
  
-   **xp_trace_setqueuecreateinfo**  
  
-   **xp_trace_setqueuedestination**  
  
 **Sp_trace_create** erstellt nur eine Ablaufverfolgungsdefinition. Diese gespeicherte Prozedur kann nicht verwendet werden, um eine Ablaufverfolgung zu starten oder zu ändern.  
  
 Parameter aller gespeicherten Prozeduren der SQL-Ablaufverfolgung (**sp_trace_xx**) haben eine strikte Typbindung. Wenn diese Parameter nicht mit den richtigen Datentypen für Eingabeparameter aufgerufen werden, wie in der Argumentbeschreibung angegeben, gibt die gespeicherte Prozedur einen Fehler zurück.  
  
 Für **Sp_trace_create**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto muss Schreibberechtigung verfügen, auf den Ordner der Ablaufverfolgungsdatei. Wenn das [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto kein Administrator auf dem Computer ist, auf dem die Ablaufverfolgungsdatei gespeichert ist, müssen Sie dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Dienstkonto explizit die Schreibberechtigung erteilen.  
  
> [!NOTE]  
>  Sie können mit erstellte Ablaufverfolgungsdatei automatisch laden **Sp_trace_create** in eine Tabelle mit den **Fn_trace_gettable** -Systemfunktion. Weitere Informationen zur Verwendung dieser Systemfunktion finden Sie unter [Sys. fn_trace_gettable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md).  
  
 Ein Beispiel zum Verwenden gespeicherter Prozeduren der Ablaufverfolgung finden Sie unter [Erstellen einer Ablaufverfolgung &#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md).  
  
 **TRACE_PRODUCE_BLACKBOX** weist folgende Merkmale auf:  
  
-   Es handelt sich um eine Rollover-Ablaufverfolgung. Der Standardwert *File_count* 2 können jedoch überschrieben werden vom Benutzer mit *Filecount* Option.  
  
-   Der Standardwert *File_size* wie bei anderen ablaufverfolgungen 5 MB ist und geändert werden kann.  
  
-   Es kann kein Dateiname angegeben werden. Die Datei wird gespeichert unter: **N'%SQLDIR%\MSSQL\DATA\blackbox.trc'**  
  
-   Nur die folgenden Ereignisse und deren Spalten sind in der Ablaufverfolgung enthalten:  
  
    -   **RPC wird gestartet**  
  
    -   **BatchStarting**  
  
    -   **Ausnahme**  
  
    -   **Aufmerksamkeit**  
  
-   Für diese Ablaufverfolgung können Ereignisse oder Spalten nicht hinzugefügt oder entfernt werden.  
  
-   Filter können für diese Ablaufverfolgung nicht angegeben werden.  
  
## <a name="permissions"></a>Berechtigungen  
 Benutzer müssen über die ALTER TRACE-Berechtigung verfügen.  
  
## <a name="see-also"></a>Siehe auch  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [SQL-Ablaufverfolgung](../../relational-databases/sql-trace/sql-trace.md)  
  
  
