---
title: Or-Operator (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.Or
helpviewer_keywords:
- Or operator [Visual Basic]
- operators [Visual Basic], bitwise
- inclusive Or operator [Visual Basic]
- bitwise operators [Visual Basic], OR operator
- Or keyword [Visual Basic]
- operators [Visual Basic], inclusive or
- operators [Visual Basic], disjunction
- bitwise comparison [Visual Basic]
- logical disjunction
- disjunction operator [Visual Basic]
ms.assetid: 41ed6905-bf3d-468a-9e3b-03c10d461891
ms.openlocfilehash: 03decb4ad32e8ff2c03e3b64a272bce779282973
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701237"
---
# <a name="or-operator-visual-basic"></a>Or-Operator (Visual Basic)
Führt eine logische Disjunktion für zwei `Boolean`-Ausdrücke oder eine bitweise Disjunktion zweier numerischer Ausdrücke aus.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
result = expression1 Or expression2  
```  
  
## <a name="parts"></a>Teile  
 `result`  
 Erforderlich. Ein `Boolean` beliebiger oder numerischer Ausdruck. Bei `Boolean`-Vergleich ist `result` die inklusivlogische Disjunktion zweier `Boolean`-Werte. Bei bitweisen Vorgängen ist `result` ein numerischer Wert, der die inklusive bitweise Disjunktion zweier numerischer Bitmuster darstellt.  
  
 `expression1`  
 Erforderlich. Ein `Boolean` beliebiger oder numerischer Ausdruck.  
  
 `expression2`  
 Erforderlich. Ein `Boolean` beliebiger oder numerischer Ausdruck.  
  
## <a name="remarks"></a>Hinweise  
 Bei `Boolean`-Vergleich ist `result` nur dann `False`, wenn `expression1` und `expression2` als `False` ausgewertet werden. In der folgenden Tabelle wird veranschaulicht, wie `result` bestimmt wird.  
  
|Wenn `expression1` ist|Und `expression2` ist|Der Wert von `result` ist|  
|-------------------------|--------------------------|------------------------------|  
|`True`|`True`|`True`|  
|`True`|`False`|`True`|  
|`False`|`True`|`True`|  
|`False`|`False`|`False`|  
  
> [!NOTE]
> Bei einem `Boolean`-Vergleich wertet der `Or`-Operator immer beide Ausdrücke aus, die das Ausführen von Prozedur aufrufen einschließen können. Der [OrElse-Operator](../../../visual-basic/language-reference/operators/orelse-operator.md) führt *Kurzschluss*Vorgänge aus. Dies bedeutet, dass `expression2` nicht ausgewertet wird, wenn `expression1` `True` ist.  
  
 Bei bitweisen Vorgängen führt der `Or`-Operator einen bitweisen Vergleich identischer positionierter Bits in zwei numerischen Ausdrücken durch und legt das entsprechende Bit in `result` gemäß der folgenden Tabelle fest.  
  
|Wenn Bit in `expression1` ist|Und Bit in `expression2` ist|Das Bit in `result` ist|  
|--------------------------------|---------------------------------|----------------------------|  
|1|1|1|  
|1|0|1|  
|0|1|1|  
|0|0|0|  
  
> [!NOTE]
> Da die logischen und bitweisen Operatoren Vorrang vor anderen arithmetischen und relationalen Operatoren sind, sollten alle bitweisen Vorgänge in Klammern eingeschlossen werden, um eine exakte Ausführung sicherzustellen.  
  
## <a name="data-types"></a>Datentypen  
 Wenn die Operanden aus einem `Boolean`-Ausdruck und einem numerischen Ausdruck bestehen, konvertiert Visual Basic den `Boolean`-Ausdruck in einen numerischen Wert (– 1 für `True` und 0 für `False`) und führt eine bitweise-Operation aus.  
  
 Bei einem `Boolean`-Vergleich ist der Datentyp des Ergebnisses `Boolean`. Bei einem bitweisen Vergleich ist der Ergebnis Datentyp ein numerischer Typ, der für die Datentypen von `expression1` und `expression2` geeignet ist. Weitere Informationen finden Sie in der Tabelle "relationale und bitweise Vergleiche" in den [Datentypen der Operator Ergebnisse](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md).  
  
## <a name="overloading"></a>Überladen  
 Der `Or`-Operator kann *überladen*werden. Dies bedeutet, dass eine Klasse oder Struktur das Verhalten neu definieren kann, wenn ein Operand den Typ dieser Klasse oder Struktur aufweist. Wenn Ihr Code diesen Operator für eine solche Klasse oder Struktur verwendet, stellen Sie sicher, dass Sie das neu definierte Verhalten verstehen. Weitere Informationen finden Sie unter [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der `Or`-Operator verwendet, um eine inklusivlogische Disjunktion für zwei Ausdrücke auszuführen. Das Ergebnis ist ein `Boolean`-Wert, der angibt, ob einer der beiden Ausdrücke `True` ist.  
  
 [!code-vb[VbVbalrOperators#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#35)]  
  
 Im vorangehenden Beispiel werden die Ergebnisse `True`, `True` und `False` erstellt.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird der `Or`-Operator verwendet, um die inklusive logische Disjunktion der einzelnen Bits zweier numerischer Ausdrücke auszuführen. Das Bit im Ergebnis Muster wird festgelegt, wenn eine der entsprechenden Bits in den Operanden auf 1 festgelegt ist.  
  
 [!code-vb[VbVbalrOperators#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#36)]  
  
 Das vorherige Beispiel erzeugt die Ergebnisse von 10, 14 und 14.  
  
## <a name="see-also"></a>Siehe auch

- [Logische/bitweise Operatoren (Visual Basic)](../../../visual-basic/language-reference/operators/logical-bitwise-operators.md)
- [Operator Precedence in Visual Basic (Operatorrangfolge in Visual Basic)](../../../visual-basic/language-reference/operators/operator-precedence.md)
- [Nach Funktionalität sortierte Operatoren](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)
- [OrElse-Operator](../../../visual-basic/language-reference/operators/orelse-operator.md)
- [Logische und bitweise Operatoren in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/logical-and-bitwise-operators.md)
