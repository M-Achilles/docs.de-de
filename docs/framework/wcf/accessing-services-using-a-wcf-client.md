---
title: Zugreifen auf Dienste mithilfe eines WCF-Clients
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- clients [WCF], consuming services
ms.assetid: d780af9f-73c5-42db-9e52-077a5e4de7fe
ms.openlocfilehash: ae589e1c418b1cf13fe9f5b34648bdf7a2210eed
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855675"
---
# <a name="accessing-services-using-a-wcf-client"></a>Zugreifen auf Dienste mithilfe eines WCF-Clients

Nachdem Sie einen Dienst erstellt haben, ist der nächste Schritt das Erstellen eines WCF-Client Proxys. Eine Client Anwendung verwendet den WCF-Client Proxy, um mit dem Dienst zu kommunizieren. Client Anwendungen importieren in der Regel die Metadaten eines dienstanders, um WCF-Client Code zu generieren, mit dem der Dienst aufgerufen werden kann.

 Die grundlegenden Schritte zum Erstellen eines WCF-Clients umfassen Folgendes:

1. Kompilieren Sie den Dienstcode.

2. Generieren Sie den WCF-Client Proxy.

3. Instanziieren Sie den WCF-Clientproxy.

Der WCF-Client Proxy kann mithilfe des Service Model Metadata Utility Tool (Svcutil. exe) manuell generiert werden. Weitere Informationen finden Sie unter [Service Model Metadata Utility-Tool (Svcutil. exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). Der WCF-Client Proxy kann auch in Visual Studio mithilfe der **Dienstverweis hinzufügen** -Funktion generiert werden. Um den WCF-Clientproxy mithilfe einer dieser Methoden zu generieren, muss der Dienst ausgeführt werden. Wenn es sich um einen selbst gehosteten Dienst handelt, müssen Sie den Host ausführen. Wenn der Dienst in IIS/WAS gehostet wird, ist kein weiterer Schritt erforderlich.

## <a name="servicemodel-metadata-utility-tool"></a>ServiceModel Metadata Utility Tool
 Das [Service Model Metadata Utility-Tool (Svcutil. exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) ist ein Befehlszeilen Tool zum Erstellen von Code aus Metadaten. Die folgende Verwendung ist ein Beispiel für einen grundlegenden Svcutil.exe-Befehl.

```console
Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>
```

 Alternativ können Sie Svcutil.exe mit WSDL (Web Services Description Language) und XSD (XML Schema Definition Language)-Dateien im Dateisystem verwenden.

```console
Svcutil.exe <list of WSDL and XSD files on file system>
```

 Das Ergebnis ist eine Codedatei, die WCF-Client Code enthält, den die Client Anwendung verwenden kann, um den Dienst aufzurufen.

 Sie können das Tool auch zum Generieren von Konfigurationsdateien verwenden.

```console
Svcutil.exe <file1 [,file2]>
```

 Wenn nur ein Dateiname angegeben wird, ist das der Name der Ausgabedatei. Wenn zwei Dateinamen angegeben werden, ist die erste Datei eine Eingabekonfigurationsdatei, deren Inhalt mit der generierten Konfiguration zusammengeführt und in die zweite Datei geschrieben wird. Weitere Informationen zur Konfiguration finden Sie unter [Konfigurieren von Bindungen für Dienste](../../../docs/framework/wcf/configuring-bindings-for-wcf-services.md).

> [!IMPORTANT]
> Unsichere Metadatenanforderungen stellen bestimmte Risiken auf die gleiche Weise wie bei allen unsicheren Netzwerk Anforderungen dar: Wenn Sie nicht sicher sind, dass der Endpunkt, mit dem Sie kommunizieren, den Namen hat, den Sie auch haben, sind die abzurufenden Informationen möglicherweise Metadaten von einem böswilligen Dienst.

## <a name="add-service-reference-in-visual-studio"></a>"Dienstverweis hinzufügen" in Visual Studio

 Wenn der Dienst ausgeführt wird, **Klicken Sie mit** > der rechten Maustaste auf das Projekt, das den WCF-Client Proxy enthalten soll, und wählen Sie**Dienst Verweis** Geben Sie im **Dialog Feld Dienstverweis hinzufügen**die URL zu dem Dienst ein, den Sie aufrufen möchten, und klicken Sie auf die Schaltfläche **Gehe** zu. Das Dialogfeld zeigt eine Liste der Dienste an, die unter der Adresse verfügbar sind. Doppelklicken Sie auf den Dienst, um die verfügbaren Verträge und Vorgänge anzuzeigen, geben Sie einen Namespace für den generierten Code an, und klicken Sie auf die Schaltfläche **OK** .

## <a name="example"></a>Beispiel
 Im folgenden Codebeispiel wird ein für einen Dienst erstellter Dienstvertrag gezeigt.

```csharp
// Define a service contract.
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]
public interface ICalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    // Other methods are not shown here.
}
```

```vb
' Define a service contract.
<ServiceContract(Namespace:="http://Microsoft.ServiceModel.Samples")> _
Public Interface ICalculator
    <OperationContract()>  _
    Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
    ' Other methods are not shown here.
End Interface
```

 Das Service Model Metadata Utility-Tool und **Dienstverweis hinzufügen** in Visual Studio generieren die folgende WCF-Client Klasse. Die Klasse erbt von der generischen <xref:System.ServiceModel.ClientBase%601>-Klasse und implementiert die `ICalculator`-Schnittstelle. Das Tool generiert auch die `ICalculator`-Schnittstelle (wird hier nicht gezeigt).

```csharp
public partial class CalculatorClient : System.ServiceModel.ClientBase<ICalculator>, ICalculator
{
    public CalculatorClient()
    {}

    public CalculatorClient(string endpointConfigurationName) :
            base(endpointConfigurationName)
    {}

    public CalculatorClient(string endpointConfigurationName, string remoteAddress) :
            base(endpointConfigurationName, remoteAddress)
    {}

    public CalculatorClient(string endpointConfigurationName,
        System.ServiceModel.EndpointAddress remoteAddress) :
            base(endpointConfigurationName, remoteAddress)
    {}

    public CalculatorClient(System.ServiceModel.Channels.Binding binding,
        System.ServiceModel.EndpointAddress remoteAddress) :
            base(binding, remoteAddress)
    {}

    public double Add(double n1, double n2)
    {
        return base.Channel.Add(n1, n2);
    }
}
```

```vb
Partial Public Class CalculatorClient
    Inherits System.ServiceModel.ClientBase(Of ICalculator)
    Implements ICalculator

    Public Sub New()
        MyBase.New
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String)
        MyBase.New(endpointConfigurationName)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String, ByVal remoteAddress As String)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal endpointConfigurationName As String,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(endpointConfigurationName, remoteAddress)
    End Sub

    Public Sub New(ByVal binding As System.ServiceModel.Channels.Binding,
        ByVal remoteAddress As System.ServiceModel.EndpointAddress)
        MyBase.New(binding, remoteAddress)
    End Sub

    Public Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double
        Implements ICalculator.Add
        Return MyBase.Channel.Add(n1, n2)
    End Function
End Class
```

## <a name="using-the-wcf-client"></a>Verwenden des WCF-Clients
 Um den WCF-Client zu verwenden, erstellen Sie eine Instanz des WCF-Clients, und rufen Sie dann die zugehörigen Methoden auf, wie im folgenden Code gezeigt.

```csharp
// Create a client object with the given client endpoint configuration.
CalculatorClient calcClient = new CalculatorClient("CalculatorEndpoint"));
// Call the Add service operation.
double value1 = 100.00D;
double value2 = 15.99D;
double result = calcClient.Add(value1, value2);
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);
```

```vb
' Create a client object with the given client endpoint configuration.
Dim calcClient As CalculatorClient = _
New CalculatorClient("CalculatorEndpoint")

' Call the Add service operation.
Dim value1 As Double = 100.00D
Dim value2 As Double = 15.99D
Dim result As Double = calcClient.Add(value1, value2)
Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result)
```

## <a name="debugging-exceptions-thrown-by-a-client"></a>Debuggen der von einem Client ausgelösten Ausnahmen

Viele von einem WCF-Client ausgelöste Ausnahmen werden durch eine Ausnahme auf dem Dienst verursacht. Im Folgenden finden Sie einige Beispiele:

- <xref:System.Net.Sockets.SocketException>: Eine vorhandene Verbindung wurde vom Remote Host geschlossen.

- <xref:System.ServiceModel.CommunicationException>: Die zugrunde liegende Verbindung wurde unerwartet geschlossen.

- <xref:System.ServiceModel.CommunicationObjectAbortedException>: Die Socketverbindung wurde abgebrochen. Mögliche Ursache: Ein Fehler beim Verarbeiten der Nachricht, eine Zeitüberschreitung durch den Remotehost beim Empfang oder ein Problem mit einer zugrunde liegenden Netzwerkressource.

Tritt eine Ausnahme dieses Typs auf, aktivieren Sie die Ablaufverfolgung auf der Dienstseite, und ermitteln Sie die dort aufgetretene Ausnahme. Weitere Informationen zur [Ablauf Verfolgung finden](../../../docs/framework/wcf/diagnostics/tracing/index.md) Sie unter Ablauf Verfolgung und [Verwenden der Ablauf Verfolgung für](../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)die Problembehandlung Ihrer Anwendung.

## <a name="see-also"></a>Siehe auch

- [Vorgehensweise: Erstellen eines Clients](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)
- [Vorgehensweise: Zugreifen auf Dienste mit einem Duplex Vertrag](../../../docs/framework/wcf/feature-details/how-to-access-services-with-a-duplex-contract.md)
- [Vorgehensweise: Asynchrones Abrufen von Dienst Vorgängen](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md)
- [Vorgehensweise: Zugreifen auf Dienste mit unidirektionalen und Anforderung-Antwort-Verträgen](../../../docs/framework/wcf/feature-details/how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md)
- [Vorgehensweise: Zugreifen auf einen WSE 3,0-Dienst](../../../docs/framework/wcf/feature-details/how-to-access-a-wse-3-0-service-with-a-wcf-client.md)
- [Grundlagen des generierten Clientcodes](../../../docs/framework/wcf/feature-details/understanding-generated-client-code.md)
- [Vorgehensweise: Verbessern der Startzeit von WCF-Client Anwendungen mit dem XmlSerializer](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md)
- [Angeben des Clientlaufzeitverhaltens](../../../docs/framework/wcf/specifying-client-run-time-behavior.md)
- [Konfigurieren von Clientverhalten](../../../docs/framework/wcf/configuring-client-behaviors.md)
