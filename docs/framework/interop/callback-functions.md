---
title: Rückruffunktionen
ms.date: 03/30/2017
helpviewer_keywords:
- callback function
- platform invoke, calling unmanaged functions
ms.assetid: c0aa8533-3b3b-42e8-9f60-84919793098c
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: eb30e7daed938b14bd0d936352c7455db6975e73
ms.sourcegitcommit: 289e06e904b72f34ac717dbcc5074239b977e707
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2019
ms.locfileid: "71051905"
---
# <a name="callback-functions"></a>Rückruffunktionen
Eine Rückruffunktion ist ein Code innerhalb einer verwalteten Anwendung, mit dem eine nicht verwaltete DLL-Funktion eine Aufgabe ausführen kann. Aufrufe einer Rückruffunktion werden indirekt von einer verwalteten Anwendung über eine DLL-Funktion und zurück an die verwaltete Implementierung übergeben. Einige der vielen DLL-Funktionen, die mit dem Plattformaufruf aufgerufen werden, erfordern eine Rückruffunktion in verwaltetem Code zur ordnungsgemäßen Ausführung.  
  
 Um die meisten DLL-Funktionen aus verwaltetem Code aufzurufen, erstellen Sie eine verwaltete Definition der Funktion, und rufen Sie sie dann auf. Der Vorgang ist einfach.  
  
 Die Verwendung einer DLL-Funktion, die eine Rückruffunktion benötigt, erfordert einige zusätzliche Schritte. Zunächst müssen Sie durch einen Blick auf die Dokumentation der Funktion ermitteln, ob die Funktion einen Rückruf erfordert. Als Nächstes müssen Sie die Rückruffunktion in einer verwalteten Anwendung erstellen. Zum Schluss rufen Sie die DLL-Funktion auf, indem Sie als Argument einen Zeiger an die Rückruffunktion übergeben. 
 
 In der folgenden Abbildung sind die Rückruffunktion und die Implementierungsschritte zusammengefasst:  
  
 ![Diagramm mit dem Plattformaufruf der Rückruffunktion](./media/callback-functions/platform-invoke-callback-process.gif)  
  
 Rückruffunktionen eignen sich ideal für die Verwendung in Situationen, in denen eine Aufgabe wiederholt ausgeführt wird. Eine weitere gängige Verwendungsmöglichkeit ist die Nutzung von Enumerationsfunktionen, wie z.B. **EnumFontFamilies**, **EnumPrinters** und **EnumWindows** in der Windows-API. Die **EnumWindows**-Funktion durchläuft alle vorhandenen Fenster auf Ihrem Computer und ruft die Rückruffunktion auf, die einen Task für jedes Fenster durchführt. Anweisungen und ein Beispiel finden Sie unter [Vorgehensweise: Implementieren von Rückruffunktionen](how-to-implement-callback-functions.md).  
  
## <a name="see-also"></a>Siehe auch

- [Vorgehensweise: Implementieren von Rückruffunktionen](how-to-implement-callback-functions.md)
- [Calling a DLL Function (Aufrufen einer DLL-Funktion)](calling-a-dll-function.md)
