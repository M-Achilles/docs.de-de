---
title: ICorProfilerCallback8::DynamicMethodJITCompilationStarted-Methode
ms.date: 04/10/2018
api_name:
- ICorProfilerCallback8.DynamicMethodJITCompilationStarted
api_location:
- mscorwks.dll
- corprof.idl
api_type:
- COM
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5a60f074ce0081df07a61d0b832d542c8873776f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67757983"
---
# <a name="icorprofilercallback8dynamicmethodjitcompilationstarted-method"></a>ICorProfilerCallback8::DynamicMethodJITCompilationStarted-Methode
[Wird nur in der .NET Framework 4.7 und höheren Versionen unterstützt]  
  
Benachrichtigt den Profiler an, wenn JIT-Kompilierung einer dynamischen Methode gestartet wurde.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT DynamicMethodJITCompilationStarted(  
     [in]  FunctionID  functionId,   
     [in]  BOOL        fIsSafeToBlock,   
     [in]  LPCBYTE     pILHeader,   
     [in]  LONG        cbILHeader   
);  
```  
  
## <a name="parameters"></a>Parameter  
[in] `functionId`  
Der Bezeichner der in-Memory-Funktion, die für die JIT-Kompilierung gestartet wird.   

[in] `fIsSafeToBlock`   
`true` um anzugeben, das blockieren die Laufzeit zu warten, bis der aufrufende Thread von diesem Rückruf zurück zur Folge haben. `false` um anzugeben, dass die Blockierung der Vorgang der Laufzeit nicht beeinflusst wird.  

[in] `pILHeader`    
Ein Zeiger auf das erste Byte des IL-Headers der Methode.   

[in] `cbILHeader`    
Die Anzahl der Bytes in der IL-Header. 

## <a name="remarks"></a>Hinweise  

Dieser Rückruf wird immer dann ausgelöst, wenn eine dynamische Methode JIT-kompiliert wird. Dies umfasst verschiedene IL-Stubs und LCG-Methoden. Das Ziel ist, die Profiler-Schreiber genügend Informationen zum Identifizieren der kompilierten Methode für Benutzer bereitstellen.

> [!NOTE]
> `functionId` Werte können nicht zum Auflösen in ihren Metadatentoken verwendet werden, da dynamische Methoden keine Metadaten haben.

Die `pILHeader` -Zeiger ist nur gültig, während des Rückrufs.

## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v47plus](../../../../includes/net-current-v47plus.md)]  
  
## <a name="see-also"></a>Siehe auch

- [DynamicMethodJITCompilationStarted-Methode](icorprofilercallback8-dynamicmethodjitcompilationfinished-method.md)
- [ICorProfilerCallback8-Schnittstelle](icorprofilercallback8-interface.md)
