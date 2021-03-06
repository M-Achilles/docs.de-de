---
title: WithEvents (Visual Basic)
ms.date: 07/20/2015
f1_keywords:
- vb.WithEvents
- WithEvents
helpviewer_keywords:
- WithEvents keyword [Visual Basic]
ms.assetid: 19d461f5-d72f-4de9-8c1d-0a6650316990
ms.openlocfilehash: e8a8fb571fa65228f3a0acec1f902d21eb9bfe04
ms.sourcegitcommit: 4c41ec195caf03d98b7900007c3c8e24eba20d34
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67268307"
---
# <a name="withevents-visual-basic"></a>WithEvents (Visual Basic)
Gibt an, dass eine oder mehrere Membervariablen auf eine Instanz einer Klasse verweisen, die Ereignisse auslösen kann.  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Variable definiert ist, mithilfe von `WithEvents`, können Sie deklarativ angeben, dass eine Methode den Wert der Variablen-Ereignisse, die mit verarbeitet die `Handles` Schlüsselwort.  
  
 Sie können `WithEvents` nur auf Klassen-oder Modulebene. Dies bedeutet, dass der Deklarationskontext für eine `WithEvents` Variable muss eine Klasse oder das Modul und eine Quelldatei, Namespace, Struktur oder Prozedur nicht möglich.  
  
 Sie können keine `WithEvents` auf einen Strukturmember.  
  
 Sie können nur einzelne Variablen deklarieren, nicht arrays – mit `WithEvents`.  
  
## <a name="rules"></a>Regeln  
  
- **Elementtypen.** Deklarieren Sie `WithEvents` Variablen so Objektvariablen, damit sie akzeptieren können-Klasseninstanzen. Allerdings kann nicht deklariert werden sie als `Object`. Sie müssen diese als spezifische Klasse deklarieren, die die Ereignisse auslösen kann.  
  
 Die `WithEvents` Modifizierer kann in diesem Kontext verwendet werden: [Dim-Anweisung](../../../visual-basic/language-reference/statements/dim-statement.md)  
 
## <a name="example"></a>Beispiel

```VB
Dim WithEvents app As Application
```
  
## <a name="see-also"></a>Siehe auch

- [Handles](../../../visual-basic/language-reference/statements/handles-clause.md)
- [Schlüsselwörter](../../../visual-basic/language-reference/keywords/index.md)
- [Ereignisse](../../../visual-basic/programming-guide/language-features/events/index.md)
