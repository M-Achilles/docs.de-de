---
title: ?? und ??= (Operatoren) – C#-Referenz
ms.custom: seodec18
ms.date: 09/10/2019
f1_keywords:
- ??_CSharpKeyword
- ??=_CSharpKeyword
helpviewer_keywords:
- null-coalescing operator [C#]
- ?? operator [C#]
- null-coalescing assignment [C#]
- ??= operator [C#]
ms.assetid: 088b1f0d-c1af-4fe1-b4b8-196fd5ea9132
ms.openlocfilehash: 1e94038a41a6a6cc19be6c67bff2891397793fb3
ms.sourcegitcommit: 33c8d6f7342a4bb2c577842b7f075b0e20a2fa40
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2019
ms.locfileid: "70924682"
---
# <a name="-and--operators-c-reference"></a>?? und ??= (Operatoren) – C#-Referenz

Der NULL-Zusammenfügungsoperator `??` gibt den Wert des linken Operanden zurück, wenn dieser nicht `null` ist. Andernfalls wertet der Operator den rechten Operanden aus und gibt dessen Ergebnis zurück. Der `??`-Operator wertet seinen rechten Operanden nicht aus, wenn der linke Operand auf einen Wert ungleich NULL ausgewertet wird.

Ab C# 8.0 können Sie den NULL-Sammelzuweisungsoperator `??=` verwenden, um den Wert des rechten Operanden dem linken Operanden nur dann zuzuweisen, wenn die Auswertung des linken Operanden `null` ergibt. Der `??=`-Operator wertet seinen rechten Operanden nicht aus, wenn der linke Operand auf einen Wert ungleich NULL ausgewertet wird.

[!code-csharp[null-coalescing assignment](~/samples/csharp/language-reference/operators/NullCoalescingOperator.cs#Assignment)]

Der linke Operand des `??=`-Operators muss eine Variable, eine [Eigenschaft](../../programming-guide/classes-and-structs/properties.md) oder ein [Indexer](../../programming-guide/indexers/index.md)-Element sein. Weitere Informationen zur NULL-Sammelzuweisung finden Sie im [Hinweis zum Featurevorschlag](~/_csharplang/proposals/csharp-8.0/null-coalescing-assignment.md).

In C# 7.3 und früher muss der Typ des linken Operanden des `??`-Operators entweder ein Verweistyp oder ein [auf NULL festlegbarer Werttyp](../../programming-guide/nullable-types/index.md) sein. Ab C# 8.0 wird diese Anforderung durch Folgendes ersetzt: der Typ des linken Operanden der Operatoren `??` und `??=` kann kein Werttyp sein, der nicht auf NULL festgelegt werden kann. Das heißt, Sie können die NULL-Sammeloperatoren mit uneingeschränkten Typparametern ab C# 8.0 verwenden:

[!code-csharp[unconstrained type parameter](~/samples/csharp/language-reference/operators/NullCoalescingOperator.cs#UnconstrainedType)]

Die NULL-Sammeloperatoren sind rechtsassoziativ. Das heißt, Ausdrücke wie

```csharp
a ?? b ?? c
d ??= e ??= f
```

werden wie folgt ausgewertet

```csharp
a ?? (b ?? c)
d ??= (e ??= f)
```

## <a name="examples"></a>Beispiele

Die Operatoren `??` und `??=` können in folgenden Szenarios nützlich sein:

- In Ausdrücken mit den [NULL-bedingten Operatoren „?.“ und „?[]“](member-access-operators.md#null-conditional-operators--and-) können Sie den NULL-Zusammenfügungsoperator verwenden, um einen alternativen Ausdruck zum Auswerten für den Fall bereitzustellen, dass das Ergebnis des NULL-bedingten Vorgangs `null` ist:

  [!code-csharp-interactive[with null-conditional](~/samples/csharp/language-reference/operators/NullCoalescingOperator.cs#WithNullConditional)]

- Wenn Sie mit [Nullable-Werttypen](../../programming-guide/nullable-types/index.md) arbeiten und den Wert eines zugrunde liegenden Werttyps bereitstellen müssen, verwenden Sie den NULL-Zusammenfügungsoperator, um den Wert für den Fall anzugeben, dass der Wert eines Nullable-Typs `null` ist:

  [!code-csharp-interactive[with nullable types](~/samples/csharp/language-reference/operators/NullCoalescingOperator.cs#WithNullableTypes)]

  Verwenden Sie die <xref:System.Nullable%601.GetValueOrDefault?displayProperty=nameWithType>-Methode, wenn der Wert, der verwenden werden soll, falls der Wert des Nullable-Typs `null` lautet, der Standardwert des zugrunde liegenden Werttyps sein soll.

- Ab C# 7.0 können Sie einen [`throw`Ausdruck](../keywords/throw.md#the-throw-expression) als rechten Operanden des NULL-Zusammenfügungsoperators verwenden, um den Code für die Überprüfung der Argumente präziser zu fassen:

  [!code-csharp[with throw expression](~/samples/csharp/language-reference/operators/NullCoalescingOperator.cs#WithThrowExpression)]

  Das oben stehende Beispiel veranschaulicht auch, wie Sie [Ausdruckskörpermember](../../programming-guide/statements-expressions-operators/expression-bodied-members.md) verwenden, um eine Eigenschaft zu definieren.

- Ab C# 8.0 können Sie den `??=`-Operator zum Ersetzen des folgenden Codes verwenden

  ```csharp
  if (variable is null)
  {
      variable = expression;
  }
  ```

  durch den folgenden Code:

  ```csharp
  variable ??= expression;
  ```

## <a name="operator-overloadability"></a>Operatorüberladbarkeit

Die Operatoren `??` und `??=` können nicht überladen werden.

## <a name="c-language-specification"></a>C#-Sprachspezifikation

Weitere Informationen über den `??`-Operator finden Sie im Abschnitt [NULL-Sammeloperatoren](~/_csharplang/spec/expressions.md#the-null-coalescing-operator) der [C#-Sprachspezifikation](~/_csharplang/spec/introduction.md).

## <a name="see-also"></a>Siehe auch

- [C#-Referenz](../index.md)
- [C#-Operatoren](index.md)
- [?.- und ?[]-Operatoren](member-access-operators.md#null-conditional-operators--and-)
- [?:-Operator](conditional-operator.md)
