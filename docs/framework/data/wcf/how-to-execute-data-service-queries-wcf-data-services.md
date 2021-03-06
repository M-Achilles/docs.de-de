---
title: 'Vorgehensweise: Ausführen von Datendienst Abfragen (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- querying the data service [WCF Data Services]
- WCF Data Services, querying
- WCF Data Services, accessing data
ms.assetid: 62997821-e0c6-4c4d-9fb7-1273fb5e5d18
ms.openlocfilehash: 984bba9f31ddaee68c6997ba6da09a511e42b4ce
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70780065"
---
# <a name="how-to-execute-data-service-queries-wcf-data-services"></a>Vorgehensweise: Ausführen von Datendienst Abfragen (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] ermöglicht es Ihnen, mit den generierten Clientdatendienstklassen einen Datendienst aus einer .NET Framework-basierten Clientanwendung abzufragen. Für die Ausführung der Abfragen stehen folgende Methoden zur Verfügung:  
  
- Ausführen einer LINQ-Abfrage für die benannte <xref:System.Data.Services.Client.DataServiceQuery%601>-Instanz, die Sie aus dem <xref:System.Data.Services.Client.DataServiceContext>-Objekt abrufen, den das Tool `Add Data Service Reference` generiert.  
  
- Implizit durch Aufzählen über die benannte <xref:System.Data.Services.Client.DataServiceQuery%601>-Instanz, die Sie aus dem <xref:System.Data.Services.Client.DataServiceContext>-Objekt abrufen, den das Tool `Add Data Service Reference` generiert.  
  
- Explizit durch Aufrufen der <xref:System.Data.Services.Client.DataServiceContext.Execute%2A>-Methode für die <xref:System.Data.Services.Client.DataServiceQuery%601>-Instanz oder der <xref:System.Data.Services.Client.DataServiceQuery%601.BeginExecute%2A>-Methode für die asynchrone Ausführung.  
  
 Weitere Informationen finden Sie unter [Abfragen des Daten Dienstanbieter](querying-the-data-service-wcf-data-services.md).  
  
 Im Beispiel in diesem Thema werden der Northwind-Beispieldatendienst und automatisch generierte Client-Datendienstklassen verwendet. Dieser Dienst und die Client Daten Klassen werden erstellt, wenn Sie den [WCF Data Services Schnellstart](quickstart-wcf-data-services.md)ausführen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird gezeigt, wie Sie eine LINQ-Abfrage definieren und ausführen, die alle `Customers` für den Northwind-Datendienst zurückgibt.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersLinq](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomerslinq)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersLinq](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomerslinq)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird gezeigt, wie Sie den vom Tool `Add Data Service Reference` generierten Kontext verwenden, um eine Abfrage implizit auszuführen, die alle `Customers` für den Northwind-Datendienst zurückgibt. Der URI der angeforderten `Customers`-Entitätenmenge wird automatisch vom Kontext bestimmt. Die Abfrage wird implizit ausgeführt, wenn die Enumeration auftritt.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomers](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomers)]
 [!code-vb[Astoria Northwind Client#GetAllCustomers](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomers)]  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird gezeigt, wie Sie den <xref:System.Data.Services.Client.DataServiceContext> verwenden, um eine Abfrage explizit auszuführen, die alle `Customers` für den Northwind-Datendienst zurückgibt.  
  
 [!code-csharp[Astoria Northwind Client#GetAllCustomersExplicit](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#getallcustomersexplicit)]
 [!code-vb[Astoria Northwind Client#GetAllCustomersExplicit](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#getallcustomersexplicit)]  
  
## <a name="see-also"></a>Siehe auch

- [Vorgehensweise: Hinzufügen von Abfrage Optionen zu einer Datendienst Abfrage](how-to-add-query-options-to-a-data-service-query-wcf-data-services.md)
