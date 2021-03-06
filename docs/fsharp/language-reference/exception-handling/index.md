---
title: Ausnahmebehandlung
description: Grundlagen der Ausnahmebehandlung in F# sowie Links zu Ausnahmebehandlung, Ausdrücke und Funktionen.
ms.date: 05/16/2016
ms.openlocfilehash: 0f4e57bfd643cba3dab5281df484ebb6162cb4b7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65645481"
---
# <a name="exception-handling"></a>Ausnahmebehandlung

Dieser Abschnitt enthält Informationen über die Unterstützung für die Ausnahmebehandlung in der Sprache F#.

## <a name="exception-handling-basics"></a>Grundlagen der Ausnahmebehandlung
Die Ausnahmebehandlung ist die Standardmethode zum Behandeln von Fehlerbedingungen in .NET Framework. Daher muss jede .NET-Sprache diesen Mechanismus unterstützen, einschließlich F#. Eine *Ausnahme* ist ein Objekt, das Information über einen Fehler kapselt. Wenn Fehler auftreten, werden Ausnahmen ausgelöst, und die reguläre Ausführung wird beendet. Stattdessen sucht die Laufzeit nach einem passenden Handler für die Ausnahme. Die Suche beginnt in der aktuellen Funktion und wird im Stapel in den höheren Ebenen der Aufrufer fortgesetzt, bis ein entsprechender Handler gefunden wird. Anschließend wird der Handler ausgeführt.

Zudem führt die Laufzeit beliebigen Code in `finally`-Blöcken aus, wenn der Stapel entladen wird, um sicherzustellen, dass Objekte ordnungsgemäß während des Endladungsprozesses bereinigt werden.

## <a name="related-topics"></a>Verwandte Themen

|Titel|Beschreibung|
|-----|-----------|
|[Ausnahmetypen](exception-types.md)|Beschreibt, wie ein Ausnahmetyp deklariert wird|
|[Ausnahmen: Die `try...with` Ausdruck](the-try-with-expression.md)|Beschreibt das Sprachkonstrukt, das Ausnahmebehandlung unterstützt|
|[Ausnahmen: Die `try...finally` Ausdruck](the-try-finally-expression.md)|Beschreibt das Sprachkonstrukt, mit dem Sie Bereinigungscode auszuführen können, während der Stapel entladen wird, wenn eine Ausnahme ausgelöst wird|
|[Ausnahmen: Die `raise`-Funktion](the-raise-Function.md)|Beschreibt, wie ein Ausnahmeobjekt ausgelöst wird|
|[Ausnahmen: Die `failwith` Funktion](the-failwith-function.md)|Beschreibt, wie eine allgemeine F#-Ausnahme generiert wird|
|[Ausnahmen: Die `invalidArg` Funktion](the-invalidArg-function.md)|Beschreibt, wie eine ungültige Argumentausnahme generiert wird|
