---
title: Was sind Big Data-Cluster?
titleSuffix: SQL Server Big Data Clusters
description: Erfahren Sie mehr über [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] (Vorschau), die auf Kubernetes ausgeführt werden, und stellen Sie Optionen für die horizontale Skalierung von relationalen und HDFS-Daten bereit.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 296a39a59521441a8f3cd5b95bd8e61710fa568a
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532509"
---
# <a name="what-are-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Was sind [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]?

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Ab [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] können Sie mit [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] skalierbare Cluster von Containern für SQL Server, Spark und HDFS bereitstellen, die auf Kubernetes ausgeführt werden. Diese Komponenten werden nebeneinander ausgeführt, sodass Sie Big Data von Transact-SQL oder Spark lesen, schreiben und verarbeiten können, während Sie Ihre wichtigen relationalen Daten mit einem hohen Big-Data-Volumen problemlos kombinieren und analysieren können.

Weitere Informationen zu neuen Features und bekannten Problemen der neuesten Version finden Sie in den dazugehörigen [Versionshinweisen](release-notes-big-data-cluster.md).

## <a name="scenarios"></a>Szenarien

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] bieten Flexibilität bei der Interaktion mit Big Data. Sie können externe Datenquellen abfragen, Big Data in dem von SQL Server verwalteten HDFS speichern oder Daten aus mehreren externen Datenquellen über den Cluster abfragen. Die Daten können Sie dann für KI, Machine Learning und andere Analyseaufgaben verwenden. In den folgenden Abschnitten finden Sie weitere Informationen zu diesen Szenarios.

### <a name="data-virtualization"></a>Datenvirtualisierung

Mit [SQL Server-PolyBase](../relational-databases/polybase/polybase-guide.md) können [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] externe Datenquellen abfragen, ohne die Daten zu verschieben oder zu kopieren. [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] führt neue Connectors für Datenquellen ein.

![Datenvirtualisierung](media/big-data-cluster-overview/data-virtualization.png)

### <a name="data-lake"></a>Data Lake

Ein Big-Data-Cluster für SQL Server enthält einen skalierbaren HDFS-*Speicherpool*. Dieser kann verwendet werden, um Big Data zu speichern, die möglicherweise aus mehreren externen Quellen erfasst wird. Sobald die Big Data im HDFS im Big-Data-Cluster gespeichert wurden, können Sie die Daten analysieren und abfragen und mit ihren relationalen Daten kombinieren.

![Data Lake](media/big-data-cluster-overview/data-lake.png)

### <a name="scale-out-data-mart"></a>Data Mart mit horizontaler Skalierung

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] bieten Rechen- und Speicherkapazitäten für die horizontale Skalierung, um die Leistung bei der Analyse beliebiger Daten zu verbessern. Daten aus einer Vielzahl von Quellen können erfasst und auf *Datenpool*-Knoten als Cache zur weiteren Analyse verteilt werden.

![Data Mart](media/big-data-cluster-overview/data-mart.png)

### <a name="integrated-ai-and-machine-learning"></a>Integrierte KI und Machine Learning

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ermöglichen KI- und Machine Learning-Aufgaben für die Daten, die in HDFS-Speicherpools und den Datenpools gespeichert werden. Mithilfe von R, Python, Scala oder Java können Sie sowohl Spark als auch integrierte KI-Tools in SQL Server verwenden.

![KI und Machine Learning](media/big-data-cluster-overview/ai-ml-spark.png)

### <a name="management-and-monitoring"></a>Verwaltung und Überwachung

Verwaltung und Überwachung werden durch eine Kombination von Befehlszeilentools, APIs, Portalen und dynamischen Verwaltungssichten bereitgestellt.

Sie können Azure Data Studio dazu verwenden, eine Vielzahl von Aufgaben im Big-Data-Cluster auszuführen. Dies wird durch die neue **SQL Server 2019-Erweiterung (Vorschauversion)** ermöglicht. Diese Erweiterung bietet Folgendes:

- Integrierte Codeausschnitte für allgemeine Verwaltungsaufgaben.
- Möglichkeit zum Durchsuchen von HDFS, zum Hochladen von Dateien, zur Vorschau von Dateien und zum Erstellen von Verzeichnissen.
- Möglichkeit zum Erstellen, Öffnen und Ausführen von Jupyter-kompatiblen Notebooks.
- Datenvirtualisierungsassistent für eine vereinfachte Erstellung externer Datenquellen.

## <a id="architecture"></a> Architektur

Ein Big-Data-Cluster für SQL Server ist ein Cluster von Linux-Containern, die von [Kubernetes](https://kubernetes.io/docs/concepts/) orchestriert werden.

### <a name="kubernetes-concepts"></a>Kubernetes-Konzepte

Kubernetes ist ein Open-Source-Containerorchestrator, mit dem Sie Containerbereitstellungen nach Bedarf skalieren können. In der folgenden Tabelle sind einige wichtige Kubernetes-Termini definiert:

|||
|:--|:--|
| **Cluster** | Ein Kubernetes-Cluster ist eine Gruppe von Computern, die als Knoten bezeichnet werden. Ein Knoten steuert den Cluster und wird als Masterknoten bezeichnet. Die übrigen Knoten sind Workerknoten. Der Kubernetes-Master ist für die Verteilung der Arbeit auf die Worker und für die Überwachung der Clusterintegrität verantwortlich. |
| **Node** | Ein Knoten führt Containeranwendungen aus. Dabei kann es sich entweder um einen physischen oder einen virtuellen Computer handeln. Ein Kubernetes-Cluster kann eine Mischung aus Knoten von physischen und virtuellen Computern enthalten. |
| **Pod** | Ein Pod ist die unteilbare Bereitstellungseinheit von Kubernetes. Ein Pod ist eine logische Gruppe von einem oder mehreren Containern und zugeordneter Ressourcen, die zum Ausführen einer Anwendung erforderlich sind. Jeder Pod läuft auf einem Knoten. Ein Knoten kann einen oder mehrere Pods ausführen. Der Kubernetes-Master weist den Knoten im Cluster automatisch Pods zu. |
| &nbsp; ||

In [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] ist Kubernetes für den Zustand der [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] verantwortlich. Dabei erstellt und konfiguriert Kubernetes die Clusterknoten, weist den Knoten Pods zu und überwacht die Integrität des Clusters.

### <a name="big-data-clusters-architecture"></a>Architektur von Big-Data-Clustern

Das folgende Diagramm zeigt die Komponenten eines Big-Data-Clusters für SQL Server.

![Übersicht über die Architektur](media/big-data-cluster-overview/architecture-diagram-overview.png)

### <a id="controlplane"></a> Controller

Der Controller bietet Verwaltungs-und Sicherheitsfunktionen für den Cluster. Er enthält den Verwaltungsdienst, den Konfigurationsspeicher und andere Dienste auf Clusterebene wie Kibana, Grafana und Elasticsearch.

### <a id="computeplane"></a> Computepool

Der Computepool stellt Rechenressourcen für den Cluster bereit. Er enthält Knoten, auf denen Pods für SQL Server für Linux laufen. Die Pods im Computepool werden für bestimmte Verarbeitungsaufgaben in *SQL-Computeinstanzen* unterteilt. 

### <a id="dataplane"></a> Datenpool

Der Datenpool wird für Datenpersistenz und zum Zwischenspeichern verwendet. Der Datenpool besteht aus mindestens einem Pod, auf dem SQL Server für Linux ausgeführt wird. Er wird zum Erfassen von Daten aus SQL-Abfragen oder Spark-Aufträgen verwendet. Data Marts für SQL Server-Big-Data-Cluster werden im Datenpool persistent gespeichert. 

### <a name="storage-pool"></a>Speicherpool

Der Speicherpool besteht aus den Speicherpoolpods, bestehend aus SQL Server für Linux, Spark und HDFS. Alle Speicherknoten in einem Big-Data-Cluster für SQL Server sind Mitglieder eines HDFS-Clusters.

> [!TIP]
> Einen detaillierten Einblick in die Architektur und Installation von Big-Data-Clustern erhalten Sie unter [Workshop: Microsoft-Architektur für [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zur Bereitstellung von Big Data-Clustern für SQL Server finden Sie unter [Erste Schritte mit Big Data-Clustern für SQL Server](deploy-get-started.md).
