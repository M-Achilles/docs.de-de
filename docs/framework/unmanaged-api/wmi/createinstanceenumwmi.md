---
title: Funktion "-Funktion" (nicht verwaltete API-Referenz)
description: Die Funktion "kreateinstanceenumwmi" gibt einen Enumerator zurück, der Instanzen einer bestimmten Klasse enthält, die die Auswahlkriterien erfüllen.
ms.date: 11/06/2017
api_name:
- CreateInstanceEnumWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CreateInstanceEnumWmi
helpviewer_keywords:
- CreateInstanceEnumWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b7709d9c50a494013ece2f91b3acc213278f0e57
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798903"
---
# <a name="createinstanceenumwmi-function"></a>Funktion "-Funktion"

Gibt einen Enumerator zurück, der die Instanzen einer bestimmten Klasse zurückgibt, die angegebene Auswahlkriterien erfüllen.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

## <a name="syntax"></a>Syntax

```cpp
HRESULT CreateInstanceEnumWmi (
   [in] BSTR                    strFilter,
   [in] long                    lFlags,
   [in] IWbemContext*           pCtx,
   [out] IEnumWbemClassObject** ppEnum,
   [in] DWORD                   authLevel,
   [in] DWORD                   impLevel,
   [in] IWbemServices*          pCurrentNamespace,
   [in] BSTR                    strUser,
   [in] BSTR                    strPassword,
   [in] BSTR                    strAuthority
);
```

## <a name="parameters"></a>Parameter

`strFilter`\
in Der Name der Klasse, für die-Instanzen gewünscht werden. Dieser Parameter darf nicht `null`sein.

`lFlags`\
in Eine Kombination von Flags, die sich auf das Verhalten dieser Funktion auswirken. Die folgenden Werte sind in der *wbemcli. h* -Header Datei definiert, oder Sie können Sie als Konstanten im Code definieren:

|Konstante  |Wert  |Beschreibung  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0x20000 | Wenn festgelegt, ruft die Funktion die im lokalisierten Namespace des Gebiets Schemas der aktuellen Verbindung gespeicherten geänderten Qualifizierer ab. <br/> Wenn nicht festgelegt, ruft die Funktion nur die Qualifizierer ab, die im unmittelbaren Namespace gespeichert sind. |
| `WBEM_FLAG_DEEP` | 0 | Die-Enumeration enthält diese und alle Unterklassen in der Hierarchie. |
| `WBEM_FLAG_SHALLOW` | 1 | Die-Enumeration enthält nur reine Instanzen dieser Klasse und schließt alle Instanzen von Unterklassen aus, die Eigenschaften bereitstellen, die in dieser Klasse nicht gefunden werden. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | Das-Flag verursacht einen semisynchronen-Rückruf. |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | Die-Funktion gibt einen vorwärts-Enumerator zurück. In der Regel sind vorwärts-Enumeratoren schneller und verbrauchen weniger Arbeitsspeicher als herkömmliche Enumeratoren, aber Sie erlauben keine Aufrufe von [Klonen](clone.md). |
| `WBEM_FLAG_BIDIRECTIONAL` | 0 | WMI behält Zeiger auf Objekte in der-Enumeration bei, bis Sie freigegeben werden. |

Die empfohlenen Flags sind `WBEM_FLAG_RETURN_IMMEDIATELY` und `WBEM_FLAG_FORWARD_ONLY` , um eine optimale Leistung zu erzielen.

`pCtx`\
in Normalerweise ist `null`dieser Wert. Andernfalls handelt es sich um einen Zeiger auf eine [IWbemContext](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemcontext) -Instanz, die vom Anbieter verwendet werden kann, der die angeforderten Instanzen bereitstellt.

`ppEnum`\
vorgenommen Empfängt den Zeiger auf den Enumerator.

`authLevel`\
in Die Autorisierungs Ebene.

`impLevel`\
in Die Ebene des Identitäts Wechsels.

`pCurrentNamespace`\
in Ein Zeiger auf ein [IWbemServices](/windows/desktop/api/wbemcli/nn-wbemcli-iwbemservices) -Objekt, das den aktuellen Namespace darstellt.

`strUser`\
in Der Benutzername. Weitere Informationen finden Sie in der [connectserverwmi](connectserverwmi.md) -Funktion.

`strPassword`\
in Das Kennwort. Weitere Informationen finden Sie in der [connectserverwmi](connectserverwmi.md) -Funktion.

`strAuthority`\
in Der Domänen Name des Benutzers. Weitere Informationen finden Sie in der [connectserverwmi](connectserverwmi.md) -Funktion.

## <a name="return-value"></a>Rückgabewert

Die folgenden Werte, die von dieser Funktion zurückgegeben werden, sind in der *wbemcli. h* -Header Datei definiert, oder Sie können Sie als Konstanten im Code definieren:

|Konstante  |Wert  |Beschreibung  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0x80041003 | Der Benutzer verfügt nicht über die Berechtigung zum Anzeigen von Instanzen der angegebenen Klasse. |
| `WBEM_E_FAILED` | 0x80041001 | Ein nicht angegebener Fehler ist aufgetreten. |
| `WBEM_E_INVALID_CLASS` | 0x80041010 | `strFilter` existiert nicht. |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | Ein Parameter ist ungültig. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Es ist nicht genügend Arbeitsspeicher verfügbar, um den Vorgang abzuschließen. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI wurde wahrscheinlich angehalten und neu gestartet. Ruft [connectserverwmi](connectserverwmi.md) erneut auf. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | Fehler beim Remote Prozedur Aufruf (RPC)-Link zwischen dem aktuellen Prozess und WMI. |
|`WBEM_S_NO_ERROR` | 0 | Der Funktions Aufrufvorgang war erfolgreich.  |

## <a name="remarks"></a>Hinweise

Diese Funktion umschließt einen aufzurufenden Befehl der Methode [IWbemServices:: | ateclassenum](/windows/desktop/api/wbemcli/nf-wbemcli-iwbemservices-createinstanceenum) .

Beachten Sie, dass der zurückgegebene Enumerator NULL Elemente aufweisen kann.

Wenn der Funktionsaufruf fehlschlägt, können Sie zusätzliche Fehlerinformationen abrufen, indem Sie die [GetErrorInfo](geterrorinfo.md) -Funktion aufrufen.

## <a name="requirements"></a>Anforderungen

**Formen** Weitere Informationen finden Sie unter [Systemanforderungen](../../get-started/system-requirements.md).

**Header:** WMINet_Utils.idl

**.NET Framework-Versionen:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]

## <a name="see-also"></a>Siehe auch

- [WMI und Leistungsindikatoren (Referenz zur nicht verwalteten API)](index.md)
