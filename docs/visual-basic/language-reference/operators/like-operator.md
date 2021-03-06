---
title: Like-Operator (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- Like
- vb.Like
helpviewer_keywords:
- similar to
- pattern matching
- Like operator [Visual Basic]
- '? symbol, wildcard character'
- string comparison [Visual Basic], Like operator
- strings [Visual Basic], comparing
- comparison operators [Visual Basic]
- symbols, wildcard
- wildcards, Like operator
- strings [Visual Basic], matching
- string comparison [Visual Basic], sorting data
- data [Visual Basic], sorting
- text [Visual Basic], comparing
- operators [Visual Basic], pattern-matching
- data [Visual Basic], string comparisons
- string comparison [Visual Basic], Like operators
ms.assetid: 966283ec-80e2-4294-baa8-c75baff804f9
ms.openlocfilehash: 795ecc2e80d57af29ccd50c50d2dd209c6425e40
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701133"
---
# <a name="like-operator-visual-basic"></a>Like-Operator (Visual Basic)
Vergleicht eine Zeichenfolge mit einem Muster.  

> [!IMPORTANT]
> Der `Like`-Operator wird derzeit in .net Core-und .NET Standard-Projekten nicht unterstützt.

## <a name="syntax"></a>Syntax  
  
```vb  
result = string Like pattern  
```  
  
## <a name="parts"></a>Teile  
 `result`  
 Erforderlich. Beliebige `Boolean`-Variable. Das Ergebnis ist ein `Boolean`-Wert, der angibt, ob die `string` der `pattern` entspricht.  
  
 `string`  
 Erforderlich. Beliebiger `String` -Ausdruck.  
  
 `pattern`  
 Erforderlich. Jeder `String`-Ausdruck, der den in "Anmerkungen" beschriebenen Muster Vergleichs Konventionen entspricht.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Wert in `string` dem Muster entspricht, das in `pattern` enthalten ist, ist `result` `True`. Wenn die Zeichenfolge das Muster nicht erfüllt, ist `result` `False`. Wenn sowohl `string` als auch `pattern` leere Zeichen folgen sind, ist das Ergebnis `True`.  
  
## <a name="comparison-method"></a>Vergleichsmethode  
 Das Verhalten des `Like`-Operators hängt von der [Option Compare-Anweisung](../../../visual-basic/language-reference/statements/option-compare-statement.md)ab. Die standardmäßige Zeichen folgen Vergleichsmethode für jede Quelldatei ist `Option Compare Binary`.  
  
## <a name="pattern-options"></a>Muster Optionen  
 Der integrierte Musterabgleich bietet ein vielseitiges Tool für Zeichen folgen Vergleiche. Die Muster Vergleichs Features ermöglichen es Ihnen, jedes Zeichen in `string` mit einem bestimmten Zeichen, einem Platzhalter Zeichen, einer Zeichen Liste oder einem Zeichenbereich abzugleichen. In der folgenden Tabelle sind die Zeichen aufgeführt, die in `pattern` zulässig sind, sowie ihre Entsprechung.  
  
|Zeichen in `pattern`|Übereinstimmungen in `string`|  
|-----------------------------|-------------------------|  
|`?`|Ein beliebiges einzelnes Zeichen|  
|`*`|NULL oder mehr Zeichen|  
|`#`|Eine beliebige einzelne Ziffer (0 – 9)|  
|`[charlist]`|Beliebiges einzelnes Zeichen in `charlist`|  
|`[!charlist]`|Alle einzelnen Zeichen, die nicht in `charlist`|  
  
## <a name="character-lists"></a>Zeichen Listen  
 Eine Gruppe mit einem oder mehreren Zeichen (`charlist`), die in eckige Klammern (`[ ]`) eingeschlossen ist, kann verwendet werden, um ein beliebiges einzelnes Zeichen in `string` abzugleichen, und kann nahezu beliebigen Zeichencode enthalten, einschließlich Ziffern.  
  
 Ein Ausrufezeichen (`!`) am Anfang `charlist` bedeutet, dass eine Entsprechung erstellt wird, wenn ein beliebiges Zeichen mit Ausnahme der Zeichen in `charlist` in `string` gefunden wird. Bei Verwendung außerhalb von Klammern entspricht das Ausrufezeichen dem Wert selbst.  
  
## <a name="special-characters"></a>Sonderzeichen  
 Zum Abgleichen der Sonderzeichen Left eckige Klammer (`[`), Fragezeichen (`?`), Nummern Zeichen (`#`) und Sternchen (`*`), schließen Sie Sie in eckige Klammern ein. Die rechte eckige Klammer (`]`) kann nicht innerhalb einer Gruppe verwendet werden, um sich selbst abzugleichen, Sie kann jedoch außerhalb einer Gruppe als einzelnes Zeichen verwendet werden.  
  
 Die Zeichenfolge `[]` wird als Zeichenfolge der Länge 0 (null) betrachtet (`""`). Sie kann jedoch nicht Teil einer Zeichen Liste sein, die in eckige Klammern eingeschlossen ist. Wenn Sie überprüfen möchten, ob eine Position in `string` mindestens eine Zeichen Gruppe oder kein Zeichen enthält, können Sie `Like` zweimal verwenden. Ein Beispiel finden Sie unter [Gewusst wie: Entsprechung für eine Zeichenfolge mit einem Muster @ no__t-0.  
  
## <a name="character-ranges"></a>Zeichen Bereiche  
 Durch die Verwendung eines Bindestrichs (`–`) zum Trennen der unteren und oberen Begrenzungen des Bereichs kann `charlist` einen Zeichenbereich angeben. Beispielsweise führt `[A–Z]` zu einer Übereinstimmung, wenn die entsprechende Zeichenposition in `string` ein beliebiges Zeichen innerhalb des Bereichs `A` – `Z` enthält, und `[!H–L]` ergibt eine Übereinstimmung, wenn die entsprechende Zeichenposition ein beliebiges Zeichen außerhalb des Bereich `H` – `L`.  
  
 Wenn Sie einen Zeichenbereich angeben, müssen Sie in aufsteigender Sortierreihenfolge angezeigt werden, d. h. von der niedrigsten zur höchsten. Daher ist `[A–Z]` ein gültiges Muster, `[Z–A]` jedoch nicht.  
  
### <a name="multiple-character-ranges"></a>Mehrere Zeichen Bereiche  
 Wenn Sie mehrere Bereiche für dieselbe Zeichenposition angeben möchten, platzieren Sie Sie ohne Trennzeichen in denselben Klammern. Beispielsweise führt `[A–CX–Z]` zu einer Übereinstimmung, wenn die entsprechende Zeichenposition in `string` ein beliebiges Zeichen innerhalb des Bereichs `A` – `C` oder den Bereich `X` – `Z` enthält.  
  
### <a name="usage-of-the-hyphen"></a>Verwendung des Bindestrichs  
 Ein Bindestrich (`–`) kann entweder am Anfang (nach einem Ausrufezeichen, falls vorhanden) oder am Ende von `charlist` angezeigt werden, um sich selbst abzugleichen. An einem beliebigen anderen Speicherort identifiziert der Bindestrich einen Zeichenbereich, der durch die Zeichen auf beiden Seiten des Bindestrichs getrennt ist.  
  
## <a name="collating-sequence"></a>Sortierreihenfolge  
 Die Bedeutung eines bestimmten Bereichs hängt von der Zeichenfolge zur Laufzeit ab, wie von `Option Compare` festgelegt, und der Gebiets Schema Einstellung des Systems, auf dem der Code ausgeführt wird. Bei `Option Compare Binary` entspricht der Bereich `[A–E]` `A`, `B`, `C`, `D` und `E`. Mit `Option Compare Text` entspricht `[A–E]` `A`, `a`, `À`, `à`, `B`, `b`, `C`, `c`, 0, 1, 2 und 3. Der Bereich entspricht nicht `Ê` oder `ê`, da die Zeichen nach Zeichen in der Sortierreihenfolge in der Sortierreihenfolge nach Zeichen sortiert werden.  
  
## <a name="digraph-characters"></a>Digraph-Zeichen  
 In einigen Sprachen gibt es alphabetische Zeichen, die zwei separate Zeichen darstellen. Beispielsweise verwenden mehrere Sprachen das Zeichen `æ`, um die Zeichen `a` und `e` darzustellen, wenn Sie gleich angezeigt werden. Der `Like`-Operator erkennt, dass das einzelne Digraph-Zeichen und die beiden einzelnen Zeichen gleichwertig sind.  
  
 Wenn in den Einstellungen des System Gebiets Schemas eine Sprache mit einem Digraph-Zeichen angegeben wird, entspricht das Vorkommen des einzelnen Digraph-Zeichens in `pattern` oder `string` der entsprechenden 2-Zeichen-Sequenz in der anderen Zeichenfolge. Entsprechend entspricht ein Digraph-Zeichen in `pattern`, das in eckige Klammern (selbst, in einer Liste oder in einem Bereich) eingeschlossen ist, mit der entsprechenden 2-Zeichen-Sequenz in `string`.  
  
## <a name="overloading"></a>Überladen  
 Der `Like`-Operator kann *überladen*werden. Dies bedeutet, dass eine Klasse oder Struktur das Verhalten neu definieren kann, wenn ein Operand den Typ dieser Klasse oder Struktur aufweist. Wenn Ihr Code diesen Operator für eine solche Klasse oder Struktur verwendet, stellen Sie sicher, dass Sie das neu definierte Verhalten verstehen. Weitere Informationen finden Sie unter [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Beispiel  
 In diesem Beispiel wird der `Like`-Operator zum Vergleichen von Zeichen folgen mit verschiedenen Mustern verwendet. Die Ergebnisse werden in eine `Boolean`-Variable umgewandelt, die angibt, ob jede Zeichenfolge dem Muster entspricht.  
  
 [!code-vb[VbVbalrOperators#30](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#30)]  
  
## <a name="see-also"></a>Siehe auch

- <xref:Microsoft.VisualBasic.Strings.InStr%2A>
- <xref:Microsoft.VisualBasic.Strings.StrComp%2A>
- [Vergleichsoperatoren](../../../visual-basic/language-reference/operators/comparison-operators.md)
- [Operator Precedence in Visual Basic (Operatorrangfolge in Visual Basic)](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [Nach Funktionalität sortierte Operatoren](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [Option Compare-Anweisung](../../../visual-basic/language-reference/statements/option-compare-statement.md)
- [Operatoren und Ausdrücke](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)
- [Vorgehensweise: Entsprechung für eine Zeichenfolge mit einem Muster @ no__t-0
