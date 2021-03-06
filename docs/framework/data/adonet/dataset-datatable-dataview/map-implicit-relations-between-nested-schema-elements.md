---
title: Zuordnen von impliziten Beziehungen zwischen geschachtelten Schemaelementen
ms.date: 03/30/2017
ms.assetid: 6b25002a-352e-4d9b-bae3-15129458a355
ms.openlocfilehash: f4b1b9e45f0cda976719b991c336463e0af05f12
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70784437"
---
# <a name="map-implicit-relations-between-nested-schema-elements"></a>Zuordnen von impliziten Beziehungen zwischen geschachtelten Schemaelementen
Ein XSD-Schema (XML Schema Definition Language) kann komplexe Typen aufweisen, die ineinander geschachtelt sind. In diesem Fall wendet der Zuordnungsprozess die Standardzuordnung an und erstellt folgende Elemente im <xref:System.Data.DataSet>:  
  
- Eine Tabelle für jeden der komplexen Typen (übergeordnet und untergeordnet).  
  
- Wenn für das übergeordnete Element keine UNIQUE-Einschränkung vorhanden ist, eine zusätzliche Primärschlüssel Spalte pro Tabellendefinition mit dem Namen *TableName*_id, wobei *TableName* der Name der übergeordneten Tabelle ist.  
  
- Eine PRIMARY KEY-Einschränkung für die übergeordnete Tabelle, die die zusätzliche Spalte als Primärschlüssel identifiziert (indem die **IsPrimaryKey** -Eigenschaft auf **true**festgelegt wird). Die Einschränkung wird mit "Constraint\#" benannt, wobei \# für 1, 2, 3 usw. steht. Beispielsweise lautet der Standardname für die erste Einschränkung "Constraint1".  
  
- Eine Fremdschlüsseleinschränkung für die untergeordnete Tabelle, die die zusätzliche Spalte als den auf den Primärschlüssel der übergeordneten Tabelle verweisenden Fremdschlüssel identifiziert. Die Einschränkung hat den Namen *ParentTable_ChildTable* , wobei " *centtable* " der Name der übergeordneten Tabelle und " *ChildTable* " der Name der untergeordneten Tabelle ist.  
  
- Eine Datenbeziehung zwischen übergeordneten und untergeordneten Tabellen.  
  
 Das folgende Beispiel zeigt ein Schema, bei dem **OrderDetail** ein untergeordnetes Element der **Reihenfolge**ist.  
  
```xml  
<xs:schema id="MyDataSet" xmlns=""   
            xmlns:xs="http://www.w3.org/2001/XMLSchema"   
            xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">  
  
 <xs:element name="MyDataSet" msdata:IsDataSet="true">  
   <xs:complexType>  
     <xs:choice maxOccurs="unbounded">  
       <xs:element name="Order">  
         <xs:complexType>  
          <xs:sequence>  
            <xs:element name="OrderNumber" type="xs:string" />  
            <xs:element name="EmpNumber" type="xs:string" />  
            <xs:element name="OrderDetail">  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="OrderNo" type="xs:string" />  
                  <xs:element name="ItemNo" type="xs:string" />  
                </xs:sequence>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
         </xs:complexType>  
       </xs:element>  
     </xs:choice>  
   </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
 Der Prozess für die XML-Schema Zuordnung erstellt Folgendes im **DataSet**:  
  
- Eine **Bestellung** und eine **Order Detail** -Tabelle.  
  
    ```  
    Order(OrderNumber, EmpNumber, Order_Id)  
    OrderDetail(OrderNo, ItemNo, Order_Id)  
    ```  
  
- Eine Unique-Einschränkung für die **Order** -Tabelle. Beachten Sie, dass die **IsPrimaryKey** -Eigenschaft auf **true**festgelegt ist.  
  
    ```  
    ConstraintName: Constraint1  
    Type: UniqueConstraint  
    Table: Order  
    Columns: Order_Id   
    IsPrimaryKey: True  
    ```  
  
- Eine FOREIGN KEY-Einschränkung für die **Order Detail** -Tabelle.  
  
    ```  
    ConstraintName: Order_OrderDetail  
    Type: ForeignKeyConstraint  
    Table: OrderDetail  
    Columns: Order_Id   
    RelatedTable: Order  
    RelatedColumns: Order_Id   
    ```  
  
- Eine Beziehung zwischen der **Order** -Tabelle und der **Order Detail** -Tabelle. Die Eigenschaft " **schsted** " für diese Beziehung wird auf " **true** " festgelegt, da die Elemente **Order** und **Order Detail** im Schema scht sind.  
  
    ```  
    ParentTable: Order  
    ParentColumns: Order_Id   
    ChildTable: OrderDetail  
    ChildColumns: Order_Id   
    ParentKeyConstraint: Constraint1  
    ChildKeyConstraint: Order_OrderDetail  
    RelationName: Order_OrderDetail  
    Nested: True  
    ```  
  
## <a name="see-also"></a>Siehe auch

- [Generieren von DataSet-Beziehungen aus einem XML-Schema (XSD)](generating-dataset-relations-from-xml-schema-xsd.md)
- [Zuordnen von XML Schema-Schlüsseleinschränkungen (XSD) zu DataSet-Einschränkungen](mapping-xml-schema-xsd-constraints-to-dataset-constraints.md)
- [Übersicht über ADO.NET](../ado-net-overview.md)
