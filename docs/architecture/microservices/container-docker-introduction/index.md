---
title: Einführung in Container und Docker
description: .NET-Microservices-Architektur für .NET-Containeranwendungen | Einführung in Container und Docker
ms.date: 08/31/2018
ms.openlocfilehash: cb6244939f6ae89ba1dc824b55a21d1e010cef5e
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "70295144"
---
# <a name="introduction-to-containers-and-docker"></a>Einführung in Container und Docker

Das Containerisieren ist ein Ansatz in der Softwareentwicklung, bei dem eine Anwendung oder ein Dienst sowie die zugehörigen Abhängigkeiten und Konfigurationen (abstrahiert als Bereitstellungsmanifestdateien) zusammen als Containerimage verpackt werden. Die Containeranwendung kann als Einheit getestet und als Instanz eines Containerimages für das Hostbetriebssystem (OS) bereitgestellt werden.

So wie das Versenden von Containern es ermöglicht, Güter unabhängig von der enthaltenen Fracht per Schiff, Zug oder LKW zu transportieren, agieren Softwarecontainer als Standardeinheit für Softwarebereitstellung und können verschiedenen Code und verschiedene Abhängigkeiten enthalten. Das Containerisieren von Software auf diese Weise ermöglicht es Entwicklern und IT-Experten, diese ohne oder mit geringfügigen Änderungen in verschiedenen Umgebungen bereitzustellen.

Container isolieren Anwendungen auf einem gemeinsamen Betriebssystem außerdem voneinander. Containeranwendungen werden auf einem Containerhost ausgeführt, der auf dem Betriebssystem (Linux oder Windows) ausgeführt wird. Daher haben Container einen erheblich geringeren Speicherbedarf als die Images für virtuelle Computer (VM).

Jeder Container kann wie in Abbildung 2-1 gezeigt eine gesamte Webanwendung oder einen gesamten Dienst ausführen. In diesem Beispiel ist Docker-Host ein Containerhost und App1, App2, Svc1 und Svc2 sind die Containeranwendungen oder -dienste.

![Zwei Anwendungen und zwei Dienste, die unter dem Betriebssystem in einer VM oder auf einem physischen Server ausgeführt werden.](./media/image1.png)

**Abbildung 2-1**. Mehrere Container, die auf einem Containerhost ausgeführt werden

Ein weiterer Vorteil der Containerisierung ist die Skalierbarkeit. Ein schnelles Skalieren ist möglich, indem Sie neue Container für kurzfristige Aufgaben erstellen. Aus der Sicht einer Anwendung ähnelt das Instanziieren eines Images (Erstellen eines Containers) dem Instanziieren eines Prozesses wie ein Dienst oder eine Web-App. Für die Zuverlässigkeit beim Ausführen von mehreren Instanzen desselben Images auf mehreren Hostservern sollte jedoch jeder Container (Instanz des Images) auf einem anderen Hostserver oder virtuellen Computer in verschiedenen Fehlerdomänen ausgeführt werden.

Kurz gesagt bieten Container die Vorteile der Isolation, Portabilität, Agilität, Skalierbarkeit und Steuerung des gesamten Workflows des Lebenszyklus der Anwendung. Der wichtigste Vorteil ist die Isolation der Umgebung zwischen Entwicklung und Betrieb (Dev and Ops).

>[!div class="step-by-step"]
>[Zurück](../index.md)
>[Weiter](docker-defined.md)
