---
title: 'Importdeklarationen: Das open-Schlüsselwort'
description: Erfahren Sie mehr über F# Importdeklarationen und wie sie ein Modul oder einen Namespace angeben, dessen Elemente Sie ohne Verwendung eines vollqualifizierten Namens verweisen können.
ms.date: 04/04/2019
ms.openlocfilehash: 816bac551692c3397290f64c6267ee22e4ce90fb
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68630575"
---
# <a name="import-declarations-the-open-keyword"></a>Importdeklarationen: Das `open`-Schlüsselwort

> [!NOTE]
> Mit dem API-Referenz-Link in diesem Artikel gelangen Sie auf MSDN.  Die docs.microsoft.com-API-Referenz ist nicht abgeschlossen.

Eine *Import Deklaration* gibt ein Modul oder einen Namespace an, auf dessen Elemente verwiesen werden kann, ohne einen voll qualifizierten Namen zu verwenden.

## <a name="syntax"></a>Syntax

```fsharp
open module-or-namespace-name
```

## <a name="remarks"></a>Hinweise

Wenn Sie den voll qualifizierten Namespace-oder Modulpfad jedes Mal auf Code verweisen, können Sie Code erstellen, der schwer zu schreiben, zu lesen und zu warten ist. Stattdessen können Sie das `open` -Schlüsselwort für häufig verwendete Module und Namespaces verwenden, sodass Sie die Kurzform des Namens anstelle des voll qualifizierten Namens verwenden können, wenn Sie auf ein Member dieses Moduls oder Namespace verweisen. Dieses Schlüssel `using` Wort ähnelt dem-Schlüsselwort in `using namespace` C#, in C++Visual und `Imports` in Visual Basic.

Das angegebene Modul oder der angegebene Namespace muss sich im selben Projekt oder in einem referenzierten Projekt oder einer referenzierten Assembly befinden. Wenn dies nicht der Fall ist, können Sie dem Projekt einen Verweis hinzufügen oder die `-reference` Befehls`-`Zeilen Option (oder die Abkürzung, `-r`) verwenden. Weitere Informationen finden Sie unter [Compileroptionen](compiler-options.md).

Die Import Deklaration stellt die Namen im Code, der der Deklaration folgt, bis zum Ende des einschließenden Namespace, Moduls oder der Datei zur Verfügung.

Wenn Sie mehrere Import Deklarationen verwenden, sollten diese in separaten Zeilen angezeigt werden.

Der folgende Code zeigt die Verwendung des `open` -Schlüssel Worts, um Code zu vereinfachen.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet6801.fs)]

Der F# Compiler gibt keinen Fehler oder eine Warnung aus, wenn Mehrdeutigkeiten auftreten, wenn derselbe Name in mehreren geöffneten Modulen oder Namespaces auftritt. Wenn Mehrdeutigkeiten auftreten, bevorzugt F# die mehr zuletzt geöffneten Modul oder einen Namespace. Im `empty` folgenden Code `Seq` bedeutet `Seq.empty`beispielsweise, dass sich sowohl `List` im- `empty` Modul als auch im-Modul befindet.

```fsharp
open List
open Seq
printfn "%A" empty
```

Daher sollten Sie beim Öffnen von Modulen oder Namespaces wie `List` oder `Seq` , die Member mit identischen Namen enthalten, vorsichtig sein. verwenden Sie stattdessen die qualifizierten Namen. Vermeiden Sie jede Situation, in der der Code von der Reihenfolge der Import Deklarationen abhängig ist.

## <a name="namespaces-that-are-open-by-default"></a>Standardmäßig geöffnete Namespaces

Einige Namespaces werden so häufig im F# Code verwendet, dass Sie implizit geöffnet werden, ohne dass eine explizite Import Deklaration erforderlich ist. In der folgenden Tabelle werden die standardmäßig geöffneten Namespaces angezeigt.

|Namespace|Beschreibung|
|---------|-----------|
|`Microsoft.FSharp.Core`|Enthält Grund F# Legende Typdefinitionen für integrierte Typen, z `int` . b. und. `float`|
|`Microsoft.FSharp.Core.Operators`|Enthält grundlegende arithmetische Operationen `+` wie `*`und.|
|`Microsoft.FSharp.Collections`|Enthält unveränderliche Auflistungs Klassen, `List` z `Array`. b. und.|
|`Microsoft.FSharp.Control`|Enthält Typen für steuerungskonstrukte, wie z. b. Lazy Evaluation und asynchrone Workflows.|
|`Microsoft.FSharp.Text`|Enthält Funktionen für formatierte e/a, `printf` z. b. die Funktion.|

## <a name="autoopen-attribute"></a>AutoOpen-Attribut

Sie können das `AutoOpen` -Attribut auf eine Assembly anwenden, wenn Sie einen Namespace oder ein Modul automatisch öffnen möchten, wenn auf die Assembly verwiesen wird. Sie können auch das `AutoOpen` -Attribut auf ein Modul anwenden, um dieses Modul automatisch zu öffnen, wenn das übergeordnete Modul oder der übergeordnete Namespace geöffnet wird. Weitere Informationen finden Sie unter [Core. AutoOpenAttribute-Klasse](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.autoopenattribute-class-%5bfsharp%5d).

## <a name="requirequalifiedaccess-attribute"></a>Requirements qualifiedaccess-Attribut

Einige Module, Datensätze oder Union-Typen können das `RequireQualifiedAccess` -Attribut angeben. Wenn Sie auf Elemente dieser Module, Datensätze oder Unions verweisen, müssen Sie einen qualifizierten Namen verwenden, unabhängig davon, ob Sie eine Import Deklaration einschließen. Wenn Sie dieses Attribut bei Typen, die häufig verwendete Namen definieren, strategisch verwenden, vermeiden Sie Namenskollisionen und sorgen dadurch für eine stabilere Codeänderung gegenüber den Änderungen in Bibliotheken. Weitere Informationen finden Sie unter [Core. Requirements qualifiedaccessattribute-Klasse](https://msdn.microsoft.com/visualfsharpdocs/conceptual/core.requirequalifiedaccessattribute-class-%5Bfsharp%5D).

## <a name="see-also"></a>Siehe auch

- [F#-Sprachreferenz](index.md)
- [Namespaces](namespaces.md)
- [Module](modules.md)
