---
title: Verwenden von Varianz in Delegaten (Visual Basic)
ms.date: 07/20/2015
ms.assetid: 7b5c20f1-6416-46a3-94b6-f109c31c842c
ms.openlocfilehash: ebba7e862e1b4677d9438aa301ef2b713fba3712
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/30/2019
ms.locfileid: "70169068"
---
# <a name="using-variance-in-delegates-visual-basic"></a>Verwenden von Varianz in Delegaten (Visual Basic)

Wenn Sie einem Delegat eine Methode zuweisen, bieten *Kovarianz* und *Kontravarianz* Flexibilität für das Abgleichen eines Delegattyps mit einer Methodensignatur. Kovarianz lässt die Verfügung einer Methode über einen Rückgabetyp zu, der stärker abgeleitet ist als der im Delegat definierte Typ. Kontravarianz lässt eine Methode zu, die über Typen verfügt, die weniger abgeleitet sind als die im Delegattyp.

## <a name="example-1-covariance"></a>Beispiel 1: Kovarianz

### <a name="description"></a>Beschreibung

In diesem Beispiel wird veranschaulicht, wie Delegaten mit Methoden verwendet werden können, die über Rückgabetypen verfügen, die von den Rückgabetypen in der Delegatsignatur abgeleitet sind. Der von `DogsHandler` zurückgegebene Datentyp ist vom Typ `Dogs`, der vom im Delegat definierten Typ `Mammals` abhängt.

### <a name="code"></a>Code

```vb
Class Mammals
End Class

Class Dogs
    Inherits Mammals
End Class
Class Test
    Public Delegate Function HandlerMethod() As Mammals
    Public Shared Function MammalsHandler() As Mammals
        Return Nothing
    End Function
    Public Shared Function DogsHandler() As Dogs
        Return Nothing
    End Function
    Sub Test()
        Dim handlerMammals As HandlerMethod = AddressOf MammalsHandler
        ' Covariance enables this assignment.
        Dim handlerDogs As HandlerMethod = AddressOf DogsHandler
    End Sub
End Class
```

## <a name="example-2-contravariance"></a>Beispiel 2: Kontravarianz

### <a name="description"></a>Beschreibung

In diesem Beispiel wird veranschaulicht, wie Delegaten mit Methoden verwendet werden können, die über Parameter verfügen, deren Typen Basis Typen vom Delegatsignatur-Parametertyp sind. Mithilfe von Kontravarianz können Sie einen Ereignishandler anstelle getrennter Handler verwenden. Im folgenden Beispiel werden zwei Delegaten verwendet:

- Ein <xref:System.Windows.Forms.KeyEventHandler> Delegat, der die Signatur des [Button. KeyDown](xref:System.Windows.Forms.Control.KeyDown) -Ereignisses definiert. Die Signatur lautet wie folgt:

   ```vb
   Public Delegate Sub KeyEventHandler(sender As Object, e As KeyEventArgs)
   ```

- Ein <xref:System.Windows.Forms.MouseEventHandler> Delegat, der die Signatur des [Button. moukliclick](xref:System.Windows.Forms.Control.MouseDown) -Ereignisses definiert. Die Signatur lautet wie folgt:

   ```vb
   Public Delegate Sub MouseEventHandler(sender As Object, e As MouseEventArgs)
   ```

Das Beispiel definiert einen Ereignishandler mit einem <xref:System.EventArgs> -Parameter und verwendet ihn, um das `Button.KeyDown` - `Button.MouseClick` Ereignis und das-Ereignis zu behandeln. Dies ist möglich, weil <xref:System.EventArgs> der Basistyp sowohl <xref:System.Windows.Forms.KeyEventArgs> von als auch <xref:System.Windows.Forms.MouseEventArgs>von ist.

### <a name="code"></a>Code

```vb
' Event handler that accepts a parameter of the EventArgs type.
Private Sub MultiHandler(ByVal sender As Object,
                         ByVal e As System.EventArgs)
    Label1.Text = DateTime.Now
End Sub

Private Sub Form1_Load(ByVal sender As System.Object,
    ByVal e As System.EventArgs) Handles MyBase.Load

    ' You can use a method that has an EventArgs parameter,
    ' although the event expects the KeyEventArgs parameter.
    AddHandler Button1.KeyDown, AddressOf MultiHandler

    ' You can use the same method
    ' for the event that expects the MouseEventArgs parameter.
    AddHandler Button1.MouseClick, AddressOf MultiHandler
End Sub
```

## <a name="see-also"></a>Siehe auch

- [Variance in Delegates (Visual Basic) (Varianz in Delegaten (Visual Basic))](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/variance-in-delegates.md)
- [Using Variance for Func and Action Generic Delegates (Visual Basic) (Verwenden von Varianz für die generischen Delegaten Func und Action (Visual Basic))](../../../../visual-basic/programming-guide/concepts/covariance-contravariance/using-variance-for-func-and-action-generic-delegates.md)
