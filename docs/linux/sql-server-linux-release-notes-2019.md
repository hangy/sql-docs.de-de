---
title: Versionshinweise für SQL Server 2019 für Linux
description: Dieser Artikel enthält Versionshinweise und Beschreibungen der unterstützten Features für SQL Server 2019 für Linux. Es werden sowohl Versionshinweise zum neuesten Release als auch zu einigen früheren Releases aufgeführt.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 8edcbf91c827ea2afafa0830aad5a26423102f17
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73594540"
---
# <a name="release-notes-for-sql-server-2019-on-linux"></a>Versionshinweise für SQL Server 2019 für Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

Die folgenden Versionshinweise gelten für SQL Server 2019 bei Ausführung unter Linux. Dieser Artikel ist in Abschnitte für jedes einzelne Release unterteilt. Jede Version verfügt über einen Link zu einem Supportartikel, in dem die Änderungen der Kapazitätseinheit und Links zu herunterladbaren Linux-Paketen enthalten sind.

> [!TIP]
> Weitere Informationen zu neuen Linux-Funktionen in SQL Server 2019 finden Sie unter [Neues in SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

## <a name="supported-platforms"></a>Unterstützte Plattformen

| Platform | Dateisystem | Installationshandbuch |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3-, 7.4-, 7.5- oder 7.6-Server | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2, SP3 oder SP4 | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS | XFS oder EXT4 | [Installationshandbuch](quickstart-install-connect-ubuntu.md) | 
| Docker-Engine 1.8+ für Windows, Mac oder Linux | – | [Installationshandbuch](quickstart-install-connect-docker.md) | 

> [!TIP]
> Weitere Informationen finden Sie in den [Systemanforderungen](sql-server-linux-setup.md#system) für SQL Server für Linux. Die neuesten Richtlinien zur Unterstützung für SQL Server 2017 finden Sie unter [Technical support policy for Microsoft SQL Server (Richtlinien für die technische Unterstützung von Microsoft SQL Server)](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Tools

Die meisten Clienttools für SQL Server können mühelos für SQL Server für Linux verwendet werden. Für einige Tools muss womöglich eine spezifische Versionsanforderung erfüllt werden, damit ihr volles Potential mit Linux genutzt werden kann. Eine vollständige Liste der SQL Server-Tools finden Sie unter [SQL Tools and Utilities for SQL Server (SQL-Tools und Hilfsprogramme für SQL Server)](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Releaseverlauf

In der folgenden Tabelle wird der Releaseverlauf für die Releases von SQL Server 2019 aufgelistet.

| Release                   | Versionsoptionen       | Veröffentlichungsdatum |
|---------------------------|---------------|--------------|
| [GA](#ga)                 | 15.0.2000.5  | 4\.11.2019    |
| [Release Candidate](#rc)  | 15.0.1900.25  | 21.8.2019   |

## <a id="cuinstall"></a> Installieren der Updates

Wenn Sie das CU-Repository (mssql-server-2019) konfiguriert haben, erhalten Sie bei der Durchführung neuer Installationen das neueste kumulative Update von SQL Server-Paketen. Wenn Sie Docker-Containerimages benötigen, verwenden Sie die offiziellen Images für [Microsoft SQL Server für Linux für die Docker-Engine](https://hub.docker.com/r/microsoft/mssql-server/). Weitere Informationen zur Repositorykonfiguration finden Sie unter [Configure repositories for SQL Server on Linux (Konfigurieren von Repositorys für SQL Server für Linux)](sql-server-linux-change-repo.md).

Führen Sie den entsprechenden Updatebefehl für jedes Paket durch, wenn Sie vorhandene SQL Server-Pakete aktualisieren, um das neueste kumulative Update zu erhalten. Spezifische Updateanweisungen für die einzelnen Pakete finden Sie in den folgenden Installationshandbüchern:

- [Installieren des SQL Server-Pakets](sql-server-linux-setup.md#upgrade)
- [Installieren des Volltextsuchepakets](sql-server-linux-setup-full-text-search.md)
- [Install SQL Server Integration Services (Installieren von SQL Server Integration Services)](sql-server-linux-setup-ssis.md)
- [Installieren von SQL Server 2019 Machine Learning Services (R und Python) unter Linux](sql-server-linux-setup-machine-learning.md)
- [Installieren des PolyBase-Pakets](../relational-databases/polybase/polybase-linux-setup.md)
- [Aktivieren des SQL Server-Agents](sql-server-linux-setup-sql-agent.md)

## <a id="ga"></a> Allgemeine Verfügbarkeit (November 2019)

Dies ist das allgemein verfügbare Release von SQL Server 2019 (15.x). Die Version der SQL Server-Datenbank-Engine für dieses Release ist 15.0.2000.5.

### <a name="package-details"></a>Paketdetails

Für manuelle oder offline durchgeführte Paketinstallationen können Sie die RPM- und Debian-Pakete herunterladen, die in der folgenden Tabelle aufgeführt werden:

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat RPM-Paket | 15.0.2000.5-5 | [RPM-Engine-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Hochverfügbarkeitspaket](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Paket für Volltextsuche](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Erweiterbarkeitspaket](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Paket für Java-Erweiterbarkeit](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[RPM-PolyBase-Paket](https://packages.microsoft.com/rhel/7/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| SLES RPM-Paket | 15.0.2000.5-5 | [RPM-Engine-Paket (mssql-server)](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Hochverfügbarkeitspaket](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-ha-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Paket für Volltextsuche](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-fts-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Erweiterbarkeitspaket](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-15.0.2000.5-5.x86_64.rpm)</br>[RPM-Paket für Java-Erweiterbarkeit](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-extensibility-java-15.0.2000.5-5.x86_64.rpm)</br>[RPM-PolyBase-Paket](https://packages.microsoft.com/sles/12/mssql-server-2019/mssql-server-polybase-15.0.2000.5-5.x86_64.rpm)|
| Debian-Paket für Ubuntu 16.04 | 15.0.2000.5-5 | [Debian-Engine-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server/mssql-server_15.0.2000.5-5_amd64.deb)</br>[Debian-Hochverfügbarkeitspaket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.2000.5-5_amd64.deb)</br>[Debian-Paket für Volltextsuche](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.2000.5-5_amd64.deb)</br>[Debian-Erweiterbarkeitspaket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.2000.5-5_amd64.deb)</br>[Debian-Paket für Java-Erweiterbarkeit](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.2000.5-5_amd64.deb)</br>[RPM-PolyBase-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2019/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.2000.5-5_amd64.deb)|

## <a id="rc"></a> Release Candidate (August 2019)

In den folgenden Abschnitten werden Paketspeicherorte und bekannte Probleme bezüglich der RC-Version bereitgestellt. Weitere Informationen zu den neuen Funktionen für SQL Server 2019 unter Linux finden Sie unter [Neues in SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Paketdetails

Für manuelle oder offline durchgeführte Paketinstallationen können Sie die RPM- und Debian-Pakete herunterladen, die in der folgenden Tabelle aufgeführt werden:

| Paket | Paketversion | Downloads |
|-----|-----|-----|
| Red Hat RPM-Paket | 15.0.1900.25-1 | [RPM-Engine-Paket](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Hochverfügbarkeitspaket](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Paket für Volltextsuche](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Erweiterbarkeitspaket](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Paket für Java-Erweiterbarkeit](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[RPM-PolyBase-Paket](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| SLES RPM-Paket | 15.0.1900.25-1 | [RPM-Engine-Paket (mssql-server)](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Hochverfügbarkeitspaket](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Paket für Volltextsuche](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Erweiterbarkeitspaket](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1900.25-1.x86_64.rpm)</br>[RPM-Paket für Java-Erweiterbarkeit](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1900.25-1.x86_64.rpm)</br>[RPM-PolyBase-Paket](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1900.25-1.x86_64.rpm)|
| Debian-Paket für Ubuntu 16.04 | 15.0.1900.25-1 | [Debian-Engine-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1900.25-1_amd64.deb)</br>[Debian-Hochverfügbarkeitspaket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1900.25-1_amd64.deb)</br>[Debian-Paket für Volltextsuche](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1900.25-1_amd64.deb)</br>[Debian-Erweiterbarkeitspaket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1900.25-1_amd64.deb)</br>[Debian-Paket für Java-Erweiterbarkeit](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1900.25-1_amd64.deb)</br>[RPM-PolyBase-Paket](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1900.25-1_amd64.deb)|

## <a name="known-issues"></a>Bekannte Probleme

In den folgenden Abschnitten werden bekannte Probleme mit dem allgemein verfügbaren Release von SQL Server 2019 (15.x) für Linux beschrieben.

#### <a name="general"></a>Allgemein

- Der Name des Hosts, auf dem [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installiert ist, darf maximal 15 Zeichen lang sein. 

    - **Lösung:** Ändern Sie den Namen unter /etc/hostname in einen Namen, der maximal 15 Zeichen enthält.

- Wenn Sie die Systemzeit manuell auf einen früheren Zeitpunkt festlegen, aktualisiert [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] die interne Systemzeit in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nicht mehr.

    - **Lösung:** Starten Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]neu.

- Nur Installationen mit einzelner Instanz werden unterstützt.

    - **Lösung:** Wenn Sie mehrere Instanzen auf einem bestimmten Host verwenden möchten, ziehen Sie die Verwendung von VMs (virtuelle Computer) oder Docker-Containern in Betracht. 

- Der [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Konfigurations-Manager kann keine Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Linux herstellen.

- Die Standardsprache der **sa**-Anmeldung ist Englisch.

    - **Lösung:** Ändern Sie die Sprache für die **sa**-Anmeldung mithilfe der Anweisung **ALTER LOGIN**.

#### <a name="databases"></a>Datenbanken

- Die Masterdatenbank kann nicht mit dem Hilfsprogramm „mssql-conf“ verschoben werden. Andere Systemdatenbanken können mit „mssql-conf“ verschoben werden.

- Beim Wiederherstellen einer Datenbank, die in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Windows gesichert wurde, müssen Sie die Klausel **WITH MOVE** in der Transact-SQL-Anweisung verwenden.

- Gewisse Algorithmen (Suites mit Verschlüsselungsverfahren) für TLS (Transport Layer Security) funktionieren in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Linux nicht ordnungsgemäß. Dies führt zu Verbindungsfehlern beim Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sowie beim Herstellen von Verbindungen zwischen Replikaten in Hochverfügbarkeitsgruppen.

   - **Lösung:** Passen Sie das Konfigurationsskript **mssql.conf** für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Linux an, um problematische Suites mit Verschlüsselungsverfahren zu deaktivieren, indem Sie wie folgt vorgehen:

      1. Fügen Sie Folgendes unter „/var/opt/mssql/mssql.conf“ hinzu.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Starten Sie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] mithilfe des folgenden Befehls neu.

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]-Datenbanken unter Windows, die In-Memory-OLTP nutzen, können nicht in SQL Server 2019 (15.x) für Linux wiederhergestellt werden. Führen Sie zunächst ein Upgrade auf [!INCLUDE[ssSQL15](../includes/sssql15-md.md)], SQL Server 2017 oder SQL Server 2019 unter Windows für die Datenbanken durch, und verschieben Sie sie anschließend per Backup/Wiederherstellung oder durch Trennen/Anfügen in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Linux, um eine [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]-Datenbank wiederherzustellen, die In-Memory-OLTP nutzt.

- Unter Linux wird die Benutzerberechtigung **ADMINISTER BULK OPERATIONS** zurzeit nicht unterstützt.

#### <a name="networking"></a>Netzwerk

Features, die ausgehende TCP-Verbindungen aus dem sqlservr-Prozess nutzen, z. B. Verbindungsserver oder Verfügbarkeitsgruppen, funktionieren möglicherweise nicht, wenn beide der folgenden Bedingungen erfüllt werden:

1. Der Zielserver wurde mit einem Hostnamen anstelle einer IP-Adresse angegeben.

1. IPv6 ist im Kernel der Quellinstanz deaktiviert. Alle der folgenden Tests müssen bestanden werden, um zu überprüfen, ob IPv6 im Kernel Ihres Systems aktiviert ist:

   - `cat /proc/cmdline` gibt die boot-Befehlszeile des aktuellen Kernels aus. Die Ausgabe darf `ipv6.disable=1` nicht enthalten.
   - Das Verzeichnis „/proc/sys/net/ipv6/“ muss vorhanden sein.
   - Ein C-Programm, das `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` aufruft, sollte erfolgreich sein – der Systemaufruf muss „fd ! = -1“ zurückgeben und darf nicht mit EAFNOSUPPORT fehlschlagen.

Der genaue Fehler hängt vom Feature ab. Bei Verbindungsservern zeigt sich dieser Fehler in Form eines Anmeldungstimeouts. Bei Verfügbarkeitsgruppen schlägt die `ALTER AVAILABILITY GROUP JOIN`-DDL auf dem sekundären Replikat nach 5 Minuten mit einem Timeout beim Download der Konfiguration fehl.

Führen Sie einen der folgenden Schritte aus, um dieses Problem zu umgehen:

1. Verwenden Sie IP-Adressen anstelle von Hostnamen, um das Ziel der TCP-Verbindung anzugeben.

1. Aktivieren Sie IPv6 im Kernel, indem Sie `ipv6.disable=1` aus der boot-Befehlszeile entfernen. Die Vorgehensweise hierfür hängt von der Linux-Verteilung und dem Bootloader (z. B. GRUB) ab. Wenn Sie IPv6 deaktivieren möchten, können Sie dennoch deaktivieren, indem Sie `net.ipv6.conf.all.disable_ipv6 = 1` in der `sysctl`-Konfiguration festlegen (z. B. `/etc/sysctl.conf`). Dadurch wird weiterhin verhindert, dass der Netzwerkadapter des Systems eine IPv6-Adresse erhält, und ermöglicht dennoch die Funktion der sqlservr-Features.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Wenn Sie **NFS-Remotefreigaben (Network File System)** in der Produktion verwenden, beachten Sie die folgenden Anforderungen für die Unterstützung:

- Verwenden Sie NFS in der Version **4.2 oder höher**. Ältere NFS-Versionen unterstützen nicht die erforderlichen Features, wie das Erstellen von Fallocate- oder Sparsedateien, die häufig in modernen Dateisystemen enthalten sind.
- Verwenden Sie nur die Verzeichnisse vom Typ **/var/opt/mssql** in der NFS-Bereitstellung. Andere Dateien, wie z. B. die [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]-Systembinärdateien, werden nicht unterstützt.
- Stellen Sie sicher, dass NFS-Clients beim Einbinden der Remotefreigabe die Option „NOLOCK“ verwenden.

#### <a name="localization"></a>Lokalisierung

- Wenn Ihr Gebietsschema während des Setups nicht Englisch (en_us) ist, müssen Sie die UTF-8-Codierung in Ihrer Bash-Sitzung bzw. Ihrem Terminal verwenden. Wenn Sie die ASCII-Codierung verwenden, kann ein Fehler ähnlich dem Folgenden auftreten:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Wenn Sie die UTF-8-Codierung nicht verwenden können, führen Sie das Setup mit der Umgebungsvariable MSSQL_LCID aus, um Ihre Sprachauswahl festzulegen.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Beim Ausführen des Befehls „mssql-conf setup“ und Durchführen einer nicht-englischen Installation von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], werden falsche erweiterte Zeichen nach dem lokalisierten Text „Configuring SQL Server...“ (SQL Server wird konfiguriert...) angezeigt. Bei Installationen basierend auf Sprachen mit nicht-lateinischen Zeichen kann der Text vollständig fehlen. Der fehlende Text sollte die folgende lokalisierte Zeichenfolge darstellen: „Die Lizenzierungs-PID wurde erfolgreich verarbeitet. Die neue Edition lautet [\<Name\>-Edition].“ Diese Zeichenfolge wird nur zu Informationszwecken ausgegeben, und das nächste kumulative Update für [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] wird dieses Problem für alle Sprachen beheben. Dies wirkt sich nicht auf die erfolgreiche Installation von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aus. 

#### <a name="full-text-search"></a>Volltextsuche

- In diesem Release sind nicht alle Filter verfügbar, einschließlich Filter für Office-Dokumente. Eine Liste aller unterstützten Filter finden Sie unter [Install SQL Server Full-Text Search on Linux (Installieren der SQL Server-Volltextsuche unter Linux)](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- Das Paket **mssql-server-is** wird in diesem Release nicht für SUSE unterstützt. Es wird derzeit für Ubuntu und Red Hat Enterprise Linux (RHEL) unterstützt.

- Mit [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] unter Linux CTP 2.1 Refresh und höher können [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Pakete ODBC-Verbindungen unter Linux verwenden. Diese Funktion wurde mit den Treibern von [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] und MySQL ODBC getestet, sollte jedoch auch mit einem Unicode-Treiber verwendet werden können, der der ODBC-Spezifikation entspricht. Zur Entwurfszeit können Sie entweder einen DSN oder eine Verbindungszeichenfolge angeben, um eine Verbindung mit den ODBC-Daten herzustellen. Sie können aber auch die Windows-Authentifizierung verwenden. Weitere Informationen hierzu finden Sie im [Blogbeitrag mit der Ankündigung zur ODBC-Unterstützung unter Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Die folgenden Features werden in diesem Release nicht unterstützt, wenn Sie SSIS-Pakete unter Linux ausführen:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]-Katalogdatenbank
  - Geplante Paketausführung des SQL Agent-Diensts
  - Windows-Authentifizierung
  - Drittanbieterkomponenten
  - Change Data Capture (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scale Out
  - Azure Feature Pack für SSIS
  - Hadoop- und HDFS-Unterstützung
  - Microsoft Connector for SAP BW

Eine Liste der integrierten SSIS-Komponenten, die derzeit nicht unterstützt oder nur bedingt unterstützt werden, finden Sie unter [Limitations and known issues for SSIS on Linux (Einschränkungen und bekannte Probleme für SSIS unter Linux)](sql-server-linux-ssis-known-issues.md#components).

Weitere Informationen zu SSIS unter Linux finden Sie in den folgenden Artikeln:
-   [Blog post announcing SSIS support for Linux (Blogbeitrag mit Ankündigung der SSIS-Unterstützung für Linux)](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Install SQL Server Integration Services (SSIS) on Linux (Installieren von SSIS (SQL Server Integration Services) unter Linux)](sql-server-linux-setup-ssis.md)
-   [Extract, transform, and load data on Linux with SSIS (Extrahieren, Transformieren und Laden von Daten unter Linux mit SSIS)](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

Die folgenden Einschränkungen gelten für [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] unter Windows mit Verbindung zu [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] für Linux.

- Wartungspläne werden nicht unterstützt.

- Verwaltungs-Data Warehouse und der Datensammler in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] werden nicht unterstützt. 

- Benutzeroberflächenkomponenten von [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], die über Optionen für die Windows-Authentifizierung oder für Windows-Ereignisprotokolle verfügen, funktionieren unter Linux nicht. Sie können diese Features mit anderen Optionen (z. B. SQL-Anmeldungen) weiterhin verwenden. 

- Die Anzahl beizubehaltender Protokolldateien kann nicht geändert werden.

## <a name="next-steps"></a>Nächste Schritte

In den folgenden Schnellstarts finden Sie Informationen zu den ersten Schritten:

- [Installieren unter Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Installation unter SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Installation unter Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ausführen unter Docker](quickstart-install-connect-ubuntu.md)
- [Provision a SQL VM in Azure (Bereitstellen einer SQL-VM in Azure)](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Ausführen und Verbinden – Cloud](quickstart-install-connect-clouds.md)

Antworten auf häufig gestellte Fragen finden Sie unter [Häufig gestellte Fragen zu SQL Server unter Linux](sql-server-linux-faq.md).
