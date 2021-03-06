---
title: IMetaDataAssemblyEmit::DefineFile-Methode
ms.date: 03/30/2017
api_name:
- IMetaDataAssemblyEmit.DefineFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataAssemblyEmit::DefineFile
helpviewer_keywords:
- IMetaDataAssemblyEmit::DefineFile method [.NET Framework metadata]
- DefineFile method [.NET Framework metadata]
ms.assetid: c065aadf-c1ca-4981-bde6-597042cb29c4
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 54d5a233da2bf033d960fd02961ac89eb57151d2
ms.sourcegitcommit: 7f616512044ab7795e32806578e8dc0c6a0e038f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2019
ms.locfileid: "67776287"
---
# <a name="imetadataassemblyemitdefinefile-method"></a>IMetaDataAssemblyEmit::DefineFile-Methode
Erstellt eine `File`-Metadatenstruktur, die Metadaten für die Assembly enthält, auf die diese Assembly verweist, und gibt das zugeordnete Metadatentoken zurück.  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
HRESULT DefineFile (  
    [in]  LPCWSTR        szName,   
    [in]  const void     *pbHashValue,   
    [in]  ULONG          cbHashValue,  
    [in]  DWORD          dwFileFlags,  
    [out] mdFile         *pmdf  
);  
```  
  
## <a name="parameters"></a>Parameter  
 `szName`  
 [in] Der Name der Datei, die verwendet werden.  
  
 `pbHashValue`  
 [in] Ein Zeiger auf den Hashwert der Daten zu dieser Assembly zugeordneten.  
  
 `cbHashValue`  
 [in] Die Größe in Bytes der `pbHashValue`.  
  
 `dwFileFlags`  
 [in] Eine bitweise Kombination von `FileFlags` Werte, die eigenschafteneinstellungen angeben.  
  
 `pmdf`  
 [out] Ein Zeiger auf das zurückgegebene `File` token.  
  
## <a name="remarks"></a>Hinweise  
 Eine `File` muss für jede Datei, die Bestandteil dieser Assembly zum Zeitpunkt, die diese Assembly erstellt wurde war, mit Ausnahme der Datei, die die Metadaten enthält, definiert werden.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattform:** Weitere Informationen finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** Cor.h  
  
 **Bibliothek:** Als Ressource in MsCorEE.dll verwendet  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch

- [IMetaDataAssemblyEmit-Schnittstelle](../../../../docs/framework/unmanaged-api/metadata/imetadataassemblyemit-interface.md)
