---
title: ICorDebugType::GetType-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugType.GetType
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugType::GetType
helpviewer_keywords:
- ICorDebugType::GetType method [.NET Framework debugging]
- GetType method, ICorDebugType interface [.NET Framework debugging]
ms.assetid: d6e64534-4d47-4ad0-a340-7590e07e2b4a
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 78f2733584e07433171c91d6a2674d3a67c8e283
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67772521"
---
# <a name="icordebugtypegettype-method"></a>ICorDebugType::GetType-Methode
Ruft einen CorElementType-Wert, der den systemeigenen Typ der common Language Runtime (CLR) beschreibt <xref:System.Type> ICorDebugType dargestellt.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetType (  
    [out] CorElementType   *ty  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `ty`  
 [out] Ein Zeiger auf den Wert der `CorElementType` -Enumeration, die die CLR gibt <xref:System.Type> , das von diesem `ICorDebugType` darstellt.  
  
## <a name="remarks"></a>Hinweise  
 Wenn der Wert des `ty` entweder ELEMENT_TYPE_CLASS oder ELEMENT_TYPE_VALUETYPE, die [ICorDebugType:: GetClass](../../../../docs/framework/unmanaged-api/debugging/icordebugtype-getclass-method.md) Methode kann aufgerufen werden, um den nicht instanziierten Typ für einen generischen Typ zu erhalten, rufen Sie andernfalls nicht `ICorDebugType::GetClass`.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
