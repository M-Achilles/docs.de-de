---
ms.openlocfilehash: a9b6af31b68c25ab58c52757f48ed23cca3f5a35
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/25/2019
ms.locfileid: "71263312"
---
### <a name="better-argument-validation-in-the-pkcs8privatekeyinfo-constructor"></a>Bessere Argumentvalidierung im Pkcs8PrivateKeyInfo-Konstruktor

Ab .NET Core 3.0 Vorschau 9 validiert der `Pkcs8PrivateKeyInfo`-Konstruktor den Parameter `algorithmParameters` als einzelnen BER-codierten Wert.

#### <a name="change-description"></a>Änderungsbeschreibung

Vor .NET Core 3.0 Vorschau 9 hat der [`Pkcs8PrivateKeyInfo`-Konstruktor](xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.%23ctor(System.Security.Cryptography.Oid,System.Nullable%7BSystem.ReadOnlyMemory%7BSystem.Byte%7D%7D,System.ReadOnlyMemory%7BSystem.Byte%7D,System.Boolean)) das Argument `algorithmParameters` nicht validiert.  Wenn dieses Argument ein ungültiger Wert war, war der Konstruktor zwar erfolgreich, aber ein Aufruf einer der Methoden <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.Encode>, <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.TryEncode%2A>, <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.Encrypt%2A> oder <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.TryEncrypt%2A> löste entweder eine <xref:System.ArgumentException> für ein nicht akzeptiertes Argument (`preEncodedValue`) oder eine <xref:System.Security.Cryptography.CryptographicException> aus.

Wenn der folgende Code mit .NET Core 3.0 vor Vorschau 9 ausgeführt wird, löst er nur dann eine Ausnahme aus, wenn die <xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.Encode>-Methode aufgerufen wird:

```csharp
byte[] algorithmParameters = { 0x05, 0x00, 0x05, 0x00 };

var info = new Pkcs8PrivateKeyInfo(algorithmId, algorithmParameters, privateKey);
// This line throws an ArgumentException for `preEncodedValue`:
byte[] encoded = info.Encode();
```

Ab .NET Core 3.0 Vorschau 9 wird das Argument im Konstruktor validiert, und ein ungültiger Wert führt dazu, dass die Methode eine <xref:System.Security.Cryptography.CryptographicException> auslöst. Diese Änderung verschiebt die Ausnahme näher an die Quelle des Datenfehlers. Beispiel:

```csharp
byte[] algorithmParameters = { 0x05, 0x00, 0x05, 0x00 };

// This line throws a CryptographicException
var info = new Pkcs8PrivateKeyInfo(algorithmId, algorithmParameters, privateKey);
```

#### <a name="version-introduced"></a>Eingeführt in Version

3.0 Vorschau 9

#### <a name="recommended-action"></a>Empfohlene Maßnahme

Stellen Sie sicher, dass nur gültige `algorithmParameters`-Werte angegeben werden, oder dass Aufrufe des `Pkcs8PrivateKeyInfo`-Konstruktortests für <xref:System.ArgumentException> und <xref:System.Security.Cryptography.CryptographicException> erfolgen, wenn Ausnahmebehandlung gewünscht wird.

### <a name="category"></a>Kategorie

Kryptografie

### <a name="affected-apis"></a>Betroffene APIs

- [Pkcs8PrivateKeyInfo-Konstruktor](xref:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.%23ctor(System.Security.Cryptography.Oid,System.Nullable%7BSystem.ReadOnlyMemory%7BSystem.Byte%7D%7D,System.ReadOnlyMemory%7BSystem.Byte%7D,System.Boolean))

<!--

### Affected APIs

- `M:System.Security.Cryptography.Pkcs.Pkcs8PrivateKeyInfo.#ctor(System.Security.Cryptography.Oid,System.Nullable{System.ReadOnlyMemory{System.Byte}},System.ReadOnlyMemory{System.Byte},System.Boolean))

-->
