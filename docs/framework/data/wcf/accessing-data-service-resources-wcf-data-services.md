---
title: Zugreifen auf Datendienstressourcen (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, querying
- getting started, WCF Data Services
- querying the data service [WCF Data Service]
- WCF Data Services, getting started
- WCF Data Services, accessing data
ms.assetid: 9665ff5b-3e3a-495d-bf83-d531d5d060ed
ms.openlocfilehash: d18ec4fd57f2437ca936074e8dcf70f17f09b877
ms.sourcegitcommit: 005980b14629dfc193ff6cdc040800bc75e0a5a5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2019
ms.locfileid: "70991118"
---
# <a name="accessing-data-service-resources-wcf-data-services"></a>Zugreifen auf Datendienstressourcen (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]unterstützt [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] , um Ihre Daten als Feed mit Ressourcen verfügbar zu machen, die durch URIs adressierbar sind. Diese Ressourcen werden entsprechend den Entitäts Beziehungs Konventionen des [Entity Data Model](../adonet/entity-data-model.md)dargestellt. In diesem Modell stellen Entitäten Funktionsbausteine von Daten, die Datentypen sind, in einer Anwendungsdomäne dar, z. B. Kunden, Bestellungen, Artikel und Produkte. Das Zugreifen auf und Ändern von Entitätsdaten erfolgt mit der REST ( Representational State Transfer)-Semantik, speziell mit den Standard-HTTP-Verben GET, PUT, POST und DELETE.  
  
## <a name="addressing-resources"></a>Adressieren von Ressourcen  
 In [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] werden alle vom Datenmodell verfügbar gemachten Daten mit einem URI adressiert. Der folgende URI gibt z. b. einen Feed zurück, bei dem es sich um die Entitätenmenge Customers handelt, die Einträge für alle Instanzen des Customer-Entitäts Typs enthält:  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers>
  
 Entitäten verfügen über besondere Eigenschaften, die als Entitätsschlüssel bezeichnet werden. Ein Entitätsschlüssel wird verwendet, um eine einzelne Entität in einer Entitätenmenge eindeutig zu identifizieren. Dies ermöglicht es Ihnen, eine bestimmte Instanz eines Entitätstyps in der Entitätenmenge zu adressieren. Der folgende URI gibt z. B. einen Eintrag für eine bestimmte Instanz des Customer-Entitätstyps mit dem Schlüsselwert `ALFKI` zurück:  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')>
  
 Primitive und komplexe Eigenschaften einer Entitätsinstanz können auch einzeln behandelt werden. Der folgende URI gibt z. B. ein XML-Element zurück, das den `ContactName`-Eigenschaftswert für einen bestimmten Kunden enthält:  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/ContactName>
  
 Wenn Sie den `$value`-Endpunkt in den vorherigen URI einschließen, wird in der Antwortnachricht nur der Wert der primitiven Eigenschaft zurückgegeben. Im folgenden Beispiel wird nur die Zeichenfolge "Maria Anders" ohne das XML-Element zurückgegeben:  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/ContactName/$value>
  
 Beziehungen zwischen Entitäten werden im Datenmodell durch Zuordnungen definiert. Diese Zuordnungen ermöglichen es Ihnen, mithilfe der Navigationseigenschaften einer Entitätsinstanz verknüpfte Entitäten zu adressieren. Eine Navigationseigenschaft kann entweder eine einzelne verknüpfte Entität (bei einer n:1-Beziehung) oder einen Satz von verknüpften Entitäten (bei einer 1:n-Beziehung) zurückgeben. Der folgende URI gibt z. B. einen Feed zurück, bei dem es sich um den Satz aller Bestellungen handelt, die sich auf einen bestimmten Kunden beziehen:  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders>
  
 Gewöhnlich bidirektionale Beziehungen werden mithilfe eines Paars von Navigationseigenschaften dargestellt. Als Gegenstück zu der Beziehung im vorherigen Beispiel gibt der folgende URI einen Verweis auf die Customer-Entität zurück, zu der eine bestimmte Order-Entität gehört:  
  
<https://services.odata.org/Northwind/Northwind.svc/Orders(10643)/Customer>
  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]ermöglicht es Ihnen außerdem, Ressourcen auf der Grundlage der Ergebnisse von Abfrage Ausdrücken zu adressieren. Dies ermöglicht es, Ressourcen Sätze auf der Grundlage eines ausgewerteten Ausdrucks zu filtern. Der folgende URI filtert z. B. die Ressourcen, um nur die Bestellungen für den angegebenen Kunden zurückzugeben, die seit dem 22. September 1997 ausgeliefert wurden:  
  
<https://services.odata.org/Northwind/Northwind.svc/Customers( "ALFKI")/Bestellungen? $Filter = ShippedDate gt DateTime "1997-09-22t00:00:00" >
  
 Weitere Informationen finden [Sie unter odata: URI-](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/)Konventionen.
  
## <a name="system-query-options"></a>Systemabfrageoptionen  
 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]definiert einen Satz von System Abfrage Optionen, mit denen Sie herkömmliche Abfrage Vorgänge für Ressourcen ausführen können, z. b. Filtern, Sortieren und Paging. Der folgende URI gibt z. b. den Satz aller `Order` Entitäten zusammen `Order_Detail` mit verknüpften Entitäten zurück, deren Postleitzahlen nicht auf `100`enden:  
  
<https://services.odata.org/Northwind/Northwind.svc/Orders? $Filter = not EndsWith (shipPostalCode, ' 100 ') & $Expand = Order_Details & $OrderBy = ShipCity >
  
 Die Einträge des zurückgegebenen Feeds werden zudem nach dem Wert der ShipCity-Eigenschaft der Bestellungen geordnet.  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]unterstützt die [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] folgenden System Abfrage Optionen:  
  
|Abfrageoption|Beschreibung|  
|------------------|-----------------|  
|`$orderby`|Definiert im zurückgegebenen Feed eine Standardsortierreihenfolge für Entitäten. Die folgende Abfrage sortiert den zurückgegebenen Kundenfeed nach Landkreis und Ort:<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$orderby=Country,City>|  
|`$top`|Gibt die Anzahl der Entitäten an, die in den zurückgegebenen Feed eingeschlossen werden soll. Im folgenden Beispiel werden die ersten zehn Kunden übersprungen und die folgenden zehn zurückgegeben:<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$skip=10&$top=10>|  
|`$skip`|Gibt die Anzahl der Entitäten an, die vor dem Beginn der Rückgabe der Entitäten im Feed übersprungen werden sollen. Im folgenden Beispiel werden die ersten zehn Kunden übersprungen und die folgenden zehn zurückgegeben:<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$skip=10&$top=10>|  
|`$filter`|Definiert einen Ausdruck, der die im Feed zurückgegebenen Entitäten anhand bestimmter Kriterien filtert. Diese Abfrageoption unterstützt einen Satz logischer Vergleichsoperatoren, arithmetische Operatoren und vordefinierte Abfragefunktionen, die zur Auswertung des Filterausdrucks verwendet werden. Im folgenden Beispiel werden alle Bestellungen zurückgegeben, deren Postleitzahlen nicht mit "100" enden:<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Orders? $Filter = nicht EndsWith (shipPostalCode, ' 100 ') >|  
|`$expand`|Gibt an, welche verknüpften Entitäten von der Abfrage zurückgegeben werden. Verknüpfte Entitäten sind entweder als Feed oder als Eintrag in der von der Abfrage zurückgegebenen Entität inline enthalten. Im folgenden Beispiel werden die Bestellungen des Kunden "ALFKI" zusammen mit den Artikeldetails der einzelnen Bestellungen zurückgegeben:<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers('ALFKI')/Orders?$expand=Order_Details>|  
|`$select`|Gibt eine Projektion an, die die Eigenschaften der Entität definiert, die in der Projektion zurückgegeben werden. In der Standardeinstellung werden alle Eigenschaften einer Entität in einem Feed zurückgegeben. Die folgende Abfrage gibt nur drei Eigenschaften der `Customer`-Entität zurück:<br /><br /> <https://services.odata.org/Northwind/Northwind.svc/Customers?$select=CustomerID,CompanyName,City>|  
|`$inlinecount`|Fordert an, dass die Anzahl der im Feed zurückgegebenen Entitäten im Feed enthalten sein muss.|  
  
## <a name="addressing-relationships"></a>Behandeln von Beziehungen  
 Zusätzlich zur Adressierung von Entitätenmengen und [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] Entitäts Instanzen ermöglicht Ihnen auch die Adressierung der Zuordnungen, die Beziehungen zwischen Entitäten darstellen. Diese Funktionalität ist erforderlich, um eine Beziehung zwischen zwei Entitätsinstanzen erstellen oder ändern zu können, z. B. das Versandunternehmen, das sich auf eine angegebene Bestellung in der Northwind-Beispieldatenbank bezieht. [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]unterstützt `$link` einen-Operator, um die Zuordnungen zwischen Entitäten zu adressieren Der folgende URI wird z. B. in einer HTTP PUT-Anforderungsnachricht angegeben, um das Versandunternehmen für die angegebene Bestellung in ein neues Versandunternehmen zu ändern.  
  
<https://services.odata.org/Northwind/Northwind.svc/Orders(10643)/$links/Shipper>
  
 Weitere Informationen finden Sie im Abschnitt `3.2. Addressing Links between Entries` unter [odata: URI-](https://www.odata.org/documentation/odata-version-2-0/uri-conventions/)Konventionen.
  
## <a name="consuming-the-returned-feed"></a>Verwenden des zurückgegebenen Feeds  
 Der URI [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] einer Ressource ermöglicht es Ihnen, vom Dienst verfügbar gemachte Entitäts Daten zu adressieren. Wenn Sie einen URI in das Adressfeld eines Webbrowsers eingeben, wird eine [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] Feed-Darstellung der angeforderten Ressource zurückgegeben. Weitere Informationen finden Sie in der [WCF Data Services Schnellstart](quickstart-wcf-data-services.md)Anleitung. Obwohl ein Webbrowser nützlich sein kann, um zu testen, ob eine Datendienst Ressource die erwarteten Daten zurückgibt, erfolgt der Zugriff auf Produktionsdaten Dienste, die auch Daten erstellen, aktualisieren und löschen können, im Allgemeinen über Anwendungscode oder Skriptsprachen auf einer Webseite. Weitere Informationen finden Sie unter [Verwenden eines Daten Dienstanbieter in einer Client Anwendung](using-a-data-service-in-a-client-application-wcf-data-services.md).  
  
## <a name="see-also"></a>Siehe auch

- [Open Data Protocol-Website](https://www.odata.org/)
