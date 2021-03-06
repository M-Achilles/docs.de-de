---
title: checked-Schlüsselwort – C#-Referenz
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- checked_CSharpKeyword
- checked
helpviewer_keywords:
- checked keyword [C#]
ms.assetid: 718a1194-988d-48a3-b089-d6ee8bd1608d
ms.openlocfilehash: 69bd8cc95012533a6be279b04dc883a56f6f78ea
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2019
ms.locfileid: "69605915"
---
# <a name="checked-c-reference"></a>checked (C#-Referenz)

Das Schlüsselwort `checked` wird verwendet, um eine Überlaufüberprüfung bei arithmetischen Operationen für ganzzahlige Typen und Konvertierungen explizit zu aktivieren.

Standardmäßig bewirkt ein Ausdruck, der nur konstante Werte enthält, einen Compilerfehler, wenn der Ausdruck einen Wert erzeugt, der außerhalb des Bereichs des Zieltyps liegt. Wenn der Ausdruck einen oder mehrere nicht konstante Werte enthält, erkennt der Compiler den Überlauf nicht. Die Auswertung des Ausdrucks, der im folgenden Beispiel `i2` zugewiesen ist, verursacht keinen Compilerfehler.

[!code-csharp[csrefKeywordsChecked#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#3)]

Standardmäßig werden diese nicht konstanten Ausdrücke zur Laufzeit auch nicht auf Überläufe überprüft und lösen keine Überlaufausnahmen aus. Das vorherige Beispiel zeigt -2,147,483,639 als Summe von zwei ganzen Zahlen.

Die Überlaufüberprüfung kann durch Compileroptionen, Umgebungskonfiguration oder Verwendung des `checked`-Schlüsselworts aktiviert werden. In den folgenden Beispielen wird veranschaulicht, wie Sie einen `checked`-Ausdruck oder einen `checked`-Block verwenden, um den Überlauf zu erkennen, der von der vorherigen Summe zur Laufzeit erzeugt wird. In beiden Beispielen wird eine Überlaufausnahme ausgelöst.

[!code-csharp[csrefKeywordsChecked#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#4)]

Das [unchecked](./unchecked.md)-Schlüsselwort kann verwendet werden, um die Überlaufüberprüfung zu verhindern.

## <a name="example"></a>Beispiel

Dieses Beispiel zeigt, wie mit `checked` die Überlaufüberprüfung zur Laufzeit aktiviert wird.

[!code-csharp[csrefKeywordsChecked#1](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsChecked/CS/csrefKeywordsChecked.cs#1)]

## <a name="c-language-specification"></a>C#-Sprachspezifikation

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Siehe auch

- [C#-Referenz](../index.md)
- [C#-Programmierhandbuch](../../programming-guide/index.md)
- [C#-Schlüsselwörter](./index.md)
- [AKtiviert und nicht aktiviert](./checked-and-unchecked.md)
- [unchecked](./unchecked.md)
