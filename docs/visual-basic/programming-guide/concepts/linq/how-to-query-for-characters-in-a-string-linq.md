---
title: 'Vorgehensweise: Abfragen von Zeichen in einer Zeichenfolge (LINQ) (Visual Basic)'
ms.date: 07/20/2015
ms.assetid: 499ebbe0-746c-4235-9dba-ce722c12b50e
ms.openlocfilehash: fba5d8ca6c0c060c76b1ecf4f66434ce0884e733
ms.sourcegitcommit: c7a7e1468bf0fa7f7065de951d60dfc8d5ba89f5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65593306"
---
# <a name="how-to-query-for-characters-in-a-string-linq-visual-basic"></a>Vorgehensweise: Abfragen von Zeichen in einer Zeichenfolge (LINQ) (Visual Basic)
Da die <xref:System.String>-Klasse die generische <xref:System.Collections.Generic.IEnumerable%601>-Schnittstelle implementiert, kann jede Zeichenfolge als Folge von Zeichen abgefragt werden. Dies ist allerdings kein üblicher Einsatz von LINQ. Verwenden Sie für komplex Musterabgleichvorgänge die <xref:System.Text.RegularExpressions.Regex>-Klasse.  
  
## <a name="example"></a>Beispiel  
 In folgendem Beispiel wird eine Zeichenfolge abgefragt, um die Zahl von enthaltenen numerischen Ziffern zu bestimmen. Beachten Sie, dass die Abfrage „wieder verwendet“ wird, nachdem sie zum ersten Mal ausgeführt wurde. Dies ist möglich, da die Abfrage selbst keine Ergebnisse speichert.  
  
```vb  
Class QueryAString  
  
    Shared Sub Main()  
  
        ' A string is an IEnumerable data source.  
        Dim aString As String = "ABCDE99F-J74-12-89A"  
  
        ' Select only those characters that are numbers  
        Dim stringQuery = From ch In aString   
                          Where Char.IsDigit(ch)   
                          Select ch  
        ' Execute the query  
        For Each c As Char In stringQuery  
            Console.Write(c & " ")  
        Next  
  
        ' Call the Count method on the existing query.  
        Dim count As Integer = stringQuery.Count()  
        Console.WriteLine(System.Environment.NewLine & "Count = " & count)  
  
        ' Select all characters before the first '-'  
        Dim stringQuery2 = aString.TakeWhile(Function(c) c <> "-")  
  
        ' Execute the second query  
        For Each ch In stringQuery2  
            Console.Write(ch)  
        Next  
  
        Console.WriteLine(System.Environment.NewLine & "Press any key to exit")  
        Console.ReadKey()  
    End Sub  
End Class  
' Output:  
' 9 9 7 4 1 2 8 9   
' Count = 8  
' ABCDE99F  
```  
  
## <a name="compiling-the-code"></a>Kompilieren des Codes  
Erstellen Sie ein Konsolenanwendungsprojekt für VB.NET, mit einem `Imports` -Anweisung für den Namespace "System.Linq".
  
## <a name="see-also"></a>Siehe auch

- [LINQ und Zeichenfolgen (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-strings.md)
- [Vorgehensweise: Kombinieren von LINQ-Abfragen mit regulären Ausdrücken (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-combine-linq-queries-with-regular-expressions.md)
