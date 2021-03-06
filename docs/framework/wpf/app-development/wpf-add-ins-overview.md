---
title: Übersicht über WPF-Add-Ins
ms.date: 03/30/2017
helpviewer_keywords:
- add-ins and XAML browser applications [WPF]
- add-ins overview [WPF]
- add-ins [WPF], performance
- add-ins [WPF], benefits
- .NET Framework add-in model [WPF]
- add-ins [WPF], user interface
- add-ins and the user interface [WPF]
- add-ins [WPF], architecture
- add-ins [WPF], limitations
ms.assetid: 00b4c776-29a8-4dba-b603-280a0cdc2ade
ms.openlocfilehash: a146f15a1c2755f254e198d471a42ca9ec29b072
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/23/2019
ms.locfileid: "71182535"
---
# <a name="wpf-add-ins-overview"></a>Übersicht über WPF-Add-Ins

<a name="Introduction"></a>Die .NET Framework enthält ein Add-in-Modell, mit dem Entwickler Anwendungen erstellen können, die Add-in-Erweiterbarkeit unterstützen. Dieses Add-In-Modell ermöglicht die Erstellung von Add-Ins, die in die Anwendungsfunktionalität integriert werden und diese erweitern. In einigen Szenarien müssen Anwendungen auch Benutzeroberflächen anzeigen, die von Add-ins bereitgestellt werden. In diesem Thema wird gezeigt, wie WPF das .NET Framework Add-in-Modell erweitert, um diese Szenarien, die dahinter liegende Architektur, die Vorteile und die Einschränkungen zu ermöglichen.

<a name="Requirements"></a>

## <a name="prerequisites"></a>Erforderliche Komponenten

Vertrautheit mit dem .NET Framework Add-in-Modell ist erforderlich. Weitere Informationen finden Sie unter [Add-Ins und Erweiterbarkeit](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100)).

<a name="AddInsOverview"></a>

## <a name="add-ins-overview"></a>Übersicht über Add-Ins

Um das mit dem Integrieren neuer Funktionen verbundene erneute Kompilieren und Bereitstellen von Anwendungen zu vermeiden, da diese Vorgänge sehr komplex sind, sind Anwendungen mit Erweiterbarkeitsmechanismen ausgestattet. Diese ermöglichen Entwicklern (sowohl Erst- als auch Drittanbieter) das Erstellen anderer Anwendungen, die integriert werden können. Diese Art von Erweiterbarkeit wird in der Regel durch die Verwendung von Add-Ins (auch als „Add-Ons“ oder „Plug-Ins“ bezeichnet) unterstützt. Es folgen Beispiele für reale Anwendungen, die eine Erweiterbarkeit mit Add-Ins verfügbar machen:

- Internet Explorer-Add-Ons

- Windows Media Player-Plug-Ins

- Visual Studio-Add-Ins

Beispielsweise können Drittanbieterentwickler mithilfe des Add-In-Modells von Windows Media Player „Plug-Ins“ implementieren, durch die der Windows Media Player auf vielfältige Weise erweitert wird. Dazu zählen das Erstellen von Decodern und Encodern für Medienformate, für die keine systemeigene Unterstützung durch Windows Media Player besteht (z. B. DVD, MP3), Audioeffekte und Skins. Jedes Add-In-Modell ist so aufgebaut, dass es die zu einer Anwendung gehörenden Funktionen verfügbar macht, obwohl verschiedene Entitäten und Verhaltensweisen für alle Add-In-Modelle gelten.

Die drei Hauptentitäten typischer Add-In-Erweiterbarkeitslösungen sind *Verträge*, *Add-Ins* und *Hostanwendungen*. Mit Verträgen wird auf zwei Arten definiert, wie Add-Ins mit Hostanwendungen integriert sind:

- Add-Ins sind in Funktionen integriert, die von Hostanwendungen implementiert werden.

- Hostanwendungen machen Funktionen verfügbar, in die Add-Ins integriert werden.

Damit Add-Ins verwendet werden können, müssen sie von Hostanwendungen gefunden und zur Laufzeit geladen werden. Daher sind Anwendungen, die Add-Ins unterstützen, zusätzlich für folgende Aufgaben verantwortlich:

- Ermittlung: Suchen von Add-Ins, die Verträge einhalten, die von Host Anwendungen unterstützt werden.

- **Aktivierung**: Laden, ausführen und Einrichten der Kommunikation mit Add-Ins.

- **Isolation**: Verwenden von Anwendungs Domänen oder Prozessen zum Einrichten von Isolations Grenzen, mit denen Anwendungen vor potenziellen Sicherheits-und Ausführungs Problemen mit Add-Ins geschützt werden.

- **Kommunikation**: Zulassen, dass Add-Ins und Host Anwendungen über Isolations Grenzen hinweg miteinander kommunizieren, indem Methoden aufgerufen und Daten übergeben werden.

- **Verwaltung der Lebensdauer**: Laden und Entladen von Anwendungs Domänen und Prozessen auf eine saubere, vorhersagbare Weise (siehe [Anwendungs Domänen](../../app-domains/application-domains.md)).

- **Versionsverwaltung**: Sicherstellen, dass Host Anwendungen und Add-Ins auch dann kommunizieren können, wenn neue Versionen von erstellt werden.

Letztlich ist es eine wichtige Aufgabe, ein stabiles Add-In-Modell zu entwickeln. Aus diesem Grund stellt die .NET Framework eine Infrastruktur zum Entwickeln von Add-in-Modellen bereit.

> [!NOTE]
> Weitere Informationen zu Add-Ins finden Sie unter [Add-Ins und Erweiterbarkeit](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100)).

<a name="NETFrameworkAddInModelOverview"></a>

## <a name="net-framework-add-in-model-overview"></a>Übersicht über das Add-In-Modell von .NET Framework

Das .NET Framework Add-in-Modell, das im <xref:System.AddIn> -Namespace enthalten ist, enthält einen Satz von Typen, die entwickelt wurden, um die Entwicklung der Add-in-Erweiterbarkeit zu vereinfachen. Die grundlegende Einheit des .NET Framework Add-in-Modells ist der *Vertrag*, der definiert, wie eine Host Anwendung und ein Add-in miteinander kommunizieren. Ein Vertrag wird mit einer für Hostanwendungen spezifischen *Ansicht* des Vertrags für eine Hostanwendung verfügbar gemacht. Auf ähnliche Weise wird eine für Add-Ins spezifische *Ansicht* des Vertrags für das Add-In verfügbar gemacht. Ein *Adapter* ermöglicht es einer Hostanwendung und einem Add-In, zwischen ihren jeweiligen Ansichten des Vertrags miteinander zu kommunizieren. Verträge, Ansichten und Adapter werden als Segmente bezeichnet, und mehrere miteinander verbundene Segmente stellen eine *Pipeline* dar. Pipelines sind die Grundlage, auf der das .NET Framework-Add-in-Modell Ermittlung, Aktivierung, Sicherheits Isolation, Ausführungs Isolation (unter Verwendung von Anwendungs Domänen und Prozessen), Kommunikation, Verwaltung von Lebensdauer und Versionsverwaltung unterstützt.

Mit dieser Unterstützung können Entwickler Add-Ins erstellen, die mit den Funktionen einer Hostanwendung integriert werden. Einige Szenarien erfordern jedoch, dass Host Anwendungen Benutzeroberflächen anzeigen, die von Add-ins bereitgestellt werden. Da jede Präsentationstechnologie in der .NET Framework über ein eigenes Modell zum Implementieren von Benutzeroberflächen verfügt, unterstützt das .NET Framework Add-in-Modell keine bestimmte Präsentationstechnologie. Stattdessen erweitert WPF das .NET Framework Add-in-Modell mit UI-Unterstützung für Add-Ins.

<a name="WPFAddInModel"></a>

## <a name="wpf-add-ins"></a>WPF-Add-Ins

WPF ermöglicht es Ihnen in Verbindung mit dem .NET Framework-Add-in-Modell, eine Vielzahl von Szenarien zu adressieren, die es erfordern, dass Host Anwendungen Benutzeroberflächen von Add-Ins anzeigen. Insbesondere werden diese Szenarien von WPF mit den folgenden zwei Programmier Modellen adressiert:

1. **Das Add-In gibt eine Benutzeroberfläche zurück**. Ein Add-in gibt eine Benutzeroberfläche an die Host Anwendung über einen Methoden Befehl zurück, wie vom Vertrag definiert. Das Szenario wird in den folgenden Fällen verwendet:

    - Die Darstellung einer Benutzeroberfläche, die von einem Add-in zurückgegeben wird, hängt entweder von Daten oder von Bedingungen ab, die nur zur Laufzeit (z. b. dynamisch generierte Berichte) vorhanden sind.

    - Die Benutzeroberfläche für Dienste, die von einem Add-in bereitgestellt werden, unterscheidet sich von der Benutzeroberfläche der Host Anwendungen, die das Add-in verwenden können.

    - Das Add-in führt hauptsächlich einen Dienst für die Host Anwendung aus und meldet den Status an die Host Anwendung mit einer Benutzeroberfläche.

2. **Das Add-In ist eine Benutzeroberfläche**. Ein Add-in ist eine Benutzeroberfläche, wie vom Vertrag definiert. Das Szenario wird in den folgenden Fällen verwendet:

    - Ein Add-In stellt ausschließlich die angezeigten Dienste bereit, z. B. eine Werbung.

    - Die Benutzeroberfläche für Dienste, die von einem Add-in bereitgestellt werden, ist für alle Host Anwendungen üblich, die das Add-in verwenden können, z. b. einen Rechner oder eine Farbauswahl.

Diese Szenarien erfordern, dass UI-Objekte zwischen der Host Anwendung und den Add-in-Anwendungs Domänen übermittelt werden können. Da das .NET Framework-Add-in-Modell für die Kommunikation zwischen Anwendungs Domänen Remoting benötigt, müssen die zwischen Ihnen weiter gegebenen Objekte Remote fähig sein.

Ein remotefähiges Objekt stellt die Instanz einer Klasse dar, für die eine oder mehrere der folgenden Aussagen gelten:

- Wird von der <xref:System.MarshalByRefObject> -Klasse abgeleitet.

- Implementiert die <xref:System.Runtime.Serialization.ISerializable>-Schnittstelle.

- Hat das <xref:System.SerializableAttribute> -Attribut angewendet.

> [!NOTE]
> Weitere Informationen zum Erstellen von Remote fähigen-.NET Framework Objekten finden Sie unter [Erstellen von Objekten Remote fähigen](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))Objekten.

Die WPF-Benutzeroberflächen Typen sind nicht Remote fähig. Um das Problem zu beheben, erweitert WPF das .NET Framework Add-in-Modell, um zu ermöglichen, dass die von Add-Ins erstellte WPF-Benutzeroberfläche von Host Anwendungen aus angezeigt wird. Diese Unterstützung wird von WPF durch zwei Arten bereitgestellt <xref:System.AddIn.Contract.INativeHandleContract> : die-Schnittstelle und zwei statische <xref:System.AddIn.Pipeline.FrameworkElementAdapters> Methoden, die <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>von der-Klasse implementiert werden: <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> und. Im Allgemeinen werden diese Typen und Methoden wie folgt verwendet:

1. WPF erfordert, dass von Add-Ins bereitgestellte Benutzeroberflächen Klassen sind, die direkt oder <xref:System.Windows.FrameworkElement>indirekt von abgeleitet werden, z. b. Formen, Steuerelemente, Benutzer Steuerelemente, Layoutpanels und Seiten.

2. Überall dort, wo der Vertrag deklariert, dass eine Benutzeroberfläche zwischen dem Add-in und der Host Anwendung übermittelt wird, muss <xref:System.AddIn.Contract.INativeHandleContract> Sie als ( <xref:System.Windows.FrameworkElement>kein) deklariert werden. <xref:System.AddIn.Contract.INativeHandleContract> ist eine Remote fähige Darstellung der Add-in-Benutzeroberfläche, die über Isolations Grenzen hinweg übermittelt werden kann.

3. Vor der Übergabe von der Anwendungsdomäne des Add-Ins wird eine <xref:System.Windows.FrameworkElement> verpackt <xref:System.AddIn.Contract.INativeHandleContract> , indem aufgerufen <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>wird.

4. Nachdem Sie an die Anwendungsdomäne der Host Anwendung weitergeleitet wurde <xref:System.AddIn.Contract.INativeHandleContract> , muss der <xref:System.Windows.FrameworkElement> durch Aufrufen <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>von neu verpackt werden.

Wie <xref:System.AddIn.Contract.INativeHandleContract>, <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> und<xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> verwendet werden, hängt vom jeweiligen Szenario ab. Die folgenden Abschnitte bieten ausführliche Informationen zu den Programmiermodellen.

<a name="ReturnUIFromAddInContract"></a>

## <a name="add-in-returns-a-user-interface"></a>Add-In gibt eine Benutzeroberfläche zurück

Damit ein Add-in eine Benutzeroberfläche an eine Host Anwendung zurückgibt, sind folgende Schritte erforderlich:

1. Die Host Anwendung, das Add-in und die Pipeline müssen erstellt werden, wie in den .NET Framework [-Add-Ins und der Erweiterbarkeits](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100)) Dokumentation beschrieben.

2. Der Vertrag muss implementieren <xref:System.AddIn.Contract.IContract> und, um eine Benutzeroberfläche zurückzugeben. der Vertrag muss eine Methode mit einem Rückgabewert vom <xref:System.AddIn.Contract.INativeHandleContract>Typ deklarieren.

3. Die Benutzeroberfläche, die zwischen dem Add-in und der Host Anwendung übermittelt wird, muss direkt <xref:System.Windows.FrameworkElement>oder indirekt von abgeleitet werden.

4. Die Benutzeroberfläche, die vom-Add-in zurückgegeben wird, muss <xref:System.Windows.FrameworkElement> <xref:System.AddIn.Contract.INativeHandleContract> vor dem Überschreiten der Isolations Grenze von einem in ein konvertiert werden.

5. Die zurückgegebene Benutzeroberfläche muss nach dem überschreiten <xref:System.AddIn.Contract.INativeHandleContract> der Isolations Grenze von einem in ein <xref:System.Windows.FrameworkElement> konvertiert werden.

6. Die Host Anwendung zeigt die zurück <xref:System.Windows.FrameworkElement>gegebene an.

Ein Beispiel für das Implementieren eines Add-Ins, das eine Benutzeroberfläche zurückgibt, finden [Sie unter Erstellen eines Add-Ins, das eine Benutzeroberfläche zurückgibt](how-to-create-an-add-in-that-returns-a-ui.md).

<a name="AddInIsAUI"></a>

## <a name="add-in-is-a-user-interface"></a>Add-In ist eine Benutzeroberfläche

Wenn ein Add-in eine Benutzeroberfläche ist, ist Folgendes erforderlich:

1. Die Host Anwendung, das Add-in und die Pipeline müssen erstellt werden, wie in den .NET Framework [-Add-Ins und der Erweiterbarkeits](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100)) Dokumentation beschrieben.

2. Die Vertrags Schnittstelle für das Add-in muss implementieren <xref:System.AddIn.Contract.INativeHandleContract>.

3. Das Add-in, das an die Host Anwendung übermittelt wird, muss direkt oder <xref:System.Windows.FrameworkElement>indirekt von abgeleitet werden.

4. Das-Add-in muss vor dem über <xref:System.Windows.FrameworkElement> schreiten der <xref:System.AddIn.Contract.INativeHandleContract> Isolations Grenze von einem in ein konvertiert werden.

5. Das Add-in muss nach dem überschreiten <xref:System.AddIn.Contract.INativeHandleContract> der Isolations Grenze von einem in ein <xref:System.Windows.FrameworkElement> konvertiert werden.

6. Die Host Anwendung zeigt die zurück <xref:System.Windows.FrameworkElement>gegebene an.

Ein Beispiel für das Implementieren eines Add-Ins, das eine Benutzeroberfläche ist, finden [Sie unter Erstellen eines Add-Ins, das eine Benutzeroberfläche ist](how-to-create-an-add-in-that-is-a-ui.md).

<a name="ReturningMultipleUIsFromAnAddIn"></a>

## <a name="returning-multiple-uis-from-an-add-in"></a>Zurückgeben mehrerer Benutzeroberflächen durch ein Add-In

Add-Ins stellen häufig mehrere Benutzeroberflächen bereit, damit Host Anwendungen angezeigt werden. Angenommen, es handelt sich um ein Add-in, bei dem es sich um eine Benutzeroberfläche handelt, die auch Statusinformationen für die Host Anwendung als Benutzeroberfläche bereitstellt. Sie können ein Add-In dieser Art implementieren, indem Sie eine Kombination der Verfahren aus den Modellen [Add-In gibt eine Benutzeroberfläche zurück](#ReturnUIFromAddInContract) und [Add-In ist eine Benutzeroberfläche](#AddInIsAUI) verwenden.

<a name="AddInsAndXBAPs"></a>

## <a name="add-ins-and-xaml-browser-applications"></a>Add-Ins und XAML-Browseranwendungen

In den bisherigen Beispielen wurde die Hostanwendung als eigenständige Anwendung installiert. [!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]-Browseranwendungen können jedoch auch Add-Ins hosten, wobei allerdings die folgenden zusätzlichen Erstellungs- und Implementierungsanforderungen gelten:

- Das [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] Anwendungs Manifest muss speziell für das Herunterladen der Pipeline (Ordner und Assemblys) und der Add-in-Assembly in den ClickOnce-Anwendungscache auf dem Client Computer im selben [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]Ordner wie der konfiguriert werden.

- Der [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] Code zum Ermitteln und laden [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] von Add-Ins muss den ClickOnce-Anwendungscache für als Pipeline-und Add-in-Speicherort verwenden.

- [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] muss das Add-In in einen speziellen Sicherheitskontext laden, wenn das Add-In auf lose Dateien verweist, die sich auf der Ursprungssite befinden. Wenn sie von [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]s gehostet werden, können Add-Ins nur auf lose Dateien verweisen, die auf der Ursprungssite der Hostanwendung gespeichert sind.

In den folgenden Unterabschnitten werden diese Aufgaben ausführlich beschrieben.

### <a name="configuring-the-pipeline-and-add-in-for-clickonce-deployment"></a>Konfigurieren der Pipeline und des Add-Ins für die ClickOnce-Bereitstellung

[!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]Sie werden in einen sicheren Ordner im ClickOnce-Bereitstellungs Cache heruntergeladen und dort ausgeführt. Damit eine [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] ein Add-In hosten kann, müssen auch Pipeline- und Add-In-Assembly in den sicheren Ordner heruntergeladen werden. Um dies zu erreichen, müssen Sie das Anwendungsmanifest so konfigurieren, dass sowohl die Pipeline- als auch die Add-In-Assembly heruntergeladen wird. Diese Aufgabe lässt sich am einfachsten in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] ausführen, obwohl Pipeline- und Add-In-Assembly im Stammordner des [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]-Hostprojekts gespeichert sein müssen, damit [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] die Pipelineassemblys ermitteln kann.

Folglich muss der erste Schritt darin bestehen, die Pipeline- und Add-In-Assembly im Stammverzeichnis des [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]-Projekts zu erstellen. Dazu wird die Buildausgabe der einzelnen Pipelineassembly- und Add-In-Assemblyprojekte festgelegt. Die folgende Tabelle zeigt die Buildausgabepfade für die Pipelineassemblyprojekte und das Add-In-Assemblyprojekt, die sich in demselben Projektmappen- und Stammordner befinden wie das [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]-Hostprojekt.

Tabelle 1: Buildausgabepfade für die von einer XBAP gehosteten Pipelineassemblys

|Pipelineassemblyprojekt|Ausgabepfad erstellen|
|-------------------------------|-----------------------|
|Vertrag|`..\HostXBAP\Contracts\`|
|Add-In-Ansicht|`..\HostXBAP\AddInViews\`|
|Add-In-seitiger Adapter|`..\HostXBAP\AddInSideAdapters\`|
|Hostseitiger Adapter|`..\HostXBAP\HostSideAdapters\`|
|Add-In|`..\HostXBAP\AddIns\WPFAddIn1`|

Der nächste Schritt besteht darin, die Pipelineassemblys und die Add-In-Assembly als die Inhaltsdateien der [!INCLUDE[TLA2#tla_xbap#plural](../../../../includes/tla2sharptla-xbapsharpplural-md.md)]s in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] anzugeben. Dazu werden folgende Schritte ausgeführt:

1. Hinzufügen der Pipeline- und Add-In-Assembly zum Projekt, indem Sie im Projektmappen-Explorer mit der rechten Maustaste auf die einzelnen Pipelineordner klicken und die Option **Zu Projekt hinzufügen** auswählen.

2. Festlegen des **Buildvorgangs** jeder Pipelineassembly und jeder Add-In-Assembly im **Eigenschaftenfenster** auf **Inhalt**.

Im letzten Schritt muss das Anwendungsmanifest so konfiguriert werden, dass sowohl die Pipelineassemblydateien als auch die Add-In-Assemblydatei heruntergeladen werden. Die Dateien sollten sich in Ordnern befinden, die sich im Stammverzeichnis des Ordners im ClickOnce- [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] Cache befinden, der von der Anwendung belegt wird. Die Konfiguration richten Sie in [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] durch folgende Schritte ein:

1. Klicken Sie mit der rechten Maustaste auf das [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]-Projekt, klicken Sie auf **Eigenschaften**, auf **Veröffentlichen** und dann auf die Schaltfläche **Anwendungsdateien**.

2. Legen Sie im Dialogfeld **Anwendungsdateien** den **Veröffentlichungsstatus** der einzelnen Pipeline- und Add-In-DLLs auf **Einschließen (Auto)** und die **Downloadgruppe** für die Pipeline- und Add-In-DLLs auf **(Erforderlich)** fest.

### <a name="using-the-pipeline-and-add-in-from-the-application-base"></a>Verwenden der Pipeline und des Add-Ins von der Anwendungsbasis

Wenn die Pipeline und das Add-in für die ClickOnce-Bereitstellung konfiguriert sind, werden Sie in denselben ClickOnce-Cache [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]Ordner wie das heruntergeladen. Damit Pipeline und Add-In aus der [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)] verwendet werden können, müssen sie vom [!INCLUDE[TLA2#tla_xbap](../../../../includes/tla2sharptla-xbap-md.md)]-Code aus der Anwendungsbasis abgerufen werden. Die verschiedenen Typen und Member des .NET Framework Add-in-Modells für die Verwendung von Pipelines und Add-Ins bieten besondere Unterstützung für dieses Szenario. Zuerst wird der Pfad durch den <xref:System.AddIn.Hosting.PipelineStoreLocation.ApplicationBase> -Enumerationswert identifiziert. Diesen Wert verwenden Sie mit Überladungen der relevanten Add-In-Member, wenn Pipelines verwendet werden sollen, die Folgendes enthalten:

- <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.FindAddIns%28System.Type%2CSystem.AddIn.Hosting.PipelineStoreLocation%2CSystem.String%5B%5D%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.Rebuild%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

- <xref:System.AddIn.Hosting.AddInStore.Update%28System.AddIn.Hosting.PipelineStoreLocation%29?displayProperty=nameWithType>

### <a name="accessing-the-hosts-site-of-origin"></a>Zugreifen auf die Ursprungssite des Hosts

Damit ein Add-In auf Dateien von der Ursprungssite verweisen kann, muss das Add-In mit einer Sicherheitsisolation geladen werden, die der Hostanwendung entspricht. Diese Sicherheitsstufe wird durch den <xref:System.AddIn.Hosting.AddInSecurityLevel.Host?displayProperty=nameWithType> -Enumerationswert identifiziert und an die <xref:System.AddIn.Hosting.AddInToken.Activate%2A> -Methode beim Aktivieren eines Add-ins übermittelt.

<a name="WPFAddInModelArchitecture"></a>

## <a name="wpf-add-in-architecture"></a>Architektur des WPF-Add-Ins

Auf der höchsten Ebene, wie wir gesehen haben, ermöglicht WPF .NET Framework-Add-Ins, Benutzeroberflächen (die direkt oder indirekt von <xref:System.Windows.FrameworkElement>abgeleitet werden) mithilfe <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> <xref:System.AddIn.Contract.INativeHandleContract>von <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A>, und zu implementieren. Das Ergebnis ist, dass die Host Anwendung einen <xref:System.Windows.FrameworkElement> zurückgibt, der von der Benutzeroberfläche in der Host Anwendung angezeigt wird.

Für einfache Benutzeroberflächen-Add-in-Szenarios ist dies so ausführlich wie Entwickler Anforderungen. Für komplexere Szenarien, insbesondere solche, die versuchen, zusätzliche WPF-Dienste wie Layout, Ressourcen und Datenbindung zu verwenden, sind ausführlichere Informationen dazu erforderlich, wie WPF das .NET Framework Add-in-Modell mit UI-Unterstützung erweitert. und Einschränkungen.

Im Grunde übergibt WPF keine Benutzeroberfläche von einem Add-in an eine Host Anwendung. Stattdessen übergibt WPF das Win32-Fenster Handle für die Benutzeroberfläche mithilfe der WPF-Interoperabilität. Wenn eine Benutzeroberfläche aus einem Add-in an eine Host Anwendung übermittelt wird, geschieht Folgendes:

- Auf der Add-in-Seite erhält WPF ein Fenster Handle für die Benutzeroberfläche, die von der Host Anwendung angezeigt wird. Das Fenster Handle wird von einer internen WPF-Klasse gekapselt <xref:System.Windows.Interop.HwndSource> , die <xref:System.AddIn.Contract.INativeHandleContract>von abgeleitet wird und implementiert. Eine Instanz dieser Klasse wird von <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> zurückgegeben und von der Anwendungsdomäne des Add-Ins an die Anwendungsdomäne der Host Anwendung gemarshallt.

- Auf der Host Anwendungsseite wird von WPF das als <xref:System.Windows.Interop.HwndSource> interne WPF-Klasse erneut verpackt, die <xref:System.Windows.Interop.HwndHost> von abgeleitet <xref:System.AddIn.Contract.INativeHandleContract>wird und die verwendet. Eine Instanz dieser Klasse wird von <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> an die Host Anwendung zurückgegeben.

<xref:System.Windows.Interop.HwndHost>Gibt an, dass Benutzeroberflächen, die durch Fenster Handles identifiziert werden, von WPF-Benutzeroberflächen angezeigt werden. Weitere Informationen finden Sie unter [Interaktion zwischen WPF und Win32](../advanced/wpf-and-win32-interoperation.md).

<xref:System.AddIn.Contract.INativeHandleContract>Zusammenfassend <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>ist,, und <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> vorhanden, damit das Fenster Handle für eine WPF-Benutzeroberfläche von einem Add-in an eine Host Anwendung übermittelt werden kann, wo Sie von <xref:System.Windows.Interop.HwndHost> einem gekapselt und die Benutzeroberfläche der Host Anwendung angezeigt wird.

> [!NOTE]
> Da die Host Anwendung einen <xref:System.Windows.Interop.HwndHost>abruft, kann die Host Anwendung das Objekt, das von <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ContractToViewAdapter%2A> zurückgegeben wird, nicht in den Typ konvertieren, den Sie durch das Add-in implementiert <xref:System.Windows.Controls.UserControl>hat (z. b.).

Naturgemäß <xref:System.Windows.Interop.HwndHost> weist bestimmte Einschränkungen auf, die sich darauf auswirken, wie Host Anwendungen Sie verwenden können. WPF erweitert <xref:System.Windows.Interop.HwndHost> jedoch mehrere Funktionen für Add-in-Szenarien. Diese Vorteile und die Einschränkungen werden nachstehend beschrieben.

<a name="WPFAddInModelBenefits"></a>

## <a name="wpf-add-in-benefits"></a>Vorteile des WPF-Add-Ins

Da WPF-Add-in-Benutzeroberflächen von Host Anwendungen mithilfe einer internen Klasse angezeigt werden, <xref:System.Windows.Interop.HwndHost>die von abgeleitet wird, werden diese Benutzeroberflächen durch <xref:System.Windows.Interop.HwndHost> die Funktionen von in Bezug auf WPF-UI-Dienste wie Layout eingeschränkt. Rendering, Datenbindung, Stile, Vorlagen und Ressourcen. WPF erweitert jedoch seine interne <xref:System.Windows.Interop.HwndHost> Unterklasse mit zusätzlichen Funktionen, die Folgendes umfassen:

- Tabstopps zwischen der Benutzeroberfläche einer Host Anwendung und der Benutzeroberfläche eines Add-Ins. Beachten Sie, dass das Programmiermodell "Add-in ist eine Benutzeroberfläche" erfordert, dass der Add-in <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> -Side-Adapter überschrieben wird, um Tab zu aktivieren, unabhängig davon, ob das Add-in voll vertrauenswürdig oder teilweise vertrauenswürdig ist

- Berücksichtigen der Barrierefreiheits Anforderungen für Add-in-Benutzeroberflächen, die von den Benutzeroberflächen von Host Anwendungen angezeigt werden.

- Das sichere Ausführen von WPF-Anwendungen in Szenarien mit mehreren Anwendungs Domänen.

- Verhindern von unzulässigem Zugriff auf Add-in-Benutzeroberflächen Fenster Handles, wenn Add-Ins mit Sicherheits Isolation ausgeführt werden (d. h. eine teilweise vertrauenswürdige Sicherheits Sandbox). Durch <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> Aufrufen von wird diese Sicherheit sichergestellt

  - Für das Programmiermodell "Add-in gibt eine Benutzeroberfläche" zurück, besteht die einzige Möglichkeit, das Fenster Handle für eine Add-in-Benutzeroberfläche über die Isolations Grenze zu übergeben, darin, aufzurufen <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A>.

  - Das Programmiermodell "Add-in ist eine Benutzeroberfläche", <xref:System.AddIn.Pipeline.ContractBase.QueryContract%2A> das Überschreiben auf dem Add-in-seitigen Adapter und das Aufrufen <xref:System.AddIn.Pipeline.FrameworkElementAdapters.ViewToContractAdapter%2A> von (wie in den obigen Beispielen gezeigt) erforderlich ist, wie das Aufrufen der `QueryContract` Implementierung des Add-in-seitigen Adapters aus dem Host seitiger Adapter.

- Bereitstellen von Ausführungsschutz für mehrere Anwendungsdomänen. Aufgrund von Einschränkungen bei Anwendungsdomänen führen unbehandelte Ausnahmen, die in Add-In-Anwendungsdomänen ausgelöst werden, zum Absturz der gesamten Anwendung, auch wenn eine Isolationsgrenze eingerichtet ist. WPF und das .NET Framework-Add-in-Modell bieten jedoch eine einfache Möglichkeit, dieses Problem zu umgehen und die Anwendungs Stabilität zu verbessern. Ein WPF-Add-in, das eine Benutzeroberfläche <xref:System.Windows.Threading.Dispatcher> anzeigt, erstellt einen für den Thread, auf dem die Anwendungsdomäne ausgeführt wird, wenn es sich bei der Host Anwendung um eine WPF-Anwendung handelt. Sie können alle nicht behandelten Ausnahmen erkennen, die in der Anwendungsdomäne auftreten, indem <xref:System.Windows.Threading.Dispatcher.UnhandledException> Sie das- <xref:System.Windows.Threading.Dispatcher>Ereignis der WPF-Add-Ins behandeln. Sie können den <xref:System.Windows.Threading.Dispatcher> aus der <xref:System.Windows.Threading.Dispatcher.CurrentDispatcher%2A> -Eigenschaft erhalten.

<a name="WPFAddInModelLimitations"></a>

## <a name="wpf-add-in-limitations"></a>Einschränkungen des WPF-Add-Ins

Zusätzlich zu den Vorteilen, die WPF den Standardverhalten hinzufügt, <xref:System.Windows.Interop.HwndSource>die <xref:System.Windows.Interop.HwndHost>von den Fenster Handles, und bereitgestellt werden, gibt es auch Einschränkungen für Add-in-Benutzeroberflächen, die von Host Anwendungen angezeigt werden:

- Von einer Host Anwendung angezeigte Add-in-Benutzeroberflächen beachten das clippingverhalten der Host Anwendung nicht.

- Der Begriff *Airspace* in Interoperabilitätsszenarien gilt auch für Add-Ins (siehe [Übersicht über die Technologieregionen](../advanced/technology-regions-overview.md)).

- Die UI-Dienste einer Host Anwendung, z. b. Ressourcen Vererbung, Datenbindung und Befehls Folge, sind nicht automatisch für Add-in-Benutzeroberflächen verfügbar. Um diese Dienste für das Add-In bereitzustellen, müssen Sie die Pipeline aktualisieren.

- Eine Add-in-Benutzeroberfläche kann nicht gedreht, skaliert, verzerrt oder anderweitig von einer Transformation beeinflusst werden (siehe [Übersicht über Transformationen](../graphics-multimedia/transforms-overview.md)).

- Inhalte innerhalb von Add-in-Benutzeroberflächen, die von Zeichnungs Vorgängen <xref:System.Drawing> aus dem-Namespace gerendert werden, können Alpha Blending enthalten. Eine Add-in-Benutzeroberfläche und die Benutzeroberfläche der Host Anwendung, die die Benutzeroberfläche enthält, muss jedoch 100% nicht transparent sein. Anders ausgedrückt, muss die `Opacity` -Eigenschaft für beide auf 1 festgelegt werden.

- Wenn die <xref:System.Windows.Window.AllowsTransparency%2A> -Eigenschaft eines Fensters in der Host Anwendung, die eine Add-in-Benutzeroberfläche enthält `true`, auf festgelegt ist, ist das Add-in nicht sichtbar. Dies gilt auch, wenn die Add-in-Benutzeroberfläche 100% deckend ist (d. `Opacity` h., die-Eigenschaft hat den Wert 1).

- Eine Add-in-Benutzeroberfläche muss auf anderen WPF-Elementen in demselben Fenster auf oberster Ebene angezeigt werden.

- Ein <xref:System.Windows.Media.VisualBrush>Teil der Benutzeroberfläche eines Add-Ins kann nicht mithilfe von gerendert werden. Stattdessen kann das Add-in eine Momentaufnahme der generierten Benutzeroberfläche erstellen, um eine Bitmap zu erstellen, die mithilfe von Methoden, die durch den Vertrag definiert werden, an die Host Anwendung übergeben werden kann.

- Mediendateien können nicht von einem <xref:System.Windows.Controls.MediaElement> in einer Add-in-Benutzeroberfläche abgespielt werden.

- Mausereignisse, die für die Add-in-Benutzeroberfläche generiert werden, werden von der Host Anwendung weder `IsMouseOver` empfangen noch ausgelöst, und die-Eigenschaft für `false`die Benutzeroberfläche der Host Anwendung hat den Wert.

- Wenn sich der Fokus zwischen Steuerelementen in einer Add-in- `GotFocus` Benutzer `LostFocus` Oberfläche verschiebt, werden das-Ereignis und das-Ereignis weder von der Host Anwendung empfangen noch ausgelöst.

- Der Teil einer Host Anwendung, die eine Add-in-Benutzeroberfläche enthält, wird beim Drucken weiß angezeigt.

- Alle Verteiler (siehe <xref:System.Windows.Threading.Dispatcher>), die von der Add-in-Benutzeroberfläche erstellt wurden, müssen manuell heruntergefahren werden, bevor das Besitzer-Add-in entladen wird, wenn die Host Anwendung die Ausführung fortsetzt. Mit dem Vertrag können Methoden implementiert werden, die es der Host Anwendung ermöglichen, das Add-in zu signalisieren, bevor das Add-in entladen wird. Dadurch kann die Add-in-Benutzeroberfläche ihre Verteiler beenden.

- Wenn eine Add-in-Benutzeroberfläche <xref:System.Windows.Controls.InkCanvas> ein ist oder <xref:System.Windows.Controls.InkCanvas>ein enthält, können Sie das Add-in nicht entladen.

<a name="PerformanceOptimization"></a>

## <a name="performance-optimization"></a>Leistungsoptimierung

Wenn mehrere Anwendungs Domänen verwendet werden, werden standardmäßig die verschiedenen .NET Framework Assemblys, die von jeder Anwendung benötigt werden, in die Domäne dieser Anwendung geladen. Aufgrund der Zeit, die zum Erstellen neuer Anwendungsdomänen und für das Starten der darin enthaltenen Anwendungen erforderlich ist, kann die Leistung beeinträchtigt werden. Die .NET Framework bietet jedoch die Möglichkeit, die Startzeiten zu verkürzen, indem Anwendungen angewiesen werden, Assemblys über Anwendungs Domänen hinweg freizugeben, wenn Sie bereits geladen sind. Verwenden Sie hierzu das <xref:System.LoaderOptimizationAttribute> -Attribut, das auf die Einstiegspunkt Methode (`Main`) angewendet werden muss. In diesem Fall müssen Sie lediglich zum Implementieren Ihrer Anwendungsdefinition Code verwenden (siehe [Übersicht über die Anwendungsverwaltung](application-management-overview.md)).

## <a name="see-also"></a>Siehe auch

- <xref:System.LoaderOptimizationAttribute>
- [Add-Ins und Erweiterbarkeit](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb384200(v%3dvs.100))
- [Anwendungsdomänen](../../app-domains/application-domains.md)
- [Übersicht über .NET Framework Remoting](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/kwdt6w2k(v=vs.100))
- [Erstellen von Objekten als remotable](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/wcf3swha(v=vs.100))
- [Themen zu Vorgehensweisen](how-to-topics.md)
