---
title: -netcf
ms.date: 03/13/2018
f1_keywords:
- /netcf
- -netcf
helpviewer_keywords:
- -netcf compiler option [Visual Basic]
- netcf compiler option [Visual Basic]
- /netcf compiler option [Visual Basic]
ms.assetid: db7cfa59-c315-401c-a59b-0daf355343d6
ms.openlocfilehash: 3df7e622f97a5a1291736180e3964b1b3deaea2f
ms.sourcegitcommit: eff6adb61852369ab690f3f047818c90580e7eb1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005449"
---
# <a name="-netcf"></a>-netcf

Legt den Compiler als Ziel für den .NET Compact Framework fest.

## <a name="syntax"></a>Syntax

```console
-netcf
```

## <a name="remarks"></a>Hinweise

Die Option "`-netcf`" bewirkt, dass der Visual Basic Compiler die .NET Compact Framework anstelle der vollständigen .NET Framework als Ziel hat. Sprachfunktionen, die nur in der vollständigen .NET Framework vorhanden sind, sind deaktiviert.

Die Option "`-netcf`" ist für die Verwendung mit [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)konzipiert. Die von `-netcf` deaktivierten sprach Features sind die gleichen sprach Features, die in den mit `-sdkpath` vorgesehenen Dateien nicht vorhanden sind.

> [!NOTE]
> Die Option "`-netcf`" ist innerhalb der Visual Studio-Entwicklungsumgebung nicht verfügbar. Sie ist nur verfügbar, wenn Sie über die Befehlszeile kompilieren. Die Option "`-netcf`" wird festgelegt, wenn ein Visual Basic Geräte Projekt geladen wird.

Mit der Option "`-netcf`" werden die folgenden sprach Features geändert:

- Das [End \<-Schlüsselwort > Statement-](../../../visual-basic/language-reference/statements/end-keyword-statement.md) Schlüsselwort, das die Ausführung eines Programms beendet, ist deaktiviert. Das folgende Programm wird ohne `-netcf` kompiliert und ausgeführt, schlägt jedoch zur Kompilierzeit mit `-netcf` fehl.

  [!code-vb[VbVbalrCompiler#34](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/netcf.vb#34)]

- Spätes Binden ist in allen Formularen deaktiviert. Kompilierzeitfehler werden generiert, wenn erkannte Szenarien mit späterer Bindung erkannt werden. Das folgende Programm wird ohne `-netcf` kompiliert und ausgeführt, schlägt jedoch zur Kompilierzeit mit `-netcf` fehl.

  [!code-vb[VbVbalrCompiler#35](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#35)]

- Die [Auto](../../../visual-basic/language-reference/modifiers/auto.md)-, [ANSI](../../../visual-basic/language-reference/modifiers/ansi.md)-und [Unicode](../../../visual-basic/language-reference/modifiers/unicode.md) -modifiziererer sind deaktiviert. Die Syntax der [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md) -Anweisung wird auch in `Declare Sub|Function name Lib "library" [Alias "alias"] [([arglist])]` geändert. Der folgende Code zeigt die Auswirkung von `-netcf` auf eine Kompilierung.

  [!code-vb[VbVbalrCompiler#36](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrCompiler/VB/OptionStrictOff.vb#36)]

- Die Verwendung von Visual Basic 6,0-Schlüsselwörtern, die aus Visual Basic entfernt wurden, generiert bei Verwendung von `-netcf` einen anderen Fehler. Dies wirkt sich auf die Fehlermeldungen für die folgenden Schlüsselwörter aus:

  - `Open`

  - `Close`

  - `Put`

  - `Print`

  - `Write`

  - `Input`

  - `Lock`

  - `Unlock`

  - `Seek`

  - `Width`

  - `Name`

  - `FreeFile`

  - `EOF`

  - `Loc`

  - `LOF`

  - `Line`

## <a name="example"></a>Beispiel

Mit dem folgenden Code wird `Myfile.vb` mit dem .NET Compact Framework kompiliert. dabei werden die Versionen von "mscorlib. dll" und "Microsoft. VisualBasic. dll" verwendet, die im Standard Installationsverzeichnis der .NET Compact Framework auf Laufwerk C gefunden werden. Normalerweise verwenden Sie die neueste Version der .NET Compact Framework.

```console
vbc -netcf -sdkpath:"c:\Program Files\Microsoft Visual Studio .NET 2003\CompactFrameworkSDK\v1.0.5000\Windows CE " myfile.vb
```

## <a name="see-also"></a>Siehe auch

- [Visual Basic-Befehlszeilencompiler](../../../visual-basic/reference/command-line-compiler/index.md)
- [Beispiele für Kompilierungsbefehlszeilen](../../../visual-basic/reference/command-line-compiler/sample-compilation-command-lines.md)
- [-sdkpath](../../../visual-basic/reference/command-line-compiler/sdkpath.md)
