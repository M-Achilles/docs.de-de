---
title: ICLRDataTarget::GetThreadContext-Methode
ms.date: 03/30/2017
api_name:
- ICLRDataTarget.GetThreadContext
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICLRDataTarget::GetThreadContext
helpviewer_keywords:
- ICLRDataTarget::GetThreadContext method [.NET Framework debugging]
- GetThreadContext method, ICLRDataTarget interface [.NET Framework debugging]
ms.assetid: b9d8c3b5-3a2e-4225-95d4-dd052c4532c3
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 1492c6d72d68a95a79925d7789a710b5b5ed14b1
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67738709"
---
# <a name="iclrdatatargetgetthreadcontext-method"></a>ICLRDataTarget::GetThreadContext-Methode
Ruft den aktuellen Ausführungskontext für den angegebenen Thread im Zielprozess. Diese Methode wird von den Datenzugriffsdiensten der common Language Runtime aufgerufen.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetThreadContext (  
    [in] ULONG32            threadID,  
    [in] ULONG32            contextFlags,  
    [in] ULONG32            contextSize,  
    [out, size_is(contextSize)]   
        BYTE                *context  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `threadID`  
 [in] Der Betriebssystem-Bezeichner eines Threads im Zielprozess.  
  
 `contextFlags`  
 [in] Flags, die angeben, welche Teile des Kontexts zurückgegeben. Die Implementierung gibt immer mindestens diese Teile des Kontexts zurück.  
  
 `contextSize`  
 [in] Die Größe des Kontexts.  
  
 `context`  
 [out] Zeiger auf einen Puffer, in dem Kontext platziert werden soll.  
  
 Die Daten in die `context` Puffer muss im Format von Win32 `CONTEXT` Struktur. Den Kontext angibt, macht prozessorspezifische Registerdaten, also die Definition von Win32 `CONTEXT` Struktur hängt von der Prozessorarchitektur. Finden Sie in der Headerdatei "WinNT.h" für die Definition von Win32 `CONTEXT` Struktur.  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode wird vom Writer der Debuganwendung implementiert.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** ClrData.idl, ClrData.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICLRDataTarget-Schnittstelle](../../../../docs/framework/unmanaged-api/debugging/iclrdatatarget-interface.md)
