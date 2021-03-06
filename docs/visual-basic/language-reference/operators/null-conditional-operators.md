---
title: NULL-Bedingte Operatoren (Visual Basic)
ms.date: 10/19/2018
helpviewer_keywords:
- null-conditional operators [Visual Basic]
- ?. operator [Visual Basic]
- ?[] operator [C#]
- ?[] operator [Visual Basic]
ms.openlocfilehash: 4815fe7ad337634cfb56127fbd24a47a37fdd74b
ms.sourcegitcommit: ca2ca60e6f5ea327f164be7ce26d9599e0f85fe4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/06/2019
ms.locfileid: "65062943"
---
# <a name="-and--null-conditional-operators-visual-basic"></a>?. und? ()-Null-Bedingte Operatoren (Visual Basic)

Testet, ob der Wert des linken Operanden für Null-Zeichen (`Nothing`) vor dem Ausführen einer Memberzugriff (`?.`) oder eines Indexes (`?()`) Vorgang; gibt `Nothing` , wenn der linke Operand `Nothing`. Beachten Sie, dass die in Ausdrücken, die normalerweise Wert zurückgeben, die Null-bedingten Operator gibt einen <xref:System.Nullable%601>.

Diese Operatoren können Sie weniger Code zum Behandeln von null-Überprüfungen, insbesondere dann, wenn in Datenstrukturen absteigend zu schreiben. Zum Beispiel:

```vb
' Nothing if customers is Nothing  
Dim length As Integer? = customers?.Length  

' Nothing if customers is Nothing
Dim first As Customer = customers?(0)

' Nothing if customers, the first customer, or Orders is Nothing
Dim count As Integer? = customers?(0)?.Orders?.Count()   
```

Zum Vergleich wird die alternative Code für das erste der folgenden Ausdrücke ohne ein Null-bedingten Operator:

```vb
Dim length As Integer
If customers IsNot Nothing Then
   length = customers.Length
End If
```

Manchmal müssen Sie eine Aktion für ein Objekt auszuführen, die null ist, möglicherweise basierend auf dem Wert eines booleschen Elements für dieses Objekt (z. B. die boolesche Eigenschaft `IsAllowedFreeShipping` im folgenden Beispiel):

```vb
  Dim customer = FindCustomerByID(123) 'customer will be Nothing if not found.
  
  If customer IsNot Nothing AndAlso customer.IsAllowedFreeShipping Then
   ApplyFreeShippingToOrders(customer)
  End If
```

Können Sie Ihren Code zu verkürzen und vermeiden, manuell eine Überprüfung auf Null mit Null-bedingten Operator wie folgt:

```vb
 Dim customer = FindCustomerByID(123) 'customer will be Nothing if not found.
 
 If customer?.IsAllowedFreeShipping Then ApplyFreeShippingToOrders(customer)
```

Die NULL-bedingten Operatoren sind Kurzschlussoperatoren.  Wenn ein Vorgang in einer Kette von Zugriffs- und Index-Vorgänge der bedingte Member zurückgibt `Nothing`, die restlichen der Kette Ausführung beendet.  Im folgenden Beispiel `C(E)` wird nicht ausgewertet, wenn `A`, `B`, oder `C` ergibt `Nothing`.

```vb
A?.B?.C?(E);
```

Ein weiterer Verwendungszweck für den bedingten Null-Memberzugriff ist zum Aufrufen von Delegaten auf threadsichere Weise mit viel weniger Code.  Das folgende Beispiel definiert zwei Typen: ein `NewsBroadcaster` und `NewsReceiver`. Nachrichtenelemente gesendet werden, an den Empfänger, durch die `NewsBroadcaster.SendNews` delegieren.

```vb
Public Module NewsBroadcaster
   Dim SendNews As Action(Of String) 

   Public Sub Main()
      Dim rec As New NewsReceiver()
      Dim rec2 As New NewsReceiver()
      SendNews?.Invoke("Just in: A newsworthy item...")
   End Sub

   Public Sub Register(client As Action(Of String))
      SendNews = SendNews.Combine({SendNews, client})
   End Sub
End Module

Public Class NewsReceiver
   Public Sub New()
      NewsBroadcaster.Register(AddressOf Me.DisplayNews)
   End Sub

   Public Sub DisplayNews(newsItem As String)
      Console.WriteLine(newsItem)
   End Sub
End Class
```

Wenn keine in Elemente der `SendNews` Aufrufliste, die `SendNews` Delegat löst eine <xref:System.NullReferenceException>. Vor dem null-Bedingte Operatoren, wie code zu Folgendes sichergestellt, dass die Aufrufliste des Delegaten nicht war `Nothing`:

```vb  
SendNews = SendNews.Combine({SendNews, client})  
If SendNews IsNot Nothing Then 
   SendNews("Just in...")
End If
```

Die neue Methode ist viel einfacher:  

```vb
SendNews = SendNews.Combine({SendNews, client})  
SendNews?.Invoke("Just in...")
```

Die neue Methode ist threadsicher, da der Compiler Code zum Auswerten von `SendNews` nur einmal generiert und das Ergebnis in einer temporären Variablen behält. Sie müssen die `Invoke`-Methode explizit aufrufen, da es keine Aufrufsyntax für Null-Bedingungsdelegate gibt `SendNews?(String)`.  

## <a name="see-also"></a>Siehe auch

- [Operatoren (Visual Basic)](index.md)
- [Visual Basic-Programmierhandbuch](../../../visual-basic/programming-guide/index.md)
- [Sprachreferenz zu Visual Basic](../../../visual-basic/language-reference/index.md)
