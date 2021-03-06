---
title: ICorProfilerCallback::ExceptionCatcherEnter-Methode
ms.date: 03/30/2017
api_name:
- ICorProfilerCallback.ExceptionCatcherEnter
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerCallback::ExceptionCatcherEnter
helpviewer_keywords:
- ICorProfilerCallback::ExceptionCatcherEnter method [.NET Framework profiling]
- ExceptionCatcherEnter method [.NET Framework profiling]
ms.assetid: 41462329-a648-46f0-ae6d-728b94c31aa9
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 6a90ae67a7d264273bd0e07a42aa6195122a06ec
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776140"
---
# <a name="icorprofilercallbackexceptioncatcherenter-method"></a>ICorProfilerCallback::ExceptionCatcherEnter-Methode
Benachrichtigt den Profiler, das Steuerelement an den entsprechenden übergebenen `catch` Block.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT ExceptionCatcherEnter(  
    [in] FunctionID functionId,  
    [in] ObjectID   objectId);  
```  
  
## <a name="parameters"></a>Parameter  
 `functionId`  
 [in] Der Bezeichner der Funktion mit dem `catch` Block.  
  
 `objectId`  
 [in] Der Bezeichner der Ausnahme behandelt wird.  
  
## <a name="remarks"></a>Hinweise  
 Die `ExceptionCatcherEnter` Methode wird aufgerufen, nur dann, wenn der Catch-Punkt im Code, der mit dem Compiler just-in-Time (JIT) kompiliert ist. Kein Aufruf eine Ausnahme, die in nicht verwaltetem Code oder in den internen Code der Laufzeit abgefangen wird diese Benachrichtigung. Die `objectId` erneut Wert übergeben wird, da eine Garbagecollection verschoben wurden, das Objekt seit konnte die `ExceptionThrown` Benachrichtigung.  
  
 Der Profiler sollte die Implementierung dieser Methode nicht blockieren, da der Stapel nicht in einem Zustand handeln, der Garbagecollection zulässt, und daher die Präemptive Garbagecollection kann nicht aktiviert werden kann. Wenn der Profiler hier blockiert und Garbagecollection wird versucht, die Laufzeit blockiert, bis dieser Rückruf zurückgegeben.  
  
 Der Profiler Implementierung dieser Methode sollte nicht in verwaltetem Code oder in einer verwalteten Speicher reservieren aufrufen.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICorProfilerCallback-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)
- [ExceptionCatcherLeave-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-exceptioncatcherleave-method.md)
