---
title: XQuery und statische Typisierung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, static typing
- static typing
- checking static types
- inference [XQuery]
ms.assetid: d599c791-200d-46f8-b758-97e761a1a5c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 5ad42a174f558202544650fb1580574f290d4466
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946081"
---
# <a name="xquery-and-static-typing"></a>XQuery und statische Typisierung
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery ist in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] eine statisch typisierte Sprache. Sie gibt bei der Abfragekompilierung einen Typfehler aus, wenn ein Ausdruck einen Wert zurückliefert, dessen Typ oder Kardinalität von einer bestimmten Funktion oder einem Operator nicht angenommen wird. Darüber hinaus kann eine Überprüfung des statischen Typs auch erkennen, ob ein Pfadausdruck eines typisierten XML-Dokuments falsch typisiert ist. Der XQuery-Compiler realisiert zuerst die Normalisierungsphase, in der die impliziten Vorgänge, wie die Atomisierung, hinzugefügt werden. Anschließend erfolgen die Inferenz und die Überprüfung des statischen Typs.  
  
## <a name="static-type-inference"></a>Inferenz des statischen Typs  
 Die Inferenz des statischen Typs ermittelt den Rückgabetyp eines Ausdrucks. Hierbei wird aus den statischen Typen der Eingabeparameter und aus der statischen Semantik des Vorgangs der statische Typ des Ergebnisses abgeleitet. Beispiel: Der statische Typ des Ausdrucks 1 + 2,3 wird wie folgt abgeleitet:  
  
-   Der statische Typ von 1 ist **xs: Integer** und der statische Typ von 2,3 ist **xs: decimal**. Auf der Grundlage der dynamischen Semantik, die statische Semantik des der **+** Vorgang konvertiert die ganze Zahl in eine Dezimalzahl ist, und klicken Sie dann eine Dezimalzahl zurückgibt. Der abgeleitete statische Typ wäre dann **xs: decimal**.  
  
 Für nicht typisierte XML-Instanzen gibt es spezielle Typen, mit deren Hilfe angegeben wird, dass die Daten nicht typisiert sind. Diese Information wird bei der Überprüfung des statischen Typs und zur Durchführung bestimmter impliziter Datentypkonvertierungen verwendet.  
  
 Bei typisierten Daten wird der Eingabetyp aus der XML-Schemaauflistung abgeleitet, die die XML-Datentypinstanz einschränkt. Wenn das Schema nur Elemente vom Typ ermöglicht z. B. **xs: Integer**, die Ergebnisse eines pfadausdrucks, der dieses Element wird auf NULL oder mehr Elemente des Typs **xs: Integer**. Dies wird derzeit durch einen Ausdruck wie z. B. ausgedrückt `element(age,xs:integer)*` , in dem das Sternchen (\*) die Kardinalität des resultierenden Typs angibt. In diesem Beispiel ist der Ausdruck möglicherweise NULL oder mehr Elemente des Namens "Age" und Typ **xs: Integer**. Weitere Kardinalitäten sind genau 1 und werden mit den Typnamen alone, NULL oder einem ausgedrückt und mit einem Fragezeichen ( **?** ), und 1 oder mehr und durch ein Pluszeichen ( **+** ) .  
  
 In manchen Fällen kann die Inferenz des statischen Typs ableiten, dass ein Ausdruck immer eine leere Zeichenfolge zurückliefert. Z. B. wenn ein Pfadausdruck in ein typisierter XML-Datentyp sucht nach einer \<Name > Element in eine \<Kunden >-Element (/ Customer/Name), aber das Schema ist nicht zulässig. eine \<Name > in eine \<Kunden >, inferenz des statischen Typs folgert, dass das Ergebnis leer sein wird. Dies wird verwendet, um fehlerhafte Abfragen erkannt und wird als ein statischer Fehler, gemeldet werden, es sei denn, der Ausdruck wurde () oder **Daten (())** .  
  
 Die detaillierten Inferenzregeln werden in der formalen Semantik der XQuery-Spezifikation angegeben. Microsoft hat diese nur geringfügig für typisierte XML-Datentypinstanzen angepasst. Die wichtigste Änderung zum Standard besteht darin, dass der implizite Dokumentknoten den Typ der XML-Datentypinstanz kennt. Aus diesem Grund wird ein Pfadausdruck der Form /age auf der Grundlage dieser Information exakt typisiert.  
  
 Mithilfe von [SQL Server Profiler-Vorlagen und Berechtigungen](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md), sehen Sie die statischen Typen im Rahmen einer Abfragekompilierung zurückgeliefert. Dazu muss die Ablaufverfolgung das XQuery Static Type-Ereignis in der TSQL-Ereigniskategorie aufweisen.  
  
## <a name="static-type-checking"></a>Überprüfung des statischen Typs  
 Die Überprüfung des statischen Typs stellt sicher, dass bei der Ausführung zur Laufzeit nur Werte des für den Vorgang passenden Typs empfangen werden. Da die Typen nicht zur Laufzeit geprüft werden müssen, können potenzielle Fehler zu einem frühen Zeitpunkt der Kompilierung festgestellt werden. Dies verbessert die Leistung. Die statische Typisierung setzt jedoch voraus, dass der Verfasser der Abfrage diese sorgfältiger formuliert.  
  
 Folgende Typen können verwendet werden:  
  
-   Typen, die durch eine Funktion oder einen Vorgang explizit zugelassen werden.  
  
-   Ein Untertyp eines explizit zugelassenen Typs.  
  
 Untertypen werden auf der Grundlage der Untertypisierungsregeln definiert, um Ableitungen durch Beschränkung oder Erweiterung des XML-Schemas zu verwenden. Ein Typ S ist beispielsweise ein Untertyp von T, wenn alle Werte, die den Typ S besitzen, auch Instanzen des Typs T sind.  
  
 Darüber hinaus sind alle Ganzzahlwerte auf der Grundlage der Typhierarchie des XML-Schemas auch Dezimalwerte. Nicht alle Dezimalwerte sind allerdings ganze Zahlen. Aus diesem Grund ist eine ganze Zahl ein Untertyp einer Dezimalzahl, aber nicht umgekehrt. Z. B. die **+** Vorgang lässt nur die Werte bestimmter Typen, z. B. die numerischen Typen **xs: Integer**, **xs: decimal**, **Xs: "float"** , und **xs: double**. Wenn Werte anderer Typen, z. B. **xs: String**, werden übergeben, die Operation einen Typfehler. Dies wird als strenge Typisierung bezeichnet. Werte anderer Typen, wie der Typ atomic, der untypisiertes XML kennzeichnet, können implizit in einen Wert eines Typs konvertiert werden, den die Operation zulässt. Dies wird als schwache Typisierung bezeichnet.  
  
 Wenn eine implizite Konvertierung notwendig ist, stellt eine anschließende Überprüfung des statischen Typs sicher, dass an eine Operation nur Werte des zugelassenen Typs mit der richtigen Kardinalität übergeben werden. Für "String" + 1 erkennt, dass der statische Typ von "String" **xs: String**. Da dies nicht für einen zulässigen Typ ist der **+** Vorgang ein Typfehler ausgelöst wird.  
  
 Wenn das Ergebnis eines beliebigen Ausdrucks E1 zu einem beliebigen Ausdruck E2 addiert wird (E1 + E2), bestimmt die Inferenz des statischen Typs zuerst die statischen Typen von E1 und E2 und prüft diese dann gegen die für den Vorgang zulässigen statischen Typen. Angenommen, der statische Typ von E1 entweder als eine **xs: String** oder **xs: Integer**, Überprüfung des statischen Typs einen Typfehler, auch wenn einige Werte zur möglicherweise zur Laufzeit ganze Zahlen sein. Die gleiche wäre der Fall, wenn der statische von E1 Typ **xs: Integer&#42;** . Da die **+** Vorgang akzeptiert nur genau einen Ganzzahlwert und E1 kann 0 (null) zurückgeben, oder mehr als 1, Überprüfung des statischen Typs ein Fehler ausgelöst.  
  
 Wie zuvor erwähnt, ermittelt die Typinferenz häufig einen Typ, der breiter angelegt ist, als dies dem Benutzer hinsichtlich des zu übergebenden Datentyps bekannt ist. In diesen Fällen muss der Benutzer die Abfrage neu schreiben. Die folgenden: Einige typische Fälle  
  
-   Der Typ folgert einen allgemeineren Typ, wie einen Untertyp oder eine Typvereinigung. Wenn der Typ atomic ist, müssen Sie den Datentypkonvertierungsausdruck oder die Konstruktorfunktion verwenden, um den tatsächlichen statischen Typ anzugeben. Wenn der abgeleitete Typ des Ausdrucks E1 eine Wahl zwischen ist z. B. **xs: String** oder **xs: Integer** und erfordert die Hinzufügung **xs: Integer**, Schreiben Sie `xs:integer(E1) + E2` anstelle von `E1+E2`. Dieser Ausdruck kann zur Laufzeit fehlschlagen, wenn ein String-Wert gefunden wird, kann nicht umgewandelt werden, um **xs: Integer**. Der Ausdruck wird jetzt jedoch die Überprüfung des statischen Typs durchlaufen. Dieser Ausdruck wird der leeren Sequenz zugeordnet.  
  
-   Aus dem Typ wird eine höhere Kardinalität abgeleitet, als die tatsächlich in den Daten enthaltene. Dies passiert häufig, da die **Xml** Datentyp kann mehr als ein Element der obersten Ebene enthalten, und eine XML-schemaauflistung dies nicht erzwingen kann. Um den statischen Typ zu reduzieren und sicherzustellen, dass stattdessen maximal ein Wert übergeben wird, müssen Sie das Positionsprädikat `[1]` verwenden. Beispiel: Um 1 zum Wert des Attributs `c` des Elements `b` unter dem Element der obersten Ebene zu addieren, müssen Sie `write (/a/b/@c)[1]+1` angeben. Zusätzlich können Sie mit einer XML-Schemaauflistung das Schlüsselwort DOCUMENT verwenden.  
  
-   Bei einigen Vorgängen geht bei der Inferenz die Typinformation verloren. Wird z. B. wenn der Typ eines Knotens kann nicht bestimmt werden, es **AnyType**. Dieser wird nicht implizit in irgendeinen anderen Typ umgewandelt. Das tritt am deutlichsten während der Navigation mithilfe der übergeordneten Achse auf. Sie sollten die Verwendung solcher Vorgänge vermeiden und die Abfrage neu schreiben, falls der Ausdruck einen statischen Typfehler erzeugt.  
  
## <a name="type-checking-of-union-types"></a>Typüberprüfung von Union-Typen  
 Union-Typen erfordern aufgrund der Typüberprüfung eine sorgfältige Handhabung. In den folgenden Beispielen sind zwei der Probleme dargestellt.  
  
### <a name="example-function-over-union-type"></a>Beispiel: Funktion für Union-Typ  
 Betrachten Sie eine Elementdefinition für <`r`> eines union-Typs:  
  
```  
<xs:element name="r">  
<xs:simpleType>  
   <xs:union memberTypes="xs:int xs:float xs:double"/>  
</xs:simpleType>  
</xs:element>  
```  
  
 XQuery-Kontext, die average-Funktion `fn:avg (//r)` einen statischen Fehler zurück, da der XQuery-Compiler Werte verschiedener Typen hinzugefügt werden kann (**xs: int**, **xs: float** oder **Xs: doppelte**) für die <`r`>-Elemente im Argument von **Fn:avg()** . Um dieses Problem zu beheben, müssen Sie den Funktionsaufruf als `fn:avg(for $r in //r return $r cast as xs:double ?)` umschreiben.  
  
### <a name="example-operator-over-union-type"></a>Beispiel: Operator für Union-Typ  
 Die Additionsoperation ('+') erfordert präzise Typen der Operanden. Als Ergebnis des Ausdrucks `(//r)[1] + 1` gibt einen statischen Fehler, die die zuvor beschriebenen Typdefinition für das Element <`r`>. Eine mögliche Lösung besteht im Umschreiben des Ausdrucks als as `(//r)[1] cast as xs:int? +1`, wobei das "?" das Auftreten von 0 oder 1 anzeigt. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] erfordert "cast as" mit "?", weil jede Umwandlung die leere Sequenz als ein Ergebnis von Laufzeitfehlern verursachen kann.  
  
## <a name="see-also"></a>Siehe auch  
 [XQuery-Sprachreferenz &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
