---
title: Schema für Compiler- und Sprachanbietereinstellungen
ms.date: 03/30/2017
helpviewer_keywords:
- configuration settings [.NET Framework], compilers
- compiler configuration elements, schema
- compiler configuration elements
- language providers
- compiler configuration settings, schema
- configuration schema [.NET Framework], compiler settings
- language providers, settings schema
- compiler configuration settings
ms.assetid: c020b139-8699-4f0d-9ac9-70d0c5b2a8c8
ms.openlocfilehash: a651e4ca76fda9e65ea4a5848c19b1f0ebfe91b1
ms.sourcegitcommit: 1b020356e421a9314dd525539da12463d980ce7a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/30/2019
ms.locfileid: "70168930"
---
# <a name="compiler-and-language-provider-settings-schema"></a>Schema für Compiler- und Sprachanbietereinstellungen
Die Compiler- und Sprachanbietereinstellungen geben Compilerkonfigurationselemente für verfügbare Sprachanbieter an. Jedes Compilerkonfigurationselement gibt den Typnamen des Codeanbieters, Compilerparameter, unterstützte Sprachnamen und unterstützte Dateierweiterungen an.  
  
.NET Framework definiert die ursprünglichen Compilereinstellungen in der Computerkonfigurationsdatei (Machine.config). Entwickler und Compileranbieter können Konfigurationseinstellungen für eine neue <xref:System.CodeDom.Compiler.CodeDomProvider>-Implementierung hinzufügen. Verwenden Sie die <xref:System.CodeDom.Compiler.CodeDomProvider.GetAllCompilerInfo%2A?displayProperty=nameWithType>-Methode, um Sprachanbieter und Compilerkonfigurationseinstellungen auf einem Computer programmgesteuert aufzulisten.  
  
[ **\<configuration>** ](../configuration-element.md)  
&nbsp;&nbsp;[ **\<System. CodeDom->** ](system-codedom-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Compiler >** ](compilers-element.md)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[ **\<Compiler>** ](compiler-element.md)  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<system.codedom>](system-codedom-element.md)|Gibt die Compilerkonfigurationseinstellungen für verfügbare Sprachanbieter an.|  
|[\<compilers>](compilers-element.md)|Der Container für Compilerkonfigurationselemente, dieser enthält 0 (null) oder mehr [\<compiler>](compiler-element.md)-Elemente.|  
|[\<compiler>](compiler-element.md)|Gibt die Compilerkonfigurationsattribute für einen Sprachanbieter an.|  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht ein typisches Compilerkonfigurationselement.  
  
```xml  
<configuration>  
   <system.codedom>  
     <compilers>  
       <!-- zero or more compiler elements -->  
       <compiler  
          language="c#;cs;csharp"  
          extension=".cs"  
          type="Microsoft.CSharp.CSharpCodeProvider, System, Version=1.0.5000.0, Culture=neutral, PublicKeyToken=b77a5c561934e089"  
          compilerOptions=""  
          warningLevel="1" />  
     </compilers>  
   </system.codedom>  
</configuration>  
```  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.CodeDom.Compiler.CompilerInfo>
- <xref:System.CodeDom.Compiler.CodeDomProvider>
- [Konfigurationsdateischema](../index.md)
- [\<compiler> Element](compiler-element.md)
