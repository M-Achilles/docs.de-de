---
title: ICorDebugNativeFrame::GetLocalRegisterMemoryValue-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugNativeFrame.GetLocalRegisterMemoryValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue
helpviewer_keywords:
- ICorDebugNativeFrame::GetLocalRegisterMemoryValue method [.NET Framework debugging]
- GetLocalRegisterMemoryValue method [.NET Framework debugging]
ms.assetid: d350f69d-9aff-4f5a-8301-daea22dee2da
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: cc179236f5453724639d47558770179a1e80f706
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67746191"
---
# <a name="icordebugnativeframegetlocalregistermemoryvalue-method"></a>ICorDebugNativeFrame::GetLocalRegisterMemoryValue-Methode
Ruft den Wert eines Arguments oder lokale Variable, die das niedrige Word und das hohe Word, werden in der Speicheradresse gespeichert, und registrieren Sie sich, bzw. für diese systemeigene Rahmen angegeben.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT GetLocalRegisterMemoryValue (  
    [in] CorDebugRegister   highWordReg,  
    [in] CORDB_ADDRESS      lowWordAddress,  
    [in] ULONG              cbSigBlob,  
    [in] PCCOR_SIGNATURE    pvSigBlob,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `highWordReg`  
 [in] Der Wert der "CorDebugRegister"-Enumeration, die angibt, die Registrierung, die das hohe Word des Werts enthält.  
  
 `lowWordAddress`  
 [in] Ein `CORDB_ADDRESS` Wert, der angibt, die Speicheradresse, die das niedrige Word der den Wert enthält.  
  
 `cbSigBlob`  
 [in] Eine ganze Zahl, die die Größe der die binäre Metadatensignatur gibt an, welche die verweist die `pvSigBlob` Parameter.  
  
 `pvSigBlob`  
 [in] Ein `PCCOR_SIGNATURE` Wert, der auf die binäre Metadatensignatur der der Typ des Werts verweist.  
  
 `ppValue`  
 [out] Ein Zeiger auf die Adresse eines "ICorDebugValue"-Objekts, die den abgerufenen Wert, der in der angegebenen registrieren und den angegebenen Speicherort gespeichert wird.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch
