---
title: ICorDebugDataTarget2::CreateVirtualUnwinder-Methode
ms.date: 03/30/2017
ms.assetid: 354c8b4c-7d23-45c6-a7d7-3be4c2a5b772
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 5445fb223e34aa82d4b93032bb059093978f6bd1
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69910334"
---
# <a name="icordebugdatatarget2createvirtualunwinder-method"></a>ICorDebugDataTarget2::CreateVirtualUnwinder-Methode
Erstellt einen neuen Stapelentlader, der mit dem Entladen bei einem Anfangskontext beginnt (welcher nicht unbedingt das Blatt eines Threads ist).  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT CreateVirtualUnwinder(  
    [in] DWORD nativeThreadID,  
    [in] ULONG32 contextFlags,  
    [in] ULONG32 cbContext,  
    [in, size_is(cbContext)] BYTE initialContext[],  
    [out] ICorDebugVirtualUnwinder ** ppUnwinder);  
};  
```  
  
## <a name="parameters"></a>Parameter  
 nativeThreadID  
 [in] Die systemeigene Thread-ID für den Thread, dessen Stapel entladen wird.  
  
 contextFlags  
 [in] Flags, die angeben, welche Teile des Kontexts in `initialContext` definiert sind.  
  
 cbContext  
 [in] Die Größe des `initialContext`.  
  
 initialContext  
 [in] Die Daten im Kontext.  
  
 ppUnwinder  
 [out] Ein Zeiger auf die Adresse eines ICorDebugVirtualUnwinder-Oberflächenobjekts.  
  
## <a name="return-value"></a>Rückgabewert  
 Bei Erfolg `S_OK`. Alle anderen `HRESULT` weisen auf Fehler hin. Alle von `HRESULT` "mscordbi empfangenen Fehler werden als schwerwiegend angesehen und bewirken, dass [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md) -Methoden zurückgegeben `CORDBG_E_DATA_TARGET_ERROR`werden.  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]
> Diese Methode ist nur mit .NET Native verfügbar.  
  
## <a name="requirements"></a>Anforderungen  
 **Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Cordebug. idl, Cordebug. h  
  
 **Fern** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_46_native](../../../../includes/net-46-native-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [ICorDebugDataTarget2-Schnittstelle](../../../../docs/framework/unmanaged-api/debugging/icordebugdatatarget2-interface.md)
- [Debuggen von Schnittstellen](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
