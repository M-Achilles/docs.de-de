---
ms.openlocfilehash: 7f551fbc194d2da2fdae6bcc7025c20b03aadda2
ms.sourcegitcommit: d55e14eb63588830c0ba1ea95a24ce6c57ef8c8c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/11/2019
ms.locfileid: "67859264"
---
### <a name="path-colon-checks-are-stricter"></a>Die Überprüfung von Pfaden auf Doppelpunkte ist genauer

|   |   |
|---|---|
|Details|In .NET Framework 4.6.2 wurde eine Reihe von Änderungen vorgenommen, um zuvor nicht unterstützte Pfade zu unterstützen (hinsichtlich Länge und Format). Die Überprüfung auf eine korrekte Syntax bei der Verwendung von Laufwerkstrennzeichen (Doppelpunkt) wurde verbessert. Als Nebenwirkung wurden mehrere URI-Pfade in einigen ausgewählten Pfad-APIs blockiert, in denen sie vorher toleriert wurden.|
|Vorschlag|Wenn ein URI an betroffene APIs übergeben wird, sollten Sie zunächst die Zeichenfolge in einen gültigen Pfad ändern.<ul><li>Entfernen Sie das Schema manuell aus den URLs (entfernen Sie z.B. <code>file://</code> aus den URLs).</li><li>Übergeben Sie den URI der Klasse <xref:System.Uri> und verwenden Sie <xref:System.Uri.LocalPath>.</li></ul>Alternativ können Sie sich gegen die Normalisierung des neuen Pfads entscheiden, indem Sie die AppContext-Option <code>Switch.System.IO.UseLegacyPathHandling</code> auf TRUE festlegen.|
|Bereich|Microsoft Edge|
|Version|4.6.2|
|Typ|Neuzuweisung|
|Betroffene APIs|<ul><li><xref:System.IO.Path.GetDirectoryName(System.String)?displayProperty=nameWithType></li><li><xref:System.IO.Path.GetPathRoot(System.String)?displayProperty=nameWithType></li></ul>|

