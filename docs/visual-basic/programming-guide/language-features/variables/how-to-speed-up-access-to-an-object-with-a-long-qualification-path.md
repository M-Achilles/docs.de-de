---
title: 'Vorgehensweise: Beschleunigen des Zugriffs auf ein Objekt mit einem langen Qualifizierungs Pfad (Visual Basic)'
ms.date: 07/20/2015
helpviewer_keywords:
- variables [Visual Basic], accessing
- variables [Visual Basic], object
- With statement [Visual Basic]
- With block
- object variables [Visual Basic], accessing
ms.assetid: 3eb7657f-c9fe-4e05-8bc3-4bb14d5ae585
ms.openlocfilehash: a8e50a2ed04037b48091321dc0c9ac2ea1db35f4
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2019
ms.locfileid: "68631097"
---
# <a name="how-to-speed-up-access-to-an-object-with-a-long-qualification-path-visual-basic"></a>Vorgehensweise: Beschleunigen des Zugriffs auf ein Objekt mit einem langen Qualifizierungs Pfad (Visual Basic)

Wenn Sie häufig auf ein Objekt zugreifen, das einen Qualifizierungs Pfad mehrerer Methoden und Eigenschaften erfordert, können Sie den Code beschleunigen, indem Sie den Qualifikations Pfad nicht wiederholen.

Es gibt zwei Möglichkeiten, um das Wiederholen des Qualifizierungs Pfads zu vermeiden. Sie können das Objekt einer Variablen zuweisen, oder Sie können es in einem `With`... `End With` blockieren.

### <a name="to-speed-up-access-to-a-heavily-qualified-object-by-assigning-it-to-a-variable"></a>So beschleunigen Sie den Zugriff auf ein stark qualifiziertes Objekt, indem Sie es einer Variablen zuweisen

1. Deklarieren Sie eine Variable des Typs des Objekts, auf das Sie häufig zugreifen. Geben Sie den Qualifikations Pfad im Initialisierungs Teil der Deklaration an.

    ```vb
    Dim ctrlActv As Control = someForm.ActiveForm.ActiveControl
    ```

2. Verwenden Sie die-Variable, um auf die Member des-Objekts zuzugreifen.

    ```vb
    ctrlActv.Text = "Test"
    ctrlActv.Location = New Point(100, 100)
    ctrlActv.Show()
    ```

### <a name="to-speed-up-access-to-a-heavily-qualified-object-by-using-a-withend-with-block"></a>So beschleunigen Sie den Zugriff auf ein stark qualifiziertes Objekt mithilfe eines mit... Mit Block beenden

1. Legen Sie den Qualifikations Pfad in `With` eine-Anweisung ein.

    ```vb
    With someForm.ActiveForm.ActiveControl
    ```

2. Greifen Sie auf die Member des- `With` Objekts innerhalb des- `End With` Blocks vor der-Anweisung zu.

    ```vb
        .Text = "Test"
        .Location = New Point(100, 100)
        .Show()
    End With
    ```

## <a name="see-also"></a>Siehe auch

- [Objektvariablen](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)
- [With...End With-Anweisung](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)
