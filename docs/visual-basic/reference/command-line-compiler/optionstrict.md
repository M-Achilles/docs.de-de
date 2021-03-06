---
title: -optionstrict
ms.date: 07/20/2015
f1_keywords:
- -optionstrict
helpviewer_keywords:
- -optionstrict compiler option [Visual Basic]
- optionstrict compiler option [Visual Basic]
- /optionstrict compiler option [Visual Basic]
ms.assetid: c7b10086-0fa4-49db-b3c8-4ae0db5957da
ms.openlocfilehash: 6d281fe07754f0471f8d6c0e31cf3ea890060504
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005347"
---
# <a name="-optionstrict"></a>-optionstrict
Erzwingt eine strikte Typsemantik, um implizite Typkonvertierungen einzuschränken.  
  
## <a name="syntax"></a>Syntax  
  
```console  
-optionstrict[+ | -]  
-optionstrict[:custom]  
```  
  
## <a name="arguments"></a>Argumente  
 `+` &#124; `-`  
 Optional. Die Option "`-optionstrict+`" schränkt die implizite Typkonvertierung ein. Der Standardwert für diese Option ist `-optionstrict-`. Die Option "`-optionstrict+`" entspricht `-optionstrict`. Sie können beide für die semantische Typsemantik verwenden.  
  
 `custom`  
 Erforderlich. Warnen, wenn die strenge sprach Semantik nicht beachtet wird.  
  
## <a name="remarks"></a>Hinweise  
 Wenn `-optionstrict+` wirksam ist, können nur erweiternde Typkonvertierungen implizit vorgenommen werden. Implizite einschränkende Typkonvertierungen, wie z. b. das Zuweisen eines `Decimal`-Typobjekts zu einem ganzzahligen Typobjekt, werden als Fehler gemeldet.  
  
 Verwenden Sie `-optionstrict:custom`, um Warnungen für implizite einschränkende Typkonvertierungen zu generieren. Verwenden Sie `-nowarn:numberlist`, um bestimmte Warnungen zu ignorieren, und `-warnaserror:numberlist`, um bestimmte Warnungen als Fehler zu behandeln.  
  
### <a name="to-set--optionstrict-in-the-visual-studio-ide"></a>So legen Sie-optionstrict in der Visual Studio-IDE fest  
  
1. Ein Projekt auswählen in **Projektmappen-Explorer**. Klicken Sie im Menü **Projekt** auf **Eigenschaften.**   
  
2. Klicken Sie auf die Registerkarte **Kompilieren**.  
  
3. Ändern Sie den Wert im Feld **Option Strict** .  
  
### <a name="to-set--optionstrict-programmatically"></a>So legen Sie-optionstrict Programm gesteuert fest  
  
- Siehe [Option Strict-Anweisung](../../../visual-basic/language-reference/statements/option-strict-statement.md).  
  
## <a name="example"></a>Beispiel  
 Der folgende Code kompiliert `Test.vb` mithilfe der strengen Typsemantik.  
  
```console
vbc -optionstrict+ test.vb  
```  
  
## <a name="see-also"></a>Siehe auch

- [Visual Basic-Befehlszeilencompiler](../../../visual-basic/reference/command-line-compiler/index.md)
- [-optioncompare](../../../visual-basic/reference/command-line-compiler/optioncompare.md)
- [-optionexplicit](../../../visual-basic/reference/command-line-compiler/optionexplicit.md)
- [-optioninfer](../../../visual-basic/reference/command-line-compiler/optioninfer.md)
- [-nowarn](../../../visual-basic/reference/command-line-compiler/nowarn.md)
- [-warnaserror (Visual Basic)](../../../visual-basic/reference/command-line-compiler/warnaserror.md)
- [Beispiele für Kompilierungsbefehlszeilen](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [Option Strict-Anweisung](../../../visual-basic/language-reference/statements/option-strict-statement.md)
- [VB-Standard, Projekte, Dialogfeld „Optionen“](/visualstudio/ide/reference/visual-basic-defaults-projects-options-dialog-box)
