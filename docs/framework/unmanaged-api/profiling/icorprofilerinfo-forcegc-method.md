---
title: ICorProfilerInfo::ForceGC-Methode
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo.ForceGC
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo::ForceGC
helpviewer_keywords:
- ICorProfilerInfo::ForceGC method [.NET Framework profiling]
- ForceGC method [.NET Framework profiling]
ms.assetid: 0da1ef80-d242-4636-87d0-43e0470b342a
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 208552dd94f587b9326280ad455ca2478ae4ac4d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67780252"
---
# <a name="icorprofilerinfoforcegc-method"></a>ICorProfilerInfo::ForceGC-Methode
Erzwingt eine Garbagecollection in der common Language Runtime (CLR) ausgeführt.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT ForceGC();  
```  
  
## <a name="remarks"></a>Hinweise  
 Die `ForceGC` -Methode muss aufgerufen werden, nur von einem Thread, der nie verwalteten Code ausgeführt hat, und verfügt nicht über die Profilerrückrufe für seinen Stapel. Die einfachste Implementierung ist die Erstellung von einem separaten Thread innerhalb des Profilers, der aufruft `ForceGC` signalisiert.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICorProfilerInfo-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)
