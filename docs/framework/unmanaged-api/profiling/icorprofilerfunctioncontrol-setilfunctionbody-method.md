---
title: ICorProfilerFunctionControl::SetILFunctionBody-Methode
ms.date: 03/30/2017
api_name:
- ICorProfilerFunctionControl.SetILFunctionBody
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerFunctionControl::SetILFunctionBody
helpviewer_keywords:
- ICorProfilerFunctionControl::SetILFunctionBody method [.NET Framework profiling]
- SetILFunctionBody method, ICorProfilerFunctionControl interface [.NET Framework profiling]
ms.assetid: 2c33f0f7-75b2-4c19-b2c7-c94b54997576
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: d831dd7a63c06327bb0f373b3be254401c6e2ee9
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780351"
---
# <a name="icorprofilerfunctioncontrolsetilfunctionbody-method"></a>ICorProfilerFunctionControl::SetILFunctionBody-Methode
Ersetzt den CIL-Text (Common Intermediate Language) der Methode.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT SetILFunctionBody(  
    [in]  ULONG   cbNewILMethodHeader,  
    [in, size_is(cbNewILMethodHeader)] LPCBYTE pbNewILMethodHeader);  
```  
  
## <a name="parameters"></a>Parameter  
 `cbNewILMethodHeader`  
 [in] Die Gesamtgröße der neuen CIL, einschließlich des Headers und aller Strukturen, die nach dem Text folgen.  
  
 `pbNewILMethodHeader`  
 [in] Ein Zeiger auf den neuen CIL-Header.  
  
## <a name="return-value"></a>Rückgabewert  
 Diese Methode gibt die folgenden spezifischen HRESULTs zurück.  
  
|HRESULT|Beschreibung|  
|-------------|-----------------|  
|S_OK|Die Ersetzung war erfolgreich.|  
  
## <a name="remarks"></a>Hinweise  
 Im Gegensatz zu den [ICorProfilerInfo:: SetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md) -Methode, die `SetILFunctionBody` Methode verwaltet den erforderlichen Speicher für den neuen CIL-Text. Dies bedeutet, dass die vom Profiler bereitgestellte CIL-Text nicht unbedingt mit zugeordnet werden die [IMethodMalloc](../../../../docs/framework/unmanaged-api/profiling/imethodmalloc-interface.md) -Schnittstelle zugeordnet oder innerhalb eines bestimmten Bereichs. Er kann auf jedem Heap zugeordnet werden. Der Profiler kann den für seinen CIL-Text, nach dem verwendeten Arbeitsspeicher frei `SetILFunctionBody` zurückgibt.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICorProfilerFunctionControl-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctioncontrol-interface.md)
