---
title: Bezeichnernamen
description: Lernen Sie die Regeln für gültige Bezeichnernamen in der C#-Programmiersprache kennen.
ms.date: 08/21/2018
ms.openlocfilehash: f8a27ddae0437ed037b59f76d60dc7e420ddc2eb
ms.sourcegitcommit: 986f836f72ef10876878bd6217174e41464c145a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2019
ms.locfileid: "69589353"
---
# <a name="identifier-names"></a>Bezeichnernamen

Ein **Bezeichner** ist der Name, den Sie einem Namespace, einem Member, einer Variable oder einem Typ (Klasse, Schnittstelle, Struktur, Delegat oder Enumeration) zuweisen. Gültige Bezeichner müssen folgende Regeln einhalten:

- Bezeichner müssen mit einem Buchstaben oder mit `_` beginnen.
- Bezeichner können Unicode-Buchstaben, Dezimalziffernzeichen, Unicode-Verbindungszeichen, Unicode-Kombinationszeichen oder Unicode-Formatierungszeichen enthalten. Weitere Informationen zu den Kategorien von Unicode finden Sie in der [Unicode-Kategoriedatenbank](https://www.unicode.org/reports/tr44/).
Sie können Bezeichner deklarieren, die mit C#-Schlüsselworten übereinstimmen, indem Sie das Präfix `@` für den Bezeichner verwenden. `@` ist nicht Teil des Namens des Bezeichners. Beispielsweise deklariert `@if` einen Bezeichner namens `if`. Diese [ausführlichen Bezeichner](../../language-reference/tokens/verbatim.md) dienen in erster Linie der Interoperabilität mit Bezeichnern, die in anderen Sprachen deklariert werden.

Eine vollständige Definition der gültigen Bezeichner finden Sie im [Thema „Bezeichner“ in der C#-Sprachspezifikation](../../../../_csharplang/spec/lexical-structure.md#identifiers).

## <a name="naming-conventions"></a>Namenskonventionen

Neben diesen Regeln gibt es mehrere [Namenskonventionen](../../../standard/design-guidelines/naming-guidelines.md) für Bezeichner, die in den .NET-APIs verwendet werden. Gemäß der Konventionen verwenden C#-Programme `PascalCase` für Typnamen, Namespaces und alle öffentlichen Member. Darüber hinaus werden folgende Konventionen häufig angewandt:

- Schnittstellennamen beginnen mit einem großen `I`.
- Attributtypen enden mit dem Wort `Attribute`.
- Enumerationstypen enthalten ein Substantiv im Singular für nicht Flags und ein Substantiv im Plural für Flags.
- Bezeichner sollten keine zwei aufeinanderfolgenden `_`-Zeichen enthalten. Diese Namen sind für Bezeichner reserviert, die der Compiler generiert.

## <a name="c-language-specification"></a>C#-Programmiersprachenspezifikation

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [C#-Programmierhandbuch](../index.md)
- [Einblicke in ein C#-Programm](./index.md)
- [C#-Referenz](../../language-reference/index.md)
- [Klassen](../classes-and-structs/classes.md)
- [Strukturen](../classes-and-structs/structs.md)
- [Namespaces](../namespaces/index.md)
- [Schnittstellen](../interfaces/index.md)
- [Delegaten](../delegates/index.md)
