---
title: Kontextabhängiges remove-Schlüsselwort – C#-Referenz
ms.custom: seodec18
ms.date: 07/20/2015
f1_keywords:
- remove_CSharpKeyword
helpviewer_keywords:
- remove event accessor [C#]
ms.assetid: c8223426-c17b-4fe2-8406-01564cf1dd2b
ms.openlocfilehash: b5c604cbb0fef158750b0fa487374ab293795fc7
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65633722"
---
# <a name="remove-c-reference"></a>remove (C#-Referenz)

Das kontextabhängige Schlüsselwort `remove` definiert einen benutzerdefinierten Ereignisaccessor, der aufgerufen wird, wenn der Clientcode das Abonnement Ihres Ereignisses ([event](event.md)) aufhebt. Wenn Sie einen benutzerdefinierten `remove`-Accessor bereitstellen, müssen Sie auch einen [add](add.md)-Accessor angeben.

## <a name="example"></a>Beispiel

Im folgende Beispiel wird ein Ereignis mit den benutzerdefinierten Accessoren [add](add.md) und `remove` gezeigt. Das vollständige Beispiel finden Sie unter [Vorgehensweise:  Implementieren von Schnittstellenereignissen](../../programming-guide/events/how-to-implement-interface-events.md).

 [!code-csharp[csrefKeywordsContextual#15](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsContextual/CS/csrefKeywordsContextual.cs#15)]

Sie müssen normalerweise keine eigenen benutzerdefinierten Ereignisaccessoren bereitstellen. Die Accessoren, die automatisch vom Compiler generiert werden, wenn Sie ein Ereignis deklarieren, sind in den meisten Szenarios ausreichend.

## <a name="see-also"></a>Siehe auch

- [Ereignisse](../../programming-guide/events/index.md)
