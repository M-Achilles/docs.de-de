---
title: CorDebugChainReason-Enumeration
ms.date: 03/30/2017
api_name:
- CorDebugChainReason
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- CorDebugChainReason
helpviewer_keywords:
- CorDebugChainReason enumeration [.NET Framework debugging]
ms.assetid: c915da51-50b2-41df-841a-2b971f4d0975
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: fce803544b393ac2c441779183cbf49d4c39bdae
ms.sourcegitcommit: 3caa92cb97e9f6c31f21769c7a3f7c4304024b39
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/25/2019
ms.locfileid: "71273976"
---
# <a name="cordebugchainreason-enumeration"></a>CorDebugChainReason-Enumeration
Gibt den Grund oder die Gründe für die Initiierung einer Aufrufkette an.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef enum CorDebugChainReason {  
    CHAIN_NONE              = 0x000,  
    CHAIN_CLASS_INIT        = 0x001,  
    CHAIN_EXCEPTION_FILTER  = 0x002,  
    CHAIN_SECURITY          = 0x004,  
    CHAIN_CONTEXT_POLICY    = 0x008,  
    CHAIN_INTERCEPTION      = 0x010,  
    CHAIN_PROCESS_START     = 0x020,  
    CHAIN_THREAD_START      = 0x040,  
    CHAIN_ENTER_MANAGED     = 0x080,  
    CHAIN_ENTER_UNMANAGED   = 0x100,  
    CHAIN_DEBUGGER_EVAL     = 0x200,  
    CHAIN_CONTEXT_SWITCH    = 0x400,  
    CHAIN_FUNC_EVAL         = 0x800  
} CorDebugChainReason;  
```  
  
## <a name="members"></a>Member  
  
|Member|Beschreibung|  
|------------|-----------------|  
|`CHAIN_NONE`|Es wurde keine Aufrufkette initiiert.|  
|`CHAIN_CLASS_INIT`|Die Kette wurde durch einen Konstruktor initiiert.|  
|`CHAIN_EXCEPTION_FILTER`|Die Kette wurde durch einen Ausnahmefilter initiiert.|  
|`CHAIN_SECURITY`|Die Kette wurde durch Code initiiert, der Sicherheit erzwingt.|  
|`CHAIN_CONTEXT_POLICY`|Die Kette wurde durch eine Kontextrichtlinie initiiert.|  
|`CHAIN_INTERCEPTION`|Nicht verwendet.|  
|`CHAIN_PROCESS_START`|Nicht verwendet.|  
|`CHAIN_THREAD_START`|Die Kette wurde durch den Start einer Threadausführung initiiert.|  
|`CHAIN_ENTER_MANAGED`|Die Kette wurde durch den Einstieg in verwalteten Code initiiert.|  
|`CHAIN_ENTER_UNMANAGED`|Die Kette wurde durch den Einstieg in nicht verwalteten Code initiiert.|  
|`CHAIN_DEBUGGER_EVAL`|Nicht verwendet.|  
|`CHAIN_CONTEXT_SWITCH`|Nicht verwendet.|  
|`CHAIN_FUNC_EVAL`|Die Kette wurde durch eine Funktionsauswertung initiiert.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie die [ICorDebugChain:: geverrat](icordebugchain-getreason-method.md) -Methode, um die Gründe für die Initiierung einer Rückruf Kette zu ermitteln.  
  
## <a name="requirements"></a>Anforderungen  
 **Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../get-started/system-requirements.md).  
  
 **Header:** Cordebug. idl, Cordebug. h  
  
 **Fern** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [Debuggen von Enumerationen](debugging-enumerations.md)
