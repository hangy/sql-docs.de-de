---
title: Verwenden der OUTPUT-Klausel mit OLE DB in SQL Server Native Client | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 53deeb99-c088-4fde-844b-b2d91d6de1eb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7f93f6dc2f8080775588168bfd6ca10733712b0
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789067"
---
# <a name="using-the-output-clause-with-ole-db-in-sql-server-native-client"></a>Verwenden der OUTPUT-Klausel mit OLE DB in SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Wenn Sie in einem INSERT-, UPDATE-, DELETE- oder MERGE-Befehl eine OUTPUT-Klausel verwenden, ist die Anzahl der betroffenen Zeilen nicht verfügbar. Die Anwendung muss die Anzahl von Zeilen im Rowset zählen, die von der OUTPUT-Klausel zurückgegeben werden.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen einer SQL Server Native Client OLE DB-Anbieteranwendung](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
