---
title: do – C#-Referenz
ms.custom: seodec18
ms.date: 05/28/2018
f1_keywords:
- do_CSharpKeyword
- do
helpviewer_keywords:
- do keyword [C#]
ms.assetid: 50725f79-9ba6-4898-aa78-6e331568a1bb
ms.openlocfilehash: 5566965e77feb9d46584146829284e9e0be71539
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66422041"
---
# <a name="do-c-reference"></a>do (C#-Referenz)

Die Anweisung `do` führt eine Anweisung oder einen Anweisungsblock aus, während ein angegebener boolescher Ausdruck `true` ergibt. Da der Ausdruck nach jeder Ausführung der Schleife ausgewertet wird, wird eine `do-while`-Schleife mindestens einmal ausgeführt. Dies unterscheidet sich von der [while](while.md)-Schleife, die entweder nie oder mehrmals ausgeführt wird.

Sie können zu jedem Zeitpunkt im Anweisungsblock `do` aus der Schleife ausbrechen, indem Sie die Anweisung [break](break.md) verwenden.

Sie können mithilfe der [continue](continue.md)-Anweisung direkt die Auswertung des `while`-Ausdrucks ausführen. Wenn der Ausdruck `true` ergibt, wird die Ausführung bei der ersten Anweisung in der Schleife fortgesetzt. Andernfalls wird die Ausführung mit der ersten Anweisung nach der Schleife ausgeführt.

Sie können eine `do-while`-Schleife auch mit den Anweisungen [goto](goto.md), [return](return.md) oder [throw](throw.md) beenden.

## <a name="example"></a>Beispiel

Im folgenden Beispiel wird die Verwendung der `do`-Anweisung veranschaulicht. Klicken Sie auf **Run** (Ausführen), um den Beispielcode auszuführen. Danach können Sie Änderungen am Code vornehmen und ihn erneut ausführen.

[!code-csharp-interactive[do loop example](~/samples/snippets/csharp/keywords/IterationKeywordsExamples.cs#4)]

## <a name="c-language-specification"></a>C#-Sprachspezifikation

Weitere Informationen finden Sie im Abschnitt [Die do-Anweisung](~/_csharplang/spec/statements.md#the-do-statement) der [C#-Sprachspezifikation](../language-specification/index.md).

## <a name="see-also"></a>Siehe auch

- [C#-Referenz](../index.md)
- [C#-Programmierhandbuch](../../programming-guide/index.md)
- [C#-Schlüsselwörter](index.md)
- [while-Anweisung](while.md)
