---
title: <ThrowUnobservedTaskExceptions>-Element
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ThrowUnobservedTaskExceptions element
- <ThrowUnobservedTaskExceptions> element
ms.assetid: cea7e588-8b8d-48d2-9ad5-8feaf3642c18
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3ed1e66c4aadab656455686a7a1e5028b035676a
ms.sourcegitcommit: 4e2d355baba82814fa53efd6b8bbb45bfe054d11
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2019
ms.locfileid: "70252268"
---
# <a name="throwunobservedtaskexceptions-element"></a>\<Throwunobservedtaskexceptions-> Element
Gibt an, ob ein laufender Prozess durch Aufgabenausnahmefehler beendet werden soll.  
  
[ **\<configuration>** ](../configuration-element.md)\
&nbsp;&nbsp;[ **\<Lauf Zeit >** ](runtime-element.md)\
&nbsp;&nbsp;&nbsp;&nbsp; **\<ThrowUnobservedTaskExceptions>**  
  
## <a name="syntax"></a>Syntax  
  
```xml  
<ThrowUnobservedTaskExceptions  
   enabled="true|false"/>  
```  
  
## <a name="attributes-and-elements"></a>Attribute und Elemente  
 In den folgenden Abschnitten werden Attribute sowie untergeordnete und übergeordnete Elemente beschrieben.  
  
### <a name="attributes"></a>Attribute  
  
|Attribut|Beschreibung|  
|---------------|-----------------|  
|`enabled`|Erforderliches Attribut.<br /><br /> Gibt an, ob der laufende Prozess durch nicht behandelte Aufgaben Ausnahmen beendet werden soll.|  
  
## <a name="enabled-attribute"></a>Enabled-Attribut  
  
|Wert|Beschreibung|  
|-----------|-----------------|  
|`false`|Beendet den laufenden Prozess für eine nicht behandelte Task Ausnahme nicht. Dies ist die Standardeinstellung.|  
|`true`|Beendet den laufenden Prozess für eine nicht behandelte Task Ausnahme.|  
  
### <a name="child-elements"></a>Untergeordnete Elemente  
 Keine  
  
### <a name="parent-elements"></a>Übergeordnete Elemente  
  
|Element|Beschreibung|  
|-------------|-----------------|  
|`configuration`|Das Stammelement in jeder von den Common Language Runtime- und .NET Framework-Anwendungen verwendeten Konfigurationsdatei.|  
|`runtime`|Enthält Informationen über Laufzeitinitialisierungsoptionen.|  
|||  
  
## <a name="remarks"></a>Hinweise  
 Wenn eine Ausnahme, die einem <xref:System.Threading.Tasks.Task> zugeordnet ist, nicht beobachtet wurde, gibt es keinen <xref:System.Threading.Tasks.Task.Wait%2A> Vorgang, das übergeordnete Element ist nicht angefügt, und die <xref:System.Threading.Tasks.Task.Exception%2A?displayProperty=nameWithType> Eigenschaft wurde nicht gelesen. die Task Ausnahme wird als nicht beobachtet betrachtet.  
  
 Standardmäßig löst der Finalizer standardmäßig eine <xref:System.Threading.Tasks.Task> Ausnahme aus und beendet den Prozess, wenn in der .NET Framework 4 eine Garbage Collection mit einer nicht beobachteten Ausnahme erfolgt. Die Beendigung des Prozesses wird durch die zeitliche Steuerung von Garbage Collection und Finalisierung bestimmt.  
  
 Um Entwicklern das Schreiben von asynchronem Code auf Grundlage von Aufgaben zu vereinfachen, ändert der .NET Framework 4,5 dieses Standardverhalten für nicht beobachtete Ausnahmen. Nicht beobachtete Ausnahmen bewirken weiterhin, <xref:System.Threading.Tasks.TaskScheduler.UnobservedTaskException> dass das Ereignis ausgelöst wird. der Prozess wird jedoch standardmäßig nicht beendet. Stattdessen wird die Ausnahme ignoriert, nachdem das-Ereignis ausgelöst wurde, unabhängig davon, ob ein Ereignishandler die Ausnahme beobachtet.  
  
 Im .NET Framework 4,5 können Sie das [ \<throwunobservedtaskexceptions >-Element](throwunobservedtaskexceptions-element.md) in einer Anwendungs Konfigurationsdatei verwenden, um das .NET Framework 4-Verhalten beim Auslösen einer Ausnahme zu aktivieren.  
  
 Sie können das Ausnahme Verhalten auch auf eine der folgenden Arten angeben:  
  
- Durch Festlegen der Umgebungsvariablen `COMPlus_ThrowUnobservedTaskExceptions` (`set COMPlus_ThrowUnobservedTaskExceptions=1`).  
  
- Durch Festlegen des DWORD-Registrierungs Werts throwunobservedtaskexceptions = 1 in der\\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft. NETFramework-Schlüssel.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird gezeigt, wie das Auslösen von Ausnahmen in Aufgaben mithilfe einer Anwendungs Konfigurationsdatei aktiviert wird.  
  
```xml  
<configuration>   
    <runtime>   
        <ThrowUnobservedTaskExceptions enabled="true"/>   
    </runtime>   
</configuration>  
```  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel wird veranschaulicht, wie eine nicht beobachtete Ausnahme von einem Task ausgelöst wird. Der Code muss als freigegebene Programm ausgeführt werden, damit er ordnungsgemäß funktioniert.  
  
 [!code-csharp[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/csharp/VS_Snippets_CLR/throwunobservedtaskexceptions/cs/program.cs#1)]
 [!code-vb[ThrowUnobservedTaskExceptions#1](../../../../../samples/snippets/visualbasic/VS_Snippets_CLR/throwunobservedtaskexceptions/vb/program.vb#1)]  
  
## <a name="see-also"></a>Siehe auch

- [Schema für Laufzeiteinstellungen](index.md)
- [Konfigurationsdateischema](../index.md)
