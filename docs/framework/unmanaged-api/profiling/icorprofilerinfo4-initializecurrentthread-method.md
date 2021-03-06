---
title: ICorProfilerInfo4::InitializeCurrentThread-Methode
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4::InitializeCurrentThread
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::InitializeCurrentThread
helpviewer_keywords:
- ICorProfilerInfo4::InitializeCurrentThread method [.NET Framework profiling]
- InitializeCurrentThread method, ICorProfilerInfo4 interface [.NET Framework profiling]
ms.assetid: 18a3335c-8c75-476c-b6de-72c0bfedae5d
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b9bb5a2629e435d76691d48feef6689191b66373
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69957888"
---
# <a name="icorprofilerinfo4initializecurrentthread-method"></a>ICorProfilerInfo4::InitializeCurrentThread-Methode
Initialisiert den aktuellen Thread vor nachfolgenden Profiler-API-aufrufen im gleichen Thread, sodass der Deadlock vermieden werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT InitializeCurrentThread ();  
```  
  
## <a name="remarks"></a>Hinweise  
 Es wird empfohlen, für `InitializeCurrentThread` jeden Thread aufzurufen, der eine Profiler-API aufruft, während Angehaltene Threads vorhanden sind. Diese Methode wird in der Regel von samplingprofilergeräten verwendet, die ihren eigenen Thread erstellen, um die [ICorProfilerInfo2::D ostacksnapshot](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-dostacksnapshot-method.md) -Methode aufzurufen, während der Zielthread angehalten wird. Durch einen `InitializeCurrentThread` Aufruf von einmal, wenn der Profiler erstmalig den Samplingthread erstellt, können Profiler sicherstellen, dass die verzögerte Initialisierung pro Thread, die die `DoStackSnapshot` CLR andernfalls während des ersten Aufrufs von ausführen würde, nun sicher auftreten kann, wenn keine anderen Threads gesperrt.  
  
> [!NOTE]
> `InitializeCurrentThread`führt die Initialisierung im Voraus aus, um Aufgaben abzuschließen, die Sperren akzeptieren und möglicherweise einen Deadlock verursachen. Wird `InitializeCurrentThread` nur aufgerufen, wenn keine angehaltenen Threads vorhanden sind.  
  
## <a name="requirements"></a>Anforderungen  
 **Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Corprof. idl, Corprof. h  
  
 **Fern** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICorProfilerInfo4-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)
- [Profilerstellungsschnittstellen](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [Profilerstellung](../../../../docs/framework/unmanaged-api/profiling/index.md)
