---
title: goto-Anweisung – C#-Referenz
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- goto_CSharpKeyword
- goto
helpviewer_keywords:
- goto keyword [C#]
ms.assetid: 2c03c9c1-8119-44ef-b740-fb3d287a42fe
ms.openlocfilehash: 675893f02a0022b403d2afc018d24d6f826b8f75
ms.sourcegitcommit: 10986410e59ff29f2ec55c6759bde3eb4d1a00cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66421802"
---
# <a name="goto-c-reference"></a>goto (C#-Referenz)

Die `goto`-Anweisung überträgt die Programmsteuerung direkt an eine Anweisung mit Bezeichnung.

`goto` wird häufig dazu verwendet, eine bestimmte Parameterbezeichnung oder die Standardbezeichnung in einer `switch`-Anweisung zu steuern.

Mit der `goto`-Anweisung können Sie auch tief geschachtelte Schleifen verlassen.

## <a name="example"></a>Beispiel

Im folgenden Beispiel wird die Verwendung von `goto` in einer [switch](switch.md)-Anweisung veranschaulicht.

[!code-csharp[csrefKeywordsJump#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#4)]

## <a name="example"></a>Beispiel

Im folgenden Beispiel wird die Verwendung von `goto` zum Verlassen geschachtelter Schleifen veranschaulicht.

[!code-csharp[csrefKeywordsJump#5](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsJump/CS/csrefKeywordsJump.cs#5)]

## <a name="c-language-specification"></a>C#-Sprachspezifikation

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Siehe auch

- [C#-Referenz](../index.md)
- [C#-Programmierhandbuch](../../programming-guide/index.md)
- [C#-Schlüsselwörter](index.md)
- [goto-Anweisung (C++)](/cpp/cpp/goto-statement-cpp)
