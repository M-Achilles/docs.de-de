---
title: Indexer in Schnittstellen – C#-Programmierhandbuch
ms.custom: seodec18
ms.date: 07/20/2015
helpviewer_keywords:
- indexers [C#], in interfaces
- accessors [C#], indexers
ms.assetid: e16b54bd-4a83-4f52-bd75-65819fca79e8
ms.openlocfilehash: 7f52df0283cf057c1cd6cc4fa87c0086da7e61d2
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2019
ms.locfileid: "70253006"
---
# <a name="indexers-in-interfaces-c-programming-guide"></a>Indexer in Schnittstellen (C#-Programmierhandbuch)
Indexer können für eine [Schnittstelle](../../language-reference/keywords/interface.md) deklariert werden. Accessoren für Schnittstellenindexer unterscheiden sich von den Accessoren für [Klassen](../../language-reference/keywords/class.md)-Indexer in den folgenden Punkten:  
  
- Schnittstellenaccessoren verwenden keine Modifizierer.  
  
- Ein Schnittstellenaccessor enthält keinen Text.  
  
 Der Zweck eines Accessors besteht darin anzugeben, ob der Indexer gleichzeitig Lese- und Schreibzugriff, nur Lesezugriff oder nur Schreibzugriff besitzt.  
  
 Das folgende Beispiel zeigt den Accessor für einen Schnittstellenindexer:  
  
 [!code-csharp[csProgGuideIndexers#3](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#3)]  
  
 Die Signatur eines Indexers muss sich von den Signaturen aller anderen in derselben Schnittstelle deklarierten Indexer unterscheiden.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel zeigt, wie Schnittstellenindexer implementiert werden.  
  
 [!code-csharp[csProgGuideIndexers#4](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideIndexers/CS/Indexers.cs#4)]  
  
 Im vorherigen Beispiel könnte der Schnittstellenmember durch Verwendung des vollqualifizierten Namens des Schnittstellenmembers explizit implementiert werden. Beispiel:  
  
```csharp  
string ISomeInterface.this[int index]   
{   
}   
```  
  
 Der vollqualifizierte Name ist jedoch nur erforderlich, um Mehrdeutigkeiten zu vermeiden, wenn mehr als eine Schnittstelle mit derselben Indexersignatur von der Klasse implementiert wird. Wenn z.B. eine `Employee`-Klasse die beiden Schnittstellen `ICitizen` und `IEmployee` implementiert und beide Schnittstellen dieselbe Indexersignatur besitzen, ist die explizite Implementierung des Schnittstellenmembers erforderlich. Das bedeutet, dass die folgende Indexerdeklaration:  
  
```csharp  
string IEmployee.this[int index]   
{   
}   
```  
  
 den Indexer für die Schnittstelle `IEmployee` implementiert. Dahingegen implementiert die folgende Deklaration:  
  
```csharp  
string ICitizen.this[int index]
{   
}   
```  
  
 den Indexer für die Schnittstelle `ICitizen`.  
  
## <a name="see-also"></a>Siehe auch

- [C#-Programmierhandbuch](../index.md)
- [Indexer](./index.md)
- [Eigenschaften](../classes-and-structs/properties.md)
- [Schnittstellen](../interfaces/index.md)
