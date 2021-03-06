---
title: -Importe (Visual Basic)
ms.date: 03/10/2018
helpviewer_keywords:
- /imports compiler option [Visual Basic]
- imports compiler option [Visual Basic]
- -imports compiler option [Visual Basic]
ms.assetid: 9a93fb53-c080-497b-bf9b-441022dbbc39
ms.openlocfilehash: 929e24a1ffd02d4e21ab1b925ddd59050b5d3cc4
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005574"
---
# <a name="-imports-visual-basic"></a>-Importe (Visual Basic)
Importiert Namespaces aus einer angegebenen Assembly.  
  
## <a name="syntax"></a>Syntax  
  
```console  
-imports:namespaceList  
```  
  
## <a name="arguments"></a>Argumente  
  
|Begriff|Definition|  
|---|---|  
|`namespaceList`|Erforderlich. Durch Trennzeichen getrennte Liste der zu importierenden Namespaces.|  
  
## <a name="remarks"></a>Hinweise  
 Mit der Option "`-imports`" werden alle Namespaces importiert, die innerhalb des aktuellen Satzes von Quelldateien oder einer beliebigen referenzierten Assembly definiert sind.  
  
 Die Elemente in einem Namespace, der mit `-imports` angegeben wird, sind für alle Quell Code Dateien in der Kompilierung verfügbar. Verwenden Sie die [Imports-Anweisung (.NET-Namespace und-Typ)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) , um einen Namespace in einer einzelnen Quell Code Datei zu verwenden.  
  
|So legen Sie/Imports in der integrierten Entwicklungsumgebung von Visual Studio fest|  
|---|  
|1.  Ein Projekt auswählen in **Projektmappen-Explorer**. Klicken Sie im Menü **Projekt** auf **Eigenschaften**. <br />2.  Klicken Sie auf die Registerkarte **Verweise**.<br />3.  Geben Sie den Namespace Namen in das Feld neben der Schaltfläche **Benutzer Import hinzufügen** ein.<br />4.  Klicken Sie auf die Schaltfläche **Benutzer Import hinzufügen** .|  
  
## <a name="example"></a>Beispiel  
 Der folgende Code wird kompiliert, wenn `/imports:system.globalization` angegeben wird. Ohne diesen Vorgang erfordert die erfolgreiche Kompilierung entweder, dass eine `Imports System.Globalization`-Anweisung am Anfang der Quell Code Datei enthalten ist, oder dass die Eigenschaft voll qualifiziert als `System.Globalization.CultureInfo.CurrentCulture.Name` ist.

```vb
Module Example
   Public Sub Main()
      Console.WriteLine($"The current culture is {CultureInfo.CurrentCulture.Name}")
   End Sub
End Module
```

## <a name="see-also"></a>Siehe auch

- [Visual Basic-Befehlszeilencompiler](../../../visual-basic/reference/command-line-compiler/index.md)
- [Verweise und die Imports-Anweisung](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)
- [Beispiele für Kompilierungsbefehlszeilen](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
