---
ms.openlocfilehash: e605e0f2636d83745815ec4ed27bf72692f18d15
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67802709"
---
### <a name="aspnet-fix-handling-of-inputattributes-and-labelattributes-for-webforms-checkbox-control"></a>Behandlung von Korrekturen in ASP.NET bei InputAttributes und LabelAttributes für WebForms CheckBox-Steuerelemente

|   |   |
|---|---|
|Details|Bei Anwendungen, die .NET Framework 4.7.2 und frühere Versionen nutzen, gehen <xref:System.Web.UI.WebControls.CheckBox.InputAttributes?displayProperty=nameWithType> und <xref:System.Web.UI.WebControls.CheckBox.LabelAttributes?displayProperty=nameWithType>, die einem WebForms <xref:System.Web.UI.WebControls.CheckBox>-Steuerelement programmgesteuert hinzugefügt wurden, nach einem Postback verloren. Bei Anwendungen, die .NET Framework 4.8 oder höhere Versionen verwenden, bleiben sie nach einem Postback erhalten.|
|Vorschlag|Wenn Sie bei der Wiederherstellung nach einem Postback das richtige Verhalten erzielen möchten, legen Sie <code>targetFrameworkVersion</code> auf 4.8 oder höher fest. Beispiel:<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;system.web&gt;&#13;&#10;&lt;httpRuntime targetFramework=&quot;4.8&quot;/&gt;&#13;&#10;&lt;/system.web&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>Wenn Sie eine frühere oder gar keine Version angeben, wird das alte falsche Verhalten beibehalten.|
|Bereich|Unbekannt|
|Version|4.8|
|Typ|Laufzeit|
|Betroffene APIs|<ul><li><xref:System.Web.UI.WebControls.CheckBox?displayProperty=nameWithType></li></ul>|

