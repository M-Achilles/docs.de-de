---
title: 'Vorgehensweise: Konvertieren von Zeichenfolgen in ein Array von Bytes in Visual Basic'
ms.date: 07/20/2015
helpviewer_keywords:
- string conversion [Visual Basic], arrays
- arrays [Visual Basic], converting strings to
- byte arrays
- examples [Visual Basic], string conversion
- arrays [Visual Basic], byte arrays
ms.assetid: f477d35c-a3fc-4a30-b1d4-cd0d353aae1d
ms.openlocfilehash: 786065fde9814d31ac36b56e1455d5b1685122ad
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64665356"
---
# <a name="how-to-convert-strings-into-an-array-of-bytes-in-visual-basic"></a>Vorgehensweise: Konvertieren von Zeichenfolgen in ein Array von Bytes in Visual Basic
In diesem Thema veranschaulicht das Konvertieren einer Zeichenfolge in ein Array von Bytes.  
  
## <a name="example"></a>Beispiel  
 Dieses Beispiel verwendet die <xref:System.Text.Encoding.GetBytes%2A> Methode der <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType> Codierungsklasse zum Konvertieren einer Zeichenfolge in ein Array von Bytes.  
  
 [!code-vb[VbVbalrStrings#74](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStrings/VB/Class2.vb#74)]  
  
 Sie können über mehrere Optionen zum Konvertieren einer Zeichenfolge in ein Bytearray:  
  
- <xref:System.Text.Encoding.ASCII%2A?displayProperty=nameWithType>: Ruft eine Codierung für den ASCII-Zeichensatz (7-Bit) ab.  
  
- <xref:System.Text.Encoding.BigEndianUnicode%2A?displayProperty=nameWithType>: Ruft eine Codierung für das UTF-16-Format mit big-Endian-Bytereihenfolge ab.  
  
- <xref:System.Text.Encoding.Default%2A?displayProperty=nameWithType>: Ruft eine Codierung für die aktuelle ANSI-Codepage des Systems ab.  
  
- <xref:System.Text.Encoding.Unicode%2A?displayProperty=nameWithType>: Ruft eine Codierung für das UTF-16-Format mit little-Endian-Bytereihenfolge ab.  
  
- <xref:System.Text.Encoding.UTF32%2A?displayProperty=nameWithType>: Ruft eine Codierung für das UTF-32-Format mit little-Endian-Bytereihenfolge ab.  
  
- <xref:System.Text.Encoding.UTF7%2A?displayProperty=nameWithType>: Ruft eine Codierung für das UTF-7-Format ab.  
  
- <xref:System.Text.Encoding.UTF8%2A?displayProperty=nameWithType>: Ruft eine Codierung für das UTF-8-Format ab.  
  
## <a name="see-also"></a>Siehe auch

- <xref:System.Text.Encoding?displayProperty=nameWithType>
- <xref:System.Text.Encoding.GetBytes%2A>
- [Vorgehensweise: Konvertiert ein Array von Bytes in eine Zeichenfolge in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/how-to-convert-an-array-of-bytes-into-a-string.md)
