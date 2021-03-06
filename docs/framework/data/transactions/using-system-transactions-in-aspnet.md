---
title: Verwenden von System.Transactions in ASP.NET
ms.date: 03/30/2017
ms.assetid: 1982c300-7ea6-4242-95ed-dc28ccfacac9
ms.openlocfilehash: bfc75661ea538ac52b244e38eb10e6ae37a8fd62
ms.sourcegitcommit: 2d792961ed48f235cf413d6031576373c3050918
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2019
ms.locfileid: "70205834"
---
# <a name="using-systemtransactions-in-aspnet"></a>Verwenden von System.Transactions in ASP.NET
In diesem Thema wird beschrieben, wie Sie <xref:System.Transactions> in einer ASP.NET-Anwendung erfolgreich verwenden können.  
  
## <a name="enable-distributedtransactionpermission-in-aspnet"></a>Aktivieren von DistributedTransactionPermission in ASP.NET  
 <xref:System.Transactions> unterstützt teilweise vertrauenswürdige Aufrufer und wird mit dem **AllowPartiallyTrustedCallers** -Attribut (APTCA) markiert. Die Vertrauensebenen für <xref:System.Transactions> werden auf der Basis der Ressourcentypen (beispielsweise Systemspeicher, freigegebene prozessübergreifende Ressourcen, systemweite Ressourcen und andere Ressourcen) definiert, die <xref:System.Transactions> verfügbar macht, und auf der Basis der Vertrauensebene, die erforderlich sein soll, um auf diese Ressourcen zuzugreifen. In einer teilweise vertrauenswürdigen Umgebung kann eine nicht vollständig vertrauenswürdige Assembly Transaktionen nur innerhalb der Anwendungsdomäne nutzen (in diesem Fall ist die einzige geschützte Ressource der Systemspeicher), sofern ihr nicht die <xref:System.Transactions.DistributedTransactionPermission>erteilt wird.  
  
 <xref:System.Transactions.DistributedTransactionPermission> wird immer dann gefordert, wenn die Transaktionsverwaltung eskaliert wird, um vom Microsoft Distributed Transaction Coordinator (MSDTC) verwaltet zu werden. Diese Art des Szenarios verwendet prozessübergreifende Ressourcen und insbesondere eine globale Ressource, bei der es sich um den reservierten Speicherplatz im MSDTC-Protokoll handelt. Ein Beispiel für diese Verwendung ist das Web-Front-End einer Datenbank oder Anwendung, die eine Datenbank nutzt, die zu den von ihr bereitgestellten Diensten gehört.  
  
 ASP.NET verfügt über einen eigenen Satz Vertrauensebenen und ordnet diesen Vertrauensebenen über Richtliniendateien einen spezifischen Satz Berechtigungen zu. Weitere Informationen finden Sie unter [ASP.net Trust Levels and Policy files](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100)). Wenn Sie die Windows SDK erstmalig installieren, wird keine der Standardrichtlinien Dateien der ASP.NET zugeordnet <xref:System.Transactions.DistributedTransactionPermission>. Wenn Ihre Transaktion in einer ASP.NET-Anwendung eskaliert wird, um vom MSDTC verwaltet zu werden, schlägt die Eskalation mit einer <xref:System.Security.SecurityException> fehl, sobald die <xref:System.Transactions.DistributedTransactionPermission> angefordert wird. Um die Transaktionseskalation in einer teilweise vertrauenswürdigen ASP.NET-Umgebung zu ermöglichen, müssen Sie die <xref:System.Transactions.DistributedTransactionPermission> auf denselben Vertrauensebenen erteilen wie <xref:System.Data.SqlClient.SqlClientPermission>. Sie können entweder Ihre eigene benutzerdefinierte Vertrauensebene und Richtliniendatei konfigurieren, um die Eskalation zu ermöglichen, oder die Standardrichtliniendateien **Web_hightrust.config** und **Web_mediumtrust.config**ändern.  
  
 Um die Richtlinien Dateien zu ändern, fügen Sie ein **SecurityClass** -Element für **distributedtransaktionsberechtigung** zum **SecurityClasses** -Element unter dem **PolicyLevel** -Element hinzu, und fügen Sie ein entsprechendes iberechtigungselement unter der ASP.net- **NamedPermissionSet** für System. Transactions. Die folgende Konfigurationsdatei veranschaulicht dies.  
  
```xml  
<SecurityClasses>  
   <SecurityClass Name="DistributedTransactionPermission" Description="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"/>  
...  
</SecurityClasses>  
  
<PermissionSet  
  class="NamedPermissionSet"  
  version="1"  
  Name="ASP.Net">  
     <IPermission  
        class="System.Transactions.DistributedTransactionPermission, System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
        version="1"  
        Unrestricted="true"  
     />  
...  
</PermissionSet>  
```  
  
 Weitere Informationen zur ASP.NET-Sicherheitsrichtlinie finden Sie unter [SecurityPolicy-Element (ASP.net-Einstellungs Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100)).  
  
## <a name="dynamic-compilation"></a>Dynamische Kompilierung  
 Wenn Sie <xref:System.Transactions> zur Verwendung in eine ASP.NET-Anwendung importieren möchten, die bei Zugriff dynamisch kompiliert wird, sollten Sie einen Verweis auf die <xref:System.Transactions>-Assembly in die Konfigurationsdatei einfügen. Der Verweis sollte unterhalb des Abschnitts **compilation**/**assemblies** der **Web.config** -Konfigurationsdatei des Standardstammverzeichnisses oder der Konfigurationsdatei einer spezifischen Webanwendung hinzugefügt werden. Dies wird im folgenden Beispiel veranschaulicht:  
  
```xml  
<configuration>  
   <system.web>  
      <compilation>  
         <assemblies>  
      <add assembly="System.Transactions, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
         </assemblies>  
      </compilation>  
   </system.web>  
</configuration>  
```  
  
 Weitere Informationen finden Sie unter [Add-Element für Assemblys für die Kompilierung (ASP.NET Settings Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/37e2zyhb(v=vs.100)).  
  
## <a name="see-also"></a>Siehe auch

- [ASP.net-Vertrauens Ebenen und-Richtlinien Dateien](https://docs.microsoft.com/previous-versions/aspnet/wyts434y(v=vs.100))
- [SecurityPolicy-Element (ASP.NET Settings-Schema)](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/zhs35b56(v=vs.100))
- [Eskalation der Transaktionsverwaltung](transaction-management-escalation.md)
