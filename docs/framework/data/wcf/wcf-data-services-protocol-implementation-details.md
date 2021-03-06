---
title: Details der WCF Data Services-Protokollimplementierung
ms.date: 03/30/2017
ms.assetid: 712d689b-fada-4cbb-bcdb-d65a3ef83b4c
ms.openlocfilehash: 1cd4204d9e1626ac45bccf3954fdaf1c156af7f8
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70779658"
---
# <a name="wcf-data-services-protocol-implementation-details"></a>Details der WCF Data Services-Protokollimplementierung
## <a name="odata-protocol-implementation-details"></a>Details der OData-Protokollimplementierung  
 [!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] erfordert, dass ein Datendienst, der das Protokoll implementiert, einen bestimmten minimalen Satz von Funktionalitäten bereitstellt. Diese Funktionen werden in den Protokoll Dokumenten in Bezug auf "sollte" und "muss" beschrieben. Weitere optionale Funktionen werden im Bereich "Mai" beschrieben. In diesem Thema werden diese optionalen Funktionen, die derzeit nicht von [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] implementiert sind, beschrieben. Weitere Informationen finden Sie in der [odata-protokolldokumentation](https://go.microsoft.com/fwlink/?LinkID=184554).  
  
### <a name="support-for-the-format-query-option"></a>Unterstützung für die $format-Abfrageoption  
 Das [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]-Protokoll unterstützt sowohl JSON- (JavaScript Notation) als auch Atom-Feeds, und [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] stellt die `$format`-Systemabfrageoption bereit, um es einem Client zu ermöglichen, das Format des Antwortfeeds anzufordern. Diese Systemabfrageoption (falls sie vom Datendienst unterstützt wird) muss den Wert des Accept-Headers der Anforderung überschreiben. [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] unterstützt das Zurückgeben von JSON- und Atom-Feeds. Die Standardimplementierung unterstützt jedoch die `$format`-Abfrageoption nicht und verwendet nur den Wert des Accept-Headers, um das Format der Antwort zu bestimmen. Es gibt Situationen, in denen der Datendienst möglicherweise die `$format`-Abfrageoption unterstützen muss, z. B., wenn Clients den Accept-Header nicht festlegen können. Um diese Szenarien zu unterstützen, müssen Sie den Datendienst erweitern, um diese Option im URI zu verwenden. Sie können diese Funktion dem Datendienst hinzufügen, indem Sie die [JSONP-und URL-gesteuerte Formatunterstützung für ADO.NET Data Services](https://go.microsoft.com/fwlink/?LinkId=208228) Beispiel Projekt von der MSDN Code Gallery-Website herunterladen und dem Datendienst Projekt hinzufügen. In diesem Beispiel wird die `$format`-Abfrageoption entfernt und der Accept-Header in `application/json` geändert. Wenn Sie das Beispielprojekt einschließen und das `JSONPSupportBehaviorAttribute` zur Datendienstklasse hinzufügen, ermöglicht es dem Dienst, die `$format`-Abfrageoption `$format=json` zu verwenden. Eine weitere Anpassung dieses Beispielprojekts ist erforderlich, um auch `$format=atom` oder andere benutzerdefinierte Formate zu verwenden.  
  
## <a name="wcf-data-services-behaviors"></a>WCF Data Services - Verhaltensweisen  
 Die folgenden [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]-Verhaltensweisen werden nicht explizit vom [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]-Protokoll definiert:  
  
### <a name="default-sorting-behavior"></a>Standardsortierverhalten  
 Wenn eine Abfrageanforderung, die an den Datendienst gesendet wird, eine `$top`-Systemabfrageoption oder eine `$skip`-Systemabfrageoption einschließt und die `$orderby`-Systemabfrageoption nicht einschließt, wird der zurückgegebene Feed nach den Schlüsseleigenschaften in aufsteigender Reihenfolge sortiert. Das liegt daran, dass die Reihenfolge erforderlich ist, um das richtige Paging von Ergebnissen sicherzustellen. Hierzu fügt der Datendienst der Abfrage einen Reihenfolgenausdruck hinzu. Dieses Verhalten tritt auch auf, wenn servergesteuertes Paging im Datendienst aktiviert wird. Weitere Informationen finden Sie unter [Konfigurieren des Daten Dienstanbieter](configuring-the-data-service-wcf-data-services.md). Wenn Sie die Reihenfolge des zurückgegebenen Feeds steuern möchten, `$orderby` sollten Sie in den Abfrage-URI einschließen.  
  
## <a name="see-also"></a>Siehe auch

- [Defining WCF Data Services](defining-wcf-data-services.md)
- [WCF Data Services-Clientbibliothek](wcf-data-services-client-library.md)
