---
title: Hinzufügen von vorhandenen Einschränkungen zu einem "DataSet"
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.openlocfilehash: db072692eba4044e854f25ff2c7f8c9960714018
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70785114"
---
# <a name="adding-existing-constraints-to-a-dataset"></a>Hinzufügen von vorhandenen Einschränkungen zu einem "DataSet"
Die **Fill** -Methode von **DataAdapter** füllt <xref:System.Data.DataSet> nur mit Tabellen Spalten und Zeilen aus einer Datenquelle. Obwohl Einschränkungen häufig von der Datenquelle festgelegt werden, fügt die **Fill** -Methode diese Schema Informationen nicht zum  **Standardmäßig DataSet** . Zum Auffüllen eines **DataSets** mit vorhandenen Primärschlüssel-Einschränkungs Informationen aus einer Datenquelle können Sie entweder die **FillSchema** -Methode des **DataAdapter**-Objekts oder die **MissingSchemaAction** -Eigenschaft des **DataAdapter** -Objekts festlegen. an **AddWithKey** , bevor **Fill**aufgerufen wird. Dadurch wird sichergestellt, dass die PRIMARY KEY-Einschränkungen im **DataSet** den Werten in der Datenquelle entsprechen. Informationen zu Fremdschlüssel Einschränkungen sind nicht eingeschlossen und müssen explizit erstellt werden, wie in [datensierungseinschränkungen](./dataset-datatable-dataview/datatable-constraints.md)gezeigt.  
  
 Wenn einem **DataSet** Schema Informationen hinzugefügt werden, bevor es mit Daten gefüllt wird, wird sichergestellt, <xref:System.Data.DataTable> dass PRIMARY KEY-Einschränkungen in den Objekten im **DataSet**enthalten sind. Wenn zusätzliche Aufrufe zum Auffüllen des **DataSets** durchgeführt werden, werden die Primärschlüssel Spalten-Informationen verwendet, um neue Zeilen aus der Datenquelle mit den aktuellen Zeilen in jeder Datentabelle abzugleichen. die aktuellen Daten in den **Tabellen werden mit**Daten aus der Datenquelle. Ohne die Schema Informationen werden die neuen Zeilen aus der Datenquelle an das **DataSet**angefügt, sodass doppelte Zeilen entstehen.  
  
> [!NOTE]
> Wenn eine Spalte in einer Datenquelle als automatische Inkrementierung identifiziert wird, die **FillSchema** -Methode oder die **Fill** -Methode mit der **MissingSchemaAction** -Eigenschaft **AddWithKey**, erstellt eine **datacolenn** mit einer **AutoIncrement** -Eigenschaft. Legen Sie `true`auf fest. Sie müssen jedoch die Werte **AutoIncrementStep** und **AutoIncrementSeed** selbst festlegen. Weitere Informationen zum automatischen Inkrementieren von Spalten finden Sie unter [Erstellen von AutoIncrement-Spalten](./dataset-datatable-dataview/creating-autoincrement-columns.md).  
  
 Die Verwendung von **FillSchema** oder das Festlegen der **MissingSchemaAction** auf **AddWithKey** erfordert zusätzliche Verarbeitung an der Datenquelle, um Informationen zur Primärschlüssel Spalte zu ermitteln. Diese zusätzlichen Verarbeitungsschritte können zu einem Leistungsabfall führen. Wenn Sie die Primärschlüsselinformationen zur Entwurfszeit kennen, empfiehlt es sich, zum Erzielen einer optimalen Leistung die Primärschlüsselspalte(n) explizit in der richtigen Reihenfolge anzugeben. Informationen zum expliziten Festlegen von Primärschlüssel Informationen für eine Tabelle finden Sie unter [Definieren von primär Schlüsseln](./dataset-datatable-dataview/defining-primary-keys.md).  
  
 Im folgenden Codebeispiel wird gezeigt, wie einem **DataSet** mithilfe von **FillSchema**Schema Informationen hinzugefügt werden.  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers")  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers");  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
 Im folgenden Codebeispiel wird veranschaulicht, wie einem **DataSet** mithilfe der **MissingSchemaAction. AddWithKey** -Eigenschaft der **Fill** -Methode Schema Informationen hinzugefügt werden.  
  
```vb  
Dim custDataSet As DataSet = New DataSet()  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
DataSet custDataSet = new DataSet();  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
## <a name="handling-multiple-result-sets"></a>Umgang mit mehreren Resultsets  
 Wenn der **DataAdapter** auf mehrere Resultsets stößt, die von **SelectCommand**zurückgegeben werden, werden mehrere Tabellen im **DataSet**erstellt. Den Tabellen wird ein NULL basierter inkrementeller Standardname von **Tabelle** *N*zugewiesen, beginnend mit **Table** anstelle von "Table0". Wenn ein Tabellenname als Argument an die **FillSchema** -Methode übergeben wird, erhalten die Tabellen den NULL basierten inkrementellen Namen **TableName** *N*, beginnend mit **TableName** anstelle von "TableName0".  
  
> [!NOTE]
> Wenn die **FillSchema** -Methode des **OleDbDataAdapter** -Objekts für einen Befehl aufgerufen wird, der mehrere Resultsets zurückgibt, werden nur die Schema Informationen aus dem ersten Resultset zurückgegeben. Beim Zurückgeben von Schema Informationen für mehrere Resultsets mit dem **OleDbDataAdapter**wird empfohlen, dass Sie die **MissingSchemaAction-Aktion** von **AddWithKey** angeben und die Schema Informationen beim Aufrufen der **Füllung** abrufen. anzuwenden.  
  
## <a name="see-also"></a>Siehe auch

- [DataAdapters und DataReaders](dataadapters-and-datareaders.md)
- [DataSets, DataTables und DataViews](./dataset-datatable-dataview/index.md)
- [Abrufen und Ändern von Daten in ADO.NET](retrieving-and-modifying-data.md)
- [Übersicht über ADO.NET](ado-net-overview.md)
