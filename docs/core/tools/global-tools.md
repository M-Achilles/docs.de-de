---
title: Globale .NET Core-Tools
description: Eine Übersicht über globale .NET Core-Tools und die .NET Core-CLI-Befehle, die ihnen zur Verfügung stehen.
author: KathleenDollard
ms.date: 05/29/2018
ms.custom: seodec18
ms.openlocfilehash: 40a0aabcf523e8dac9a3ad226064bbb3c1b3ce5b
ms.sourcegitcommit: 8b8dd14dde727026fd0b6ead1ec1df2e9d747a48
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71332020"
---
# <a name="net-core-global-tools-overview"></a>Übersicht über globale .NET Core-Tools

[!INCLUDE [topic-appliesto-net-core-21plus.md](../../../includes/topic-appliesto-net-core-21plus.md)]

Ein globales .NET Core-Tool ist ein spezielles NuGet-Paket, das eine Konsolenanwendung enthält. Ein globales Tool kann an einem benutzerdefinierten Speicherort oder einem Standardspeicherort auf ihrem Computer installiert werden, der in der Umgebungsvariable „PATH“ enthalten ist.

Wenn Sie ein globales .NET Core-Tool verwenden möchten:

* Erfahren Sie mehr über das Tool (in der Regel über eine Website oder GitHub-Seite).
* Überprüfen Sie den Autor und die Statistiken auf der Startseite des Feeds (in der Regel NuGet.org).
* Installieren Sie das Tool.
* Rufen Sie das Tool auf.
* Aktualisieren Sie das Tool.
* Deinstallieren Sie das Tool.

> [!IMPORTANT]
> Globale .NET Core-Tools werden in Ihrem Pfad angezeigt und mit voller Vertrauenswürdigkeit ausgeführt. Installieren Sie nur globale .NET Core-Tools von Autoren, denen Sie vertrauen.

## <a name="find-a-net-core-global-tool"></a>Finden eines globalen .NET Core-Tools

Derzeit gibt es kein Suchfeature für globale Tools in der .NET Core-CLI (Befehlszeilenschnittstelle).

Sie können globale .NET Core-Tools auf [NuGet](https://www.nuget.org) finden. Allerdings können Sie auf der NuGet-Website nicht spezifisch nach globalen .NET Core-Tools suchen.

Empfehlungen von Tools können Sie auch in Blogbeiträgen oder im GitHub-Repository [natemcmaster/dotnet-tools](https://github.com/natemcmaster/dotnet-tools) finden.

Sie können sich auch den Quellcode für die vom ASP.NET-Team erstellten globalen Tools im GitHub-Repository [aspnet/DotNetTools](https://github.com/aspnet/DotNetTools/) ansehen.

## <a name="check-the-author-and-statistics"></a>Überprüfen des Autors und der Statistiken

Da globale .NET Core-Tools mit voller Vertrauenswürdigkeit ausgeführt und in der Regel auf Ihrem Pfad installiert werden, können sie sehr nützlich sein. Laden Sie keine Tools von Personen herunter, denen Sie nicht vertrauen.

Wenn das Tool auf NuGet gehostet wird, können Sie den Autor und seine Statistiken überprüfen, indem Sie nach dem Tool suchen.

## <a name="install-a-global-tool"></a>Installieren eines globalen Tools

Verwenden Sie den .NET Core-CLI-Befehl [dotnet tool install](dotnet-tool-install.md), um ein globales Tool zu installieren. Im folgenden Beispiel wird gezeigt, wie ein globales Tool am Standardspeicherort installiert wird:

```dotnetcli
dotnet tool install -g dotnetsay
```

Wenn das Tool nicht installiert werden kann, werden Fehlermeldungen angezeigt. Stellen Sie sicher, dass die erwarteten Feeds überprüft werden.

Wenn Sie versuchen, eine Vorabversion oder eine spezifische Version des Tools zu installieren, können Sie die Versionsnummer im folgenden Format angeben:

```dotnetcli
dotnet tool install -g <package-name> --version <version-number>
```

Wenn die Installation erfolgreich abgeschlossen wurde, wird eine Meldung angezeigt, die den Befehl zum Aufrufen des Tools und die installierte Version ähnlich wie im folgenden Beispiel anzeigt:

```output
You can invoke the tool using the following command: dotnetsay
Tool 'dotnetsay' (version '2.0.0') was successfully installed.
```

Globale Tools können im Standardverzeichnis oder an einem spezifischen Speicherort installiert werden. Die Standardverzeichnisse sind:

| Betriebssystem          | Pfad                          |
|-------------|-------------------------------|
| Linux/macOS | `$HOME/.dotnet/tools`         |
| Windows     | `%USERPROFILE%\.dotnet\tools` |

Diese Speicherorte werden dem Pfad des Benutzers hinzugefügt, wenn das SDK zum ersten Mal ausgeführt wird, damit dort installierte globale Tools direkt aufgerufen werden können.

Beachten Sie, dass die globalen Tools benutzerspezifisch gespeichert werden und nicht global auf dem Computer. Deshalb können Sie kein globales Tool installieren, das für alle Benutzer auf dem Computer verfügbar ist. Das Tool ist nur für jedes Benutzerprofil verfügbar, auf denen das Tool installiert wurde.

Globale Tools können auch in einem spezifischen Verzeichnis installiert werden. Wenn sie in einem spezifischen Verzeichnis installiert werden, muss der Benutzer sicherstellen, dass der Befehl verfügbar ist, indem das Verzeichnis in den Pfad eingefügt, der Befehl mit dem angegebenen Verzeichnis aufgerufen oder das Tool aus dem angegebenen Verzeichnis aufgerufen wird.
In diesem Fall fügt die .NET Core-CLI diesen Speicherort nicht automatisch der Umgebungsvariable „PATH“ hinzu.

## <a name="use-the-tool"></a>Verwenden des Tools

Nachdem das Tool installiert wurde, können Sie es mit dem entsprechenden Befehl aufrufen. Beachten Sie, dass der Befehl möglicherweise nicht mit dem Paketnamen übereinstimmt.

Wenn der Befehl `dotnetsay` ist, rufen Sie ihn wie folgt auf:

```console
dotnetsay
```

Wenn der Autor des Tools das Tool im Kontext der `dotnet`-Eingabeaufforderung anzeigen wollte, ist es möglicherweise so geschrieben, dass Sie es als `dotnet <command>` aufrufen, zum Beispiel:

```dotnetcli
dotnet doc
```

Sie können herausfinden, welche Tools in einem installierten Paket globaler Tools enthalten sind, indem Sie den Befehl [dotnet tool list](dotnet-tool-list.md) verwenden.

Darüber hinaus können Sie sich die Anweisungen auf der Website zum Tool ansehen oder einen der folgenden Befehle eingeben:

```console
<command> --help
dotnet <command> --help
```

## <a name="other-cli-commands"></a>Andere CLI-Befehle

Das .NET Core SDK enthält andere Befehle, die globale .NET Core-Tools unterstützen. Verwenden Sie einen beliebigen `dotnet tool`-Befehl mit einer der folgenden Optionen:

* `--global` oder `-g` gibt an, dass der Befehl für benutzerweite globale Tools anwendbar ist.
* `--tool-path` legt einen benutzerdefinierten Speicherort für globale Tools fest.

So finden Sie heraus, welche Befehle für globale Tools verfügbar sind:

```dotnetcli
dotnet tool --help
```

Das Aktualisieren eines globalen Tools umfasst das Deinstallieren und Neuinstallieren mit der neuesten stabilen Version. Verwenden Sie den Befehl [dotnet tool update](dotnet-tool-update.md), um ein globales Tool zu aktualisieren:

```dotnetcli
dotnet tool update -g <packagename>
```

Entfernen Sie ein globales Tool mit [dotnet tool uninstall](dotnet-tool-uninstall.md):

```dotnetcli
dotnet tool uninstall -g <packagename>
```

Verwenden Sie den Befehl [dotnet tool list](dotnet-tool-list.md), um alle derzeit auf dem Computer installierten globalen Tools mit ihren Versionen und Befehlen anzuzeigen:

```dotnetcli
dotnet tool list -g
```

## <a name="see-also"></a>Siehe auch

* [Behandlung von Problemen bei der Nutzung von .NET Core-Tools](troubleshoot-usage-issues.md)
