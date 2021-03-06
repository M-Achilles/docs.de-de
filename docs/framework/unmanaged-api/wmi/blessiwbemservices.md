---
title: Blessiwbemservices-Funktion (Referenz zur nicht verwalteten API)
description: Die blessiwbemservices-Funktion gibt an, ob Benutzer Anmelde Informationen den Zugriff auf eine IWbemServices-Klasse zulassen.
ms.date: 11/06/2017
api_name:
- BlessIWbemServices
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- BlessIWbemServices
helpviewer_keywords:
- BlessIWbemServices function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: e00197b72ca7fc8941475ae51159351d53da12d3
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855975"
---
# <a name="blessiwbemservices-function"></a>BlessIWbemServices-Funktion
Gibt an, ob die Benutzer Anmelde Informationen den Zugriff auf die angegebene [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) -Klasse zulassen.   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Syntax  
  
```cpp
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser, 
   [in] BSTR strPassword, 
   [in] BSTR strAuthority, 
   [in] DWORD impLevel, 
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a>Parameter

`pIWbemServices`\
in Ein Zeiger auf das [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) -Objekt, für das Berechtigungen erforderlich sind.

`strUser`\
in Der Benutzername.

`strPassword`\
in Das Kennwort, `strUser`das zugeordnet ist.

`strAuthority`\
in Der Domänen Name des Benutzers. Weitere Informationen finden Sie in der [connectserverwmi](connectserverwmi.md) -Funktion.

`impLevel`\
in Die Ebene des Identitäts Wechsels.

`authnLevel`\
in Die Autorisierungs Ebene.

## <a name="return-value"></a>Rückgabewert

Die folgenden Werte, die von dieser Funktion zurückgegeben werden, sind in der Header Datei " *Winerror. h* " definiert, oder Sie können Sie als Konstanten im Code definieren:

|Konstante  |Wert  |Beschreibung  |
|---------|---------|---------|
| `E_INVALIDARG` | 0x80070057 | Mindestens ein Argument ist ungültig. |
| `E_POINTER` | 0x80004003 | `pIWbemServices` ist `null`. | 
| `E_FAIL` | 0x80000008 | Ein nicht angegebener Fehler ist aufgetreten. |
| `E_OUTOFMEMORY` | 0x80000002 | Es ist nicht genügend Arbeitsspeicher verfügbar, um den Vorgang auszuführen. | 
| `S_OK` | 0 | Der Funktions Aufrufvorgang war erfolgreich. | 

## <a name="requirements"></a>Anforderungen  

 **Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../get-started/system-requirements.md).  
  
 **Header:** WMINet_Utils.idl  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Siehe auch

- [WMI und Leistungsindikatoren (Referenz zur nicht verwalteten API)](index.md)
