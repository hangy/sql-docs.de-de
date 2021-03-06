---
title: Verwalten von Notebooks in Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Erfahren Sie, wie Sie Notebooks in Azure Data Studio verwalten. Hierzu gehört das Öffnen und Speichern von Notebooks sowie das Ändern der Verbindung mit Ihrem Big Data-Cluster.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5417166ea69abe726f47b6bf2adede4b937d5b00
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958284"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Verwalten von Notebooks in Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Dieser Artikel zeigt, wie Sie Notebookdateien in Azure Data Studio mit SQL Server 2019 (Vorschauversion) öffnen und speichern. Sie erfahren außerdem, wie Sie die Verbindung mit Ihrem SQL Server-Big Data-Cluster ändern.

## <a name="prerequisites"></a>Voraussetzungen

In diesem Artikel wird davon ausgegangen, dass Sie bereits über ein Notebook verfügen, das Sie in Azure Data Studio verwenden möchten. Wenn Sie ein Notebook erstellen möchten, finden Sie weitere Informationen unter [Verwenden von Notebooks in SQL Server 2019 (Vorschauversion)](notebooks-guidance.md). Um Notebooks in Azure Data Studio verwenden zu können, müssen folgende Voraussetzungen erfüllt sein:

- [Bereitgestellter Big Data-Cluster](quickstart-big-data-cluster-deploy.md)
- [Big Data-Tools für SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Erweiterung von SQL Server 2019**
   - **kubectl**

## <a name="open-a-notebook"></a>Öffnen eines Notebooks

Es gibt verschiedene Möglichkeiten, das Dialogfeld **Notebook öffnen** anzuzeigen. Die können das Menü „Datei“, das Dashboard und die Befehlspalette verwenden. Diese Methoden werden in den nächsten Abschnitten beschrieben.

### <a name="file-menu"></a>Menü „Datei“

Wählen Sie im Menü „Datei“ die Option **Datei öffnen** aus (STRG+O unter Windows und BEFEHLSTASTE+O unter Mac).

![Anzeigen des Dialogfelds „Datei öffnen“ durch Auswählen von „Datei öffnen“](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>Dashboard

Klicken Sie auf dem Dashboard auf **Notebook öffnen**, um das Dialogfeld „Datei öffnen“ anzuzeigen.

![Anzeigen des Dialogfelds „Datei öffnen“ durch Auswählen von „Notebook öffnen“ auf dem Dashboard](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>Befehlspalette

Verwenden Sie den Befehl **File: Open** aus der Befehlspalette, indem Sie STRG+UMSCHALT+P (unter Windows) oder BEFEHLSTASTE+P (unter Mac) drücken.

![Anzeigen des Dialogfelds „Datei öffnen“ durch Eingeben von „File:Open“ in der Befehlspalette](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Speichern eines Notebooks

Zurzeit gibt es nur eine Möglichkeit, ein Notebook zu speichern. Sie müssen in der Symbolleiste des Notebooks die Option **Speichern** auswählen.

![Speichern einer Datei durch Klicken auf „Speichern“ in der Symbolleiste des Notebooks](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> Mit den folgenden Methoden werden Änderungen an Notebooks derzeit nicht gespeichert:
>
> - Befehle **Datei speichern**, **Datei speichern unter...** und **Alle Dateien speichern** im Menü „Datei“.
> - **File: Save**-Befehle, die in der Befehlspalette eingegeben werden.

## <a name="change-the-big-data-cluster"></a>Ändern des Big Data-Clusters

So ändern Sie den SQL Server-Big Data-Cluster für ein Notebook:

1. Klicken Sie in der Symbolleiste des Notebooks auf das Menü **Anfügen an**.

   ![Klicken auf das Menü „Anfügen an“ in der Symbolleiste des Notebooks](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. Klicken Sie im Menü **Anfügen an** auf einen Server.

   ![Auswählen eines Servers im Menü „Anfügen an“](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Notebooks in Azure Data Studio finden Sie unter [Verwenden von Notebooks in SQL Server 2019 (Vorschauversion)](notebooks-guidance.md).