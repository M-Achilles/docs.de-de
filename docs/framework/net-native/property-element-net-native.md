---
title: <Property>-Element (.net Native)
ms.date: 03/30/2017
ms.assetid: ad4ba56d-3bcb-4c10-ba90-1cc66e2175a1
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 54daf15c593327bf3255f40f6eb6931ffc8bd3c6
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2019
ms.locfileid: "71049313"
---
# <a name="property-element-net-native"></a>\<Property >-Element (.net Native)
Wendet eine Laufzeitreflektionsrichtlinie auf eine Eigenschaft an.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<Property Name="property_name"  
          Browse="policy_type"  
          Dynamic="policy_type"  
          Serialize="policy_type" />  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Attributtyp|Beschreibung|  
|---------------|--------------------|-----------------|  
|`Name`|Allgemein|Erforderliches Attribut. Gibt den Eigenschaftennamen an.|  
|`Browse`|Spiegelung|Optionales Attribut. Steuert das Abfragen nach Informationen über die Eigenschaft oder das Auflisten der Eigenschaft, aber ermöglicht keinen dynamischen Zugriff zur Laufzeit.|  
|`Dynamic`|Spiegelung|Optionales Attribut. Steuert den Laufzeitzugriff auf die Eigenschaft, um dynamische Programmierung zu ermöglichen. Diese Richtlinie stellt sicher, dass eine Eigenschaft zur Laufzeit dynamisch festgelegt oder abgerufen werden kann.|  
|`Serialize`|Serialisierung|Optionales Attribut. Steuert den Laufzeitzugriff auf eine Eigenschaft, damit Typinstanzen von Bibliotheken wie dem Newtonsoft JSON-Serialisierungsprogramm serialisiert werden können oder für die Datenbindung verwendet werden können.|  
  
## <a name="name-attribute"></a>Namensattribut  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|*method_name*|Der Eigenschaftenname. Der Typ der Eigenschaft wird durch das übergeordnete [\<Type>](type-element-net-native.md)- oder [\<TypeInstantiation>](typeinstantiation-element-net-native.md)-Element definiert.|  
  
## <a name="all-other-attributes"></a>Alle anderen Attribute  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|*policy_setting*|Die Einstellung, die auf diesen Richtlinientyp für die Eigenschaft angewendet werden soll. Mögliche Werte sind `Auto`, `Excluded`, `Included` und `Required`. Weitere Informationen finden Sie unter [Richtlinieneinstellungen für die Laufzeitanweisung](runtime-directive-policy-settings.md).|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keine  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|[\<Type>](type-element-net-native.md)|Wendet die Reflektionsrichtlinie auf einen Typ und alle seine Member an.|  
|[\<TypeInstantiation>](typeinstantiation-element-net-native.md)|Wendet die Reflektionsrichtlinie auf einen konstruierten generischen Typ und alle seine Member an.|  
  
## <a name="remarks"></a>Hinweise  
 Wenn die Richtlinie einer Eigenschaft nicht explizit definiert ist, erbt sie die Laufzeitrichtlinie des übergeordneten Elements.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird Reflektion zum Instanziieren eines `Book`-Objekts und zum Anzeigen seiner Eigenschaftenwerte verwendet. Die ursprüngliche Datei default.rd.xml für das Projekt sieht folgendermaßen aus:  
  
```xml  
<Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
   <Application>  
      <Namespace Name="LibraryApplications"  Browse="Required Public" >  
         <Type Name="Book"   Activate="All" />  
      </Namespace>  
   </Application>  
</Directives>  
```  
  
 Die Datei wendet den Wert `All` auf die `Activate`-Richtlinie für die `Book`-Klasse an, die den Zugriff auf Klassenkonstruktoren über Reflektion ermöglicht. Die `Browse`-Richtlinie für die `Book`-Klasse wird vom übergeordneten Namespace geerbt. Diese wird auf `Required Public` festgelegt, wodurch Metadaten zur Laufzeit verfügbar werden.  
  
 Der Quellcode für das Beispiel lautet wie folgt. Die `outputBlock` -Variable stellt <xref:Windows.UI.Xaml.Controls.TextBlock> ein-Steuerelement dar.  
  
 [!code-csharp[ProjectN_Reflection#6](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn_reflection/cs/property1.cs#6)]  
  
 Das Kompilieren und Ausführen dieses Beispiels löst jedoch eine [MissingRuntimeArtifactException](missingruntimeartifactexception-class-net-native.md)-Ausnahme aus. Obwohl wir Metadaten für den `Book`-Typ verfügbar gemacht haben, haben wir keine Implementierungen der Eigenschaftengetter dynamisch zur Verfügung gestellt. Wir können diesen Fehler auf eine von zwei Arten beheben:  
  
- Durch Definieren der `Dynamic`-Richtlinie für den `Book`-Typ in dessen [\<Type>](type-element-net-native.md)-Element.  
  
- Durch Hinzufügen eines verschachtelten [\<Property>](property-element-net-native.md)-Elements für jede Eigenschaft, deren Getter wir wie in der folgenden Datei „default.rd.xml“ aufrufen möchten.  
  
    ```xml  
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata">  
       <Application>  
          <Namespace Name="LibraryApplications"  Browse="Required Public" >  
             <Type Name="Book"   Activate="All" >  
                <Property Name="Title" Dynamic="Required" />  
                <Property Name="Author" Dynamic="Required" />  
                  <Property Name="ISBN" Dynamic="Required" />  
             </Type>  
          </Namespace>  
       </Application>  
    </Directives>  
    ```  
  
## <a name="see-also"></a>Siehe auch

- [Runtime Directives (rd.xml) Configuration File Reference (Referenz zur Laufzeitanweisungs-Konfigurationsdatei (rd.xml))](runtime-directives-rd-xml-configuration-file-reference.md)
- [Elemente der Laufzeitanweisung](runtime-directive-elements.md)
- [Richtlinieneinstellungen für die Laufzeitanweisung](runtime-directive-policy-settings.md)
