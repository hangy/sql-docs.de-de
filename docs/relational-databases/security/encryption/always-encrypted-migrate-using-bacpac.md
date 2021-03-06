---
title: Exportieren und Importieren von Datenbanken mit Always Encrypted | Microsoft-Dokumentation
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1f2f44a6cf1172b779160d4ee17e584c7a7b2452
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595805"
---
# <a name="export-and-import-databases-using-always-encrypted"></a>Exportieren und Importieren von Datenbanken mit Always Encrypted 
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

In diesem Artikel wird beschrieben, wie Sie Datenbanken exportieren und importieren, die mit [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) geschützte Spalten enthalten.

Beim Exportieren einer Datenbank werden alle in verschlüsselten Spalten gespeicherten Daten aus der Datenbank in verschlüsselter Form (ciphertext) abgerufen und in der resultierenden [BACPAC-Datei](../../data-tier-applications/data-tier-applications.md) abgelegt. Die resultierende BACPAC-Datei enthält außerdem die Metadaten der Always Encrypted-Schlüssel.

Wenn Sie eine BACPAC-Datei in eine Datenbank importieren, werden die verschlüsselten Daten der BACPAC-Datei ebenso in die Datenbank geladen, und die Metadaten der Always Encrypted-Schlüssel werden neu erstellt. 

Wenn eine Anwendung dazu konfiguriert ist, in der Quelldatenbank (die, die Sie exportiert haben) gespeicherte verschlüsselte Spalten abzufragen, können Sie die Anwendung ganz einfach für Abfragen der verschlüsselten Daten in der Zieldatenbank aktivieren, da die Schlüssel in beiden Datenbanken identisch sind.

Weitere Informationen zum Exportieren und Importieren einer Datenbank finden Sie hier:
- [Exportieren einer Datenebenenanwendung](../../data-tier-applications/export-a-data-tier-application.md)
- [Importieren einer BACPAC-Datei zum Erstellen einer neuen Benutzerdatenbank](../../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)
- [Exportieren einer Azure SQL-Datenbank in eine BACPAC-Datei](https://docs.microsoft.com/azure/sql-database/sql-database-export)
- [Importieren einer BACPAC-Datei in eine Datenbank in Azure SQL-Datenbank](https://docs.microsoft.com/azure/sql-database/sql-database-import)
- [SqlPackage.exe](../../../tools/sqlpackage.md)

## <a name="permissions-for-migrating-databases-with-encrypted-columns"></a>Berechtigungen für das Migrieren von Datenbanken mit verschlüsselten Spalten

Sie benötigen für die Quelldatenbank die Berechtigungen *ALTER ANY COLUMN MASTER KEY* und *ALTER ANY COLUMN ENCRYPTION KEY* . Sie benötigen für die Zieldatenbank die Berechtigungen *ALTER ANY COLUMN MASTER KEY*, *ALTER ANY COLUMN ENCRYPTION KEY*, *VIEW ANY COLUMN MASTER KEY DEFINITION* und *VIEW ANY COLUMN ENCRYPTION DEFINITION*.

Sie benötigen keinen Zugriff auf die Spaltenhauptschlüssel, die für die verschlüsselten Spalten konfiguriert sind, da die Daten während der Export- und Importvorgänge verschlüsselt bleiben.

## <a name="next-steps"></a>Next Steps
- [Entwickeln von Anwendungen mit Always Encrypted](always-encrypted-client-development.md)

## <a name="see-also"></a>Weitere Informationen
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Sichern und Wiederherstellen von Datenbanken mit Always Encrypted](always-encrypted-migrate-using-backup-restore.md)
- [Migrieren von Daten zu oder aus Spalten mithilfe von Always Encrypted mit dem SQL Server-Import/Export-Assistenten](always-encrypted-migrate-using-import-export-wizard.md)
- [Massenladen von verschlüsselten Daten in Spalten mithilfe von Always Encrypted](migrate-sensitive-data-protected-by-always-encrypted.md)