---
ms.openlocfilehash: 69b25db88c7580787bbb47fb0902b6bb072f8dde
ms.sourcegitcommit: 5b6d778ebb269ee6684fb57ad69a8c28b06235b9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2019
ms.locfileid: "59235739"
---
### <a name="assemblies-compiled-with-regexcompiletoassembly-breaks-between-40-and-45"></a>Mit der Regex.CompileToAssembly-Methode kompilierte Assemblys zwischen 4.0 und 4.5 werden unterbrochen

|   |   |
|---|---|
|Details|Wenn eine Assembly aus kompilierten regulären Ausdrücken mit .NET Framework 4.5 erstellt wird und auf .NET Framework 4 ausgerichtet ist, wird bei dem Versuch, die regulären Ausdrücke in dieser Assembly auf einem System zu verwenden, auf dem .NET Framework 4 installiert ist, eine Ausnahme ausgelöst.|
|Vorschlag|Um dieses Problem zu umgehen, haben Sie die folgenden Möglichkeiten:<ul><li>Erstellen Sie die Assembly, die die regulären Ausdrücke enthält, mit .NET Framework 4.</li><li>Verwenden Sie einen interpretierten regulären Ausdruck.</li></ul>|
|Bereich|Gering|
|Version|4.5|
|Typ|Laufzeit|
|Betroffene APIs|<ul><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName)?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[])?displayProperty=nameWithType></li><li><xref:System.Text.RegularExpressions.Regex.CompileToAssembly(System.Text.RegularExpressions.RegexCompilationInfo[],System.Reflection.AssemblyName,System.Reflection.Emit.CustomAttributeBuilder[],System.String)?displayProperty=nameWithType></li></ul>|
