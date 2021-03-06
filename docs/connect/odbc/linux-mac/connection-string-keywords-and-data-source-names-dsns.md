---
title: Herstellen einer Verbindung mit SQL Server | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source names
- connection string keywords
- DSNs
ms.assetid: f95cdbce-e7c2-4e56-a9f7-8fa3a920a125
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 486d26dd3afeb91cb43181875e22592fb482af5f
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702806"
---
# <a name="connecting-to-sql-server"></a>Herstellen einer Verbindung mit SQL Server
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

In diesem Artikel wird beschrieben, wie Sie eine Verbindung mit einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Datenbank herstellen können.  
  
## <a name="connection-properties"></a>Verbindungseigenschaften  

Informationen zu den Schlüsselwörtern und Attributen der Verbindungs Zeichenfolge, die unter Linux und Mac unterstützt werden, finden Sie unter [DSN](../../../connect/odbc/dsn-connection-string-attribute.md)

> [!IMPORTANT]  
> Geben Sie beim Herstellen einer Verbindung mit einer Datenbank, welche Datenbankspiegelung verwendet (oder einen Failoverpartner hat), nicht den Namen der Datenbank in der Verbindungszeichenfolge an. Schicken Sie stattdessen den Befehl **use** _database_name_, um sich mit der Datenbank zu verbinden, bevor Sie Ihre Abfragen ausführen.  
  
Der Wert, der an das **Driver** -Schlüsselwort übermittelt wird, kann einer der folgenden sein:  
  
-   Der Name, den Sie verwendet haben, als Sie den Treiber installiert haben.

-   Der Pfad zur Treiberbibliothek, welcher in der Vorlagen-INI-Datei angegeben war, die wiederum verwendet wurde, um den Treiber zu installieren.  

Um einen DSN zu erstellen, erstellen Sie (falls erforderlich), und bearbeiten Sie die`.odbc.ini` Datei **~ ODBC.in** (in Ihrem Basisverzeichnis) für einen Benutzer-DSN, der nur `/etc/odbc.ini` für den aktuellen Benutzer verfügbar ist, oder für einen System-DSN (Administratorrechte erforderlich). Hier folgt eine Beispieldatei, welche die erforderlichen Einträge für eine DSN zeigt:  

```  
[MSSQLTest]  
Driver = ODBC Driver 13 for SQL Server  
Server = [protocol:]server[,port]  
#   
# Note:  
# Port is not a valid keyword in the odbc.ini file  
# for the Microsoft ODBC driver on Linux or macOS
#  
```  

Sie können optional das Protokoll und den Port für die Verbindung mit dem Server angeben. Beispiel: **Server = TCP: Server**_Name_ **, 12345**. Beachten Sie, dass das einzige Protokoll, das von Linux-und `tcp`macOS-Treibern unterstützt wird.

Um eine Verbindung mit einer benannten Instanz auf einem statischen Port herzustellen, verwenden Sie <b>Server=</b>*servername*,**port_number**. Das Herstellen einer Verbindung mit einem dynamischen Port wird vor Version 17.4 nicht unterstützt.

Alternativ können Sie die DSN-Informationen auch einer Vorlagendatei hinzufügen und den folgenden Befehl ausführen, um sie `~/.odbc.ini` hinzuzufügen:
 - **odbcinst -i -s -f** _template_file_  
 
Sie können überprüfen, ob der Treiber funktioniert, `isql` indem Sie verwenden, um die Verbindung zu testen, oder Sie können den folgenden Befehl verwenden:
 - **bcp master.INFORMATION_SCHEMA.TABLES out OutFile.dat -S <server> -U <name> -P <password>**  

## <a name="using-secure-sockets-layer-ssl"></a>Secure Sockets Layer (SSL) verwenden  
Sie können Secure Sockets Layer (SSL) verwenden, um Verbindungen mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]zu verschlüsseln. SSL schützt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Benutzernamen und -Kennwörter über das Netzwerk. SSL überprüft auch die Identität des Servers, um Schutz vor „man-in-the-middle“-Attacken (MITM) zu bieten.  

Das Aktivieren der Verschlüsselung erhöht die Sicherheit auf Kosten der Leistung.

Weitere Informationen finden Sie unter [Verschlüsseln von Verbindungen zu SQL Server](https://go.microsoft.com/fwlink/?LinkId=220900) und [Verwenden von Verschlüsselung ohne Überprüfung](https://docs.microsoft.com/sql/relational-databases/native-client/features/using-encryption-without-validation).

Unabhängig von den Einstellungen für **Encrypt** und **TrustServerCertificate**werden die Serveranmeldeinformationen (Benutzername und Kennwort) immer verschlüsselt. Die folgende Tabelle zeigt den Effekt der Einstellungen für **Encrypt** und **TrustServerCertificate** .  

||**TrustServerCertificate=no**|**TrustServerCertificate=yes**|  
|-|-------------------------------------|------------------------------------|  
|**Encrypt=no**|Das Serverzertifikat wird nicht überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind nicht verschlüsselt.|Das Serverzertifikat wird nicht überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind nicht verschlüsselt.|  
|**Encrypt=yes**|Serverzertifikat wird überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind verschlüsselt.<br /><br />Der Name (oder die IP-Adresse) in einem allgemeinen Namen (Common Name (CN)) oder alternativen Antragsstellernamen (Subject Alternative Name (SAN)) in einem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -SSL-Zertifikat sollte genau mit dem Servernamen (oder der IP-Adresse), der in der Verbindungszeichenfolge angegeben wurde, übereinstimmen.|Das Serverzertifikat wird nicht überprüft.<br /><br />Zwischen dem Client und dem Server verschickte Daten sind verschlüsselt.|  

Standardmäßig überprüfen verschlüsselte Verbindungen immer das Zertifikat des Servers. Wenn Sie jedoch eine Verbindung mit einem Server herstellen, der über ein selbst signiertes Zertifikat verfügt, `TrustServerCertificate` können Sie auch die Option zum Umgehen der Überprüfung des Zertifikats mit der Liste der vertrauenswürdigen Zertifizierungsstellen hinzufügen:  

```  
Driver={ODBC Driver 13 for SQL Server};Server=ServerNameHere;Encrypt=YES;TrustServerCertificate=YES  
```  
  
SSL verwendet die OpenSSL-Bibliothek. Die folgende Tabelle zeigt die minimalen unterstützten Versionen von OpenSSL und die Zertifikatsvertrauensspeicherorte für jede Plattform:

|Platform|Minimale OpenSSL-Version|Standard-Zertifikatsvertrauensspeicherort|  
|------------|---------------------------|--------------------------------------------|
|Debian 10|1.1.1|/etc/ssl/certs|
|Debian 9|1.1.0|/etc/ssl/certs|
|Debian 8.71|1.0.1|/etc/ssl/certs|
|OS X 10,11, macOS 10,12, 10,13, 10,14|1.0.2|/usr/local/etc/openssl/certs|
|Red Hat Enterprise Linux 8|1.1.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 7|1.0.1|/etc/pki/tls/cert.pem|
|Red Hat Enterprise Linux 6|1.0.0-10|/etc/pki/tls/cert.pem|
|SuSE Linux Enterprise 15|1.1.0|/etc/ssl/certs|
|SuSE Linux Enterprise 11, 12|1.0.1|/etc/ssl/certs|
|Ubuntu 18.10, 19.04|1.1.1|/etc/ssl/certs|
|Ubuntu 18.04|1.1.0|/etc/ssl/certs|
|Ubuntu 16.04, 16.10, 17.10|1.0.2|/etc/ssl/certs|
|Ubuntu 14.04|1.0.1|/etc/ssl/certs|

Sie können auch die Verschlüsselung in der Verbindungs Zeichenfolge `Encrypt` mithilfe der Option angeben, wenn Sie **SQLDriverConnect** verwenden, um eine Verbindung herzustellen.

## <a name="adjusting-the-tcp-keep-alive-settings"></a>Anpassen der TCP-Keep-Alive-Einstellungen

Beginnend mit dem ODBC-Treiber 17,4, wie oft der Treiber Keep-Alive-Pakete sendet und Sie erneut überträgt, wenn eine Antwort nicht empfangen wird, ist konfigurierbar.
Fügen Sie zum Konfigurieren von die folgenden Einstellungen entweder dem Abschnitt des Treibers `odbcinst.ini`in oder dem Abschnitt des DSN in `odbc.ini`hinzu. Beim Herstellen einer Verbindung mit einem DSN verwendet der Treiber die Einstellungen im Abschnitt des DSN, sofern vorhanden. Andernfalls werden die Einstellungen im Abschnitt des Treibers in `odbcinst.ini`verwendet, wenn nur eine Verbindung mit einer Verbindungs Zeichenfolge hergestellt wird. Wenn die Einstellung an keinem der Orte vorhanden ist, verwendet der Treiber den Standardwert.

- `KeepAlive=<integer>`steuert, wie oft TCP versucht, zu überprüfen, ob eine Verbindung im Leerlauf noch intakt ist, indem ein Keep-Alive-Paket gesendet wird. Der Standardwert ist **30** Sekunden.

- `KeepAliveInterval=<integer>`bestimmt das Intervall, das Keep-Alive-Neuübertragungen trennt, bis eine Antwort empfangen wird.  Der Standardwert beträgt **1** Sekunde.


## <a name="see-also"></a>Weitere Informationen  
[Installieren des Microsoft ODBC Driver for SQL Server unter Linux und macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)  
[Programmierrichtlinien](../../../connect/odbc/linux-mac/programming-guidelines.md)
