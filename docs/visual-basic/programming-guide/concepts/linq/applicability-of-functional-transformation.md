---
title: Anwendbarkeit der funktionalen Transformation (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 3b74e134-e19b-44bc-8d06-e26c48305040
ms.openlocfilehash: 1903a59ec666c7d0b4c585abe5424cc1a0fd902d
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64642425"
---
# <a name="applicability-of-functional-transformation-visual-basic"></a>Anwendbarkeit der funktionalen Transformation (Visual Basic)
Reine funktionale Transformationen können in vielen Situationen angewendet werden.  
  
 Funktionale Transformationen sind hervorragend für das Abfragen und Bearbeiten strukturierter Daten geeignet, sodass dieser Ansatz gut zu LINQ-Technologien passt. Die Palette der Anwendungsmöglichkeiten der funktionalen Transformation ist aber viel größer als die bloße Verwendung mit LINQ. Alle Prozesse, bei denen es hauptsächlich um das Transformieren von Daten von einer Form in eine andere Form geht, sollten als potenzielle Kandidaten für die funktionale Transformation angesehen werden.  
  
 Dieser Ansatz ist auf viele Probleme anwendbar, die zunächst als nicht geeignet erscheinen mögen. Funktionale Transformationen können &#150; in Verbindung mit oder separat von LINQ &#150; für die folgenden Bereiche in Erwägung gezogen werden:  
  
- XML-basierte Dokumente: Wohlgeformte Daten eines beliebigen XML-Dialekts können durch funktionale Transformation leicht bearbeitet werden. Weitere Informationen finden Sie unter [funktionale Transformation von XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-transformation-of-xml.md).  
  
- Andere strukturierte Dateiformate: Angefangen bei <legacyBold>Windows.ini</legacyBold>-Dateien bis hin zu Nur-Text-Dokumenten besitzen die meisten Dateien eine gewisse Struktur, die zu Analyse- und Transformationszwecken verwendet werden kann.  
  
- Datenstreamingprotokolle: Das Codieren von Daten in und das Decodieren von Daten aus Kommunikationsprotokollen kann häufig als einfache funktionale Transformation dargestellt werden.  
  
- RDBMS- und OODBMS-Daten: Relationale und objektorientierte Datenbanken sind, wie XML, häufig verwendete strukturierte Datenquellen.  
  
- Mathematische, statistische und naturwissenschaftliche Lösungen: In diesen Bereichen werden gern große Datensätze bearbeitet, um den Benutzer bei der Visualisierung, Schätzung oder eigentlichen Lösung schwieriger Probleme zu unterstützen.  
  
 Siehe [Refactoring in reine Funktionen (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/refactoring-into-pure-functions.md), Verwendung von reinen Funktionen ist ein Beispiel der funktionalen Programmierung. Neben ihren unmittelbaren Vorteilen sorgt die Verwendung reiner Funktionen auch für wertvolle Erfahrungen, wenn es darum geht, Probleme aus der Perspektive einer funktionalen Transformation zu betrachten. Dieser Ansatz kann sich auch signifikant auf die Programm- und Klassenentwicklung auswirken. Dies gilt insbesondere dann, wenn sich ein Problem für eine Datentransformationslösung geradezu anbietet (siehe oben).  
  
 Da eine weitere Erläuterung dieses Themas den Rahmen dieses Lehrprogramms sprengen würde, sei hier nur so viel gesagt: Entwürfe, die von der Perspektive der funktionalen Transformation beeinflusst sind, sind tendenziell mehr auf Prozesse als auf Objekte als Hauptakteure ausgerichtet. Die sich so ergebende Lösung wird zumeist als Serie groß angelegter Transformationen implementiert, statt in Form individueller Objektzustandsänderungen.  
  
 In diesem Fall Denken Sie daran, dass Visual Basic unterstützt sowohl den imperativen als auch den funktionalen Ansatz, damit der optimale Entwurf für Ihre Anwendung der beide Elemente beinhaltet möglicherweise.  
  
## <a name="see-also"></a>Siehe auch

- [Einführung in reine funktionale Transformationen (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/introduction-to-pure-functional-transformations.md)
- [Funktionale Transformation von XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/functional-transformation-of-xml.md)
- [Refactoring in reine Funktionen (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/refactoring-into-pure-functions.md)
