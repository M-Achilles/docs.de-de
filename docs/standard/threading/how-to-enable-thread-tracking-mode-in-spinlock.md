---
title: 'Vorgehensweise: Aktivieren des Modus zum Nachverfolgen von Threads in SpinLock'
ms.date: 03/30/2017
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- SpinLock, how to enable thread-tracking
ms.assetid: 62ee2e68-0bdd-4869-afc9-f0a57a11ae01
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 111ab87ca419217f425eb5d4bc9b52f5f30f0237
ms.sourcegitcommit: 2701302a99cafbe0d86d53d540eb0fa7e9b46b36
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2019
ms.locfileid: "64644848"
---
# <a name="how-to-enable-thread-tracking-mode-in-spinlock"></a>Vorgehensweise: Aktivieren des Modus zum Nachverfolgen von Threads in SpinLock
<xref:System.Threading.SpinLock?displayProperty=nameWithType> ist eine gegenseitige Low-Level- Ausschlusssperre, die Sie für Szenarien mit sehr kurzen Wartezeiten verwenden können. <xref:System.Threading.SpinLock> ist nicht wiedereintrittsfähig. Wenn ein Thread in die Sperre eintritt, muss er die Sperre ordnungsgemäß beenden, bevor er erneut eintreten kann. In der Regel würde jeder Versuch, erneut in die Sperre einzutreten, einen Deadlock verursachen, und Deadlocks sind sehr schwer zu beheben. Als Hilfe zur Entwicklung unterstützt <xref:System.Threading.SpinLock?displayProperty=nameWithType> einen Modus zum Nachverfolgen von Threads, der bewirkt, dass eine Ausnahme ausgelöst wird, wenn ein Thread versucht, erneut in eine Sperre einzutreten, in der er sich bereits befindet. So können Sie leichter den Punkt lokalisieren, an dem die Sperre nicht ordnungsgemäß beendet wurde. Sie können den Modus zum Nachverfolgen von Threads mithilfe des <xref:System.Threading.SpinLock>-Konstruktors einschalten, der einen booleschen Eingabeparameter akzeptiert, und ein `true`-Argument übergeben. Deaktivieren Sie den Modus zum Nachverfolgen von Threads nach Abschluss der Entwicklungs- und Testphase im Interesse besserer Leistung.  
  
## <a name="example"></a>Beispiel  
 Das folgende Beispiel veranschaulicht den Modus zum Nachverfolgen von Threads. Die Zeilen zum ordnungsgemäßen Beenden der Sperre sind auskommentiert, um einen Codefehler zu simulieren, der eines der folgenden Ergebnisse bewirkt:  
  
- Eine Ausnahme wird ausgelöst, wenn <xref:System.Threading.SpinLock> mit dem Argument `true` (`True` in Visual Basic) erstellt wird.  
  
- Ein Deadlock wird ausgelöst, wenn <xref:System.Threading.SpinLock> mit dem Argument `false` (`False` in Visual Basic) erstellt wird.  
  
 [!code-csharp[CDS_SpinLock#01](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinlock/cs/spinlockdemo.cs#01)]
 [!code-vb[CDS_SpinLock#01](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinlock/vb/spinlock_threadtracking.vb#01)]  
  
## <a name="see-also"></a>Siehe auch

- [SpinLock](../../../docs/standard/threading/spinlock.md)
