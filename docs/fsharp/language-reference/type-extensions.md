---
title: Typerweiterungen
description: Erfahren Sie F# , wie Sie mit Typerweiterungen einem zuvor definierten Objekttyp neue Member hinzufügen können.
ms.date: 02/08/2019
ms.openlocfilehash: 5d31d87095d3381e66dc32da4b6d7bb746886406
ms.sourcegitcommit: 6f28b709592503d27077b16fff2e2eacca569992
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2019
ms.locfileid: "70106844"
---
# <a name="type-extensions"></a>Typerweiterungen

Typerweiterungen (auch als _Erweiterungen_bezeichnet) sind eine Reihe von Funktionen, mit denen Sie einem zuvor definierten Objekttyp neue Member hinzufügen können. Die drei Features sind:

- Systeminterne Typerweiterungen
- Optionale Typerweiterungen
- Erweiterungsmethoden

Jede kann in verschiedenen Szenarien verwendet werden und hat unterschiedliche Kompromisse.

## <a name="syntax"></a>Syntax

```fsharp
// Intrinsic and optional extensions
type typename with
    member self-identifier.member-name =
        body
    ...

// Extension methods
open System.Runtime.CompilerServices

[<Extension>]
type Extensions() =
    [static] member self-identifier.extension-name (ty: typename, [args]) =
        body
    ...
```

## <a name="intrinsic-type-extensions"></a>Systeminterne Typerweiterungen

Eine intrinsische Typerweiterung ist eine Typerweiterung, die einen benutzerdefinierten Typ erweitert.

Systeminterne Typerweiterungen müssen in derselben Datei **und** im gleichen Namespace oder Modul wie der Typ, den Sie erweitern, definiert werden. Jede andere Definition führt zu [optionalen Typerweiterungen](type-extensions.md#optional-type-extensions).

Systeminterne Typerweiterungen sind manchmal eine saubere Möglichkeit, um die Funktionalität von der Typdeklaration zu trennen. Im folgenden Beispiel wird gezeigt, wie eine systeminterne Typerweiterung definiert wird:

```fsharp
namespace Example

type Variant =
    | Num of int
    | Str of string
  
module Variant =
    let print v =
        match v with
        | Num n -> printf "Num %d" n
        | Str s -> printf "Str %s" s

// Add a member to Variant as an extension
type Variant with
    member x.Print() = Variant.print x
```

Die Verwendung einer Typerweiterung ermöglicht es Ihnen, die folgenden voneinander zu trennen:

- Die Deklaration eines `Variant` Typs.
- Funktionalität zum Drucken der `Variant` Klasse, abhängig von ihrer Form.
- Eine Möglichkeit für den Zugriff auf die Druck Funktionalität mit Objekt `.`Stil Notation

Dies ist eine Alternative zum Definieren alles als Member in `Variant`. Obwohl es sich nicht um einen naturgemäß besseren Ansatz handelt, kann es in einigen Situationen eine saubere Darstellung der Funktionalität sein.

Systeminterne Typerweiterungen werden als Member des Typs, den Sie erweitern, kompiliert und für den Typ angezeigt, wenn der Typ durch Reflektion untersucht wird.

## <a name="optional-type-extensions"></a>Optionale Typerweiterungen

Eine optionale Typerweiterung ist eine Erweiterung, die außerhalb des ursprünglichen Moduls, Namespace oder der Assembly des erweiterten Typs angezeigt wird.

Optionale Typerweiterungen sind nützlich zum Erweitern eines Typs, den Sie nicht selbst definiert haben. Zum Beispiel:

```fsharp
module Extensions

open System.Collections.Generic

type IEnumerable<'T> with
    /// Repeat each element of the sequence n times
    member xs.RepeatElements(n: int) =
        seq {
            for x in xs do
                for i in 1 .. n do
                    yield x
        }
```

Sie können jetzt so `RepeatElements` aufrufen, als ob es ein Member <xref:System.Collections.Generic.IEnumerable%601> von ist, solange `Extensions` das Modul in dem Bereich geöffnet ist, in dem Sie arbeiten.

Optionale Erweiterungen werden nicht für den erweiterten Typ angezeigt, wenn Sie durch Reflektion untersucht werden. Optionale Erweiterungen müssen sich in Modulen befinden und befinden sich nur im Gültigkeitsbereich, wenn das Modul, das die Erweiterung enthält, geöffnet ist oder sich andernfalls im Gültigkeitsbereich befindet.

Member optionaler Erweiterungen werden in statische Member kompiliert, für die die Objektinstanz implizit als erster Parameter übergeben wird. Sie agieren jedoch so, als ob Sie Instanzmember oder statische Member sind, je nachdem, wie Sie deklariert werden.

Optionale Erweiterungs Mitglieder sind auch für C# -oder-VB-Consumer nicht sichtbar. Sie können nur in anderem F# Code verwendet werden.

## <a name="generic-limitation-of-intrinsic-and-optional-type-extensions"></a>Generische Einschränkung von systeminternen und optionalen Typerweiterungen

Es ist möglich, eine Typerweiterung für einen generischen Typ zu deklarieren, bei dem die Typvariable eingeschränkt ist. Die Anforderung ist, dass die Einschränkung der Erweiterungs Deklaration mit der Einschränkung des deklarierten Typs übereinstimmt.

Auch wenn Einschränkungen zwischen einem deklarierten Typ und einer Typerweiterung abgeglichen werden, ist es möglich, dass eine Einschränkung durch den Text eines erweiterten Members abgeleitet wird, der eine andere Anforderung für den Typparameter als den deklarierten Typ auferlegt. Zum Beispiel:

```fsharp
open System.Collections.Generic

// NOT POSSIBLE AND FAILS TO COMPILE!
//
// The member 'Sum' has a different requirement on 'T than the type IEnumerable<'T>
type IEnumerable<'T> with
    member this.Sum() = Seq.sum this
```

Es gibt keine Möglichkeit, diesen Code zu erhalten, um mit einer optionalen Typerweiterung zu arbeiten:

- Der `Sum` Member hat eine andere Einschränkung für `'T` (`static member get_Zero` und `static member (+)`) als für die Typerweiterung definiert ist.
- Wenn Sie die Typerweiterung so ändern, dass Sie `Sum` die gleiche Einschränkung wie hat, stimmt nicht `IEnumerable<'T>`mehr mit der definierten Einschränkung für überein.
- Wenn `member this.Sum` Sie `member inline this.Sum` in ändern, wird ein Fehler ausgegeben, dass Typeinschränkungen nicht übereinstimmen.

Was gewünscht ist, sind statische Methoden, die "float in Space" sind, und können so dargestellt werden, als ob Sie einen Typ erweitern. An dieser Stelle werden Erweiterungs Methoden benötigt.

## <a name="extension-methods"></a>Erweiterungsmethoden

Schließlich können Erweiterungsmethoden (manchmal als "Erweiterungsmember des C#-Stil" bezeichnet) in F# als statische Membermethode in einer Klasse deklariert werden.

Erweiterungs Methoden sind hilfreich, wenn Sie Erweiterungen für einen generischen Typ definieren möchten, der die Typvariable einschränkt. Zum Beispiel:

```fsharp
namespace Extensions

open System.Runtime.CompilerServices

[<Extension>]
type IEnumerableExtensions() =
    [<Extension>]
    static member inline Sum(xs: IEnumerable<'T>) = Seq.sum xs
```

Wenn Sie verwendet wird, wird dieser Code so angezeigt, `Sum` als ob für <xref:System.Collections.Generic.IEnumerable%601>definiert ist, `Extensions` solange geöffnet ist oder sich im Gültigkeitsbereich befindet.

## <a name="other-remarks"></a>Weitere Hinweise

Typerweiterungen verfügen auch über die folgenden Attribute:

- Alle Typen, auf die zugegriffen werden kann, können erweitert werden.
- Systeminterne und optionale Typerweiterungen können _einen beliebigen_ Elementtyp definieren, nicht nur Methoden. Erweiterungs Eigenschaften sind z. b. ebenfalls möglich.
- Das `self-identifier` Token in der [Syntax](type-extensions.md#syntax) stellt die Instanz des aufgerufenen Typs dar, genau wie normale Member.
- Erweiterte Member können statische Member oder Instanzmember sein.
- Typvariablen für eine Typerweiterung müssen mit den Einschränkungen des deklarierten Typs identisch sein.

Für Typerweiterungen gibt es auch die folgenden Einschränkungen:

- Typerweiterungen unterstützen keine virtuellen oder abstrakten Methoden.
- Typerweiterungen unterstützen keine Überschreibungs Methoden als Erweiterungen.
- Typerweiterungen unterstützen keine [statisch aufgelösten Typparameter](./generics/statically-resolved-type-parameters.md).
- Optionale Typerweiterungen unterstützen keine Konstruktoren als Erweiterungen.
- Typerweiterungen können nicht für [typabkürzungen](type-abbreviations.md)definiert werden.
- Typerweiterungen sind für `byref<'T>` ungültig (obwohl Sie deklariert werden können).
- Typerweiterungen sind für Attribute ungültig (Sie können jedoch als deklariert werden).
- Sie können definieren, Erweiterungen, die andere Methoden, mit dem gleichen Namen zu überladen, aber F#-Compiler bevorzugt nicht-Erweiterungsmethoden gibt es ist ein Mehrdeutiger Aufruf.

Wenn zum Schluss mehrere systeminterne Typerweiterungen für einen Typ vorhanden sind, müssen alle Elemente eindeutig sein. Bei optionalen Typerweiterungen können Member in unterschiedlichen Typerweiterungen, die auf den gleichen Typ erweitert werden, die gleichen Namen aufweisen. Mehrdeutigkeitsfehler treten nur auf, wenn Clientcode zwei unterschiedliche Gültigkeitsbereiche öffnet, die die gleichen Membernamen definieren.

## <a name="see-also"></a>Siehe auch

- [F#-Sprachreferenz](index.md)
- [Mitglieder](./members/index.md)
