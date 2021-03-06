---
title: <remove>-Element für bypasslist (Netzwerkeinstellungen)
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/defaultProxy/bypasslist/remove
- http://schemas.microsoft.com/.NetConfiguration/v2.0#remove
helpviewer_keywords:
- <bypasslist>, remove element
- remove element, bypasslist
- bypasslist, remove element
- remove element, bypasslist
ms.assetid: 61dcfb4a-e3d9-4abf-a2cd-7d685fe2f64b
ms.openlocfilehash: 97b49a8a520d6a4f72945366874991d2deb18710
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71697897"
---
# <a name="remove-element-for-bypasslist-network-settings"></a>\<remove >-Element für bypasslist (Netzwerkeinstellungen)

Entfernt eine IP-Adresse oder einen DNS-Namen aus der Proxy Umgehungs Liste.

[ **\<configuration>** ](../configuration-element.md)  
&nbsp; @ no__t-1[ **@no__t -4system. net >** ](system-net-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3[ **\<defaultproxy >** ](defaultproxy-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5[ **\<bypasslist >** ](bypasslist-element-network-settings.md)  
&nbsp; @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5 @ no__t-6 @ no__t-7 **\<remove >**  

## <a name="syntax"></a>Syntax

```xml
<remove
  address="regular expression"
/>
```

## <a name="attributes-and-elements"></a>Attribute und Elemente

In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.

### <a name="attributes"></a>Attribute

|**Attribut**|**Beschreibung**|
|-------------------|---------------------|
|`address`|Einen regulären Ausdruck, der eine IP-Adresse oder einen DNS-Namen beschreibt.|

### <a name="child-elements"></a>Untergeordnete Elemente

Keine

### <a name="parent-elements"></a>Übergeordnete Elemente

|**Element**|**Beschreibung**|
|-----------------|---------------------|
|[bypasslist](bypasslist-element-network-settings.md)|Stellt eine Reihe von regulären Ausdrücken bereit, die Adressen beschreiben, die keinen Proxy verwenden.|

## <a name="remarks"></a>Hinweise

Das `remove`-Element entfernt reguläre Ausdrücke, in denen IP-Adressen oder DNS-Servernamen aus der Liste der Adressen, die einen Proxy Server umgehen, beschrieben werden. Die Adressen wurden zuvor in der Konfigurationsdatei oder auf einer höheren Ebene in der Konfigurations Hierarchie definiert.

Der Wert für das `address`-Attribut muss ein regulärer Ausdruck sein, der einen Satz von IP-Adressen oder Hostnamen beschreibt.

Weitere Informationen zu regulären Ausdrücken finden Sie unter. [.NET Framework reguläre Ausdrücke](../../../../standard/base-types/regular-expressions.md).

## <a name="configuration-files"></a>Konfigurationsdateien

Dieses Element kann in der Anwendungskonfigurationsdatei oder in der Computerkonfigurationsdatei ("Machine.config") verwendet werden.

## <a name="example"></a>Beispiel

Im folgenden Beispiel werden alle vorherigen Definitionen für die Domäne Adventure-Works.com entfernt und dann der Umgehungs Liste die contoso.com-Domäne hinzugefügt.

```xml
<configuration>
  <system.net>
    <defaultProxy>
      <bypasslist>
        <remove address="[a-z]+\.adventure-works\.com$" />
        <add address="[a-z]+\.contoso\.com$" />
      </bypasslist>
    </defaultProxy>
  </system.net>
</configuration>
```

## <a name="see-also"></a>Siehe auch

- <xref:System.Net.WebProxy?displayProperty=nameWithType>
- [Network Settings Schema (Schema für Netzwerkeinstellungen)](index.md)
