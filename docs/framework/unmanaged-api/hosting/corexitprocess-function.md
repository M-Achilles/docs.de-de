---
title: CorExitProcess-Funktion
ms.date: 03/30/2017
api_name:
- CorExitProcess
api_location:
- mscoree.dll
- clr.dll
- mscorwks.dll
- mscoreei.dll
- mscorsvr.dll
api_type:
- DLLExport
f1_keywords:
- CorExitProcess
helpviewer_keywords:
- CorExitProcess function [.NET Framework hosting]
ms.assetid: a5cab4c6-990e-47f3-8798-cf422b791015
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6e1104a98afb32dea687949e9c723124014c1e62
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69925317"
---
# <a name="corexitprocess-function"></a>CorExitProcess-Funktion
Beendet den aktuellen nicht verwalteten Prozess.  
  
 Diese Funktion wurde im .NET Framework 4 als veraltet markiert. Verwenden Sie stattdessen die [ICLRMetaHost:: ExitProcess](../../../../docs/framework/unmanaged-api/hosting/iclrmetahost-exitprocess-method.md) -Methode.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
void STDMETHODCALLTYPE CorExitProcess (   
  int  exitCode  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `exitCode`  
 Eine ganze Zahl, die den Prozessexitcode angibt.  
  
## <a name="remarks"></a>Hinweise  
  
> [!NOTE]
> Beginnend mit dem .NET Framework 4 wird `CorExitProcess` jede gestartete Laufzeit im Prozess beendet, nicht nur die Laufzeit, an die die Legacy-APIs gebunden wurden.  
  
## <a name="requirements"></a>Anforderungen  
 **Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MSCorEE.h  
  
 **Fern** MSCorEE.dll  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [Veraltete CLR-Hostingfunktionen](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
