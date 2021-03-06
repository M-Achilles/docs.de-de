---
title: Migrationsanleitung
ms.date: 03/30/2017
ms.assetid: cb65c132-58c9-4028-b3d4-1efc71d5e60e
ms.openlocfilehash: 45f81b29f63701f690e396de2e9834f9933fd775
ms.sourcegitcommit: bbfcc913c275885381820be28f61efcf8e83eecc
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2019
ms.locfileid: "68796801"
---
# <a name="migration-guidance"></a>Migrationsanleitung
[!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]In gibt Microsoft die zweite Hauptversion von Windows Workflow Foundation (WF) frei. [!INCLUDE[wf1](../../../includes/wf1-md.md)]wurde in WinFX veröffentlicht (das enthielt die Typen in System. Workflow.\* Namespaces, die jetzt als WF3 bezeichnet werden) und wurde in [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)]erweitert. WF3 ist auch Bestandteil von [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)], ist aber dort neben neuer Workflow Technologie vorhanden (die Typen in System. Activities.\* Namespaces, die als WF4 bezeichnet werden). Beim Erwägen des Zeitpunkts für die Umstellung auf WF4 sollten Sie zuerst bedenken, dass Sie allein den zeitlichen Ablauf steuern können.  
  
- WF3 ist ein vollständig unterstützter Teil von [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)].  
  
- WF3-Anwendungen werden unter [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] ohne Änderung ausgeführt und weiterhin voll unterstützt.  
  
- Neue WF3-Anwendungen können erstellt werden, und vorhandene Anwendungen können in Visual Studio 2012 bearbeitet werden und werden vollständig unterstützt.  
  
 Daher ist die Entscheidung, die .NET Framework 4 zu übernehmen, von ihrer Entscheidung, zu WF4 (System. Activities.\*) von WF3 (System. Workflow.\*) zu wechseln, entkoppelt. Dieses Thema enthält Links zu WF-Migrationsanleitungen mit Informationen zum Arbeiten mit WF3 und WF4.  
  
## <a name="wf-migration-whitepapers-and-cookbooks"></a>Whitepaper und Cookbooks zur WF-Migration  
 Das Thema Übersicht über die [WF-Migration](https://go.microsoft.com/fwlink/?LinkId=153873) bietet eine umfassende Übersicht über die Beziehung zwischen WF3 und WF4 und Migrationsstrategien. Speziellere Themenbereiche werden in Begleitthemen behandelt.  
  
 [Übersicht der WF-Migration](https://go.microsoft.com/fwlink/?LinkId=153873)  
 Beschreibt die Beziehung zwischen WF3 und WF4 sowie die Optionen, die Sie als Benutzer oder potenzieller Benutzer der Workflowtechnologie unter .NET 4 haben.  
  
 [WF-Migration: Bewährte Methoden für die WF3-Entwicklung](https://go.microsoft.com/fwlink/?LinkId=153852)  
 Beschreibt, wie Sie WF3-Artefakte so entwerfen, dass diese einfacher nach WF4 migriert werden können.  
  
 [WF-Leitfaden: Werks](https://go.microsoft.com/fwlink/?LinkId=153854)  
 Erläutert, wie Sie regelbezogene Investitionen in [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]-Projektmappen umsetzen.  
  
 [WF-Leitfaden: Zustands Automat](https://go.microsoft.com/fwlink/?LinkId=153855)  
 Erläutert die WF4-Ablaufsteuerungsmodellierung bei Nichtvorhandensein einer Zustandsautomataktivität (State Machine).  
  
 Beachten Sie, dass diese Anleitung nur für Workflowprojekte gilt, die .NET Framework 4 als Zielframework verwenden. Zustandsautomatworkflows wurden in .NET 4.0.1 mit dem Plattform Update 1 hinzugefügt und in .NET Framework 4.5 beibehalten. Weitere Informationen zu Zustandsautomatworkflows in .NET 4.0.1-4.0.3 und .NET Framework 4,5 finden Sie unter [Update 4.0.1 for Microsoft .NET Framework 4 Features](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/hh290669(v=vs.100)) und [State Machine Workflows](state-machine-workflows.md).  
  
 [Cookbook zur WF-Migration: Benutzerdefinierte Aktivitäten](https://go.microsoft.com/fwlink/?LinkId=153856)  
 Enthält Beispiele und Anweisungen zum Umgestalten von benutzerdefinierten WF3-Aktivitäten unter WF4.  
  
 [Cookbook zur WF-Migration: Erweiterte benutzerdefinierte Aktivitäten](https://go.microsoft.com/fwlink/?LinkId=275560)  
 Stellt eine Anleitung zur Neuentwicklung erweiterter benutzerdefinierter WF3-Aktivitäten bereit, die WF3-Warteschlangen verwenden und untergeordnete Aktivitäten als benutzerdefinierte WF4-Aktivitäten planen.  
  
 [Cookbook zur WF-Migration: Workflows](https://go.microsoft.com/fwlink/?LinkId=153858)  
 Enthält Beispiele und Anleitungen zum Umgestalten von WF3-Workflows unter WF4.  
  
 [Cookbook zur WF-Migration: Workflow Hosting](https://go.microsoft.com/fwlink/?LinkId=275561)  
 Stellt eine Anleitung zur Umgestaltung des WF3-Hostingcodes als WF4-Hostingcode bereit. Damit sollen die wesentlichen Unterschiede beim Workflowhosting zwischen WF3 und WF4 veranschaulicht werden.  
  
 [Cookbook zur WF-Migration: Workflow Überwachung](https://go.microsoft.com/fwlink/?LinkId=275562)  
 Bietet Hilfestellung bei der Umgestaltung von WF3-Nachverfolgungscode und -Konfiguration mithilfe eines äquivalenten Nachverfolgungscodes und einer äquivalenten Konfiguration auf der Basis von WF4.  
  
 [WF-Leitfaden: Workflow Dienste](https://go.microsoft.com/fwlink/?LinkId=275564)  
 Stellt anhand eines Beispiels schrittweise Anweisungen zur Neuentwicklung von Workflows bereit, die in WF3 erstellte Windows Communication Foundation (WCF)-Webdienste (auch als Workflowdienste bezeichnet) für die Verwendung allgemeiner, vordefinierter Aktivitäten in WF4 implementieren.  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Activities.Statements.Interop>
