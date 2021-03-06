---
title: ICorDebugCodeEnum::Next-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugCodeEnum.Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugCodeEnum::Next
helpviewer_keywords:
- ICorDebugCodeEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugEnum interface [.NET Framework debugging]
ms.assetid: 644ece86-384d-4c63-9fba-52c789616ff7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 076b5d628dfe83decdbbe2f5e74c50e08262c580
ms.sourcegitcommit: 3094dcd17141b32a570a82ae3f62a331616e2c9c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2019
ms.locfileid: "71700684"
---
# <a name="icordebugcodeenumnext-method"></a>ICorDebugCodeEnum::Next-Methode

Ruft die angegebene Anzahl von "ICorDebugCode"-Instanzen aus der-Enumeration ab, beginnend bei der aktuellen Position.

## <a name="syntax"></a>Syntax

```cpp
HRESULT Next (
    [in] ULONG  celt,
    [out, size_is(celt), length_is(*pceltFetched)]
        ICorDebugCode *values[],
    [out] ULONG *pceltFetched
);
```

## <a name="parameters"></a>Parameter

 `celt`  
 in Die Anzahl der abzurufenden `ICorDebugCode`-Instanzen.

 `values`  
 vorgenommen Ein Array von Zeigern, von denen jedes auf ein `ICorDebugCode`-Objekt zeigt.

 `pceltFetched`  
 vorgenommen Ein Zeiger auf die Anzahl von `ICorDebugCode`-Instanzen, die tatsächlich zurückgegeben wurden. Dieser Wert kann NULL sein, wenn `celt` ein Wert ist.

## <a name="requirements"></a>Anforderungen

 **Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../get-started/system-requirements.md).

 **Header:** Cordebug. idl, Cordebug. h

 **Fern** CorGuids.lib

 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
 
