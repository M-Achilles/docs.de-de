---
title: ICorDebugClass2::SetJMCStatus-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugClass2.SetJMCStatus
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugClass2::SetJMCStatus
helpviewer_keywords:
- ICorDebugClass2::SetJMCStatus method [.NET Framework debugging]
- SetJMCStatus method, ICorDebugClass2 interface [.NET Framework debugging]
ms.assetid: 077e6c7f-f857-480c-bebb-76ee1de4e8fc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 23f248625753c15a4798ea69a1eb3b377b79f95d
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67747748"
---
# <a name="icordebugclass2setjmcstatus-method"></a>ICorDebugClass2::SetJMCStatus-Methode
Für jede Methode der Klasse wird einen Wert, der angibt, ob die Methode benutzerdefinierten Code ist.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT SetJMCStatus (  
    [in] BOOL   bIsJustMyCode  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `bIsJustMyCode`  
 [in] Legen Sie auf `true` , um anzugeben, dass die Methode den benutzerdefinierten code, legen Sie andernfalls auf `false`.  
  
## <a name="remarks"></a>Hinweise  
 Eine nur mein Code (JMC) zugeordnetem wird nicht auf eine benutzerdefinierte Code überspringen. Benutzerdefinierter Code muss es sich um eine Teilmenge der debugfähiger Code sein.  
  
 `SetJMCStatus` Gibt einen HRESULT-Wert, der S_FALSE zurück, wenn sie zum Festlegen des Werts für eine beliebige Methode, schlägt fehl, selbst wenn der Wert für alle anderen Methoden erfolgreich festgelegt.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
