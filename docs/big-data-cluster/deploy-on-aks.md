---
title: Konfigurieren von Azure Kubernetes Service
titleSuffix: SQL Server big data clusters
description: Erfahren Sie, wie Sie Azure Kubernetes Service (AKS) für die Bereitstellung von [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] konfigurieren können.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 9a3b52a87927eb85d638ed97c1e145efd50602bf
ms.sourcegitcommit: 6413b7495313830ad1ae5aefe0c09e8e7a284b07
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016890"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>Konfigurieren von Azure Kubernetes Service für die Bereitstellung von Big-Data-Clustern für SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

In diesem Artikel erfahren Sie, wie Sie Azure Kubernetes Service (AKS) für die Bereitstellung von [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] konfigurieren können.

AKS vereinfacht das Erstellen, Konfigurieren und Verwalten von VM-Clustern, die mithilfe eines Kubernetes-Clusters für die Ausführung von Containeranwendungen vorkonfiguriert werden. Dadurch können Sie Ihre eigenen Kenntnisse oder die der stetig wachsenden Community einsetzen, um containerbasierte Anwendungen in Microsoft Azure bereitzustellen und zu verwalten.

In diesem Artikel wird ausführlich beschrieben, wie Sie mithilfe der Azure CLI Kubernetes für AKS bereitstellen können. Wenn Sie nicht über ein Azure-Abonnement verfügen, können Sie ein kostenloses Konto erstellen, bevor Sie beginnen.

> [!TIP]
> Sie können auch ein Skript erstellen, mit dem die Bereitstellung von AKS und eines Big-Data-Clusters in einem Schritt ausgeführt wird. Weitere Informationen finden Sie im Artikel zur Verwendung eines [Python-Skripts](quickstart-big-data-cluster-deploy.md) oder im Artikel zur Nutzung eines [Notebooks](deploy-notebooks.md) in Azure Data Studio.

## <a name="prerequisites"></a>Voraussetzungen

- [Stellen Sie die Big-Data-Tools für SQL Server 2019 bereit:](deploy-big-data-tools.md)
   - **Kubectl**
   - **Azure Data Studio**
   - **Erweiterung für SQL Server 2019**
   - **Azure CLI**

- Mindestens Version 1.13 für Kubernetes-Server. Für AKS müssen Sie den Parameter `--kubernetes-version` verwenden, um eine andere als die Standardversion anzugeben.

- Sie können einen einzelnen Knoten oder einen AKS-Cluster mit mehreren Knoten verwenden, um eine erfolgreiche Bereitstellung und eine optimale Leistung bei der Überprüfung grundlegender Szenarios auf AKS zu gewährleisten:
   - 8 vCPUs, die auf alle Knoten verteilt sind
   - 64 GB Arbeitsspeicher pro VM
   - mindestens 24 angefügte Datenträger, die auf alle Knoten verteilt sind

   > [!TIP]
   > Die Azure-Infrastruktur bietet mehrere Größenoptionen für VMS. Weitere Informationen zu den Optionen, die für die Region zur Verfügung, für die Sie die Bereitstellung planen, [finden Sie hier](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).

## <a name="create-a-resource-group"></a>Erstellen einer Ressourcengruppe

Eine Azure-Ressourcengruppe ist eine logische Gruppe, in der Azure-Ressourcen bereitgestellt und verwaltet werden. In den folgenden Schritten wird erläutert, wie Sie sich bei Azure anmelden und eine Ressourcengruppe für den AKS-Cluster erstellen können.

1. Führen Sie über die Eingabeaufforderung den folgenden Befehl aus, und befolgen Sie die Anweisungen, um sich bei Ihrem Azure-Abonnement anzumelden:

    ```azurecli
    az login
    ```

1. Wenn Sie über mehrere Abonnements verfügen, können Sie alle Abonnements anzeigen lassen, indem Sie den folgenden Befehl ausführen:

   ```azurecli
   az account list
   ```

1. Wenn Sie zu einem anderen Abonnement wechseln möchten, können Sie den folgenden Befehl ausführen:

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. Erstellen Sie mithilfe des Befehls **az group create** eine Ressourcengruppe. Im folgenden Beispiel wird eine Ressourcengruppe mit dem Namen `sqlbdcgroup` am Standort `westus2` erstellt.

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>Überprüfen von verfügbaren Kubernetes-Versionen

Verwenden Sie die neuste verfügbare Kubernetes-Version. Welche Version die neuste ist, hängt von dem Standort ab, für den Sie den Cluster bereitstellen möchten. Der folgende Befehl gibt die Kubernetes-Versionen zurück, die an einem bestimmten Standort verfügbar sind.

Aktualisieren Sie das Skript, bevor Sie den Befehl ausführen. Ersetzen Sie `<Azure data center>` durch den Standort des Clusters.

   **Bash**

   ```bash
   az aks get-versions \
   --location <Azure data center> \
   --query orchestrators \
   --o table
   ```

   **PowerShell**

   ```powershell
   az aks get-versions `
   --location <Azure data center> `
   --query orchestrators `
   --o table
   ```

Wählen Sie die neuste für Ihren Cluster verfügbare Version aus. Notieren Sie sich die Versionsnummer. Sie werden sie im nächsten Schritt benötigen.

## <a name="create-a-kubernetes-cluster"></a>Erstellen eines Kubernetes-Clusters

1. Erstellen Sie mithilfe des Befehls [az aks create](https://docs.microsoft.com/cli/azure/aks) einen Kubernetes-Cluster in AKS. Im folgenden Beispiel wird ein Kubernetes-Cluster mit dem Namen *kubcluster* und einem Linux-Agent-Knoten der Größe **Standard_L8s** erstellt.

   Ersetzen Sie `<version number>` vor dem Ausführen des Skripts durch die Versionsnummer, die Sie im vorherigen Schritt ermittelt haben.

   Stellen Sie sicher, dass Sie den AKS-Cluster in derselben Ressourcengruppe erstellen, die Sie in den vorherigen Abschnitten verwendet haben.

   **Bash:**

   ```bash
   az aks create --name kubcluster \
   --resource-group sqlbdcgroup \
   --generate-ssh-keys \
   --node-vm-size Standard_L8s \
   --node-count 1 \
   --kubernetes-version <version number>
   ```

   **PowerShell:**

   ```powershell
   az aks create --name kubcluster `
   --resource-group sqlbdcgroup `
   --generate-ssh-keys `
   --node-vm-size Standard_L8s `
   --node-count 1 `
   --kubernetes-version <version number>
   ```

   Sie können die Anzahl der Kubernetes-Agent-Knoten erhöhen oder verringern, indem Sie den Wert für `--node-count <n>` ändern. Dabei steht `<n>` für die Anzahl der Agent-Knoten, die Sie verwenden möchten. Dies schließt nicht den Kubernetes-Masterknoten ein, der im Hintergrund von AKS verwaltet wird. Im vorherigen Beispiel wird nur ein einzelner Knoten zu Evaluierungszwecken verwendet.

   Nach einigen Minuten wird der Befehl abgeschlossen und gibt Informationen über den Cluster im JSON-Format zurück.

   > [!TIP]
   > Wenn beim Erstellen des Clusters in AKS eine Fehlermeldung angezeigt wird, lesen Sie sich den Abschnitt [Problembehandlung](#troubleshoot) dieses Artikels durch.

1. Speichern Sie die JSON-Ausgabe des vorherigen Befehls für später.

## <a name="connect-to-the-cluster"></a>Herstellen einer Verbindung mit dem Cluster

1. Führen Sie den Befehl [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) aus, um kubectl für die Herstellung einer Verbindung mit dem Kubernetes-Cluster zu konfigurieren. In diesem Schritt werden Anmeldeinformationen heruntergeladen, und die kubectl-CLI wird für deren Verwendung konfiguriert.

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. Überprüfen Sie die Verbindung mit Ihrem Cluster mithilfe des Befehls [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands), um eine Liste der Clusterknoten zurückzugeben.  Wenn Sie beispielsweise über einen Master- und drei Agent-Knoten verfügen, wird die folgende Ausgabe angezeigt.

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> Problembehandlung

Wenn Sie die oben genannten Befehle verwenden und Probleme beim Erstellen einer AKS-Instanz auftreten sollten, probieren Sie Folgendes aus:

- Vergewissern Sie sich, dass Sie die [neueste Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) installiert haben.
- Führen Sie dieselben Schritte noch einmal mit einer anderen Ressourcengruppe und einem anderen Clusternamen.

## <a name="next-steps"></a>Nächste Schritte

In diesem Artikel wurde beschrieben, wie Sie einen Kubernetes-Cluster in AKS konfigurieren können. Der nächste Schritt ist die Bereitstellung eines Big-Data-Clusters für SQL Server 2019 im AKS-Cluster. Weitere Informationen zum Bereitstellen von Big-Data-Clustern finden Sie im folgenden Artikel:

[Bereitstellen von [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] in Kubernetes](deployment-guidance.md)
