---
title: 'Identifizieren von Schlüsselspalten mithilfe von SQL: Key-Feldern (SQLXML 4.0) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nesting XML results
- proper nesting in results [SQLXML]
- sql:key-fields
- XSD schemas [SQLXML], key columns
- identifying key columns [SQLXML]
- annotated XSD schemas, key columns
- key columns [SQLXML]
- relationships [SQLXML], key columns
- hierarchical relationships [SQLXML]
- key-fields annotation
ms.assetid: 1a5ad868-8602-45c4-913d-6fbb837eebb0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc3c063da7bb9133f8687a908c4bd7e0e13bae8f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2019
ms.locfileid: "66013820"
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>Identifizieren von Schlüsselspalten mithilfe von sql:key-Feldern (SQLXML 4.0)
  Wenn eine XPath-Abfrage für ein XSD-Schema angegeben wird, ist die Schlüsselinformationen in den meisten Fällen erforderlich, um richtige Schachtelung im Ergebnis zu erhalten. Durch die Angabe der `sql:key-fields`-Anmerkung lässt sich sicherstellen, dass die entsprechende Hierarchie generiert wird.  
  
> [!NOTE]  
>  Um die richtige Schachtelung sicherzustellen, wird empfohlen, `sql:key-fields` für diejenigen Elemente anzugeben, die Tabellen zugeordnet werden. Das erzeugte XML wird durch die Anordnung des zugrunde liegenden Resultsets beeinflusst. Wenn `sql:key-fields` nicht angegeben wird, hat das generierte XML unter Umständen nicht das richtige Format.  
  
 Der Wert von `sql:key-fields` identifiziert die Spalte(n), welche die Zeilen in der Beziehung eindeutig identifiziert bzw. identifizieren. Wenn mehrere Spalten zur eindeutigen Identifizierung einer Zeile erforderlich sind, werden die Spaltenwerte jeweils durch ein Leerzeichen voneinander getrennt.  
  
 Verwenden Sie die `sql:key-fields` -Anmerkung verwenden, wenn ein Element enthält eine  **\<SQL: Relationship >** , die zwischen dem Element und einem untergeordneten Element definiert ist jedoch nicht den Primärschlüssel der Tabelle, die in angegeben ist das übergeordnete Element.  
  
## <a name="examples"></a>Beispiele  
 Es müssen bestimmte Anforderungen erfüllt sein, damit aus den folgenden Beispielen funktionierende Beispiele erstellt werden können. Weitere Informationen finden Sie unter [Anforderungen für die Ausführung von SQLXML-Beispielen](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. Erzeugen der entsprechenden Schachtelung, wenn \<SQL: Relationship > nicht genügend Informationen bereitstellt  
 Dieses Beispiel zeigt, wo `sql:key-fields` angegeben werden muss.  
  
 Betrachten Sie folgendes Schema. Das Schema gibt eine hierarchische Beziehung zwischen der  **\<Reihenfolge >** und  **\<Kunden >** Elemente, in denen die  **\<Reihenfolge >** ist das übergeordnete Element und die  **\<Kunden >** -Element untergeordnet ist.  
  
 Die  **\<SQL: Relationship >** Tag wird verwendet, um die über-/ unterordnungsbeziehung geben. In diesem Tag wird CustomerID als übergeordneter Schlüssel identifiziert, der auf die untergeordnete CustomerID-Schlüsselspalte in der Sales.Customer-Tabelle verweist. Die Informationen in  **\<SQL: Relationship >** reicht nicht aus, um Zeilen in der übergeordneten Tabelle (Sales.SalesOrderHeader) eindeutig zu identifizieren. Ohne die `sql:key-fields`-Anmerkung wird daher eine ungenaue Hierarchie generiert.  
  
 Mit `sql:key-fields` angegeben  **\<Reihenfolge >** eindeutig identifiziert die Anmerkung die Zeilen im übergeordneten Element (Sales.SalesOrderHeader-Tabelle) und die untergeordneten Elemente werden unter dem übergeordneten Element.  
  
 Das ist das Schema:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrdCust"  
        parent="Sales.SalesOrderHeader"  
        parent-key="CustomerID"  
        child="Sales.Customer"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
               sql:key-fields="SalesOrderID">  
   <xsd:complexType>  
     <xsd:sequence>  
     <xsd:element name="Customer" sql:relation="Sales.Customer"   
                       sql:relationship="OrdCust"  >  
       <xsd:complexType>  
         <xsd:attribute name="CustID" sql:field="CustomerID" />  
         <xsd:attribute name="SoldBy" sql:field="SalesPersonID" />  
       </xsd:complexType>  
     </xsd:element>  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name= "CustomerID" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>So erstellen Sie ein funktionstüchtiges Beispiel für dieses Schema  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen KeyFields1.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen KeyFields1T.xml im gleichen Verzeichnis, in dem Sie KeyFields1.xml gespeichert haben. Die XPath-Abfrage in der Vorlage gibt alle dem  **\<Reihenfolge >** Elemente, deren CustomerID-Wert kleiner als 3.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="KeyFields1.xml">  
            /Order[@CustomerID < 3]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (KeyFields1.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields1.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [Verwenden von ADO zum Ausführen von SQLXML-Abfragen](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Im Folgenden wird ein Teil des Resultsets aufgeführt:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
    <Order SalesOrderID="43860" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="44501" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="45283" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    .....  
</ROOT>  
```  
  
### <a name="b-specifying-sqlkey-fields-to-produce-proper-nesting-in-the-result"></a>B. Angeben der sql:key-Felder, um die richtige Schachtelung im Ergebnis zu erzeugen  
 Im folgenden Schema, es gibt keine durch festgelegte Hierarchie  **\<SQL: Relationship >** . Das Schema erfordert trotzdem die Angabe der `sql:key-fields`-Anmerkung, um Mitarbeiter in der HumanResources.Employee-Tabelle eindeutig zu identifizieren.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="HumanResources.Employee" sql:key-fields="EmployeeID" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Title">  
          <xsd:complexType>  
            <xsd:simpleContent>  
              <xsd:extension base="xsd:string">  
                 <xsd:attribute name="EmployeeID" type="xsd:integer" />  
              </xsd:extension>  
            </xsd:simpleContent>  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>So erstellen Sie ein funktionstüchtiges Beispiel für dieses Schema  
  
1.  Kopieren Sie den oben stehenden Schemacode, und fügen Sie ihn in eine Textdatei ein. Speichern Sie die Datei unter dem Dateinamen KeyFields2.xml.  
  
2.  Kopieren Sie die folgende Vorlage, und fügen Sie sie in eine Textdatei ein. Speichern Sie die Datei unter dem Namen KeyFields2T.xml im gleichen Verzeichnis, in dem Sie KeyFields2.xml gespeichert haben. Die XPath-Abfrage in der Vorlage gibt alle dem  **\<HumanResources.Employee >** Elemente:  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="KeyFields2.xml">  
        /HumanResources.Employee  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     Der für das Zuordnungsschema (KeyFields2.xml) angegebene Verzeichnispfad bezieht sich auf das Verzeichnis, in dem die Vorlage gespeichert wird. Es kann auch ein absoluter Pfad angegeben werden. Beispiel:  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields2.xml"  
    ```  
  
3.  Erstellen und verwenden Sie das SQLXML 4.0-Testskript (Sqlxml4test.vbs), um die Vorlage auszuführen.  
  
     Weitere Informationen finden Sie unter [Verwenden von ADO zum Ausführen von SQLXML-Abfragen](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Dies ist das Ergebnis:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <HumanResources.Employee>  
    <Title EmployeeID="1">Production Technician - WC60</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="2">Marketing Assistant</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="3">Engineering Manager</Title>   
  </HumanResources.Employee>  
  ...  
</ROOT>  
```  
  
  
