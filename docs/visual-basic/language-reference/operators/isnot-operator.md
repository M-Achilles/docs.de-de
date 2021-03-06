---
title: IsNot-Operator (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.isnot
helpviewer_keywords:
- IsNot operator [Visual Basic]
ms.assetid: 8dd2bcdb-0166-48a2-9094-60dfb448f36c
ms.openlocfilehash: 32e8f9532244679d2994b0e3d98279d75f7e77b4
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71701037"
---
# <a name="isnot-operator-visual-basic"></a>IsNot-Operator (Visual Basic)

Vergleicht zwei Objekt Verweis Variablen.

## <a name="syntax"></a>Syntax

```vb
result = object1 IsNot object2
```

## <a name="parts"></a>Teile
 `result` ist erforderlich. Ein `Boolean`-Wert.

 `object1` ist erforderlich. Beliebige `Object`-Variable oder-Ausdruck.

 `object2` ist erforderlich. Beliebige `Object`-Variable oder-Ausdruck.

## <a name="remarks"></a>Hinweise
 Der `IsNot`-Operator bestimmt, ob zwei Objekt Verweise auf unterschiedliche Objekte verweisen. Es werden jedoch keine Wert Vergleiche durchgeführt. Wenn `object1` und `object2` auf genau dieselbe Objektinstanz verweisen, `result` `False`; Wenn dies nicht der Fall ist, ist `result` `True`.

 `IsNot` ist das Gegenteil des `Is`-Operators. Der Vorteil von `IsNot` besteht darin, dass Sie eine umständliche Syntax mit `Not` und `Is` vermeiden können, was schwierig zu lesen ist.

 Sie können die Operatoren `Is` und `IsNot` verwenden, um früh gebundene und spät gebundene Objekte zu testen.

## <a name="example"></a>Beispiel
 Im folgenden Codebeispiel werden sowohl der `Is`-Operator als auch der `IsNot`-Operator verwendet, um denselben Vergleich durchzuführen.

 [!code-vb[VbVbalrOperators#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrOperators/VB/Class1.vb#29)]

## <a name="see-also"></a>Siehe auch

- [Is-Operator](is-operator.md)
- [TypeOf-Operator](typeof-operator.md)
- [Operator Precedence in Visual Basic (Operatorrangfolge in Visual Basic)](operator-precedence.md)
- [Vorgehensweise: Testen, ob zwei Objekte identisch sind @ no__t-0
