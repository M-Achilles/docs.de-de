---
title: IValidator::Validate-Methode
ms.date: 03/30/2017
api_name:
- IValidator.Validate
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- Validate
helpviewer_keywords:
- IValidator::Validate method [.NET Framework hosting]
- Validate method, IValidator interface [.NET Framework hosting]
ms.assetid: 7d68666a-fb73-4455-bebd-908d49a16abc
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 840a3779ca5692787c2c352db60a29d6a4d4ba4f
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67768590"
---
# <a name="ivalidatorvalidate-method"></a>IValidator::Validate-Methode
Überprüft die angegebene Datei (portable Executable) oder Microsoft intermediate Language (MSIL)-Datei.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT Validate (  
    [in] IVEHandler            *veh,  
    [in] IUnknown              *pAppDomain,  
    [in] unsigned long          ulFlags,  
    [in] unsigned long          ulMaxError,  
    [in] unsigned long          token,  
    [in] LPWSTR                 fileName,  
    [in, size_is(ulSize)] BYTE *pe,  
    [in] unsigned long          ulSize  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `veh`  
 [in] Ein Zeiger auf ein `IVEHandler` -Instanz, die Validierungsfehler behandelt.  
  
 `pAppDomain`  
 [in] Ein Zeiger auf die Anwendungsdomäne, in der die Datei geladen wird.  
  
 `ulFlags`  
 [in] Eine bitweise Kombination von [ValidatorFlags](../../../../docs/framework/unmanaged-api/hosting/validatorflags-enumeration.md) Werte, der angibt, Überprüfungen, die ausgeführt werden soll.  
  
 `ulMaxError`  
 [in] Die maximale Anzahl von Fehlern, die vor dem Beenden der Überprüfungsprozess zulassen.  
  
 `token`  
 [in] Nicht verwendet.  
  
 `fileName`  
 [in] Eine Zeichenfolge, die mit dem Namen der Datei, die überprüft werden soll.  
  
 `pe`  
 [in] Ein Zeiger auf den Speicherpuffer, die in dem die Datei gespeichert ist.  
  
 `ulSize`  
 [in] Die Größe in Bytes der Datei, die überprüft werden.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** IValidator.idl, IValidator.h  
  
 **Bibliothek:** Als Ressource in MSCorEE.dll enthalten  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
