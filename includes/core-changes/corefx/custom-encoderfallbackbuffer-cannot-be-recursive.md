---
ms.openlocfilehash: 4075eadf7cfb39c913b7657d43335bae5497deff
ms.sourcegitcommit: 56f1d1203d0075a461a10a301459d3aa452f4f47
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/24/2019
ms.locfileid: "71216930"
---
### <a name="custom-encoderfallbackbuffer-instances-cannot-fall-back-recursively"></a>Benutzerdefinierte EncoderFallbackBuffer-Instanzen können kein rekursives Fallback ausführen

Benutzerdefinierte <xref:System.Text.EncoderFallbackBuffer>-Instanzen können kein rekursives Fallback ausführen. Die Implementierung von <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> muss zu einer Zeichensequenz führen, die in die Zielcodierung konvertiert werden kann. Andernfalls tritt eine Ausnahme auf.

#### <a name="details"></a>Details

Bei einem Zeichen-zu-Byte-Transcodierungsvorgang erkennt die Runtime falsch formatierte oder nicht konvertierbare UTF-16-Sequenzen und stellt diese Zeichen für die <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>-Methode bereit. Die `Fallback`-Methode bestimmt, welche Zeichen die ursprünglichen nicht konvertierbaren Daten ersetzen, und diese Zeichen werden durch Aufrufen von <xref:System.Text.EncoderFallbackBuffer.GetNextChar%2A?displayProperty=nameWithType> in einer Schleife ausgeglichen.

Die Runtime versucht dann, diese Ersetzungszeichen in die Zielcodierung zu transcodieren. Wenn dieser Vorgang erfolgreich ist, setzt die Runtime die Transcodierung an der Stelle fort, an der sie die ursprüngliche Eingabezeichenfolge verlassen hat.

In .NET Core Vorschau 7 und früheren Versionen können von benutzerdefinierten Implementierungen von <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> Zeichensequenzen zurückgegeben werden, die nicht in die Zielcodierung konvertiert werden können. Wenn die ersetzten Zeichen nicht in die Zielcodierung transcodiert werden können, ruft die Runtime die <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>-Methode erneut mit den Ersetzungszeichen auf, wobei erwartet wird, dass die <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType>-Methode eine neue Ersetzungssequenz zurückgibt. Dieser Vorgang wird fortgesetzt, bis die Laufzeit eine wohlgeformte, konvertierbare Ersetzung erkennt oder eine maximale Anzahl von Rekursionen erreicht wird.

Ab .NET Core 3.0 müssen von benutzerdefinierten Implementierungen von <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType> Zeichensequenzen zurückgegeben werden, die in die Zielcodierung konvertiert werden können. Wenn die ersetzten Zeichen nicht in die Zielcodierung transcodiert werden können, wird eine <xref:System.ArgumentException> ausgelöst. Die Laufzeit führt keine rekursiven Aufrufe der <xref:System.Text.EncoderFallbackBuffer>-Instanz mehr durch.

Dieses Verhalten gilt nur, wenn alle drei der folgenden Bedingungen erfüllt sind:

- Die Runtime erkennt eine falsch formatierte UTF-16-Sequenz oder eine UTF-16-Sequenz, die nicht in die Zielcodierung konvertiert werden kann.
- Ein benutzerdefinierter <xref:System.Text.EncoderFallback> wurde angegeben.
- Der benutzerdefinierte <xref:System.Text.EncoderFallback> versucht, eine neue falsch formatierte oder nicht konvertierbare UTF-16-Sequenz zu ersetzen.

#### <a name="version-introduced"></a>Eingeführt in Version

3.0

#### <a name="recommended-action"></a>Empfohlene Maßnahme

Die meisten Entwickler müssen keine Maßnahmen ergreifen.

Wenn eine Anwendung eine benutzerdefinierte <xref:System.Text.EncoderFallback>- und <xref:System.Text.EncoderFallbackBuffer>-Klasse verwendet, stellen Sie sicher, dass die Implementierung von <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType> den Fallbackpuffer mit wohlgeformten UTF-16-Daten auffüllt, die direkt in die Zielcodierung konvertiert werden können, wenn die <xref:System.Text.EncoderFallbackBuffer.Fallback%2A>-Methode zuerst von der Runtime aufgerufen wird.

#### <a name="category"></a>Kategorie

CoreFx

#### <a name="affected-apis"></a>Betroffene APIs

- <xref:System.Text.EncoderFallbackBuffer.Fallback%2A?displayProperty=nameWithType>
- <xref:System.Text.EncoderFallbackBuffer.GetNextChar?displayProperty=nameWithType>

<!--

### Affected APIs

- `Overload:System.Text.EncoderFallbackBuffer.Fallback`
- `M:System.Text.EncoderFallbackBuffer.GetNextChar`

-->
