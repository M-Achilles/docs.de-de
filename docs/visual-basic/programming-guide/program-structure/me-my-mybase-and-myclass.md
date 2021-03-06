---
title: Me, "My", "MyBase" und "MyClass" in Visual Basic
ms.date: 07/20/2015
f1_keywords:
- MyClass
- vb.Me
- MyBase
- vb.MyBase
- Me
- vb.MyClass
- vb.This
- vb.My
helpviewer_keywords:
- My object
- self-reference [Visual Basic], Me keyword
- MyClass keyword [Visual Basic], relationship to similar programming elements
- Me keyword [Visual Basic], relationship to similar programming elements
- Me keyword [Visual Basic], referring to the current instance of an object
- Me keyword [Visual Basic]
- self-reference
- current instance [Visual Basic], Me keyword
- MyBase keyword [Visual Basic], relationship to similar programming elements
ms.assetid: f8e241ae-b1ed-4886-9aa0-08c632154029
ms.openlocfilehash: 7df146e09a1d7cd730f4cf539d6823f7ced44bd1
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "72002532"
---
# <a name="me-my-mybase-and-myclass-in-visual-basic"></a>Me, "My", "MyBase" und "MyClass" in Visual Basic
`Me`, `My`, `MyBase` und `MyClass` in Visual Basic haben ähnliche Namen, aber unterschiedliche Zwecke. In diesem Thema werden diese Entitäten beschrieben, um Sie zu unterscheiden.  
  
## <a name="me"></a>Me  
 Das Schlüsselwort "`Me`" bietet eine Möglichkeit, auf die jeweilige Instanz einer Klasse oder Struktur zu verweisen, in der der Code gerade ausgeführt wird. `Me` verhält sich wie eine Objekt Variable oder eine Struktur Variable, die auf die aktuelle Instanz verweist. Die Verwendung von `Me` ist besonders nützlich, wenn Informationen über die derzeit ausgeführte Instanz einer Klasse oder Struktur an eine Prozedur in einer anderen Klasse, Struktur oder einem anderen Modul übergeben werden.  
  
 Nehmen Sie beispielsweise an, dass Sie das folgende Verfahren in einem Modul ausführen.  
  
```vb  
Sub ChangeFormColor(FormName As Form)  
   Randomize()  
   FormName.BackColor = Color.FromArgb(Rnd() * 256, Rnd() * 256, Rnd() * 256)  
End Sub  
```  
  
 Sie können diese Prozedur aufzurufen und die aktuelle Instanz der <xref:System.Windows.Forms.Form>-Klasse als Argument übergeben, indem Sie die folgende-Anweisung verwenden.  
  
```vb  
ChangeFormColor(Me)  
```  
  
## <a name="my"></a>My  
 Das Feature "`My`" bietet einfachen und intuitiven Zugriff auf eine Reihe von .NET Framework Klassen, sodass der Visual Basic Benutzer mit dem Computer, der Anwendung, den Einstellungen, den Ressourcen usw. interagieren kann.  
  
## <a name="mybase"></a>MyBase  
 Das `MyBase`-Schlüsselwort verhält sich wie eine Objekt Variable, die auf die Basisklasse der aktuellen Instanz einer Klasse verweist. `MyBase` wird häufig verwendet, um auf Basisklassenmember zuzugreifen, die von einer abgeleiteten Klasse überschrieben oder überschattet werden. `MyBase.New` wird verwendet, um explizit einen Basisklassenkonstruktor aus einem abgeleiteten Klassenkonstruktor aufzurufen.  
  
## <a name="myclass"></a>MyClass  
 Das `MyClass`-Schlüsselwort verhält sich wie eine Objekt Variable, die auf die aktuelle Instanz einer Klasse verweist, die ursprünglich implementiert wurde. `MyClass` ist `Me` ähnlich, aber alle Methodenaufrufe darauf werden so behandelt, als wäre die Methode `NotOverridable`.  
  
## <a name="see-also"></a>Siehe auch

- [Grundlagen der Vererbung](../../../visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics.md)
