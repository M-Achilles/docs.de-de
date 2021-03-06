---
title: StackTrace_SimpleContext-Struktur
ms.date: 03/30/2017
api_name:
- StackTrace_SimpleContext
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- SimpleContext
helpviewer_keywords:
- SimpleContext structure [.NET Framework debugging]
- StackTrace_SimpleContext structure [.NET Framework debugging]
ms.assetid: d4cef11f-a8ca-49bc-a1b8-6631f9e28f3e
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: bc0fc18e31b89b22ffd30d99a8b079ed7b87fa1b
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67752502"
---
# <a name="stacktracesimplecontext-structure"></a>StackTrace_SimpleContext-Struktur
Stellt einen einfachen Kontext bereit, der statt einer vollständigen `CONTEXT`-Struktur verwendet werden kann.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
struct StackTrace_SimpleContext  
{  
    ULONG64 StackOffset;       // ESP on x86  
    ULONG64 FrameOffset;       // EBP on x86  
    ULONG64 InstructionOffset; // EIP on x86  
};  
```  
  
## <a name="members"></a>Member  
  
|Member|Beschreibung|  
|------------|-----------------|  
|`StackOffset`|Der Stapelzeiger oder der EINGABETASTE Stapelzeiger (ESP) auf X86 Plattformen.|  
|`FrameOffset`|Die Frameoffset oder die EBP-Register auf X86 Plattformen.|  
|`InstructionOffset`|Der Anweisungszeiger oder der EINGABETASTE Anweisungszeiger (EIP) auf X86 Plattformen.|  
  
## <a name="remarks"></a>Hinweise  
 Da die Funktionen der Aufrufliste-Ablaufverfolgung in der Regel nur die Adresse, Frameoffset und Stapeladresse zurückgeben müssen, können Sie optional mithilfe der `SimpleContext` Struktur anstelle einer großen `CONTEXT` Struktur.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** SOS_Stacktrace.h  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [Debuggen von Strukturen](../../../../docs/framework/unmanaged-api/debugging/debugging-structures.md)
- [Debuggen](../../../../docs/framework/unmanaged-api/debugging/index.md)
