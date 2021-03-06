---
title: CancelBatch-Methode (ADO) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_CancelBatch
- Recordset15::CancelBatch
helpviewer_keywords:
- CancelBatch method [ADO]
ms.assetid: dbdc2574-e44e-4d95-b03d-4a5d9e9adf3c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f1c6a9f57d30b47641b9280e25a97336c28b0496
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920162"
---
# <a name="cancelbatch-method-ado"></a>CancelBatch-Methode (ADO)
Bricht eine ausstehende Batchaktualisierung ab.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
recordset.CancelBatchAffectRecords  
```  
  
#### <a name="parameters"></a>Parameter  
 *AffectRecords*  
 Optional. Ein [AffectEnum](../../../ado/reference/ado-api/affectenum.md) Wert, der angibt, wie viele Datensätze der **CancelBatch** Methode wirkt sich auf.  
  
## <a name="remarks"></a>Hinweise  
 Verwenden der **CancelBatch** Methode, um alle ausstehenden Updates in Abbrechen einer [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) im Modus "Batch-Update". Wenn die **Recordset** befindet sich im sofortupdatemodus Aufrufen **CancelBatch** ohne **AdAffectCurrent** wird ein Fehler generiert.  
  
 Wenn Sie den aktuellen Datensatz bearbeiten oder ein neues Datensatzes beim Aufrufen hinzufügen **CancelBatch**, ADO-ruft zunächst die [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Methode, um eine Abbrechen-zwischengespeicherte Änderungen. Danach alle ausstehenden Änderungen in der **Recordset** werden abgebrochen.  
  
 Der aktuelle Datensatz möglicherweise nicht bestimmbarer nach einer **CancelBatch** aufrufen, insbesondere dann, wenn Sie gerade einen neuen Datensatz hinzufügen würden. Aus diesem Grund ist es ratsam, legen Sie die Position des aktuelle Datensatzes an einem bekannten Speicherort in der **Recordset** nach der **CancelBatch** aufrufen. Beispielsweise rufen Sie die [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) Methode.  
  
 Wenn der Versuch zum Abbrechen der ausstehenden Updates ein Fehler auftritt, aufgrund eines Konflikts mit dem zugrunde liegenden Daten (z. B., wenn ein Datensatz von einem anderen Benutzer gelöscht wurde), gibt der Anbieter Warnungen an, die die [Fehler](../../../ado/reference/ado-api/errors-collection-ado.md) Auflistung jedoch nicht angehalten wird Ausführung des Programms. Ein Laufzeitfehler tritt auf, nur dann, wenn Konflikte für alle angeforderten Datensätze bestehen. Verwenden der [Filter](../../../ado/reference/ado-api/filter-property.md) Eigenschaft (**AdFilterAffectedRecords**) und die [Status](../../../ado/reference/ado-api/status-property-ado-recordset.md) Eigenschaft, um Datensätze mit Konflikten zu suchen.  
  
## <a name="applies-to"></a>Gilt für  
 [Recordset-Objekt (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Siehe auch  
 [UpdateBatch und CancelBatch-Methode – Beispiel (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [UpdateBatch und CancelBatch-Methode – Beispiel (VC++)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Cancel-Methode (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)   
 [Cancel-Methode (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)   
 [CancelUpdate-Methode (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [CancelUpdate-Methode (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Clear-Methode (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [LockType-Eigenschaft (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [UpdateBatch-Methode](../../../ado/reference/ado-api/updatebatch-method.md)
