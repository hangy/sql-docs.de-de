---
title: Zugreifen auf Zeilen in einem hierarchischen Recordset | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e73b2ca96cc5e7eb7683b72aa19fd59a318b8596
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67926357"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>Zugreifen auf Zeilen in einem hierarchischen Recordset (Beispiel)
Das folgende Beispiel zeigt die Schritte in einer hierarchischen Zeilen mit Zugriff zum [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **Recordset** Objekte aus der **Autoren** und **Titleauthor** Tabellen nach Autor-ID verknüpft sind

2.  Die äußere Schleife zeigt die vor-und Nachnamen des Autors, Status und Identifikation.

3.  Das angefügte **Recordset** für jede Zeile abgerufen wird, aus der [Felder](../../../ado/reference/ado-api/fields-collection-ado.md) Auflistung zugewiesen *RstTitleAuthor*.

4.  Die innere Schleife zeigt vier Felder aus jeder Zeile in der angefügten **Recordset**.

 Die [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) -Eigenschaftensatz auf **"false"** zur Veranschaulichung, damit Sie sehen im Kapitel über das Ändern explizit in jeder Iteration der äußeren Schleife. Um das Codebeispiel effizienter zu gestalten, können Sie die Zuweisung in Schritt 3 vor der ersten Zeile in Schritt 2: verschieben, damit die Zuweisung wird nur einmal ausgeführt. Legen Sie dann die [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) Eigenschaft **"true"** , sodass *RstTitleAuthor* implizit automatisch ändert und im entsprechenden Kapitel immer *Rst* in eine neue Zeile verschoben wird.

## <a name="example"></a>Beispiel

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>Siehe auch
 [Daten strukturieren (Übersicht)](../../../ado/guide/data/data-shaping-overview.md) [Field-Objekt](../../../ado/reference/ado-api/field-object.md) [Fields-Collection (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [formale Grammatik für Formen](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft Data Shaping Service für OLE DB (ADO-Dienstanbieter) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [erforderliche Anbieter für die Datenstrukturierung](../../../ado/guide/data/required-providers-for-data-shaping.md) [Shape APPEND-Klausel](../../../ado/guide/data/shape-append-clause.md) [Befehle in Form Allgemeine](../../../ado/guide/data/shape-commands-in-general.md) [Shape COMPUTE-Klausel](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic for Applications-Funktionen](../../../ado/guide/data/visual-basic-for-applications-functions.md)
