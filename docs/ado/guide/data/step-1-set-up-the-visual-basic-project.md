---
title: 'Schritt 1: Einrichten von Visual Basic-Projekt | Microsoft-Dokumentation'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 77d3bfa5-fc9f-4a72-93b4-790c7d227988
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bd44990c38a30f26e682fbb7f1f6aef642043215
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924074"
---
# <a name="step-1-set-up-the-visual-basic-project"></a>Schritt 1: Einrichten des Visual Basic-Projekts
In diesem Szenario wird davon ausgegangen, dass Sie Microsoft Visual Basic 6.0, ADO 2.5 oder höher und Microsoft OLE DB-Anbieter für Internet Publishing auf Ihrem System installiert haben. Sie erstellen zunächst ein neues Projekt, und klicken Sie dann einige Steuerelemente hinzufügen, um das Standardformular in das Projekt.  
  
### <a name="to-create-an-ado-project"></a>So erstellen Sie ein ADO-Projekt:  
  
1.  Erstellen Sie in Microsoft Visual Basic, ein neues Standard-EXE-Projekt.  
  
2.  Wählen Sie im Menü Projekt verweisen.  
  
3.  Wählen Sie "Microsoft ActiveX Data Objects 2.5 Library", und klicken Sie auf OK.  
  
### <a name="to-insert-controls-on-the-main-form"></a>So fügen Sie Steuerelemente auf dem Hauptformular:  
  
1.  Fügen Sie ein ListBox-Steuerelement zu Form1 hinzu. Legen Sie die Name-Eigenschaft auf **IstMain**.  
  
2.  Fügen Sie ein anderes ListBox-Steuerelement zu Form1 hinzu. Legen Sie die Name-Eigenschaft auf **LstDetails**.  
  
3.  Fügen Sie ein TextBox-Steuerelement zu Form1 hinzu. Legen Sie die Name-Eigenschaft auf **TxtDetails**.  
  
## <a name="see-also"></a>Siehe auch  
 [Internet Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Schritt 2: Initialisieren der wichtigsten Listenfelder](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)
