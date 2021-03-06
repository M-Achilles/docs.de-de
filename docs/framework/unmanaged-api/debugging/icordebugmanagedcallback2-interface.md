---
title: ICorDebugManagedCallback2-Schnittstelle
ms.date: 03/30/2017
api_name:
- ICorDebugManagedCallback2
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugManagedCallback2
helpviewer_keywords:
- ICorDebugManagedCallback2 interface [.NET Framework debugging]
ms.assetid: cf7b7cfa-1c4b-4d8c-be70-4f9ed15a788b
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: ca33436d98edf5844a5ca27c9ac89648f10ec0c5
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69909982"
---
# <a name="icordebugmanagedcallback2-interface"></a>ICorDebugManagedCallback2-Schnittstelle
Stellt Methoden bereit, um Debugger-Ausnahmebehandlung und Assistenten für verwaltetes Debuggen (MDA) zu unterstützen. `ICorDebugManagedCallback2`ist eine logische Erweiterung der [ICorDebugManagedCallback](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md) -Schnittstelle.  
  
## <a name="methods"></a>Methoden  
  
|Methode|Beschreibung|  
|------------|-----------------|  
|[ChangeConnection-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-changeconnection-method.md)|Benachrichtigt den Debugger, dass sich der Satz der Tasks, die der angegebenen Verbindung zugeordnet sind, geändert hat.|  
|[CreateConnection-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-createconnection-method.md)|Benachrichtigt den Debugger, dass eine neue Verbindung erstellt wurde.|  
|[DestroyConnection-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-destroyconnection-method.md)|Benachrichtigt den Debugger, dass die angegebene Verbindung beendet wurde.|  
|[Exception-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-exception-method.md)|Benachrichtigt den Debugger, dass eine Suche nach einem Ausnahmehandler gestartet wurde.|  
|[ExceptionUnwind-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-exceptionunwind-method.md)|Stellt während des Entwicklungs Vorgangs der Ausnahme eine Status Benachrichtigung bereit.|  
|[FunctionRemapComplete-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-functionremapcomplete-method.md)|Benachrichtigt den Debugger, dass die Codeausführung zu einer neuen Version einer bearbeiteten Funktion gewechselt hat.|  
|[FunctionRemapOpportunity-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-functionremapopportunity-method.md)|Benachrichtigt den Debugger, dass die Codeausführung einen Sequenz Punkt in einer älteren Version einer bearbeiteten Funktion erreicht hat.|  
|[MDANotification-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-mdanotification-method.md)|Stellt eine Benachrichtigung bereit, dass bei der Codeausführung eine MDA-Nachricht (Managed Debug Assistant) aufgetreten ist.|  
  
## <a name="remarks"></a>Hinweise  
 Die `ICorDebugManagedCallback2` -Schnittstelle `ICorDebugManagedCallback` erweitert die-Schnittstelle, um neue Debugereignisse zu verarbeiten, die in der .NET Framework Version 2,0  
  
 Ein Debugger muss implementieren `ICorDebugManagedCallback2` , wenn er .NET Framework 2,0-Anwendungen debuggt. Eine Instanz von `ICorDebugManagedCallback` oder `ICorDebugManagedCallback2` wird als Rückruf Objekt an [ICorDebug:: SetManagedHandler](../../../../docs/framework/unmanaged-api/debugging/icordebug-setmanagedhandler-method.md)übermittelt.  
  
> [!NOTE]
> Diese Schnittstelle kann weder computerübergreifend noch prozessübergreifend remote aufgerufen werden.  
  
## <a name="requirements"></a>Anforderungen  
 **Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Cordebug. idl, Cordebug. h  
  
 **Fern** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [Diagnosing Errors with Managed Debugging Assistants (Diagnostizieren von Fehlern mit Assistenten für verwaltetes Debuggen)](../../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)
- [Debuggen von Schnittstellen](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
- [ICorDebugManagedCallback-Schnittstelle](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback-interface.md)
